# Investment Flow

This page describes the settlement workflow model: the sequence of steps that carries capital from a subscription to a fund token, and the SLA target attached to each. It is a model with a partial implementation. The on-chain steps run today on the **Base Sepolia testnet**; the off-chain steps are recorded by an operator workflow tracker and have never been executed against a live counterparty, because no counterparty is engaged. Read every step below as a specification, not as a description of operations in progress.

The description uses the only product open in this build — Korea Logistics Income, Tier 2, on testnet — for concrete illustration. The same pattern is intended to carry to further jurisdictions and asset categories.

## The 00–08 Workflow

```
[00] Product onboarding               → T+30
│       (sourcing, diligence, product upload — once per product)
▼
[01] Customer onboarding              → T+2 to T+5
│       (KYB / eligibility, SFA §275 consent, AML/CFT screening)
▼
[02] Payment in                       → T+0
│       (settlement token received at the receiving wallet)
▼
[03] Certificate issue                → T+1 to T+2
│       (ERC-4626 deposit certificate, non-transferable) — ON CHAIN
▼
[04] FX and deposit                   → T+2 to T+3
│       (settlement token → USD; deposit to the fund account)
▼
[05] Remittance                       → T+1 to T+2
│       (cross-border transfer; AML explanatory pack)
▼
[06] Capital call                     → T+3 to T+5
│       (USD → local currency; foreign investment filing; LP contribution)
▼
[07] RWA issue                        → T+5 to T+7
│       (certificate redeemed; ERC-7943 fund token issued) — ON CHAIN
▼
[08] Distribution (recurring)         → Per product schedule
```

Steps 02 through 07 carry a combined target of **12 to 19 calendar days**, payment received to token issued. First-time customer onboarding (step 01) is **2 to 5 days** and is reported separately, because it happens once per investor rather than once per subscription. Steps 04, 05 and 06 apply to the inbound-foreign route only; a domestic-currency deal has no conversion, no wire and no foreign-investment filing to make.

Elapsed time is counted in calendar days in this build. A live deployment would count business days per jurisdiction.

## Where the Demonstration Stops

The demo agent advances the workflow to step 04 and halts there. Steps 04 through 06 require outcomes that only a human counterparty can produce — a conversion confirmation, a remittance message, a foreign-investment filing receipt — and the agent will not write an outcome it cannot source.

That halt is enforced by the off-chain workflow tracker and by the demo script. It is **not** enforced by the smart contracts. `RwaToken.issue()` carries no access control, so a wallet that holds a deposit certificate and passes the eligibility registry could in principle issue itself fund tokens on chain without any of the intervening steps having occurred. Closing that gap — binding the on-chain issue to off-chain workflow state — is future work and is not built.

## Step-by-Step Detail

**Step 00 — Product onboarding.** Sourcing and due diligence on the asset, an NDA with a partner asset manager, and upload of the product to the platform. This runs once per product, before any investor is admitted. It is recorded, not executed, in this build.

**Step 01 — Customer onboarding.** The prospective investor completes KYB (corporate entities) or KYC (individuals), AI/II eligibility verification, AML/CFT screening (OFAC, UN, EU sanctions; PEP; adverse media), and signs the SFA §275 acknowledgment. A live deployment would run identity verification, sanctions screening and document forensics through licensed vendors. This build records a decision only. See Onboarding & KYB.

**Step 02 — Payment in.** The investor transfers the settlement token from their registered wallet to the receiving wallet, and the transaction is recorded. On testnet the settlement token is `MockUSDC`, a mock ERC-20 deployed for this demonstration — it is not Circle USDC and it carries no value. A live deployment would receive into a licensed payment institution's wallet under that institution's own custody controls. No such institution is engaged.

**Step 03 — Certificate issue.** The deposit contract issues an ERC-4626 deposit certificate to the investor's wallet, representing the claim between payment and fund token issuance. The certificate is non-transferable and is redeemed at issuance. **This step executes on chain**, on Base Sepolia, in this build.

**Step 04 — FX and deposit.** Conversion of the settlement token to USD and deposit to the fund account, performed by a payment institution and a fund manager. Inbound-foreign route only. This is where the demonstration halts.

**Step 05 — Remittance.** Cross-border transfer by a remitting bank, accompanied by an AML explanatory pack. Inbound-foreign route only.

**Step 06 — Capital call.** A receiving bank in the asset jurisdiction converts USD to local currency; a partner asset manager files the foreign capital inflow notification required locally — for a Korean asset this is the Foreign Investment Promotion Act (FIPA) filing — and local currency is committed as LP capital to the local asset-holding vehicle. Inbound-foreign route only.

**Step 07 — RWA issue.** The fund interest is recorded by an administrator, then in a single on-chain transaction the deposit certificate is redeemed and the corresponding **ERC-7943 (uRWA)** fund token is issued to the investor's wallet. The multi-day SLA target covers the administrator's recording; the on-chain leg settles in one transaction. **This step executes on chain**, on Base Sepolia, in this build.

**Step 08 — Distribution.** Asset income flows up the structure and is paid out to holders. Distribution mechanics are described in Yield Distribution. No distribution has been paid.

## Document Slots

Each step carries document slots that must be filled before the step can be completed. The workflow tracker defines them; the slots are empty in this build, because the steps that would produce the documents have not been run.

| **Step** | **Document slots** |
| --- | --- |
| 00 Product onboarding | Information Memorandum; Term Sheet; NDA |
| 02 Payment in | On-chain receipt |
| 04 FX and deposit | Partner transaction confirmation |
| 05 Remittance | Remittance message; AML explanatory pack |
| 06 Capital call | Foreign investment registration; LP contribution agreement |
| 08 Distribution | Distribution statement; Payment confirmation |

Steps 03 and 07 record a transaction hash rather than a document, because they execute on chain.

## Counterparty Roles

The workflow assigns each step an owner by role: a compliance desk, a payment institution, a fund manager, a remitting bank, a receiving bank in the asset jurisdiction, a partner asset manager, a fund administrator.

**None of these roles is filled.** No payment institution, fund manager, asset manager, bank, administrator or auditor has been engaged, and no agreement with any such party exists. The roles describe what a live deployment would require, which is also why the demonstration does not advance past step 04: there is no counterparty to produce the outcomes those steps record, and the agent will not write an outcome it cannot source.
