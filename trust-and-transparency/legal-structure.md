# Legal Structure

This page describes the legal entity structure OmniFlow intends to build, the chain of legal rights it is designed to produce, and the counterparty roles it depends on.

**Status.** None of it exists yet. OmniFlow is pre-funding. No entity described below has been incorporated, no licence of any kind is held or applied for, no counterparty in any role has been engaged, and no legal opinion has been commissioned. What exists today is a smart contract deployment on the Base Sepolia **testnet** and an off-chain settlement workflow model. This page is a design document, not a disclosure of an operating structure. Read it as such.

## Entity Map

The structure below is the target design. It is intended to give investors Singapore-jurisdiction legal rights while retaining access to Korean asset economics. No box in this diagram has been incorporated.

```
┌────────────────────────────────────────────────────────────────┐
│                       INVESTOR LAYER                             │
│  Institutional and Accredited Investors — none today             │
│  (Testnet holders of an ERC-7943 uRWA token)                    │
└────────────────────────────┬───────────────────────────────────┘
│ Beneficial interest in
│ VCC sub-fund
▼
┌────────────────────────────────────────────────────────────────┐
│                  SINGAPORE ISSUANCE LAYER                        │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OmniFlow VCC (Variable Capital Company) — not formed     │   │
│  │  └─ Sub-Fund A — Tier 1 Listed REIT Income               │   │
│  │  └─ Sub-Fund B — Tier 2 Korea Logistics Income           │   │
│  │  └─ Sub-Fund C — Tier 3 Senior Development Credit        │   │
│  │  └─ Sub-Fund D — Tier 4 Opportunistic Credit             │   │
│  │                                                           │   │
│  │  Operator: a licensed fund manager — not engaged         │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OmniFlow Pte. Ltd. (Singapore Operating Company)        │   │
│  │  Intended holder of technology IP and protocol ops       │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  OmniFlow Foundation (Cayman, Phase 2+)                  │   │
│  │  $OMNI token issuance and governance — not active        │   │
│  └──────────────────────────────────────────────────────────┘   │
└────────────────────────────┬───────────────────────────────────┘
│ Limited partnership
│ commitment
▼
┌────────────────────────────────────────────────────────────────┐
│                ASSET JURISDICTION LAYER (KOREA)                  │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Korean Real Estate Fund (REF) — not established         │   │
│  │  Per-deal vehicle, intended to hold real estate or       │   │
│  │  real estate-backed credit positions                     │   │
│  │                                                           │   │
│  │  Operator: a Korean AMC — not engaged                    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│                         ┌─────────────┐                          │
│                         │             ▼                          │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  Underlying Assets — none acquired                        │  │
│  │  Target sector is Seoul Capital Area logistics at a       │  │
│  │  5.32% going-in cap (RSquare Q2 2026)                     │  │
│  └───────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

## Entity Roles

Each role below describes what the entity is intended to do. None has been incorporated, licensed or engaged.

**OmniFlow VCC (Singapore Variable Capital Company).** The intended issuance vehicle. Each product tier would correspond to a separate sub-fund, providing legal segregation between products. The VCC is purpose-built for fund operations under Singapore law. No VCC has been incorporated and no sub-fund exists.

**OmniFlow Pte. Ltd. (Singapore Operating Company).** The intended operating entity, holding technology IP and running the protocol's day-to-day functions. It would not itself issue securities and would not require a CMS licence; the regulated function would sit with a licensed fund manager.

**OmniFlow LFMC Pte. Ltd. (Capital Markets Services Licensee, Phase 2+).** A future MAS-licensed fund management company. No CMS licence is held and no application has been filed. Earlier phases would depend on a licensed fund manager acting as operator — none has been engaged.

**OmniFlow Foundation (Cayman Foundation Company, Phase 2+).** A future non-profit foundation intended to issue the $OMNI governance token and hold protocol governance separate from operating-company activity. The Foundation does not exist, the $OMNI token does not exist, and there is no token sale of any kind.

**Korean Real Estate Fund (REF).** A Korean fund vehicle that would be established under the Financial Investment Services and Capital Markets Act and managed by a MOLIT-licensed Korean Asset Management Company. Each deal would correspond to a dedicated REF. No REF has been established.

**OmniFlow Korea AMC (Phase 3+).** A future Korean Asset Management Company, contemplated for vertical integration of deal sourcing and asset management. No acquisition target has been identified.

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

This chain is the design, not the current state. None of its four links exists: the token is deployed on testnet only, there is no VCC sub-fund, no Korean REF, and no underlying asset.

In the intended structure, the on-chain RWA token would be a cryptographic representation of the investor's beneficial interest in the VCC sub-fund. The legal source of truth for ownership would be the VCC sub-register, maintained by the licensed fund manager. Where on-chain state and the sub-register disagreed, the sub-register would prevail as the legal record, and the reconciliation process described in Architecture Overview would exist to prevent and detect such disagreement. No sub-register exists today, so nothing is currently being reconciled.

## Why Singapore VCC

The Singapore Variable Capital Company structure was selected for the following reasons:

- **Regulatory clarity.** VCC is a purpose-built fund structure under Singapore law (VCC Act 2018), with clear regulatory treatment by MAS.

- **Cross-border efficiency.** Singapore's network of double-tax treaties (including the Korea-Singapore treaty, under which dividend income to a qualifying Singapore resident is withheld at 15% rather than the 22% domestic rate) provides tax-efficient access to Asian asset economics.

- **Sub-fund segregation.** Each product would be structured as a separate sub-fund, providing legal segregation of assets and liabilities between products.

- **Jurisdictional acceptance.** Singapore is a top-tier financial jurisdiction recognized by global institutional investors for compliance and dispute resolution standards.

- **Token issuance compatibility.** VCC sub-fund interests are capable of being issued in tokenized form. Whether a given on-chain representation is legally enforceable as beneficial interest is a question for counsel, and OmniFlow has not obtained an opinion on it.

## Why Not Tokenize the Korean REF Directly

Direct tokenization of Korean REF beneficial certificates would conflict with Korean securities law (the Capital Markets Act and Electronic Securities Act). The VCC intermediary structure is intended to resolve this by making the tokenized instrument the VCC sub-fund interest under Singapore law, rather than the underlying Korean REF certificate. This is OmniFlow's own structural reasoning. It has not been tested by counsel in either jurisdiction, and no legal opinion supports it.

## Counterparties

The structure above depends on counterparties in the following roles. **None of these roles is filled.** No party has been engaged, appointed, retained, or placed under a letter of intent in any of them, and no negotiation is disclosed as being under way.

| **Role** | **Status** |
| --- | --- |
| Singapore CMS LFMC | Not engaged |
| Singapore MPI DPT provider | Not engaged |
| Korean AMC | Not engaged |
| VCC service provider | Not engaged |
| Korean legal counsel | Not engaged |
| Singapore legal counsel | Not engaged |
| Auditor | Not engaged |
| Fund administrator | Not engaged |
| Custodian | Not engaged |
| Independent valuer | Not engaged |

Engaging a counterparty in any of these roles would be disclosed here. Until then, this table should be read as the list of things that still have to happen before OmniFlow can accept a single dollar.

## Legal Opinions

**No legal opinion has been commissioned or obtained on any aspect of this structure.** That includes the Singapore VCC structure, the SFA §274/§275 exemption basis, the Korean cross-border analysis, the tax treaty position, and the classification of any token. The structural reasoning on this page is OmniFlow's own and has not been validated by counsel.
