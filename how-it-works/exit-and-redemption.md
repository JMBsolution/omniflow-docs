# Exit & Redemption

This page sets out the six exit layers OmniFlow is designed around.

**None of them operates.** No redemption has been made, no asset has been sold, no refinancing has been executed, no buyback program exists, and there is no secondary market — no venue, no order book, no counterparties, no transaction has ever occurred. The only exit-related behaviour that exists today is what the deployed testnet contracts enforce, which is described under Transfer Restriction below. Read the layers as a design, and read the limitations at the end as the current position.

## Layer 1 — Maturity Redemption

The intended default exit path. At the product's maturity date — three years for Tier 2 — all outstanding fund tokens are redeemed at NAV, with proceeds paid in the settlement currency to the registered wallet.

For Tier 1 and Tier 2, maturity redemption would be unconditional once the product reaches its scheduled term end. For Tiers 3 and 4, redemption would occur at deal-by-deal realization (loan repayment, recovery, or disposition), with formal maturity being the date all underlying positions have been realized.

No redemption path is implemented. The deployed token has no burn function, so retiring units would require a redemption mechanism that does not yet exist.

## Layer 2 — Strategic Asset Sale

If the underlying asset were sold prior to maturity, proceeds would be distributed as an early redemption, pro-rata after settlement of senior debt, transaction costs and reserves. The sale decision would rest with a licensed fund manager and the local asset manager.

Such a sale would combine accrued income with any capital appreciation realized at sale. Capital gains treatment varies by investor jurisdiction; an exit is separately taxable in Korea.

## Layer 3 — Refinancing Cash-Out

For a stabilized asset with meaningful appreciation, a refinancing could re-leverage the asset to release part of the invested capital before maturity, distributed pro-rata as a partial principal return with NAV adjusted for the cash-out. The fund token would continue to represent the residual equity interest.

This depends on a lender, an underwriting process and a fund manager with discretion to act. None is in place.

## Layer 4 — DeFi Collateralization

The intent is eventual integration with permissioned DeFi protocols that accept **ERC-7943 (uRWA)** tokens as collateral, letting eligible holders pledge tokens for stablecoin liquidity without selling the position.

This depends on permissioned DeFi infrastructure that maintains eligibility gating across collateral and credit positions, and on regulatory clarity for RWA tokens as collateral. Neither condition is met. Nothing is in development and no integration exists.

## Layer 5 — Issuer Buyback (NAV Defense)

A buyback program is part of the design: on a material discount to NAV, the issuer would purchase tokens and hold them, restoring price toward NAV.

**No buyback program exists.** There is no treasury funding one, no trigger implemented, and no market on which a purchase could be made. The address described elsewhere as a subscription account is a demo wallet, not a treasury.

Two constraints on any future program follow from how the deployed token is actually built, and both are deliberate. The token has no burn function: a repurchase cannot quietly reduce supply. And there is no general mint — new units come into existence only by exchanging a deposit certificate — so a repurchased holding cannot be re-issued as if it were a new subscription. A buyback could therefore only park units; it could not manufacture or destroy them.

## Layer 6 — Secondary Market Sale

**There is no secondary market.** No venue exists, no RFQ or matching system is built, no eligible counterparties exist, and no transfer between holders has ever taken place. No transaction fee is charged because no transaction occurs.

The design is a permissioned matched-bargain facility: holders register a sell offer or buy interest, the venue matches counterparties subject to eligibility verification on both sides, and the transfer settles atomically and non-custodially through the smart contract.

**What this would not be, even if built.** A matched-bargain facility is not a continuous market. There would be no order book, no automated market maker, and no commitment by OmniFlow or any third party to quote two-way prices or stand behind a bid. A holder needing to exit at a particular moment could find no counterparty at any price, and should plan around maturity redemption rather than secondary sale. Permissioned secondary venues for security tokens are, across the industry, thin and fragmented; regulated trading venues frequently have no market makers at all. Any move to a licensed venue or to dealer-supported liquidity will be stated as a fact when it exists, not as an expectation.

## Transfer Restriction — What the Contract Actually Enforces

This is the one part of this page that is live, and it runs on the **Base Sepolia testnet**.

The deployed `RwaToken` is configured with a lock-up of 15,552,000 seconds — **180 days**. The clock is set **per parcel, not per account**. Each issuance creates its own lot with its own unlock date, and lots are consumed oldest-first.

Two consequences worth stating plainly. A later subscription does **not** re-restrict units already held — it adds a new restricted lot alongside them. And units received in a secondary transfer from another holder arrive **unrestricted**, because the restriction attaches to newly issued units rather than to the act of receiving them, which mirrors the ordinary treatment of a buyer tacking a seller's holding period.

An earlier version of the contract set a single unlock timestamp per account and re-armed it on every credit. That rule was replaced because it let any eligible holder immobilise any other indefinitely by repeatedly sending one unit, and because it was stricter than the restriction it was modelling. The per-parcel contract is the one deployed; `lotsOf(address)` on the deployed token returns the live lots for any holder.

Because parcels are spent oldest-first, selling and repurchasing destroys seasoning rather than manufacturing it — a round trip resets the units involved to a fresh 180 days.

The token additionally checks eligibility on every transfer against the deployed `EligibilityRegistry`. A transfer to a wallet that does not pass reverts automatically. The registry is populated by hand for the demonstration; it is not connected to any KYC, sanctions or jurisdiction data source.

The 180-day restriction is imposed by the issuer. It is not required by SFA §275, which contains no holding period.

## Important Limitations

- **No exit is available.** Layers 1 through 6 are design, not capability. A holder of testnet fund tokens has no redemption path, no buyer, and no venue.

- **Lock-up.** Units carry a 180-day transfer restriction imposed by the issuer, enforced per parcel from issuance. A later subscription does not re-restrict units already seasoned. See Transfer Restriction above.

- **No liquidity of any kind.** There is no secondary market, no market maker, no bid, and no commitment by anyone to provide one. Secondary depth is not merely thin; it is zero, because the venue does not exist.

- **No buyback backstop.** There is no treasury and no buyback program, so there is no price floor of any kind.

- **Tiers 3 and 4.** Deal-by-deal structures would not offer refinancing or buyback even in a live deployment.

Detailed exit terms would be specified in a product Investment Memorandum and an LP Investment Agreement. Neither document has been issued.
