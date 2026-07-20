# Architecture Overview

This page describes OmniFlow's protocol architecture at a level appropriate for technical due diligence and integration planning. Detailed contract interfaces are documented in the smart contract repository; this page provides the conceptual map.

Read it with one distinction in mind. A subset of this architecture is deployed and exercised end to end on **Base Sepolia testnet**; the rest is design. Each section below states which it is. Nothing described here runs on mainnet, and no real asset, fund vehicle or counterparty stands behind any of it.

## Design Principles

OmniFlow's architecture rests on five design principles, each chosen to address a specific class of risk that has surfaced in prior on-chain RWA deployments.

**1. Off-chain truth, on-chain mirror.** The intended legal source of truth for ownership is a fund register maintained off chain by a licensed fund manager. The on-chain RWA token is designed as a cryptographic mirror of that register, updated through a defined reconciliation process. The purpose of the separation is that token holders' legal rights would be anchored in established corporate law rather than dependent solely on smart contract state. Only the on-chain half of this model exists today: there is no fund vehicle, no manager, and no register to reconcile against.

**2. Eligibility enforced in the contracts.** Eligibility gating and the transfer lock-up are enforced by the deployed contracts on Base Sepolia testnet, not by external policy. A transfer to a wallet that is not marked eligible in the EligibilityRegistry, or of tokens still inside the 180-day lock-up, reverts on chain regardless of the sender's intent. Issuance is not gated the same way — see Known Gaps.

**3. Single source of truth for token supply.** RWA tokens exist on a single primary issuance chain. Other chains may serve as deposit rails (where investors send stablecoins) but do not hold native RWA tokens. This eliminates the lock-and-mint bridge attack surface that has caused over USD 2 billion in losses across the industry. See Cross-Chain Architecture.

**4. Modular jurisdiction support (designed).** The compliance engine is designed to decompose into per-jurisdiction modules, so that adding a new asset category would require deploying a new jurisdiction module without modifying core token or settlement logic. No jurisdiction module has been built. The deployed registry is a single global eligibility list with no jurisdictional dimension.

**5. Non-upgradeable core.** The deployed contracts have no proxy and no upgrade path. The lock-up duration, the settlement asset and the registry address are set at construction and are immutable; changing any of them means redeploying and reissuing. This is a deliberate trade: it removes the upgrade key as an attack surface, and it means a bug cannot be patched in place.

## System Module Map

What is deployed on Base Sepolia testnet:

```
┌──────────────────────────────────────────────────────────────┐
│           ON-CHAIN — BASE SEPOLIA TESTNET (DEPLOYED)         │
│                                                               │
│   ┌──────────────────────────────────────────────────┐       │
│   │  EligibilityRegistry                              │       │
│   │  owner-maintained address allow-list              │       │
│   └────────────────────┬─────────────────────────────┘       │
│                        │ consulted on transfer & issuance     │
│   ┌────────────────────▼─────────────────────────────┐       │
│   │  DepositCertificate  (ERC-4626, non-transferable) │       │
│   │  issued on mUSDC deposit; burned at issuance      │       │
│   └────────────────────┬─────────────────────────────┘       │
│                        │                                      │
│   ┌────────────────────▼─────────────────────────────┐       │
│   │  RwaToken  (ERC-20 + ERC-7943 uRWA)               │       │
│   │  180-day lock-up from issuance                    │       │
│   │  freeze / forced transfer / pause — owner only    │       │
│   └───────────────────────────────────────────────────┘       │
│                                                               │
│   MockUSDC — a mock settlement token, not Circle USDC        │
└──────────────────────────────────────────────────────────────┘
```

Designed but **not built**: the off-chain register and its reconciliation process, per-jurisdiction compliance modules, a distribution entitlement mechanism, the NAV and risk oracles, reserve attestation, and a multi-signature or timelocked governance layer. None of these exists as code or as an engaged counterparty.

## Module Descriptions

**EligibilityRegistry (deployed, testnet).** A mapping of wallet address to a boolean eligibility flag, set by the contract owner. It is consulted on every issuance and every transfer. It is not an identity registry: it does not bind a wallet to a verified identity record, does not carry an accreditation classification, does not carry a jurisdiction, and has no expiry. Whatever verification stands behind an entry happens off chain and leaves no on-chain trace beyond the flag itself.

