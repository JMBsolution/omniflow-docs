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

For the Korean asset the local currency is KRW, and the withholding rate is published as a **band — 10% / 15% / 22% — with 15% as the central case.** Which rate applies is a structuring question that is not yet settled, and stating a single figure would imply a certainty we do not have.

- **10%** — Article 10(2)(a) of the Korea-Singapore treaty, available only where the recipient is a **company directly owning at least 25% of the capital** of the company paying the dividend. Reaching it requires a **company-form Korean fund** and a holding at or above that threshold. That is the structure we intend to form, so 10% is the design target — not the published assumption.
- **15%** — Article 10(2)(b), the portfolio rate, inclusive of Korean local income tax. **This is the central case in every published bridge**, because it is what applies if the 25% test is not met.
- **22%** — the Korean domestic rate (20% plus a 10% local surtax) where treaty relief is unavailable or is denied pending a refund claim.

Three dependencies sit behind this band and none is resolved. **First**, whether a distribution from a *trust-form* Korean fund is an Article 10 "dividend paid by a company" at all — the treaty defines a company as a body corporate, and trust-form holders take beneficiary certificates rather than capital. If it falls outside Article 10 it falls to Other Income, which carries no source-state cap. **Second**, whether a Singapore VCC sub-fund is accepted as the beneficial owner: Korea's default is to look through an offshore investment vehicle to its investors, in which case **there is no single net figure across a register** — holders resident in different jurisdictions can face different withholding on the same distribution, and any quoted net applies only to a single named holder profile. **Third**, whether Korean corporate tax applies at the fund level before withholding at all; it does unless the fund satisfies the dividend-paid-deduction distribution test, and a failure there would dwarf every rate above.

**Preliminary structuring advice, 2026-08-19.** A first pass with a Korean structuring adviser gives working answers to all three, and they point the same way — toward a **company-form fund (회사형 REF)** rather than a trust.

- **Character.** A company-form fund is expected to fall under the treaty's dividend article rather than Other Income, which is the difference between a capped rate and no source-state cap at all. This is the primary reason to prefer the company form.
- **The 10% rate** is formally reachable with a company-form fund and a holding at or above the 25% threshold, and beneficiary interests are generally recognised as capital for that test — but it requires documentation that does not yet exist.
- **Beneficial ownership is not automatic.** A Singapore VCC is not accepted as beneficial owner by default. It requires an IRAS tax residency certificate renewed annually, plus evidence of genuine substance. This is an operating obligation, not a one-time filing.
- **Entity-level tax can be eliminated.** A company-form fund that distributes at least 90% of distributable income, and actually pays it, is expected to reach a 0% corporate rate. One structural condition attaches: **any disposal performance fee must be paid at the holding-vehicle level through the distribution waterfall, not charged inside the fund** — a fee charged inside the fund reduces distributable income and puts the 90% test, and therefore the 0% rate, at risk.

None of this is yet documented, no entity is formed, and the adviser's answers are preliminary rather than a formal opinion. **So the published central case stays 15%, and 10% is recorded as the design target rather than an assumption.** Every published yield carries the band and not a point estimate until the structure exists and the documentation is in place. For future asset categories, the equivalent local currency and treaty rates apply.

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

Only one yield figure is published: an **illustrative net distribution yield of 3.43%** for Tier 2, derived from a 5.32% going-in cap on Seoul Capital Area logistics and 60% LTV interest-only senior debt at 4.93% all-in — both RSquare Q2 2026, one source and one quarter — with fund fees assumed at 0.75% of GAV and 15% Korean withholding: 5.91% levered cash-on-cash, 4.03% after fees, 3.43% after withholding. Across the withholding band it is 3.63% at 10% and 3.14% at 22%. FX hedge carry is excluded and no hedge is in place. It is illustrative and has never been earned or paid. **This figure was corrected on 2026-08-19 from a previously published 5.50%, which mixed a 2025 cap rate with a policy-rate debt proxy and overstated the yield by roughly 207 basis points.**

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
