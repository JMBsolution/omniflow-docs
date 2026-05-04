# Regulatory Framework

This page summarizes the regulatory frameworks that govern OmniFlow's operations across the relevant jurisdictions. Detailed regulatory analysis is provided in legal opinions available to qualified investors under NDA.

## License and Regulatory Stack

OmniFlow operates within a multi-jurisdictional license stack. Each license addresses a specific regulated function.

```
REGULATORY STACK
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

OmniFlow's primary regulatory home is Singapore. The relevant frameworks:

### Capital Markets Services (CMS) License

Fund management activities — including investment management of the OmniFlow VCC sub-funds — require a CMS license issued by MAS. The applicable category is **CMS A/I LFMC** (Accredited Investor / Institutional Investor Licensed Fund Management Company), which permits fund management for AI/II investors.

|  |  |
| --- | --- |
| **Phase 1** | Fund management conducted under partnership with a CMS A/I LFMC partner |
| **Phase 2** | OmniFlow LFMC Pte. Ltd. CMS A/I LFMC application targeted for completion |
| **Application status** | [TBD — pre-application preparation] |
| **Expected timeline** | [TBD] |

### Major Payment Institution (MPI) License

Stablecoin handling — receipt, conversion, and transmission of digital payment tokens — requires an MPI license under the Payment Services Act, with the Digital Payment Token (DPT) service authorization specifically.

|  |  |
| --- | --- |
| **Phase 1** | Stablecoin settlement conducted through MPI DPT-licensed partner |
| **Phase 2** | OmniFlow MPI license application targeted |
| **Application status** | [TBD — pre-application preparation] |
| **Expected timeline** | [TBD] |

### Variable Capital Company (VCC) Structure

The OmniFlow VCC is established under the Variable Capital Companies Act 2018, the purpose-built fund structure for Singapore-based investment vehicles. Each product tier corresponds to a separate sub-fund within the VCC, providing legal asset segregation.

|  |  |
| --- | --- |
| **VCC entity** | [TBD — to be incorporated as part of Phase 1] |
| **Sub-fund count at launch** | 3 (Tier 1, 2, 3) |
| **Additional sub-funds planned** | Tier 4 (Phase 3), additional jurisdictions (Phase 3+) |

### SFA §274 and §275 Exemptions

OmniFlow's investor offering relies on the institutional investor (§274) and accredited investor (§275) exemptions under the Securities and Futures Act. Compliance with these exemptions is verified at the investor level (eligibility) and at the transfer level (smart contract gating).

|  |  |
| --- | --- |
| **§275 lock-up period** | 6 months from issuance, enforced on-chain |
| **AI/II verification** | Pre-issuance KYC/KYB process |
| **Acknowledgment** | §275 acknowledgment executed at subscription |

### MAS PSN02 (AML/CFT)

OmniFlow's anti-money laundering and counter-terrorism financing program is designed to satisfy MAS PSN02 requirements, which apply to digital payment service providers and to fund management activities involving cross-border capital flows.

The program covers:

- KYC/KYB onboarding (institutional and accredited investor)

- Sanctions screening (OFAC, UN, EU, MAS)

- PEP screening and adverse media monitoring

- Source of funds verification

- Travel Rule compliance (transfers above SGD 1,500)

- Transaction monitoring and suspicious transaction reporting

Annual independent review of the AML/CFT program is conducted by [TBD — independent reviewer].

### Digital Token Service Provider (DTSP) Framework

The Financial Services and Markets Act Part 9 framework, effective 30 June 2025, requires Singapore-based entities providing DPT services to overseas customers to hold a DTSP license unless an alternative license (such as MPI) covers the same activity. OmniFlow operates under the MPI partnership exemption in Phase 1; the planned MPI license acquisition in Phase 2 maintains the exemption.

## Korean Regulatory Framework

OmniFlow's underlying assets are sourced and managed in Korea, requiring compliance with Korean fund management and foreign capital regulations.

### Korean Asset Management Company (AMC)

The Korean REF that holds the underlying assets is operated by a MOLIT-licensed Korean AMC.

|  |  |
| --- | --- |
| **Phase 1** | Partner Korean AMC operates the REF on OmniFlow's behalf |
| **Phase 3** | OmniFlow Korea AMC acquisition targeted |
| **Acquisition status** | [TBD — target identification phase] |

### Foreign Investment Promotion Act (FIPA)

Foreign LP capital commitments to Korean REFs are filed with Korea's Ministry of Trade, Industry and Energy under FIPA. The OmniFlow VCC's commitment to each Korean REF is filed at the time of capital call.

|  |  |
| --- | --- |
| **Filing entity** | Partner Korean AMC (Phase 1-2); OmniFlow Korea AMC (Phase 3+) |
| **Filing trigger** | Capital commitment from VCC to REF |
| **Typical timeline** | [TBD] business days |

### Foreign Exchange Transactions Act

Cross-border USD-to-KRW conversion is subject to Foreign Exchange Transactions Act disclosure requirements administered by the Bank of Korea and the Ministry of Economy and Finance.

### Tax Treaty Application

Distributions from the Korean REF to the OmniFlow VCC are subject to 10% withholding under Article 10 of the Korea-Singapore tax treaty, applicable where the recipient qualifies for treaty benefits.

|  |  |
| --- | --- |
| **Treaty article** | Korea-Singapore Tax Treaty Article 10 (Dividends) |
| **Treaty rate** | 10% withholding (subject to qualifying ownership and treaty benefit eligibility) |
| **Eligibility certification** | Renewed annually with Korean tax authority |

## Investor Jurisdiction Compliance

OmniFlow accepts investors from jurisdictions where private placement to qualified investors is permitted. The applicable framework varies by investor jurisdiction:

| **Jurisdiction** | **Framework** | **Eligibility Standard** |
| --- | --- | --- |
| Singapore | SFA §274 / §275 | AI / II per SFA §4A |
| United States | Reg D 506(c) / Reg S | Qualified Purchaser / Accredited Investor |
| European Union | MiFID II | Professional Investor |
| United Kingdom | FCA HNW / Sophisticated | High Net Worth / Sophisticated Investor |
| United Arab Emirates | SCA / DIFC / ADGM | Qualified Investor |
| Hong Kong | SFO | Professional Investor |
| Switzerland | FinSA / FINMA | Professional / Qualified Investor |
| Other jurisdictions | Per local law | Per local law |

Jurisdiction-specific eligibility verification is performed during onboarding. Investors from jurisdictions where private placement to local persons is prohibited are not onboarded.

## Restricted Jurisdictions

OmniFlow does not accept investors from:

- Jurisdictions subject to comprehensive sanctions by OFAC, UN, EU, or MAS

- Jurisdictions whose securities laws may apply extraterritorially to the underlying asset offering — currently configured to exclude residents of South Korea for Korean asset products

- Jurisdictions where the offering of private placement securities to local persons is prohibited

The list of restricted jurisdictions is reviewed quarterly and updated as regulatory conditions change.

## Regulatory Reporting

OmniFlow files the regulatory reports required by each license and framework:

| **Report** | **Authority** | **Frequency** |
| --- | --- | --- |
| AML/CFT Annual Compliance Report | MAS | Annual |
| CMS LFMC Returns | MAS | Quarterly (under partner LFMC, Phase 1) |
| MPI DPT Returns | MAS | Quarterly (under partner MPI, Phase 1) |
| FIPA Capital Commitment Filings | Korean MOTIE | Per transaction |
| Korean Tax Treaty Benefit Certifications | Korean NTS | Annual |
| FATCA / CRS Information Returns | IRAS | Annual |

The reporting calendar is maintained by OmniFlow's compliance team and shared with MAS and Korean regulators on the standard cadence.

## Regulatory Change Management

Regulatory frameworks evolve. OmniFlow's compliance team monitors regulatory developments in Singapore, Korea, and primary investor jurisdictions, and adjusts protocol operations as required.

Material regulatory changes that affect investor rights, tax treatment, or product availability are communicated to investors through the institutional dashboard and the relationship manager. Where material changes require investor consent (for example, modifications to the LP agreement), consent procedures follow the standard disclosed in the LP Investment Agreement.
