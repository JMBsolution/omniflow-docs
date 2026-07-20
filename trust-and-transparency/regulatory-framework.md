# Regulatory Framework

This page summarizes the regulatory frameworks that would govern OmniFlow's operations if it were operating.

**Status. OmniFlow holds no licence of any kind, in any jurisdiction.** It is not MAS-regulated. No licence application has been filed and no partner licensee has been engaged. Nothing has been offered to any investor, no investor has been onboarded, and no regulatory report has been filed with any authority. What exists is a Base Sepolia **testnet** contract deployment and an off-chain settlement workflow model. No legal opinion has been obtained on any of the analysis below; it is OmniFlow's own reading of the applicable rules.

## Target Licence Stack

The licences below are the ones a live version of this structure would require. **None is held.**

```
TARGET LICENCE STACK — NONE HELD
┌─────────────────────────────────────────────┐
│  Singapore — Issuance & Settlement           │
├─────────────────────────────────────────────┤
│  • CMS A/I LFMC (Fund Management)            │
│  • MPI DPT (Stablecoin Settlement)           │
│  • VCC Act (Fund Vehicle)                    │
│  • SFA §274/§275 (Exemption Basis)           │
│  • PSN02 (AML/CFT)                           │
└──────────────────────┬──────────────────────┘
│
┌──────────────────────▼──────────────────────┐
│  Korea — Asset Management                    │
├─────────────────────────────────────────────┤
│  • MOLIT AMC License                         │
│  • Capital Markets Act (REF Operation)       │
│  • FIPA (Foreign Capital Notification)       │
│  • Foreign Exchange Transactions Act         │
└──────────────────────┬──────────────────────┘
│
┌──────────────────────▼──────────────────────┐
│  Investor Jurisdictions — Eligibility        │
├─────────────────────────────────────────────┤
│  • US: Reg D 506(c) / Reg S                  │
│  • EU: MiFID II Professional Investor        │
│  • UAE: SCA / DIFC / ADGM Qualified Investor │
│  • HK: SFO Professional Investor             │
└─────────────────────────────────────────────┘
```

## Singapore Regulatory Framework

Singapore is the intended regulatory home. The relevant frameworks:

### Capital Markets Services (CMS) Licence

Fund management activities — including investment management of a VCC sub-fund — require a CMS licence issued by MAS. The applicable category would be **CMS A/I LFMC** (Accredited Investor / Institutional Investor Licensed Fund Management Company), which permits fund management for AI/II investors.

|  |  |
| --- | --- |
| **Licence held** | None |
| **Application filed** | None |
| **Partner licensee engaged** | None |
| **Intended path** | Operate initially under a licensed fund manager; own CMS A/I LFMC application at a later phase |

### Major Payment Institution (MPI) Licence

Stablecoin handling — receipt, conversion, and transmission of digital payment tokens — requires an MPI licence under the Payment Services Act, with the Digital Payment Token (DPT) service authorization specifically.

|  |  |
| --- | --- |
| **Licence held** | None |
| **Application filed** | None |
| **Partner licensee engaged** | None |
| **Today** | No live-value stablecoin is handled. Settlement is exercised on testnet against a mock USDC contract, which is outside the scope of the Payment Services Act. |

### Variable Capital Company (VCC) Structure

A VCC would be established under the Variable Capital Companies Act 2018, the purpose-built fund structure for Singapore-based investment vehicles. Each product tier would correspond to a separate sub-fund, providing legal asset segregation.

|  |  |
| --- | --- |
| **VCC entity** | Not incorporated |
| **Sub-funds in existence** | None |
| **Fund administrator / register of members** | None appointed; no register exists |

### SFA §274 and §275 Exemptions

A live offering would rely on the institutional investor (§274) and accredited investor (§275) exemptions under the Securities and Futures Act. There is no offering today. Compliance would be verified at the investor level (eligibility) and at the transfer level (smart contract gating).

|  |  |
| --- | --- |
| **Transfer restriction** | 180 days from issuance, enforced on-chain by the deployed token on testnet. The clock is set per parcel: each issuance seasons independently, and a later acquisition does not re-restrict units already held. See [Exit & Redemption](../how-it-works/exit-and-redemption.md) |
| **AI/II verification** | Designed as a pre-issuance KYC/KYB process; not operating, no investor has been verified |
| **Acknowledgment** | §275 acknowledgment would be executed at subscription; no subscription has occurred |

### MAS PSN02 (AML/CFT)

MAS PSN02 sets AML/CFT requirements for digital payment service providers and for fund management activities involving cross-border capital flows. OmniFlow has designed a program against those requirements. **The program is a design. It is not running, no onboarding has been performed, and it has not been reviewed by anyone.**

The design covers:

- KYC/KYB onboarding (institutional and accredited investor)

- Sanctions screening (OFAC, UN, EU, MAS)

- PEP screening and adverse media monitoring

- Source of funds verification

- Travel Rule compliance (transfers above SGD 1,500)

