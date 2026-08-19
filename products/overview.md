# Products Overview

OmniFlow documents four product tiers within its first asset category, Korean real estate and real estate-backed credit. **One of them is live: Tier 2, Korea Logistics Income, running as a demonstration on the Base Sepolia testnet.** The other three are documented so the shape of the range is legible. None of them is open, and none of them publishes a yield.

The tiers differ in the assets they would hold and in the resulting risk profile. They share the same intended structure, settlement workflow and compliance gating.

## Intended Structure

No vehicle has been formed. The diagram below is the structure the products are designed to use, not a description of anything that exists today:

```
Investor (stablecoin settlement)
│
▼
OmniFlow VCC Sub-Fund (Singapore)
│  LP capital
▼
Local Asset-Holding Vehicle (e.g., Korean REF)
│  acquires
▼
Underlying Asset(s)
```

Under this design an investor would hold a tokenized representation of a sub-fund interest, and the sub-fund would hold a limited partnership interest in the local asset-holding vehicle, which in turn holds the underlying asset — Singapore-jurisdiction legal rights against local asset economics. The sub-fund, the asset-holding vehicle and the asset are all prospective. See Legal Structure for the intended legal architecture and for what has and has not been established.

## Current Products

| **Tier** | **Strategy** | **Availability** | **Illustrative Net Yield** | **Min. Subscription** | **Term** | **Risk Profile** |
| --- | --- | --- | --- | --- | --- | --- |
| T1 | Listed REIT Income | Documented · not open in this build | Not published | Not set | Not set | Lowest |
| T2 | Korea Logistics Income | **Live — Base Sepolia testnet** | 3.43% p.a. — illustrative | SGD 200,000 | 3 years | Moderate |
| T3 | Senior Development Credit | Pipeline | Not published | Not set | Not set | High |
| T4 | Opportunistic Credit | Pipeline | Not published | Not set | Not set | Highest |

**One tier is live, and it is live on a testnet.** Tier 2 has been exercised end to end on Base Sepolia — subscription, deposit certificate, eligibility check and token issuance — against a mock settlement token. No mainnet deployment exists, no capital has been raised and no asset has been acquired.

The other three tiers are documented so the intended range is legible. None carries a published yield, and each will be opened only when its return can be evidenced rather than modelled.

The ladder ascends in **risk**, which is the ordering we can state honestly today.

## How This Range Was Rebuilt

The tiers were previously ordered by target yield. Re-deriving each of them from sourced inputs showed that ordering did not survive contact with the arithmetic: on a net basis the higher-yielding rungs did not out-earn the lower ones, and two of them turned out to underwrite the same thing at two price points. Those targets have been withdrawn and are not republished here.

So the range has been rebuilt around **risk**, which we can order honestly, rather than around yield, which we could not.

**One product was withdrawn outright, and it is the clearest thing on this page.** A Seoul prime office product could not clear its own cost of capital: a 4.2% going-in cap rate against a 4.10% debt cost produces no yield at any leverage. Rather than soften the target and keep the asset, we repositioned to Seoul Capital Area logistics — which is Tier 2. On 2026 data that logistics cap is 5.32% against senior debt at 4.93% all-in, a spread of 39 basis points, so leverage still adds but thinly.

**Only Tier 2 publishes a yield**, and it publishes the full gross-to-net bridge behind it, including the assumption we could not source. Tier 1 publishes none; its page explains why.

**Credit tiers — T3 and T4 — do not publish a yield, and this is the substantive finding.** A fixed coupon does not survive this structure. Korean withholding at 15% plus the fee load takes a 7% senior coupon down to roughly 3.8% net — below the income tier, for materially more risk. Equity tiers can use leverage to lift the return; a loan book held through a fund cannot. That means Korean credit does not work as an *income* product here at all: its return has to come from credit spread and recovery, which cannot be published as a target until loss experience can be evidenced rather than modelled.

We would rather say that than manufacture a number.

**Tier 1's wrapper adds no return, and we say so on its page.** Korea abolished the Investment Registration Certificate in December 2023, so a foreign institution can buy listed Korean REITs directly at its own treaty rate. What the wrapper provides is stablecoin settlement, small-ticket aggregation and a single consolidated treaty filing — operational benefits, not access value.

## How to Read a Yield Figure

The Tier 2 figure above is an objective, not a forecast and not a guarantee. It is illustrative: it describes a structure that has been modelled and demonstrated on testnet, not a fund that has been raised or an asset that has been bought. No distribution has ever been paid.

**A net yield is only meaningful with its bridge.** The distance between an asset's cap rate and what reaches an investor is large, and most of it is not optional: financing cost, fund-level fees and expenses, and Korean withholding levied at source. Withholding in particular is deducted before money reaches the Singapore sub-fund — it is not an investor-level tax that can be set aside as a footnote, and any figure presented "before tax" for this structure overstates what an investor receives.

**Tier 2 publishes its bridge** on its own page, including the fee assumption that could not be independently sourced. Where the evidence does not support a number, we say so instead of estimating: Tiers 1, 3 and 4 publish no target at all, and Tier 2 publishes its estimate with the load-bearing assumption named in the same sentence.

**One correction applies across every tier.** Distributions from a Korean collective investment vehicle reach a Singapore investor as *dividend* income, not as interest — so the Korea–Singapore treaty's 10% interest rate is not available on this route and 15% applies. Earlier material that assumed the interest rate overstated net yields. The 15% rate itself is not settled: whether a Singapore VCC sub-fund qualifies for treaty benefits appears untested, and there is an operational risk that Korean withholding agents apply 22% at source pending a refund claim.

**And every model here rests on a rate environment that can move against it.** The 4.10% debt cost is a public proxy struck in July 2026, not a term sheet from a lender. An underwriting assumption built on expected rate cuts is a hope, not an input, and the figures on this page will be revisited as the sourced inputs move.

Actual returns will differ from any target based on asset performance, market conditions, vacancy and re-leasing, and the timing of distributions. Disposal is separately taxable in Korea and is not protected by the Korea–Singapore treaty.

## Future Categories

Other jurisdictions and asset classes — Japanese real estate, Southeast Asian infrastructure, pan-Asian credit — are directions we have looked at on paper. None is scheduled, structured or funded, and no subscription is being accepted for any of them. They are listed here only so the intended direction is legible.

## Distributions

No distribution has been paid, by any tier. Tier 2's terms contemplate distribution in the settlement currency to the registered investor wallet; the issuance and transfer mechanics behind that have been exercised on Base Sepolia testnet only. Distribution terms for the other three tiers are not set.

## Settlement Currency

In this build, settlement is a mock USDC contract deployed on Base Sepolia (`0x0f77b3a298c6c1b6940a6147b536cbe687aa98ef`). It is a test token. It is not Circle USDC and it carries no value.

Production settlement currency, stablecoin conversion and any currency hedging would depend on counterparties that have not been engaged. The Tier 2 yield excludes FX hedge carry of +75 to 100 bp.

## Liquidity

Tier 2 tokens carry a **180-day transfer restriction from issuance**, issuer-imposed and enforced by the token contract on testnet. After that window a token can move only to a wallet the eligibility registry marks as eligible.

There is no secondary market, no buyback facility and no DeFi integration. Exit at term would depend on realisation of the underlying asset, and disposal is separately taxable in Korea. Nothing beyond the transfer restriction and the eligibility check is built.

## Contact

Only Tier 2 is live, and only as a testnet demonstration — there is nothing to subscribe to today. For diligence questions, contact archiyong217@gmail.com.
