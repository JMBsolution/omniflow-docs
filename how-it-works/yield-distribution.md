# Yield Distribution

Yield distributions are paid in stablecoin directly to the investor's registered wallet. Distribution timing, amount, and currency are determined by product terms, underlying asset performance, and investor preferences set at onboarding. The same distribution mechanics apply across all product tiers and asset categories.

## Distribution Frequency

| **Tier** | **Frequency** |
| --- | --- |
| Tier 1 — Prime Income | Semi-annual |
| Tier 2 — Growth Plus | Semi-annual |
| Tier 3 — Alpha Opportunity | Deal-by-deal at realization |
| Tier 4 — Core REIT | Quarterly |

Specific distribution dates within each cycle are published in advance in the product distribution calendar, available through the investor dashboard.

## Distribution Calculation

For each distribution cycle, OmniFlow computes the per-token distribution amount as follows:

Per-Token Distribution =

(Distributable Income from local fund, in local currency)

× (FX rate local currency → USD at distribution date)

× (1 − Withholding tax under applicable tax treaty)

× (1 − Fund-level operating expenses)

÷ (Total Outstanding RWA Tokens for the Product)

For current Korean asset products, the local currency is KRW and the applicable withholding rate is 10% under the Korea-Singapore tax treaty (subject to treaty benefit eligibility). For future asset categories, the equivalent local currency and tax treaty rates apply.

The calculation is performed by OmniFlow's fund accounting team, reviewed by the partner LFMC, and audited annually by the Big 4 auditor. The detailed calculation methodology and any exceptional adjustments are disclosed in each distribution statement.

## Distribution Mechanics

Distributions are executed via a pull-based mechanism. For each cycle, OmniFlow:

1. Publishes the record block and the per-unit amount **before** the record instant, so any transfer can be priced with the entitlement known

1. Reconstructs the register as it stood at the record block, and reconciles it: the sum of holder balances must equal total supply at that block, exactly. A cycle that does not reconcile cannot proceed

1. Funds the distribution contract with the aggregate amount in the settlement stablecoin, in the same transaction that opens the cycle — an unfunded cycle does not exist

1. Records each holder's entitlement, derived from their balance at the record block rather than supplied by the issuer

1. Notifies investors that distributions are claimable

**Entitlement is determined by the holder of record at the record block, with no time weighting.** This is the rule every transferable fund uses. An investor who acquires units after the record block receives nothing for that period and should have paid a price reflecting that; an investor who sells before it keeps the distribution, having already been compensated through the sale price. The obligation this creates is disclosure ahead of the record instant, which is why the first step above comes first.

Investors may claim at any time. Unclaimed distributions remain claimable; there is no expiry and no sweep to the issuer.

**Distributions are paid in the settlement currency only.** They are never paid in fund units. Paying in units would re-arm the transfer restriction on every recipient at every payment, which over a semi-annual cycle would leave holdings permanently restricted. Investors wishing to reinvest do so through a new subscription, and the resulting units carry a new restriction because a reinvestment is a new acquisition.

For investors who prefer push-based distribution (delivery without manual claim), an opt-in standing instruction is available. Push distributions are executed in batches following each distribution cycle.

## Distribution Currency

Each investor specifies a preferred distribution currency at onboarding (USDT, USDC, or USD1). Distributions are paid in the preferred currency where operationally feasible. Where conversion is required (for example, if the underlying USD-to-stablecoin conversion is paused for a specific stablecoin), distributions are paid in the next-available preferred currency and the variation is disclosed in the distribution statement.

## Tax Treatment

Distributions to investors are paid net of applicable withholding tax in the asset jurisdiction. For current Korean asset products, this means a 15% withholding under the Korea-Singapore tax treaty, inclusive of local income tax and applicable where the investor's beneficial owner of the income qualifies for treaty benefits. Investors are responsible for their own income tax compliance in their jurisdiction of tax residency.

For institutional investors qualifying for tax-exempt status in Singapore (under IRAS §13(8) and §13(12) where applicable), OmniFlow assists with the documentation required to claim treaty benefits at source.

For investors in jurisdictions with FATCA or CRS reporting requirements, OmniFlow files the required information returns with the relevant tax authorities.

Detailed tax treatment for each investor situation is the subject of individual tax advisory; OmniFlow does not provide tax advice.

## Variability of Distributions

Actual distribution amounts will vary from period to period and from product targets, based on:

- Underlying asset performance (occupancy, rent collection, loan repayment, asset sale outcomes)

- FX movements between the asset jurisdiction's local currency and USD

- Operating expenses at the fund and asset level

- Reserves established for capital expenditure or risk mitigation

- Timing of underlying cash flow events relative to distribution cycle dates

Target yields communicated at subscription represent OmniFlow's good-faith expected range. Actual distributions will differ, sometimes materially, and may be zero in particular cycles.

## Distribution Statements

For each distribution cycle, each investor receives a distribution statement detailing:

- Per-token distribution amount and total distribution to the investor

- Distribution currency and exchange rates applied

- Withholding tax applied

- Operating expenses charged

- Reconciliation to the prior NAV and the post-distribution NAV

- Any exceptional adjustments

Distribution statements are delivered through the investor dashboard and are also auditable on-chain through the distribution contract event log.