- Transaction monitoring and suspicious transaction reporting

A live program would require annual independent review. No reviewer has been engaged and no review has taken place.

### Digital Token Service Provider (DTSP) Framework

The Financial Services and Markets Act Part 9 framework, effective 30 June 2025, requires Singapore-based entities providing DPT services to overseas customers to hold a DTSP licence unless an alternative licence (such as MPI) covers the same activity. OmniFlow provides no DPT service to any customer and therefore does not currently fall within the framework. Beginning to do so would require a licence it does not hold.

## Korean Regulatory Framework

OmniFlow's target assets are Korean, which would require compliance with Korean fund management and foreign capital regulations. No asset has been acquired, so none of the following is currently in effect.

### Korean Asset Management Company (AMC)

A Korean REF holding the underlying assets would have to be operated by a MOLIT-licensed Korean AMC.

|  |  |
| --- | --- |
| **REF established** | None |
| **Korean AMC engaged** | None |
| **Own AMC acquisition** | Contemplated at a later phase; no target identified |

### Foreign Investment Promotion Act (FIPA)

Foreign LP capital commitments to Korean REFs are filed with Korea's Ministry of Trade, Industry and Energy under FIPA. A VCC commitment to a Korean REF would be filed at the time of capital call.

|  |  |
| --- | --- |
| **Filing entity** | A Korean AMC — none engaged |
| **Filing trigger** | Capital commitment from VCC to REF |
| **Filings made to date** | None |

### Foreign Exchange Transactions Act

Cross-border USD-to-KRW conversion is subject to Foreign Exchange Transactions Act disclosure requirements administered by the Bank of Korea and the Ministry of Economy and Finance.

### Tax Treaty Application

Distributions from a Korean REF to a Singapore VCC would be subject to 15% withholding under Article 10 of the Korea-Singapore tax treaty, applicable where the recipient qualifies for treaty benefits. The 10% tier under the same article requires a corporate holder of at least 25% of the capital of a company and is not expected to be available here. Treaty rates are inclusive of Korean local income tax; without relief the domestic rate of 22% applies.

|  |  |
| --- | --- |
| **Treaty article** | Korea-Singapore Tax Treaty Article 10 (Dividends) |
| **Treaty rate** | 15% withholding, inclusive of local income tax (subject to treaty benefit eligibility; 22% domestic rate applies without relief) |
| **Eligibility certification** | Would be renewed annually with the Korean tax authority; no certification has been sought |

The 15% rate is the input used throughout OmniFlow's published yield derivation. It is the reason the Tier 3 and Tier 4 yield targets are unpublished: 15% withholding plus fees reduces a 7% senior credit coupon to roughly 3.8% net, which is not an income product, so the target was withdrawn rather than published.

## Investor Jurisdiction Compliance

**No offering is open and no investor has been onboarded from any jurisdiction.** The table below is the eligibility model the platform is built against, not a list of jurisdictions currently being served. If an offering opens, it would be limited to jurisdictions where private placement to qualified investors is permitted, and the applicable framework would vary by investor jurisdiction:

| **Jurisdiction** | **Framework** | **Eligibility Standard** |
| --- | --- | --- |
| Singapore | SFA §274 / §275 | AI / II per SFA §4A |
| United States | Reg D 506(c) / Reg S | Qualified Purchaser / Accredited Investor |
| European Union | MiFID II | Professional Investor |
| United Kingdom | FCA HNW / Sophisticated | High Net Worth / Sophisticated Investor |
| United Arab Emirates | SCA / DIFC / ADGM | Qualified Investor |
| Hong Kong | SFO | Professional Investor |
| Switzerland | FinSA / FINMA | Professional / Qualified Investor |
| South Korea | — | **Restricted. Not eligible on this track.** |
| Other jurisdictions | Per local law | Per local law |

## Restricted Jurisdictions

The eligibility model excludes:

- Jurisdictions subject to comprehensive sanctions by OFAC, UN, EU, or MAS

- **South Korea.** The global track is not available to Korean entities or residents, whose participation in a Korean-asset offering raises extraterritorial securities law questions this structure does not answer. A separate Korean track is contemplated against the Korean token-securities regime commencing 2027-02-04. That track is not built.

- Jurisdictions where the offering of private placement securities to local persons is prohibited

## Regulatory Reporting

A licensed, operating version of this structure would file returns with MAS, Korean MOTIE, the Korean NTS and IRAS, on cadences set by each licence and framework.

**OmniFlow has filed nothing with any regulator, because it holds no licence and conducts no regulated activity.** There is no reporting calendar in operation and no supervisory relationship with MAS or with any Korean authority.

## Regulatory Change Management

Regulatory frameworks evolve, and the two that matter most here are moving: the Singapore DTSP framework took effect in June 2025, and Korea's token-securities regime commences 2027-02-04. OmniFlow tracks both, and the structure on this page is expected to change as they settle.

There are no investors to notify of such changes, and no LP agreement in force.
