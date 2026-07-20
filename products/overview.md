# Products Overview

OmniFlow currently offers four product tiers within its first asset category, Korean prime real estate and real estate-backed credit. The tiers target different points on the risk-return spectrum. All products share the same regulatory structure, settlement infrastructure, and compliance gating; they differ in the underlying assets they hold and the resulting risk-return profile.

Additional asset categories — including Japanese real estate, Southeast Asian infrastructure, and pan-Asian credit — are planned for future phases and will be offered through the same protocol framework.

## Common Structure

Every OmniFlow product, regardless of jurisdiction, is structured as follows:

```
Investor (USDT/USDC/USD1)
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

Investors hold tokenized representations of their VCC Sub-Fund interests. The VCC holds limited partnership interests in the local asset-holding vehicle (a Korean Real Estate Fund for current products), which in turn holds the underlying assets. This structure provides investors with Singapore-jurisdiction legal rights while accessing local asset economics. See Legal Structure for the complete legal architecture.

## Current Products

| **Tier** | **Strategy** | **Availability** | **Illustrative Net Yield** | **Min. Investment** | **Term** | **Risk Profile** |
| --- | --- | --- | --- | --- | --- | --- |
| T1 | Listed REIT Income | **Offered** | 4.5–5.1% p.a. | SGD 200,000 | Open-ended | Lowest |
| T2 | Logistics Income | **Offered** | ≈5.5% p.a. | SGD 200,000 | 3–5 yrs | Moderate |
| T3 | Senior Development Credit | Pipeline | To be published | SGD 200,000 | 2–4 yrs | High |
| T4 | Opportunistic Credit | Pipeline | To be published | SGD 500,000 | 1–3 yrs | Highest |

**Two tiers are offered and two are in the pipeline.** T1 and T2 are equity income strategies with a published gross-to-net bridge. T3 and T4 are credit strategies that are not currently open for subscription and carry no published yield; they are documented here so the intended range is legible, and each will be opened only when its return can be evidenced rather than modelled.

The ladder ascends in **risk**, which is the ordering we can state honestly today.

## How This Range Was Rebuilt

The previous four tiers were ordered by target yield: 5–7%, 8–9%, 9–12%, 6–7%. Re-deriving each of them from sourced inputs showed that ordering did not survive contact with the arithmetic. On a net basis the old Tier 2 paid *less* than the old Tier 1 while taking more risk; the old Tier 2 and Tier 3 turned out to underwrite the same thing at two price points; and the old Tier 4 delivered less net income than Tier 1 while adding daily mark-to-market.

So the range has been rebuilt around **risk**, which we can order honestly, rather than around yield, which we could not.

**Income tiers — T1 and T2 — publish a yield.** Both are equity exposures with a distributable cash return, and both publish a full gross-to-net bridge on their own page, including the assumptions we could not source.

**Credit tiers — T3 and T4 — do not publish a yield, and this is the substantive finding.** A fixed coupon does not survive this structure. Korean withholding at 15% plus the fee load takes a 7% senior coupon down to roughly 3.8% net — below Tier 1, for more risk. Equity tiers can use leverage to lift the return; a loan book held through a fund cannot. That means Korean credit does not work as an *income* product here at all: its return has to come from credit spread and recovery, which cannot be published as a target until loss experience can be evidenced rather than modelled.

We would rather say that than manufacture a number. For Tier 4 in particular, the incumbent professionals in Korean distressed credit — the five licensed buyers — earned a median levered return on equity of 3.7%, 5.3% and about 8.7% over 2023–2025 at four to five times leverage. We will not publish a target that implies an unlevered offshore vehicle can beat them.

**Tier 1's wrapper adds no return, and we say so on its page.** Korea abolished the Investment Registration Certificate in December 2023, so a foreign institution can buy listed Korean REITs directly at its own treaty rate. What the wrapper provides is stablecoin settlement, small-ticket aggregation and a single consolidated treaty filing — operational benefits, not access value.

## How to Read a Yield Figure

Every figure above is an objective, not a forecast and not a guarantee.

**A net yield is only meaningful with its bridge.** The distance between an asset's cap rate and what reaches an investor is large, and most of it is not optional: financing cost, fund-level fees and expenses, and Korean withholding levied at source. Withholding in particular is deducted before money reaches the Singapore sub-fund — it is not an investor-level tax that can be set aside as a footnote, and any figure presented "before tax" for this structure overstates what an investor receives.

**Every tier now publishes its bridge** on its own page, including the assumptions that could not be independently sourced. Where the evidence does not support a number, we say so instead of estimating: Tier 3 publishes no target at all, and Tier 2 publishes its estimate with the load-bearing assumption named in the same sentence.

**One correction applies across every tier.** Distributions from a Korean collective investment vehicle reach a Singapore investor as *dividend* income, not as interest — so the Korea–Singapore treaty's 10% interest rate is not available on this route and 15% applies. Earlier material that assumed the interest rate overstated net yields. The 15% rate itself is not settled: whether a Singapore VCC sub-fund qualifies for treaty benefits appears untested, and there is an operational risk that Korean withholding agents apply 22% at source pending a refund claim.

**And every model here rests on a rate environment that has just changed.** The Bank of Korea raised its base rate in July 2026, its first increase in three and a half years. Underwriting assumptions built on expected cuts — including the refinancing tailwind thesis common in Korean real-estate research — are stale, and figures on this page will be revisited.

Actual returns will differ from any target based on asset performance, market conditions, vacancy and re-leasing, and the timing of distributions. Disposal is separately taxable in Korea and is not protected by the Korea–Singapore treaty.

## Future Categories

OmniFlow's protocol architecture supports expansion to additional jurisdictions and asset classes. Categories under active exploration include:

- **Japan prime real estate** — targeting Phase 3 launch, leveraging the Singapore-Japan tax treaty and TMK structures

- **Southeast Asian infrastructure** — targeting Phase 4, focused on logistics, data centers, and renewable energy assets in Vietnam, Thailand, and Indonesia

- **Pan-Asian credit and structured products** — targeting Phase 4+, including private credit, trade finance, and asset-backed receivables across multiple Asian markets

Specific timing depends on regulatory milestones, partner agreements, and market conditions. See Roadmap for current planning. Subscriptions for future categories are not currently being accepted.

## Distribution Frequency

Tier 1, 2, and 4 products distribute yield semi-annually. Tier 3 products distribute on a deal-by-deal basis tied to the underlying loan or asset realization schedule. All distributions are paid in the investor's chosen settlement currency (USDT, USDC, or USD1) and delivered directly to the registered investor wallet.

## Currency Support

All products accept subscriptions and pay distributions in USDT (primary), USDC, and USD1. Investors specify their preferred settlement currency at onboarding. Conversion between stablecoins, where required for fund operations, is handled by OmniFlow's MPI partner at institutional OTC rates and is fully transparent in distribution statements.

## Liquidity Options

Each product offers up to six layers of exit optionality:

1. **Maturity redemption** — full redemption of principal plus accrued yield at term end

1. **Strategic asset sale** — distribution of sale proceeds upon underlying asset disposition

1. **Refinancing cash-out** — partial principal return through asset re-leveraging

1. **DeFi collateralization** — pledge tokens as collateral within OmniFlow's permissioned DeFi integrations (Phase 3+)

1. **Issuer buyback** — protocol-level buyback at NAV-defended levels (subject to issuer capital constraints)

1. **Secondary market sale** — peer-to-peer transfer to another qualified investor (subject to the issuer-imposed 6-month restriction on each parcel)

Liquidity availability varies by product. See individual Tier pages for product-specific exit terms.

## Selecting a Product

OmniFlow's relationship managers provide tailored guidance on product selection based on each investor's risk tolerance, investment horizon, and existing portfolio composition. To begin, contact partners@omniflow.xyz or your assigned relationship manager.
