# Yield Distribution

This page describes how yield distributions are designed to work: paid in the settlement currency directly to the holder's registered wallet, with timing and amount set by product terms and underlying asset performance.

**No distribution has been paid.** There is no distribution contract deployed, no asset generating income, and no holder to pay. What follows is the distribution model, which is worth reading for the rules it commits to rather than for any payment it describes.

## Distribution Frequency

| **Tier** | **Product** | **Frequency** |
| --- | --- | --- |
| Tier 1 | Listed REIT Income | Not set |
| Tier 2 | Korea Logistics Income | Semi-annual, as modelled |
| Tier 3 | Senior Development Credit | Not set. The design contemplates deal-by-deal distribution at realization |
| Tier 4 | Opportunistic Credit | Not set. The design contemplates deal-by-deal distribution at realization |

Only Tier 2 is open in this build, and only on testnet, and its frequency is a modelled term rather than a schedule anything has been paid on. Tier 1 is documented but not open, and its terms are not set. Tiers 3 and 4 are pipeline. No yield target is published for Tier 1, 3 or 4.

Specific distribution dates would be published in advance in a product distribution calendar. No calendar exists.

## Distribution Calculation

The model computes a per-token distribution amount for each cycle as follows. Nothing computes this today: there is no distributable income, no holder and no deployed contract.

Per-Token Distribution =

(Distributable Income from local fund, in local currency)

× (FX rate local currency → USD at distribution date)

× (1 − Withholding tax under applicable tax treaty)

× (1 − Fund-level operating expenses)

÷ (Total Outstanding RWA Tokens for the Product)

For the Korean asset, the local currency is KRW and the applicable withholding rate is **15%** — the Korea-Singapore treaty rate, inclusive of local income tax, subject to treaty benefit eligibility. For future asset categories, the equivalent local currency and treaty rates apply.

A live deployment would have this calculation performed by a fund accounting function, reviewed by a licensed fund manager, and audited annually. None of those parties is engaged, no audit of any kind has been performed, and no distribution statement has been produced.

## Distribution Mechanics

The model is pull-based. No distribution contract is deployed, so the sequence below is a specification the implementation would have to satisfy, not a description of code running on chain. For each cycle:

1. Publishes the record block and the per-unit amount **before** the record instant, so any transfer can be priced with the entitlement known

1. Reconstructs the register as it stood at the record block, and reconciles it: the sum of holder balances must equal total supply at that block, exactly. A cycle that does not reconcile cannot proceed

1. Funds the distribution contract with the aggregate amount in the settlement stablecoin, in the same transaction that opens the cycle — an unfunded cycle does not exist

1. Records each holder's entitlement, derived from their balance at the record block rather than supplied by the issuer

1. Notifies holders that distributions are claimable

**Entitlement is determined by the holder of record at the record block, with no time weighting.** This is the rule every transferable fund uses. An investor who acquires units after the record block receives nothing for that period and should have paid a price reflecting that; an investor who sells before it keeps the distribution, having already been compensated through the sale price. The obligation this creates is disclosure ahead of the record instant, which is why the first step above comes first.

The specification commits to claims being open-ended: an investor could claim at any time, unclaimed distributions would remain claimable, and there would be no expiry and no sweep to the issuer. No claim can be made today, because no distribution contract is deployed.

**Distributions are paid in the settlement currency only.** They are never paid in fund units. A distribution paid in units would be a fresh issuance of a security rather than a payment of income: it would compound the position instead of distributing it, each payment would arrive as a newly restricted parcel, and every recipient would have to be re-checked against the eligibility register at every payment date. Investors wishing to reinvest do so through a new subscription, and the resulting units carry their own 180-day restriction because a reinvestment is a new issuance.

A push-based option — delivery without a manual claim, batched after each cycle — is part of the design. It is not built.

## Distribution Currency

The design has each investor specify a preferred distribution currency at onboarding, with payment in that currency where operationally feasible and any substitution disclosed in the distribution statement. Multi-stablecoin settlement is not integrated; see Stablecoin Settlement.

## Tax Treatment

Distributions would be paid net of applicable withholding tax in the asset jurisdiction. For the Korean asset this means **15% withholding** under the Korea-Singapore tax treaty, inclusive of local income tax, applicable where the beneficial owner of the income qualifies for treaty benefits. Without treaty relief the domestic rate of 22% applies, which is the sensitivity case in the yield derivation. Investors are responsible for their own income tax compliance in their jurisdiction of tax residency.

Treaty-benefit documentation, Singapore tax-exemption claims under IRAS §13(8) and §13(12), and FATCA/CRS information returns would all be part of a live deployment's obligations. None is being performed, because there are no investors and no distributions.

Detailed tax treatment for each investor situation is the subject of individual tax advisory; OmniFlow does not provide tax advice.

## Variability of Distributions

Only one yield figure is published: an **illustrative net distribution yield of 5.50%** for Tier 2, derived from a 5.80% going-in cap on Seoul Capital Area logistics, 60% LTV interest-only senior debt at 4.10%, fund fees assumed at 0.75% of GAV, and 15% Korean withholding — 8.35% levered cash-on-cash, 6.47% after fees, 5.50% after withholding. It falls to approximately 5.0% if withholding reverts to the 22% domestic rate. FX hedge carry of +75 to 100 bp is excluded. It is illustrative and has never been earned or paid.

Actual distribution amounts would vary from period to period and from that figure, based on:

- Underlying asset performance (occupancy, rent collection, loan repayment, asset sale outcomes)

- FX movements between the asset jurisdiction's local currency and USD

- Operating expenses at the fund and asset level

- Reserves established for capital expenditure or risk mitigation

- Timing of underlying cash flow events relative to distribution cycle dates

Actual distributions would differ from the illustrative figure, sometimes materially, and may be zero in particular cycles.

## Distribution Statements

The design provides each holder, each cycle, with a distribution statement detailing:

- Per-token distribution amount and total distribution to the investor

- Distribution currency and exchange rates applied

- Withholding tax applied

- Operating expenses charged

- Reconciliation to the prior NAV and the post-distribution NAV

- Any exceptional adjustments

Statements would be delivered through the investor application. On-chain auditability of a cycle depends on a distribution contract, which is not deployed; the append-only event log that exists today records workflow steps, not payments.
