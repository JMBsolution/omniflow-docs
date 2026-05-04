# Exit & Redemption

OmniFlow provides up to six layers of exit optionality. The availability and timing of each layer depends on the product, market conditions, and investor circumstances. The same six-layer framework applies across all product tiers and asset categories.

## Layer 1 — Maturity Redemption

The default exit path. At the product's maturity date, OmniFlow redeems all outstanding RWA tokens at NAV. Redemption proceeds are paid in the investor's preferred stablecoin (USDT, USDC, or USD1) and delivered to the registered wallet.

For Tier 1, 2, and 4 products, maturity redemption is unconditional once the product reaches its scheduled term end. For Tier 3 products, redemption occurs at deal-by-deal realization (loan repayment, NPL recovery, or asset disposition); the formal "maturity" of a Tier 3 fund is the date by which all underlying positions have been realized.

## Layer 2 — Strategic Asset Sale

If the underlying asset is sold prior to maturity (whether through a value-realization sale or strategic exit decision), proceeds are distributed to investors as an early redemption. The sale decision is made by the partner LFMC and the local asset manager in consultation with major investors. Sale proceeds are distributed pro-rata after settlement of any senior debt, transaction costs, and reserves.

Strategic asset sales typically generate combined returns from accrued income (held during the period) and capital appreciation (realized at sale). Tax treatment of capital gains components varies by investor jurisdiction.

## Layer 3 — Refinancing Cash-Out

For Tier 1 and Tier 2 products with stabilized assets and meaningful capital appreciation, OmniFlow may execute refinancing transactions in which the underlying asset is re-leveraged to release a portion of investor capital prior to maturity.

Refinancing proceeds are distributed pro-rata to investors as a partial principal return. The investor's RWA token continues to represent the residual equity interest, with NAV adjusted to reflect the cash-out.

Refinancing is at the discretion of the partner LFMC and is subject to underwriting analysis, market conditions, and investor consent where the threshold is exceeded.

## Layer 4 — DeFi Collateralization (Phase 3+)

In Phase 3, OmniFlow plans to integrate with permissioned DeFi protocols that accept ERC-3643 RWA tokens as collateral. Eligible investors will be able to pledge their RWA tokens to obtain stablecoin liquidity without selling the underlying position.

This option is contingent on (a) the readiness of permissioned DeFi infrastructure that maintains AI/II gating across collateral and credit positions, and (b) regulatory clarity on the treatment of RWA tokens as collateral. Layer 4 is currently in development and not available in Phase 1 or Phase 2.

## Layer 5 — Issuer Buyback (NAV Defense)

OmniFlow operates a protocol-level buyback program designed to defend NAV during periods of dislocation. The program is triggered when the secondary market price of an RWA token declines 15% or more below NAV.

Upon trigger, OmniFlow's treasury executes open-market purchases of the affected token at prices designed to restore the secondary market price toward NAV. Purchased tokens are held in treasury and may be subsequently re-issued, redeemed, or burned, depending on circumstances.

The buyback program is funded by OmniFlow's treasury and is subject to capital availability. The program is not a redemption guarantee and does not eliminate the possibility of NAV decline. Tier 3 products are not eligible for the buyback program.

## Layer 6 — Secondary Market Sale

After the SFA §275 6-month lock-up period, RWA tokens may be transferred between qualified investors through OmniFlow's secondary market.

The secondary market operates as a permissioned RFQ (Request-for-Quote) and matching system. Investors register their order (sell offer or buy interest), OmniFlow matches counterparties subject to AI/II eligibility verification on both sides, and the transfer is executed atomically through the smart contract.

OmniFlow charges a transaction fee of 0.10–0.30% per side, depending on the transaction size and product. OmniFlow may also provide liquidity through its own market-making inventory, in which case spreads of 0.5–2.0% may apply between OmniFlow's bid and ask quotes.

The secondary market is subject to ongoing AI/II eligibility verification at the smart contract level. A transfer attempt to a wallet that does not pass eligibility checks (for example, due to expired KYC, sanctions list match, or jurisdictional ineligibility) will be reverted automatically.

## Exit Selection

The optimal exit path depends on the investor's circumstances, the product's stage in its lifecycle, and prevailing market conditions. OmniFlow's relationship managers provide guidance on exit selection on request, but the final decision rests with the investor.

For institutional allocators with portfolio-level requirements (rebalancing, redemption obligations to underlying LPs, regulatory capital adjustments), OmniFlow can structure coordinated exits combining multiple layers; for example, a partial Layer 3 refinancing cash-out followed by a Layer 6 secondary market sale of the residual position.

## Important Limitations

- **Lock-up period.** All RWA tokens are subject to a 6-month transfer restriction following issuance (SFA §275). Layers 1, 2, 3, and 5 may operate within the lock-up period; Layer 6 (secondary market) is unavailable until the lock-up has elapsed.

- **Buyback capital constraint.** Layer 5 issuer buyback is dependent on treasury capacity and is not a guarantee of price floor.

- **Secondary market liquidity.** Secondary market depth depends on the number of qualified investors actively trading. In early product stages, secondary market liquidity may be thin.

- **Tier 3 limitations.** Tier 3 products do not offer Layers 3 (refinancing) or 5 (issuer buyback) and have limited Layer 6 secondary liquidity due to deal-by-deal structure.

Detailed exit terms for each product are specified in the product Investment Memorandum and the LP Investment Agreement.
