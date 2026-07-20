# Onboarding & KYB

This page sets out the onboarding standard OmniFlow is designed against: verified institutional and accredited investors only, with the process drawn against MAS PSN02 (AML/CFT), FATF recommendations, and the Singapore Securities and Futures Act §274/§275 exemptions.

**No investor has been onboarded.** This is a requirements specification, not a description of a desk in operation. The build records an onboarding decision; it does not perform identity verification, sanctions screening or document forensics, and no licensed vendor is engaged to perform them. Read the sections below as what a live deployment would require.

## Required Documents — Institutional Investors

For institutional entities, the following documents are required:

Corporate Identity

- Certificate of incorporation

- Certificate of good standing (issued within 6 months)

- Memorandum and articles of association

- Register of members / shareholder list

- Register of directors

Beneficial Ownership

- Ultimate Beneficial Owner (UBO) declaration covering all individuals owning 25% or more directly or indirectly

- Identity documents for each declared UBO (passport or national ID)

- Proof of address for each declared UBO (utility bill or bank statement issued within 3 months)

Financial Standing

- Audited financial statements (most recent two fiscal years)

- Bank statement evidencing operating account (within 3 months)

- Source of funds documentation specific to the proposed investment

Authorization

- Board resolution or equivalent authorizing the investment and identifying authorized signatories

- Power of attorney (where applicable)

- Identity and contact verification of authorized signatories

## Required Documents — Accredited Individual Investors

For individual investors qualifying under SFA §4A as Accredited Investors, the following documents are required:

- Government-issued photo identification (passport)

- Proof of address (within 3 months)

- Evidence of accredited investor status — net asset statement, financial asset statement, or annual income confirmation, depending on which qualifying threshold is met

- Source of funds documentation

- Tax residency declaration (FATCA / CRS self-certification)

## Verification Workflow

| **Step** | **Activity** | **Target Duration** |
| --- | --- | --- |
| 1 | Initial inquiry and preliminary eligibility check | Same day – 1 day |
| 2 | KYB document submission and entity verification | 1–2 days |
| 3 | AML/CFT screening (sanctions, PEP, adverse media) | Same day – 1 day |
| 4 | AI/II eligibility certification | 1 day |
| 5 | Subscription agreement execution | 1–3 days |
| 6 | RWA token issuance (after settlement) | 5–7 days |

Onboarding proper — steps 1 through 4, corresponding to step 01 of the settlement workflow — carries a target of **2 to 5 days**, which is what those four rows sum to. It is reported separately from settlement because it happens once per investor rather than once per subscription. Steps 5 and 6 sit inside the settlement cycle rather than inside onboarding: settlement, from payment received to token issued, targets **12 to 19 calendar days**. See Investment Flow.

These are targets in a model. No onboarding has been run against them, so there is no observed elapsed time to report.

## Document Submission

Documents would be submitted through the investor application, with the compliance review queue held in a separate operator application that is not part of the public build. The submission and review surfaces are not built.

Document authenticity would be established by cross-verification against official corporate registries where available, third-party document forensic analysis, and direct verification with the issuing authority where appropriate. None of these checks is implemented, and no forensics or registry-verification vendor is engaged.

## Risk Classification

After verification, each investor would be assigned a risk classification of Standard or Enhanced. Enhanced classification triggers additional due diligence and may include:

- Engagement of a third-party enhanced due diligence provider

- Additional source-of-funds documentation

- Enhanced beneficial ownership tracing

- Periodic re-verification at intervals shorter than the standard annual schedule

Risk classification is internal and would not be disclosed to the investor; any incremental documentation requirement would be communicated directly.

## Periodic Re-Verification

KYC/KYB is not intended as a one-time event. The design calls for continuous re-screening of active investors against updated sanctions lists, full re-verification at least annually, and an obligation on investors to report material changes to corporate structure, beneficial ownership, or contact information.

There are no active investors and no screening is running. Continuous screening requires a sanctions data vendor, which is not engaged.

## Restricted Persons

The global track excludes:

- **Korean entities and residents.** South Korea is restricted on the global track without exception. Nothing is offered to anyone today, and the global track would exclude Korean persons if it opened; a separate Korean track is dated to the commencement of Korea's token-securities regime on **2027-02-04** and is not built. Korea appears on this page as restricted and nowhere as accepted.

- Residents of other jurisdictions whose securities laws may apply extraterritorially to the underlying asset offering — determined per asset category, on the same principle that future asset categories may exclude residents of their respective asset jurisdictions

- Residents of jurisdictions where the offering of private placement securities to local persons is prohibited

- Persons appearing on OFAC, UN, EU, or MAS sanctions lists

- Persons identified as politically exposed in connection with adverse media risk indicators (subject to enhanced due diligence)

## Onboarding Refusal

OmniFlow reserves the right to decline onboarding without disclosed cause, in line with standard institutional banking and asset management practice. Anticipated bases for refusal include:

- Unverifiable beneficial ownership

- Source of funds insufficient or unverifiable

- Sanctions list match or close-match

- Adverse media indicating regulatory or law enforcement concern

- Jurisdictional ineligibility

Where a decision can be communicated, the prospective investor is informed and may withdraw without prejudice.

OmniFlow has no compliance function and cannot render an eligibility determination today. For diligence questions, contact archiyong217@gmail.com.
