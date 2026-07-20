# Architecture Overview

This page describes OmniFlow's protocol architecture at a level appropriate for technical due diligence and integration planning. Detailed contract interfaces are documented in the smart contract repository; this page provides the conceptual map.

## Design Principles

OmniFlow's architecture rests on five design principles, each chosen to address a specific class of risk that has surfaced in prior on-chain RWA deployments.

**1. Off-chain truth, on-chain mirror.** The legal source of truth for ownership of OmniFlow VCC sub-fund interests is the VCC's official sub-register, maintained by the partner LFMC under MAS oversight. The on-chain RWA token is a cryptographic mirror of this register, updated through a defined reconciliation process. This separation ensures that token holders' legal rights are anchored in established Singapore corporate law rather than dependent solely on smart contract state.

**2. Compliance enforced at the protocol level.** Eligibility gating, transfer restrictions, and lock-up periods are enforced by the smart contracts themselves, not by external policies. A transfer that would violate compliance — for example, to a wallet that has not passed AI/II verification — reverts at the contract level, regardless of the sender's intent.

**3. Single source of truth for token supply.** RWA tokens exist on a single primary issuance chain. Other chains may serve as deposit rails (where investors send stablecoins) but do not hold native RWA tokens. This eliminates the lock-and-mint bridge attack surface that has caused over USD 2 billion in losses across the industry. See Cross-Chain Architecture.

**4. Modular jurisdiction support.** The compliance engine is decomposed into per-jurisdiction modules. Adding a new asset category — Japanese real estate, Southeast Asian infrastructure — requires deploying a new jurisdiction module without modifying core token, settlement, or distribution logic.

**5. Constitutional limits.** Certain protocol parameters cannot be modified by governance, multi-signature, or any operational role. These constitutional limits include the supply invariant, the AI/II gating requirement, and the burn-and-reissue exclusivity property. Constitutional limits are enforced through immutable contract code, not through policy.

## System Module Map

```
┌─────────────────────────────────────────────────────────────────┐
│                    OFF-CHAIN TRUTH LAYER                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  VCC Sub-Register (LFMC-managed, MAS-supervised)         │   │
│  │  Big 4 Audit (Annual)                                    │   │
│  │  Independent Valuation (CBRE / JLL / Cushman&Wakefield)  │   │
│  └──────────────────────────────────────────────────────────┘   │
└────────────────────────────────┬────────────────────────────────┘
│
Reconciliation & Attestation
│
┌────────────────────────────────▼────────────────────────────────┐
│                    ON-CHAIN MIRROR LAYER                         │
│                                                                   │
│   ┌───────────────┐    ┌──────────────┐    ┌─────────────────┐  │
│   │ Identity      │    │ Compliance   │    │ Jurisdiction    │  │
│   │ Registry      ├───►│ Module       │◄───┤ Modules         │  │
│   │ (KYC/KYA)     │    │ (Pre-trade)  │    │ (KR, JP, ...)   │  │
│   └───────┬───────┘    └──────┬───────┘    └─────────────────┘  │
│           │                    │                                  │
│           ▼                    ▼                                  │
│   ┌──────────────────────────────────────────────────┐           │
│   │         Token Layer                                │           │
│   │  ┌──────────────┐  ┌──────────────┐  ┌─────────┐ │           │
│   │  │ Deposit      │  │ RWA Token    │  │ Yield   │ │           │
│   │  │ Receipt      │─►│ (ERC-3643)   │─►│ Distrib │ │           │
│   │  │ (ERC-4626)   │  │              │  │         │ │           │
│   │  └──────────────┘  └──────┬───────┘  └─────────┘ │           │
│   └─────────────────────────────┼─────────────────────┘           │
│                                 │                                  │
│   ┌─────────────────────────────▼─────────────────────┐           │
│   │         Oracle & Attestation Layer                 │           │
│   │  NAV Oracle │ Risk Oracle │ Reserve Attestation   │           │
│   └────────────────────────────────────────────────────┘           │
│                                                                    │
│   ┌────────────────────────────────────────────────────┐          │
│   │         Governance Layer                             │          │
│   │  Multi-sig (5/9) │ Timelock (24-72h) │ Constitutional│         │
│   │                                          Limits      │          │
│   └────────────────────────────────────────────────────┘          │
└────────────────────────────────────────────────────────────────────┘
```

## Module Descriptions

**Identity Registry.** The on-chain registry of verified investor wallets. Each entry binds a wallet address to a verified KYC or KYA identity, the eligibility status (AI/II), the jurisdictional classification (resident/non-resident of restricted jurisdictions), and the expiration of the verification. The Identity Registry is the gatekeeper for all token transfers.

