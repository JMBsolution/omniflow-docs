# Stablecoin Settlement

## What Settles Today

The settlement token in this build is **`MockUSDC`** (`0x0f77b3a298c6c1b6940a6147b536cbe687aa98ef`), a mock ERC-20 deployed on the **Base Sepolia testnet** for the demonstration. It is not Circle USDC, it is not any other issuer's stablecoin, and it carries no value. Every settlement figure shown in the application moves this mock token on testnet.

There is no mainnet deployment. No real stablecoin has been received, converted or transmitted, and no payment institution is engaged to do so. The rest of this page describes the settlement design a live deployment would implement.

## The Intended Tri-Currency Design

The design calls for subscriptions and distributions in three stablecoins — **USDT**, **USDC** and **USD1** — rather than USDC alone.

USDT is the dominant stablecoin in the Middle East, Southeast Asia, and Greater China. USDC is the regulatory standard for U.S. and European institutional capital. USD1 has seen adoption in specific corridors. Supporting all three would remove the conversion step that otherwise sits between an investor's holdings and a subscription.

None of the three is integrated. Multi-stablecoin support is design intent, not a shipped capability.

## Settlement Architecture (Design)

```
Investor Wallet                    Fund Account
│                                    ▲
│ (1) Stablecoin                    │ (3) USD
▼                                    │
Payment Institution ── (2) Conversion ── Singapore Bank
                          to USD              │
│ (4) Cross-border wire
▼
Asset Jurisdiction Bank
│ (5) USD → Local Currency
▼
Local Asset-Holding Vehicle
```

## Step-by-Step (Design)

1. **Investor deposit.** The investor transfers stablecoin from their registered wallet to a receiving wallet operated by a licensed payment institution.

1. **Stablecoin-to-USD conversion.** The payment institution converts the deposited stablecoin to USD at institutional OTC rates. Conversion spreads would be disclosed at the time they are quoted; no rate has been quoted to OmniFlow by any counterparty, so no spread range is published here.

1. **USD settlement to the fund account.** Converted USD is transferred to a USD account at a Singapore correspondent bank.

1. **Cross-border wire to the asset jurisdiction.** USD is transmitted to a receiving bank in the asset jurisdiction. Travel Rule data and source-of-funds documentation accompany the transfer.

1. **USD-to-local currency conversion.** The receiving bank converts USD to local currency at the prevailing institutional rate, and local currency is committed as LP capital to the local asset-holding vehicle. For the Korean asset the local currency is KRW.

Steps 1 through 5 correspond to steps 02 and 04 through 06 of the settlement workflow. The demonstration halts at step 04 — the conversion — because no counterparty exists to perform it.

## Distribution Path (Reverse)

The design runs the same path in reverse: local currency out of the asset-holding vehicle, converted to USD and wired to Singapore, converted to the investor's preferred stablecoin, and transferred to the registered wallet.

No distribution has been paid, and the reverse path has never been exercised.

## Regulatory Framework — Singapore (Settlement Side)

A live deployment's stablecoin handling would sit within MAS's framework for digital payment services. OmniFlow holds no licence of any kind and is not regulated by MAS. The relevant anchors a deployment would have to satisfy:

- **Payment Services Act (PSA) 2019**: Establishes Major Payment Institution (MPI) licensing for entities providing DPT services

- **PSN02**: AML/CFT requirements for DPT service providers

- **DTSP (effective 30 June 2025)**: Requires Singapore-based entities providing DPT services to overseas customers to hold an FSMA Part 9 license; MPI licensees are exempted from this separate requirement

Operating this path would require a partnership with an MPI DPT-licensed entity. No such partnership exists.

## Regulatory Framework — Asset Jurisdiction Side

A live cross-border flow would also be subject to the asset jurisdiction's foreign capital inflow regulations. For the Korean asset, this means:

- **Foreign Investment Promotion Act (FIPA)**: Foreign LP capital commitments to Korean Real Estate Funds are filed with the Ministry of Trade, Industry and Energy

- **Foreign Exchange Transactions Act**: Cross-border USD-to-KRW conversion is subject to disclosure requirements administered by the Bank of Korea and the Ministry of Economy and Finance

- **Korean tax withholding**: Distributions out of the Korean fund to a Singapore holding vehicle would be subject to 15% withholding under the Korea-Singapore tax treaty, inclusive of local income tax, subject to treaty benefit eligibility certification. Without relief the 22% domestic rate applies

Equivalent local frameworks apply to future asset jurisdictions and are documented on the relevant product pages at the time of category launch.

## Stablecoin Issuers

All three stablecoins in the intended design are Digital Payment Tokens under the PSA, and each would be received, converted and transmitted by an MPI-licensed entity acting within its own licence scope rather than by OmniFlow. Which of the three a given deployment could actually support depends on that entity's support at the time.

OmniFlow has no relationship with Tether, Circle, or any other stablecoin issuer, and no routing arrangement with any of them.

## Settlement Fees

Stablecoin-to-USD conversion would be charged at whatever institutional rate the converting counterparty quotes, and passed through with the fee schedule disclosed in subscription documents and distribution statements.

No fee schedule exists, because no counterparty has quoted one. Fund fees, separately, are assumed at 0.75% of GAV for yield modelling — an assumption, not a sourced or agreed figure.
