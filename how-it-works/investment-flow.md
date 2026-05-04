# Investment Flow

This page describes the end-to-end flow of capital from investor subscription to RWA token issuance and ongoing yield distribution. The flow involves coordinated actions across regulated entities in Singapore and the asset jurisdiction. The description below uses OmniFlow's current asset category — Korean prime real estate and real estate-backed credit — for concrete illustration. The same architectural pattern applies to additional jurisdictions and asset categories as they are added in future phases, with jurisdiction-specific routing and regulatory steps adapted accordingly.

## Eight-Step Flow

```
[1] Eligibility Verification         → 1–7 business days
│
▼
[2] Subscription & Investor Agreement → 1–3 business days
│
▼
[3] Stablecoin Deposit                → T+0
│       (USDT / USDC / USD1 to MPI partner wallet)
▼
[4] Deposit Receipt Issuance          → T+1 to T+2
│       (ERC-4626 receipt token)
▼
[5] Conversion & Cross-Border Settlement → T+2 to T+3
│       (stablecoin → USD via MPI partner; SWIFT to asset jurisdiction)
▼
[6] Local Capital Call                → T+3 to T+5
│       (USD → local currency; regulatory filing; LP commitment)
▼
[7] RWA Token Issuance                → T+5 to T+7
│       (deposit receipt burned; ERC-3643 RWA token minted)
▼
[8] Yield Distribution (recurring)    → Per product schedule
(asset income → local fund → VCC → investor wallet)
```

Total time from subscription to RWA token receipt: typically 7 to 15 business days, depending on the speed of supporting documentation and cross-border settlement.

## Step-by-Step Detail

**Step 1 — Eligibility Verification.** The prospective investor completes KYB (corporate entities) or KYC (individuals), AI/II eligibility verification, AML/CFT screening (OFAC, UN, EU sanctions; PEP; adverse media), and signs the SFA §275 acknowledgment. See Onboarding & KYB for required documents and the workflow.

**Step 2 — Subscription & Investor Agreement.** The investor reviews the product Investment Memorandum (IM), executes the LP Investment Agreement, the VCC Subscription Form, and any product-specific risk acknowledgments. Document execution is conducted via DocuSign or equivalent qualified e-signature.

**Step 3 — Stablecoin Deposit.** The investor transfers USDT, USDC, or USD1 from their registered wallet to the OmniFlow MPI partner's designated receiving wallet. The receiving wallet is operated by an MAS-licensed Major Payment Institution holding a Digital Payment Token license. The receiving wallet address and transaction reference are pre-confirmed by the MPI partner. Travel Rule data is exchanged for transfers above SGD 1,500.

**Step 4 — Deposit Receipt Issuance.** OmniFlow's deposit contract issues an ERC-4626 deposit receipt token to the investor's registered wallet. The receipt represents the investor's claim during the period between deposit and final RWA token issuance. The receipt is non-transferable and is burned upon RWA token issuance.

**Step 5 — Conversion & Cross-Border Settlement.** The MPI partner converts the deposited stablecoin to USD at institutional OTC rates. USD is then transferred to OmniFlow's designated USD account at a Singapore correspondent bank, and from there transmitted via SWIFT MT103 to the receiving bank in the asset jurisdiction. AML supporting documentation (typically 11 documents covering source of funds, beneficial ownership, and corporate structure) is prepared and accompanies the SWIFT message.

**Step 6 — Local Capital Call.** The receiving bank in the asset jurisdiction converts USD to the local currency at the prevailing institutional rate. The partner local asset manager files the regulatory notification required for foreign capital inflow — for current Korean asset products, this is the Foreign Investment Promotion Act (FIPA) notification filed with Korea's Ministry of Trade, Industry and Energy. Local currency is then committed as LP capital to the local asset-holding vehicle (currently a Korean Real Estate Fund operated by the partner Korean AMC).

**Step 7 — RWA Token Issuance.** Upon confirmation of the LP capital commitment and the corresponding VCC sub-fund interest registration, the OmniFlow RWA contract atomically (a) burns the investor's deposit receipt and (b) mints the corresponding ERC-3643 RWA token to the investor's wallet. The RWA token represents the investor's beneficial interest in the VCC sub-fund.

**Step 8 — Yield Distribution.** As the underlying assets generate income (rental payments, loan coupon receipts, or operational cash flow), the income flows from the underlying asset to the local asset-holding vehicle, from there to the VCC sub-fund as LP distributions, and from the VCC sub-fund to investors as token-level distributions. Distribution mechanics are described in detail in Yield Distribution.

## Key Documents

The following documents are generated and retained for each subscription:

- KYB/KYC verification report

- AI/II eligibility certification

- SFA §275 acknowledgment (executed)

- LP Investment Agreement (executed)

- VCC Subscription Form (executed)

- Product Investment Memorandum (delivered)

- Travel Rule transfer record

- MPI conversion confirmation

- SWIFT MT103 settlement message

- Local jurisdiction regulatory filing receipt (e.g., FIPA notification for Korean asset products)

- Local asset-holding vehicle LP capital commitment record

- RWA token issuance transaction hash

All documents are retained in OmniFlow's compliance archive for the duration required by MAS regulations and applicable tax authorities.

## Operational Counterparties

| **Function** | **Counterparty** |
| --- | --- |
| Fund Operation (Phase 1) | MAS-licensed CMS LFMC partner |
| Stablecoin Settlement (Phase 1) | MAS MPI DPT-licensed partner |
| Local Asset Management (Korea) | MOLIT-licensed Korean AMC partner |
| Banking (Singapore) | Tier-1 Singapore bank |
| Banking (Korea) | Tier-1 Korean bank |
| Audit (Annual) | Big 4 accounting firm |

For asset categories outside Korea, equivalent licensed counterparties in the relevant jurisdiction are engaged before the category is opened to subscriptions. Specific counterparty identities are disclosed under non-disclosure agreement during institutional due diligence and on the Legal Structure page following operational launch.
