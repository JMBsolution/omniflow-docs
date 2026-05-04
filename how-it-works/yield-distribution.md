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

Distributions are executed via a pull-based mechanism. For each distribution cycle, OmniFlow:

1. Computes per-token distribution amounts and the corresponding investor allocations

1. Generates a Merkle tree mapping investor wallets to distribution amounts

1. Posts the Merkle root on-chain to the distribution contract

1. Funds the distribution contract with the aggregate distribution amount in the appropriate stablecoin

1. Notifies investors that distributions are claimable

Investors may then claim their distribution at any time by submitting a claim transaction to the distribution contract. Unclaimed distributions remain in the contract indefinitely; there is no expiry.

For investors who prefer push-based distribution (delivery without manual claim), an opt-in standing instruction is available. Push distributions are executed in batches following each distribution cycle.

## Distribution Currency

Each investor specifies a preferred distribution currency at onboarding (USDT, USDC, or USD1). Distributions are paid in the preferred currency where operationally feasible. Where conversion is required (for example, if the underlying USD-to-stablecoin conversion is paused for a specific stablecoin), distributions are paid in the next-available preferred currency and the variation is disclosed in the distribution statement.

## Tax Treatment

Distributions to investors are paid net of applicable withholding tax in the asset jurisdiction. For current Korean asset products, this means a 10% withholding under the Korea-Singapore tax treaty, applicable where the investor's beneficial owner of the income qualifies for treaty benefits. Investors are responsible for their own income tax compliance in their jurisdiction of tax residency.

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
