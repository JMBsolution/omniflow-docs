# Korea Logistics Income (Tier 2)

Stable income from Korean commercial real estate, led by Seoul Capital Area logistics. Illustrative net distribution yield of approximately 5.50% per annum, before any currency hedge carry. The gross-to-net bridge is published in full below — the bridge, not the headline, is the number to read.

This is the one tier live in this build, and it is live as a **testnet demonstration on Base Sepolia**. No fund vehicle has been established, no asset has been acquired, and no subscription is open. The yield below is a model, not a record of anything paid.

## What It Is

Korea Logistics Income is designed to invest in stabilized, income-producing logistics assets in the Seoul Capital Area, with selective exposure to other stabilized commercial property. It is the range's core direct-equity income tier: it sits above the listed-REIT tier on the risk ladder, concentrated and illiquid where a listed product is diversified and marked daily.

## Strategy

The strategy is to acquire direct equity positions or senior secured debt positions in assets with established tenants, long-duration leases, and verified rent rolls. Asset selection would prioritize properties with weighted average lease terms (WALT) of three years or more, occupancy rates above 95%, and credit-tenant rosters. No position has been acquired.

The fund is modelled with senior leverage at 60% LTV, interest-only — the same assumption the bridge below is built on. Yield is generated primarily from rental income and, where applicable, secured note coupons.

## Eligible Underlying Assets

| **Asset Type** | **Going-In Cap Rate** | **Basis** |
| --- | --- | --- |
| Seoul Capital Area logistics centres | 5.80% | A 2025 comparable institutional transaction, reported by Newmark |
| Seoul prime office (CBD, GBD, YBD) | approximately 4.2% | Carried here only as the basis for the withdrawal described below |

Logistics leads the allocation for a specific reason. Korean senior debt for commercial real estate is taken here at roughly 4.10% — the Bank of Korea new corporate loan rate, used as a public proxy, because actual stabilised pricing is not publicly disclosed. That sits at or above the prime office cap rate — so leverage on prime office adds no yield. Across a 50% to 65% loan-to-value range, levered cash-on-cash on a 4.2% cap moves by under 10 basis points. Logistics clears above the debt cost and is therefore the asset where leverage does useful work.

That is not a hypothetical. A Seoul prime office product was withdrawn during yield re-derivation for exactly this reason: a 4.2% cap against a 4.10% debt cost cannot produce the target yield at any leverage. The asset was repositioned to logistics at a 5.80% cap rather than carried at a number the bridge would not support.

## How the Yield Is Built

An illustrative bridge for a Seoul Capital Area logistics asset, modelled on a Singapore holding structure taking Korea–Singapore treaty relief, and stated so that it can be reproduced and challenged. No such vehicle has been established.

| **Line** | **Value** | **Basis** |
| --- | --- | --- |
| Going-in cap rate | 5.80% | A 2025 comparable institutional transaction, reported by Newmark |
| Less senior debt interest, 60% LTV interest-only at 4.10% | −2.46 pts of asset value | Bank of Korea new corporate loan rate as a public proxy; actual stabilised pricing is not publicly disclosed |
| **Levered cash-on-cash to the fund** | **8.35%** | (5.80 × 100 − 4.10 × 60) ÷ 40 |
| Less fund-level fees and expenses, 0.75% of gross asset value | −1.88 pts on equity | **Assumption — not independently sourced.** Korean fund fee schedules are not public |
| Pre-withholding distribution to the holding vehicle | 6.47% | |
| Less Korean withholding at the 15% treaty rate | −0.97 pts | Korea–Singapore double tax agreement, dividend article. The treaty rate is inclusive of Korean local income tax |
| **Illustrative net distribution yield** | **≈5.50%** | |
| Plus currency hedge carry, if hedged to USD | +75 to 100 bp | Analytical inference from the policy rate differential before cross-currency basis. Excluded from the yield above; no hedge is in place |

**Sensitivity.** If treaty relief is unavailable and the domestic 22% withholding rate applies, the net figure falls to approximately 5.0%. The spread between the treaty rate and the domestic rate is worth roughly 45 basis points of net yield here — meaningful, but not the variable that decides the investment.

**What this bridge excludes.** Capital appreciation, vacancy and re-leasing risk, and any expense beyond the assumed fee load. Disposal is separately taxable in Korea and is not treaty-protected; any model showing a tax-free exit is wrong.

## Modelled Product Terms

These are the terms the demonstration is built to. They are design parameters, not an offer.

|  |  |
| --- | --- |
| **Availability** | **Not offered.** Testnet demonstration only; no subscription is open |
| **Illustrative Net Yield** | ≈5.50% per annum, before hedge carry. An illustration, not a forecast or a guarantee |
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
