# Korea Logistics Income (Tier 2)

Stable income from Korean commercial real estate, led by Seoul Capital Area logistics. Illustrative net distribution yield of approximately 3.43% per annum, before any currency hedge carry. The gross-to-net bridge is published in full below — the bridge, not the headline, is the number to read.

This is the one tier live in this build, and it is live as a **testnet demonstration on Base Sepolia**. No fund vehicle has been established, no asset has been acquired, and no subscription is open. The yield below is a model, not a record of anything paid.

> **Correction — 2026-08-19. This page previously published ≈5.50% net. The correct figure is ≈3.43%.**
>
> The earlier bridge took its cap rate from a 2025 comparable transaction and its debt cost from the Bank of Korea new-corporate-loan rate, used as a public proxy. Checked against a single source for a single quarter — RSquare Q2 2026 — that proxy is close for Seoul office (4.03% coupon) but not for logistics, where senior debt is 4.74% coupon and 4.93% all-in against a 5.32% cap. Mixing a 2025 cap with a policy-rate debt proxy **overstated the net yield by roughly 207 basis points.**
>
> We are publishing the corrected number rather than withdrawing the page, and stating plainly what it means: **at 3.43% this product does not clear a matched-tenor liquid alternative.** The Korean 10-year sovereign yields about 4.38% in KRW — same country, same currency, under the same buildings, daily liquid, no manager, no lock-up. A reader should require a substantial illiquidity premium over that before an unlisted, levered, single-asset position is worth holding, and this does not currently offer one.
>
> This is the second time a published figure of ours has moved against us on re-derivation; the first was the withholding rate, corrected from 10% to 15%. Both corrections were found by checking our own arithmetic against a single consistent source. That check is now a standing requirement: **a cap rate and a debt cost must come from the same source and the same quarter, or the bridge is not published.**

## What It Is

Korea Logistics Income is designed to invest in stabilized, income-producing logistics assets in the Seoul Capital Area, with selective exposure to other stabilized commercial property. It is the range's core direct-equity income tier: it sits above the listed-REIT tier on the risk ladder, concentrated and illiquid where a listed product is diversified and marked daily.

## Strategy

The strategy is to acquire direct equity positions or senior secured debt positions in assets with established tenants, long-duration leases, and verified rent rolls. Asset selection would prioritize properties with weighted average lease terms (WALT) of three years or more, occupancy rates above 95%, and credit-tenant rosters. No position has been acquired.

The fund is modelled with senior leverage at 60% LTV, interest-only — the same assumption the bridge below is built on. Yield is generated primarily from rental income and, where applicable, secured note coupons.

## Eligible Underlying Assets

| **Asset Type** | **Going-In Cap Rate** | **Basis** |
| --- | --- | --- |
| Seoul Capital Area logistics centres | 5.32% | RSquare Q2 2026 — one source and one vintage with the debt line below |
| Seoul prime office (CBD, GBD, YBD) | approximately 4.2% | Carried here only as the basis for the withdrawal described below |

Logistics leads the allocation for a specific reason. Korean senior debt for logistics is taken here at 4.93% all-in (RSquare Q2 2026), against a 5.32% logistics cap from the same source and the same quarter. That is a spread of 39 basis points, so leverage still adds — 5.32% unlevered becomes 5.91% at 60% LTV — but thinly. Seoul prime office does not clear at all: at a roughly 4.2% cap against a comparable debt cost, levered cash-on-cash moves by under 10 basis points across a 30% to 65% loan-to-value range, which is why that product was withdrawn.

That is not a hypothetical. A Seoul prime office product was withdrawn during yield re-derivation for exactly this reason: a 4.2% cap against a 4.10% debt cost cannot produce the target yield at any leverage. The asset was repositioned to logistics rather than carried at a number the bridge would not support. On 2026 data that withdrawal reason has not softened: it has widened.

## How the Yield Is Built

An illustrative bridge for a Seoul Capital Area logistics asset, modelled on a Singapore holding structure taking Korea–Singapore treaty relief, and stated so that it can be reproduced and challenged. No such vehicle has been established.

