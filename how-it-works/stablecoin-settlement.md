# Stablecoin Settlement

OmniFlow accepts subscriptions and pays distributions in three stablecoins: **USDT** (primary), **USDC**, and **USD1**. This tri-currency framework is a deliberate design choice that distinguishes OmniFlow from competing RWA platforms, which typically support USDC alone. The same settlement framework applies regardless of the asset category the investor subscribes to.

## Why Three Stablecoins

USDT is the dominant stablecoin in the Middle East, Southeast Asia, and Greater China — the regions where OmniFlow's primary investor base operates. USDC is the regulatory standard for U.S. and European institutional capital. USD1 has gained adoption in specific corridors, particularly Middle East sovereign and quasi-sovereign capital. Supporting all three eliminates the friction that would otherwise force investors to convert between stablecoins before participating.

## Settlement Architecture

```
Investor Wallet                    OmniFlow VCC Sub-Fund
│                                    ▲
│ (1) USDT/USDC/USD1                │ (3) USD
▼                                    │
MPI Partner ──── (2) Conversion ───── Singapore Bank
(DPT-licensed)         to USD               │
│ (4) SWIFT
▼
Asset Jurisdiction Bank
│ (5) USD → Local Currency
▼
Local Asset-Holding Vehicle
(e.g., Korean REF)
```

## Step-by-Step

1. **Investor deposit.** The investor transfers stablecoin from their registered wallet to the MPI partner's receiving wallet. The receiving wallet is operated by an MAS-licensed Major Payment Institution holding a Digital Payment Token license.

1. **Stablecoin-to-USD conversion.** The MPI partner converts the deposited stablecoin to USD at institutional OTC rates. Typical bid-ask spreads are 0.05–0.15% for USDT and 0.10–0.25% for USDC, with USD1 spreads varying by market depth at the time of conversion.

1. **USD settlement to OmniFlow account.** Converted USD is transferred from the MPI partner to OmniFlow's designated USD account at a Singapore correspondent bank.

1. **SWIFT to asset jurisdiction.** USD is transmitted via SWIFT MT103 to the receiving bank in the asset jurisdiction. Travel Rule data and source-of-funds documentation accompany the transfer.

1. **USD-to-local currency conversion.** The receiving bank in the asset jurisdiction converts USD to the local currency at the prevailing institutional rate. Local currency is then committed as LP capital to the local asset-holding vehicle. For current Korean asset products, the receiving bank is a Tier-1 Korean bank and the local currency is KRW.

## Distribution Path (Reverse)

Distributions flow in reverse:

1. The local asset-holding vehicle distributes income in local currency to the VCC sub-fund's local jurisdiction account

1. Local currency is converted to USD and transmitted via SWIFT to OmniFlow's Singapore USD account

1. USD is converted to the investor's preferred stablecoin (USDT, USDC, or USD1) by the MPI partner

1. Stablecoin is transferred directly to the investor's registered wallet

Investors specify their preferred distribution stablecoin at onboarding and may change the preference between distribution cycles.

## Regulatory Framework — Singapore (Settlement Side)

OmniFlow's stablecoin handling operates within MAS's framework for digital payment services. The relevant regulatory anchors:

- **Payment Services Act (PSA) 2019**: Establishes Major Payment Institution (MPI) licensing for entities providing DPT services

- **PSN02**: AML/CFT requirements for DPT service providers

- **DTSP (effective 30 June 2025)**: Requires Singapore-based entities providing DPT services to overseas customers to hold an FSMA Part 9 license; MPI licensees are exempted from this separate requirement

Phase 1 operations rely on a partnership with an existing MPI DPT-licensed entity. OmniFlow has commenced its own MPI application, with Phase 2 self-licensing targeted following completion of operational scale milestones.

## Regulatory Framework — Asset Jurisdiction Side

In addition to Singapore-side regulation, the cross-border flow is subject to the asset jurisdiction's foreign capital inflow regulations. For current Korean asset products, this means:

- **Foreign Investment Promotion Act (FIPA)**: Foreign LP capital commitments to Korean Real Estate Funds are filed with the Ministry of Trade, Industry and Energy

- **Foreign Exchange Transactions Act**: Cross-border USD-to-KRW conversion is subject to disclosure requirements administered by the Bank of Korea and the Ministry of Economy and Finance

- **Korean tax withholding**: Distributions from the Korean REF to the VCC sub-fund are subject to 15% withholding under the Korea-Singapore tax treaty, inclusive of local income tax (subject to treaty benefit eligibility certification; 22% applies without relief)

Equivalent local frameworks apply to future asset jurisdictions and are documented on the relevant product pages at the time of category launch.

## USDT-Specific Note

Tether Limited, the issuer of USDT, does not hold an MAS MPI license directly. However, MPI-licensed entities in Singapore are permitted to receive, convert, and transmit USDT under their existing license scope, and OmniFlow's Phase 1 partner is an MPI entity that handles USDT settlement at institutional volume. This structure is operationally equivalent to the USDC settlement path and does not create incremental regulatory risk for the investor.

## USDC-Specific Note

Circle Internet Financial holds an MAS MPI license through Circle Singapore (granted September 2024). For investors who require direct settlement through Circle's regulated infrastructure, OmniFlow can route USDC settlement directly through Circle's institutional channels.

## USD1-Specific Note

USD1 is treated as a Digital Payment Token under PSA and is handled through the same MPI partner infrastructure as USDT. Direct settlement availability for USD1 depends on the MPI partner's then-current support; investors should confirm USD1 routing with their relationship manager prior to subscription.

## Settlement Fees

Stablecoin-to-USD conversion fees are charged at institutional OTC rates and are passed through transparently. The fee schedule is disclosed in the subscription documents and reflected in the distribution statements. OmniFlow does not earn margin on stablecoin conversion in Phase 1; following Phase 2 self-licensing, conversion is conducted internally and any spread is disclosed in protocol financials.
