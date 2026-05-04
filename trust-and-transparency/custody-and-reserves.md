# Custody & Reserves

This page describes the custody arrangements for OmniFlow's underlying assets, the verification mechanisms that confirm reserves match the on-chain RWA token supply, and the disclosure cadence for reserve attestations.

## Custody Architecture

OmniFlow does not custody investor assets directly. Custody is distributed across regulated counterparties at each stage of the asset chain.

```
CUSTODY DISTRIBUTION
Stablecoin (in transit)
│
▼
┌──────────────────────────────────────┐
│ MPI Partner (DPT-licensed custody)   │
│ Hot wallets and institutional cold   │
│ storage during settlement window     │
└────────────────────┬─────────────────┘
│ Converted to USD
▼
┌──────────────────────────────────────┐
│ Singapore Bank (Tier 1)              │
│ USD operating account, OmniFlow VCC  │
│ name                                 │
└────────────────────┬─────────────────┘
│ SWIFT to Korea
▼
┌──────────────────────────────────────┐
│ Korean Bank (Tier 1)                 │
│ KRW account, Korean REF name         │
└────────────────────┬─────────────────┘
│ Asset acquisition
▼
┌──────────────────────────────────────┐
│ Korean Real Estate / Asset Custody   │
│ Real estate: title held by Korean    │
│ Trust Company (KSD-licensed)         │
│ Loans: held in custodian-attested    │
│ form per Korean Capital Markets Act  │
└──────────────────────────────────────┘
```

## Custody Counterparties

### Stablecoin Custody (Pre-Settlement)

During the brief window between investor deposit and conversion to USD, stablecoins are held by the MPI partner in licensed custody arrangements consistent with MAS DPT requirements.

|  |  |
| --- | --- |
| **Custody provider** | [TBD — MPI partner] |
| **Custody form** | Institutional cold storage (cold-warm tiered) |
| **Insurance** | [TBD — provider's institutional crime insurance] |
| **Typical custody duration** | T+0 to T+3 (deposit to conversion) |

### USD Custody (Singapore)

|  |  |
| --- | --- |
| **Custody provider** | [TBD — Tier 1 Singapore bank] |
| **Account type** | Corporate operating account, OmniFlow VCC sub-fund name |
| **Account segregation** | Per sub-fund segregated accounts |
| **Reconciliation** | Daily by OmniFlow finance team |

### KRW and Korean Asset Custody

|  |  |
| --- | --- |
| **KRW custody provider** | [TBD — Tier 1 Korean bank] |
| **Real estate title custody** | Korean Trust Company (Korean Securities Depository-licensed) |
| **Loan position custody** | Custodian-attested per Korean Capital Markets Act |
| **Reconciliation cadence** | Daily for cash; per-event for asset positions |

## Reserve Verification

OmniFlow operates a formal Proof-of-Reserve mechanism to confirm that the on-chain RWA token supply is fully backed by the corresponding sub-fund interests in the VCC sub-register.

### Verification Process

```
RESERVE VERIFICATION CYCLE
[1] On-chain supply snapshot
│
▼
[2] VCC sub-register snapshot (LFMC-attested)
│
▼
[3] Reconciliation by OmniFlow finance team
│
▼
[4] LFMC counter-attestation
│
▼
[5] Big 4 auditor independent verification
│
▼
[6] On-chain attestation publication
- Snapshot Merkle root
- LFMC signature
- OmniFlow signature
- Auditor signature
- Timestamp
```

Each cycle produces an on-chain attestation that is independently verifiable through the Reserve Attestation contract.

### Verification Cadence

| **Verification Component** | **Cadence** |
| --- | --- |
| Internal reconciliation | Daily |
| LFMC counter-attestation | Monthly |
| Big 4 auditor verification | Quarterly |
| Comprehensive year-end audit | Annual |

### Attestation Schema

Each on-chain attestation publishes the following data:

| **Field** | **Description** |
| --- | --- |
| attestation_id | Unique identifier for the attestation |
| as_of_timestamp | Effective date of the snapshot |
| total_token_supply | Aggregate on-chain RWA token supply across all products |
| sub_register_balance | Aggregate VCC sub-register balance |
| discrepancy_amount | Difference (target: zero) |
| lfmc_signature | LFMC EIP-712 signature |
| omniflow_signature | OmniFlow operations EIP-712 signature |
| auditor_signature | Big 4 auditor signature (quarterly cycles only) |

Discrepancy detection triggers an immediate freeze on token issuance and a 48-hour investigation window before further operations resume. Any unresolved discrepancy is disclosed under the standard in Trust & Security.

## Reserve Attestation Archive

Completed reserve attestations are archived on this page in perpetuity.

| **Attestation Date** | **Total Supply** | **Sub-Register Balance** | **Discrepancy** | **Auditor** | **Report Link** |
| --- | --- | --- | --- | --- | --- |
| [TBD] | [TBD] | [TBD] | [TBD] | [TBD] | [TBD] |

*No attestations available — protocol is in pre-deployment status. Attestation cycle begins with Phase 1 mainnet launch.*

## Insurance and Risk Mitigation

| **Coverage** | **Provider** | **Coverage Limit** | **Status** |
| --- | --- | --- | --- |
| Stablecoin custody (MPI partner) | [TBD] | [TBD] | [TBD — placeholder pending Phase 1] |
| Real estate property and liability | [TBD — per asset] | Per Korean property insurance standard | [TBD] |
| Professional liability (LFMC) | [TBD] | Per MAS LFMC requirements | [TBD] |
| Cyber and smart contract | [TBD] | [TBD] | [TBD — being evaluated] |

Insurance arrangements supplement, but do not replace, the architectural and operational controls described elsewhere in this documentation. Insurance coverage is not a guarantee of recovery and is subject to policy terms.

## Smart Contract Reserve

OmniFlow operates an on-chain Safety Reserve for select scenarios:

- Slashed bonds from KYA violations (see KYA Framework)

- Operational reserves for Layer 5 issuer buyback (see Exit & Redemption)

- Bug bounty payouts (see Smart Contract Audits)

|  |  |
| --- | --- |
| **Safety Reserve address** | [TBD] |
| **Funding source** | Protocol revenue allocation, slashed bonds |
| **Withdrawal authority** | Governance multi-signature with 72-hour timelock |
| **Reserve balance** | [TBD — published per attestation cycle] |

Safety Reserve balance is included in the periodic Reserve Attestation cycle.
