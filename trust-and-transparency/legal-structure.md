# Legal Structure

This page describes OmniFlow's legal entity structure, the chain of legal rights from underlying assets to the on-chain RWA token, and the contractual relationships that govern the protocol. Detailed legal opinions are available to qualified institutional investors under non-disclosure agreement during due diligence.

## Entity Map

OmniFlow's legal structure is composed of multiple entities, each playing a defined role within its respective regulatory framework. The structure is designed to provide investors with Singapore-jurisdiction legal rights while maintaining efficient access to Asian asset economics.

```
┌────────────────────────────────────────────────────────────────┐
│                       INVESTOR LAYER                             │
│  Institutional and Accredited Investors                          │
│  (Holding ERC-3643 RWA Tokens in registered wallets)            │
└────────────────────────────┬───────────────────────────────────┘
│ Beneficial interest in
│ VCC sub-fund
▼
┌────────────────────────────────────────────────────────────────┐
│                  SINGAPORE ISSUANCE LAYER                        │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OmniFlow VCC (Variable Capital Company)                 │   │
│  │  └─ Sub-Fund A — Tier 1 Korea Prime Income               │   │
│  │  └─ Sub-Fund B — Tier 2 Korea Growth Plus                │   │
│  │  └─ Sub-Fund C — Tier 3 Korea Alpha Opportunity          │   │
│  │  └─ Sub-Fund D — Tier 4 Korea Core REIT (Phase 3)        │   │
│  │                                                           │   │
│  │  Operated by: [TBD — Partner LFMC] (Phase 1)             │   │
│  │  Operated by: OmniFlow LFMC Pte. Ltd. (Phase 2)          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OmniFlow Pte. Ltd. (Singapore Operating Company)        │   │
│  │  Protocol operations, technology, IR, partner management │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OmniFlow Foundation (Cayman, Phase 2+)                  │   │
│  │  $OMNI token issuance and governance                     │   │
│  └──────────────────────────────────────────────────────────┘   │
└────────────────────────────┬───────────────────────────────────┘
│ Limited partnership
│ commitment
▼
┌────────────────────────────────────────────────────────────────┐
│                ASSET JURISDICTION LAYER (KOREA)                  │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Korean Real Estate Fund (REF)                           │   │
│  │  Per-deal vehicle, holds underlying real estate or       │   │
│  │  real estate-backed credit positions                     │   │
│  │                                                           │   │
│  │  Operated by: [TBD — Partner Korean AMC] (Phase 1-2)     │   │
│  │  Operated by: OmniFlow Korea AMC (Phase 3+)              │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│                         ┌─────────────┐                          │
│                         │             ▼                          │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  Underlying Assets                                         │  │
│  │  Prime offices, logistics centers, hotels, PF loans,      │  │
│  │  bridge loans, NPLs, REIT beneficial interests            │  │
│  └───────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

## Entity Roles

**OmniFlow VCC (Singapore Variable Capital Company).** The primary issuance vehicle. Each product tier corresponds to a separate sub-fund within the VCC, providing legal segregation between products. The VCC structure is purpose-built for fund operations under Singapore law and provides tax-transparent treatment for cross-border investors who qualify under the Singapore-jurisdiction tax exemption framework.

**OmniFlow Pte. Ltd. (Singapore Operating Company).** The protocol's operating entity. Holds technology IP, employs Singapore-based staff, manages partner relationships, conducts investor relations, and operates the protocol's day-to-day functions. This entity does not directly issue securities and does not require a CMS license; the LFMC partner (Phase 1) or OmniFlow's own LFMC subsidiary (Phase 2+) holds the regulated function.

**OmniFlow LFMC Pte. Ltd. (Capital Markets Services Licensee, Phase 2+).** OmniFlow's own MAS-licensed Capital Markets Services Licensed Fund Management Company. Phase 1 fund operations are conducted under partnership with an established LFMC; OmniFlow's CMS A/I LFMC application is targeted for completion in Phase 2 following operational scale milestones.

**OmniFlow Foundation (Cayman Foundation Company, Phase 2+).** A non-profit foundation with no beneficial owners that issues the $OMNI governance token, deploys protocol smart contracts, and manages the protocol treasury. The Foundation structure is the standard for permissioned DeFi protocols and provides separation between protocol governance and operating company commercial activities. The Foundation is not active prior to Phase 2.

**Korean Real Estate Fund (REF).** A Korean fund vehicle established under the Financial Investment Services and Capital Markets Act and managed by a MOLIT-licensed Korean Asset Management Company. Each deal typically corresponds to a dedicated REF, providing asset-level segregation. The OmniFlow VCC sub-fund holds limited partnership interests in the relevant REF.

**OmniFlow Korea AMC (Phase 3+).** OmniFlow's own Korean Asset Management Company. Phase 1 and Phase 2 deals are managed by partner Korean AMCs; OmniFlow's acquisition of a Korean AMC is targeted for Phase 3, enabling full vertical integration of deal sourcing through asset management.

## Chain of Legal Rights

```
RWA Token (on-chain)
│
│  Represents — beneficial interest in
▼
VCC Sub-Fund Interest (Singapore)
│
│  Holds — limited partnership commitment in
▼
Korean REF Beneficial Certificate (Korea)
│
│  Holds — direct title or first-lien debt position over
▼
Underlying Real Estate or Loan Asset
```

The on-chain RWA token is a cryptographic representation of the investor's beneficial interest in the VCC sub-fund. The legal source of truth for ownership is the VCC sub-register, maintained by the LFMC under MAS oversight. The on-chain token mirrors this register through the reconciliation process described in Architecture Overview.

In the event of any inconsistency between the on-chain state and the VCC sub-register, the VCC sub-register prevails as the legal record. OmniFlow operates reconciliation processes designed to prevent such inconsistencies and to detect them immediately if they arise.

## Why Singapore VCC

The Singapore Variable Capital Company structure was selected for the following reasons:

- **Regulatory clarity.** VCC is a purpose-built fund structure under Singapore law (VCC Act 2018), with clear regulatory treatment by MAS.

- **Cross-border efficiency.** Singapore's network of double-tax treaties (including the Korea-Singapore treaty, under which dividend income to a qualifying Singapore resident is withheld at 15% rather than the 22% domestic rate) provides tax-efficient access to Asian asset economics.

- **Sub-fund segregation.** Each product is structured as a separate sub-fund, providing legal segregation of assets and liabilities between products.

- **Jurisdictional acceptance.** Singapore is a top-tier financial jurisdiction recognized by global institutional investors for compliance and dispute resolution standards.

- **Token issuance compatibility.** VCC sub-fund interests can be issued in tokenized form under MAS guidance, with the on-chain representation legally enforceable as beneficial interest.

## Why Not Tokenize the Korean REF Directly

Direct tokenization of Korean REF beneficial certificates would conflict with Korean securities law (the Capital Markets Act and Electronic Securities Act). The VCC intermediary structure resolves this by ensuring that the tokenized instrument is the VCC sub-fund interest (under Singapore law), not the underlying Korean REF certificate. This structural choice has been the subject of formal legal opinions from Korean and Singapore counsel; summaries are provided to qualified investors under NDA.

## Counterparty Disclosure

The following counterparties are central to OmniFlow's legal structure. Specific entity identities for the Phase 1 partners are disclosed during institutional due diligence.

| **Role** | **Entity** | **Status** |
| --- | --- | --- |
| Singapore CMS LFMC (Phase 1) | [TBD — Partner LFMC, disclosed under NDA] | Engaged |
| Singapore MPI DPT (Phase 1) | [TBD — Partner MPI, disclosed under NDA] | Engaged |
| Korean AMC (Phase 1) | [TBD — Partner Korean AMC, disclosed under NDA] | Engaged |
| VCC Service Provider | [TBD] | [TBD] |
| Korean Legal Counsel | [TBD] | [TBD] |
| Singapore Legal Counsel | [TBD] | [TBD] |
| Big 4 Auditor | [TBD] | [TBD] |

Counterparty changes are announced in advance to investors. Adverse counterparty changes (loss of license, material adverse event) trigger immediate disclosure under the standard disclosed in Trust & Security.

## Legal Opinions

The following legal opinions support OmniFlow's legal structure. Full opinions are available to qualified institutional investors under NDA.

| **Opinion Subject** | **Counsel** | **Issued** | **Status** |
| --- | --- | --- | --- |
| Singapore VCC structure and SFA §274/§275 exemptions | [TBD — Singapore counsel] | [TBD] | [TBD] |
| Korean cross-border structure and securities law applicability | [TBD — Korean counsel] | [TBD] | [TBD] |
| Korea-Singapore tax treaty application | [TBD — Tax counsel] | [TBD] | [TBD] |
| MAS Digital Token Guidance applicability to RWA tokens | [TBD — Singapore counsel] | [TBD] | [TBD] |
| $OMNI token classification (Phase 2+) | [TBD] | [TBD] | [TBD] |

Updates to legal opinions following regulatory changes or structural modifications are reflected in this list.