**Transfer checks (deployed, testnet).** There is no separate compliance contract. The checks live in RwaToken and run on every transfer: sender and receiver both eligible, the transferred amount not frozen, the sender's lock-up elapsed, and the contract not paused. A failed check reverts with a reason. Sanctions screening and jurisdictional rules are not implemented on chain.

**Jurisdiction modules (not built).** Per-asset-jurisdiction rule sets that a compliance module would consult during transfer evaluation. This is a design for how new asset categories would be added; no module has been written, and the Korean-resident exclusion that applies to the global track is an off-chain policy, not an on-chain rule.

**Token layer.** Two token types are deployed; the third is designed.

- **DepositCertificate (ERC-4626, deployed on testnet)**: issued on deposit of the mock settlement token, before RWA token issuance. Non-transferable. Burned at the moment of RWA token issuance.

- **RwaToken (ERC-20 with the ERC-7943 uRWA interface, deployed on testnet)**: the asset token. It implements the ERC-7943 uRWA interface for vendor-neutral transfer validation, freezing and enforcement actions. It is **not** an ERC-3643 token and does not use the ERC-3643 framework. In the intended structure it would represent a beneficial interest in a fund vehicle; on testnet it represents nothing.

- **Distribution entitlements (designed, not built)**: per-cycle claims against the register as it stood at a stated record block, with entitlement derived from token balances rather than supplied by the issuer, and a cycle unable to pay until the sum of the snapshot equals total supply at that block — so an incomplete holder list would be unusable rather than merely wrong. No distribution contract has been deployed and no distribution has been paid.

**Oracle and attestation layer (not built).** The design calls for a NAV oracle publishing NAV per token on the product's cadence, a risk oracle publishing standardized per-asset metrics (see Risk Oracle Standard), and periodic attestation that on-chain supply matches the off-chain register. None of the three is deployed, and the signing parties each design assumes — a fund manager, an independent valuer, an auditor — are not engaged.

**Administration (deployed, testnet).** The deployed contracts are owned by a single deployer account. That owner can pause and unpause, freeze a holder's tokens, and execute a forced transfer. There is no multi-signature, no timelock and no governance process behind that key. A multi-signature and timelock arrangement is a design target for production; it is not a deployed control.

## Token Lifecycle

The intended lifecycle of an OmniFlow RWA token, from issuance to redemption:

```
[ISSUED] ──────► [LOCKED]   (180 days from issuance)
│
▼
[ACTIVE]    (transferable to eligible wallets)
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
[BURNED]   (token destroyed; register reconciled)
```

Only the first three states are implemented. Issuance, the 180-day lock-up and transfer between eligible wallets are enforced by the deployed contracts and emit on-chain events. The deployed RwaToken has no redemption or burn function, and no secondary market, buyback or refinance path exists. Everything below [ACTIVE] in the diagram is design.

## Upgrades

There is no upgrade mechanism. The deployed contracts are not behind a proxy and cannot be upgraded; a change to contract logic requires a fresh deployment and a reissuance of tokens to holders. Parameters fixed at construction — lock-up duration, settlement asset, registry address — are immutable.

## Security Posture

The deployed contracts have **not been audited**. No independent security review, no formal verification, and no bug bounty programme exists. The contracts build on OpenZeppelin implementations of ERC-20, ERC-4626, Ownable and Pausable, and are covered by the repository's own test suite, which is not a substitute for review.

Multi-firm audit and formal verification of supply and gating invariants are prerequisites we have set for any mainnet deployment. They have not been started.

### Known Gaps

**`RwaToken.issue()` has no access control.** Any wallet that is marked eligible in the registry and holds a deposit certificate can call `issue()` and mint itself fund tokens on chain. In the demonstration, the agent does not advance past workflow step 04 — steps 04 through 06 require human counterparties, and the agent will not write an outcome it cannot source. That halt is enforced by the off-chain operator workflow tracker and by the demo script. **It is not enforced by the smart contracts.** Closing this gap — restricting issuance to an authorized issuer role — is required future work and a precondition for any deployment outside testnet.

See Smart Contract Addresses for deployment details.