**Compliance Module.** A pre-trade compliance check invoked on every token transfer. The module verifies (a) sender and receiver are both in the Identity Registry with valid status, (b) lock-up period has elapsed where applicable, (c) sender and receiver are not on the protocol's sanctions list, (d) jurisdictional restrictions are satisfied, and (e) any product-specific transfer rules are met. A failed check reverts the transfer.

**Jurisdiction Modules.** Per-asset-jurisdiction rule sets that the Compliance Module consults during transfer evaluation. The Korea module, currently the only active module, configures restrictions specific to Korean asset products (e.g., Korean resident exclusion). Future jurisdiction modules — Japan, Vietnam, Thailand — are deployed as new asset categories are launched, without modifying the core Compliance Module.

**Token Layer.** Three token types serve different stages of the investor lifecycle:

- **Deposit Receipt (ERC-4626)**: Issued upon stablecoin deposit, before final RWA token issuance. Non-transferable. Burned at the moment of RWA token issuance.

- **RWA Token (ERC-3643 framework, ERC-7943 uRWA interface)**: The primary asset token. Represents beneficial interest in the VCC sub-fund. Subject to all compliance gating. The token exposes the ERC-7943 uRWA interface (finalized May 2026) for vendor-neutral transfer validation, freezing, and enforcement actions, implemented within the ERC-3643 compliance framework.

- **Distribution entitlements**: Per-cycle claims against the register as it stood at a stated record block. Entitlement is derived from token balances rather than supplied by the issuer, and a cycle cannot pay until the sum of the snapshot equals total supply at that block — so an incomplete holder list is unusable rather than merely wrong. Distributions are paid in the settlement currency, never in fund units.

**Oracle & Attestation Layer.** Provides on-chain access to off-chain truths.

- **NAV Oracle**: Publishes the latest NAV per RWA token, updated on the product's NAV cadence (monthly or event-based). Each NAV update is signed by the LFMC, OmniFlow, and the independent valuer.

- **Risk Oracle**: Publishes standardized risk metrics per asset (see Risk Oracle Standard).

- **Reserve Attestation**: Periodic attestations that the on-chain RWA token supply matches the VCC sub-register, signed by the LFMC and the Big 4 auditor.

**Governance Layer.** Controls protocol parameters that are not constitutional.

- **5-of-9 multi-signature** for routine administrative actions

- **24-hour timelock** for parameter changes (transfer fees, oracle update authorities)

- **72-hour timelock** for contract upgrades

- **Constitutional limits** enforced by immutable code: supply invariant, AI/II gating, and burn-and-reissue exclusivity cannot be modified by any role

## Token Lifecycle

The lifecycle of an OmniFlow RWA token, from issuance to redemption, follows a defined state machine:

```
[ISSUED] ──────► [LOCKED]   (6-month issuer-imposed restriction)
│
▼
[ACTIVE]    (transferable to qualified investors)
│
┌───────────┼───────────┐
▼           ▼           ▼
[SECONDARY]  [BUYBACK]   [REFINANCE]
transfer    by issuer   cash-out
│           │           │
└───────────┼───────────┘
▼
[REDEEMED]  (at maturity, asset sale, or redemption)
│
▼
[BURNED]   (token destroyed; cap table reconciled)
```

State transitions are enforced by the smart contracts and produce on-chain events for full audit traceability.

## Upgrade Mechanism

OmniFlow uses the UUPS (Universal Upgradeable Proxy Standard) pattern for upgradeable contracts, with the upgrade authority controlled by the governance layer. Upgrade history, including the proposing transaction, the timelock period, the executing transaction, and the new implementation hash, is recorded on-chain.

Constitutional limits are implemented in immutable contract code that the upgrade mechanism cannot reach. The list of constitutional limits is published in the smart contract repository and any change to that list would require redeploying the protocol from genesis.

## Security Posture

- **Audits**: At least two independent firms audit each production contract before mainnet deployment.

- **Formal verification**: Critical invariants (supply, compliance gating) are formally verified using Certora or equivalent.

- **Bug bounty**: Continuous program through Immunefi with payouts up to USD 500,000 for critical findings.

- **Key management**: Multi-signature keys held in HSMs distributed across multiple geographies and counterparty types (no single failure point).

- **Monitoring**: 24/7 anomaly detection on all production contracts with automated freeze on detected anomalies pending governance review.

See Smart Contract Audits for current audit status and Smart Contract Addresses for deployment details.