| **Line** | **Value** | **Basis** |
| --- | --- | --- |
| Going-in cap rate | 5.32% | RSquare Q2 2026 |
| Less senior debt interest, 60% LTV interest-only at 4.93% all-in | −2.96 pts of asset value | RSquare Q2 2026 logistics senior, all-in (coupon 4.74%) |
| **Levered cash-on-cash to the fund** | **5.91%** | (5.32 × 100 − 4.93 × 60) ÷ 40 |
| Less fund-level fees and expenses, 0.75% of gross asset value | −1.88 pts on equity | **Assumption — not independently sourced.** Korean fund fee schedules are not public |
| Pre-withholding distribution to the holding vehicle | 4.03% | |
| Less Korean withholding at the 15% treaty rate | −0.60 pts | Korea–Singapore double tax agreement, dividend article. The treaty rate is inclusive of Korean local income tax |
| **Illustrative net distribution yield** | **≈3.43%** | |
| Plus currency hedge carry, if hedged to USD | +75 to 100 bp | Analytical inference from the policy rate differential before cross-currency basis. Excluded from the yield above; no hedge is in place |

**Withholding sensitivity.** The rate is published as a band rather than a single figure, because which rate applies is a structuring question that is not yet settled. At the 10% rate — available only where the holder is a company directly owning at least 25% of the capital of a company-form fund — the net figure is 3.63%. At the 15% portfolio rate, the central case above, it is 3.43%. If treaty relief is unavailable and the domestic 22% rate applies, it is 3.14%. The full band is worth 49 basis points. Korea also looks through offshore investment vehicles to their investors by default, so a single net figure may not hold across a whole register; see Yield Distribution.

**What this bridge excludes.** Capital appreciation, vacancy and re-leasing risk, and any expense beyond the assumed fee load. Disposal is separately taxable in Korea and is not treaty-protected; any model showing a tax-free exit is wrong.

## Modelled Product Terms

These are the terms the demonstration is built to. They are design parameters, not an offer.

|  |  |
| --- | --- |
| **Availability** | **Not offered.** Testnet demonstration only; no subscription is open |
| **Illustrative Net Yield** | ≈3.43% per annum, before hedge carry. An illustration, not a forecast or a guarantee |
| **Minimum Subscription** | SGD 200,000 |
| **Term** | 3 years |
| **Distribution Frequency** | Semi-annual, as modelled. No distribution has been paid |
| **Settlement Currency** | Testnet mock USDC (`MockUSDC`) on Base Sepolia. Not Circle USDC, and not a live currency |
| **Transfer Restriction** | 180 days from issuance, issuer-imposed and enforced on chain. See the note below |
| **Secondary Market** | The token permits transfer between eligible holders once the restriction lapses. No secondary market or venue exists. See Exit & Redemption |

**On the transfer restriction.** The 180-day restriction is imposed by the issuer. It is not required by SFA §275, which is a prospectus exemption for offers to accredited and institutional investors and contains no holding period. The transfer restriction that does apply to a fund interest placed under that exemption limits *who* a transferee may be, not *when* a transfer may occur — and in this design that requirement is discharged by the on-chain eligibility register. On testnet, a registry entry records a workflow decision; it is not identity verification and no investor has been verified.

The restriction is retained for two reasons of our own. It aligns holders with the fund's semi-annual distribution cycle rather than its block time. And where treaty relief depends on documenting each underlying investor's tax residence at each payment date, a register that turns over freely makes that documentation volatile; a settled register is a tax-operational requirement, not a limitation.

The deployed contract applies the restriction per parcel, not per holder. Each issuance creates its own lot with its own unlock date; lots are consumed oldest-first, so a round trip destroys seasoning rather than manufacturing it, and a later subscription does not re-restrict units already held. Units arriving from another holder in a secondary transfer are unrestricted, because the restriction attaches at issuance rather than on receipt.

An earlier version set one unlock timestamp per account and re-armed it on every credit. It was replaced: that rule let any eligible holder immobilise any other indefinitely by repeatedly sending a single unit, and it restarted a holding period that a buyer from a non-affiliate would ordinarily tack.

## Risks

Tier 2 sits in the middle of the OmniFlow ladder: above the listed-REIT tier, below the two credit tiers. The principal risks the product is designed against include:

- **Tenant credit risk** — vacancies or tenant defaults reduce rental income

- **Real estate market risk** — declines in Korean commercial property values would reduce the value of the underlying interest

- **Currency risk** — KRW/USD movements affect distribution amounts in stablecoin terms. No hedge is in place; the +75 to 100 bp carry above is excluded from the yield for that reason

- **Liquidity risk** — no secondary market exists; maturity redemption is the expected exit

- **Smart contract risk** — the contracts have not been audited. See Trust & Security

This list is not a complete risk disclosure, and no risk disclosure document has been issued.

## How to Invest

You cannot. This tier is not open for subscription and no offer is being made. What exists today is a testnet demonstration on Base Sepolia: a deposit certificate, an eligibility registry and a fund token, exercised end to end with mock currency. The settlement workflow that would sit behind a real subscription is documented, but the steps that require human counterparties are not built.
