# Eligibility

OmniFlow products would be restricted to qualified investors, with participation conditioned on verification of investor status under applicable regulatory frameworks.

No offering is currently open and no investor has been onboarded. The current build is a Base Sepolia testnet demonstration. This page documents the eligibility model that would apply, not a live subscription process. Read the sections below as what a live deployment would require.

## Singapore: Accredited and Institutional Investors

A live offering would rely on the institutional investor (§274) and accredited investor (§275) exemptions under the Singapore Securities and Futures Act. There is no offering today, and nothing has been offered or issued to anyone under those exemptions. Eligible participants under that model would be:

**Institutional Investors (II)** as defined in SFA §4A:

- Banks licensed under the Banking Act

- Merchant banks

- Finance companies

- Insurance companies

- Holders of capital markets services licenses

- Sovereign wealth funds and central banks

- Pension funds and collective investment schemes

- Corporations with net assets exceeding SGD 10 million

**Accredited Investors (AI)** as defined in SFA §4A:

- Individuals with net personal assets exceeding SGD 2 million, or

- Individuals with net financial assets exceeding SGD 1 million, or

- Individuals with annual income exceeding SGD 300,000, or

- Corporations with net assets exceeding SGD 10 million

## Other Jurisdictions

The eligibility model contemplates investors from jurisdictions where private placement to qualified investors is permitted under local law, including but not limited to:

- **United States**: accredited investors under Rule 506(c) of Regulation D, and offshore purchasers under Regulation S. If a vehicle is later structured to rely on Investment Company Act §3(c)(7), the higher "qualified purchaser" standard would apply instead; that determination has not been made.

- **European Union**: Professional Investors under MiFID II

- **United Arab Emirates**: Qualified Investors under SCA, DIFC, and ADGM regimes

- **Hong Kong**: Professional Investors under SFO

South Korea is excluded. The global track is not available to Korean entities or residents. A separate Korean track is dated to the commencement of the Korean token-securities regime on 2027-02-04 and has not been built.

The eligibility model excludes investors who are residents of, or whose investment funds originate from, jurisdictions subject to comprehensive sanctions by OFAC, the United Nations, the European Union, or the Monetary Authority of Singapore.

## AI Agent Eligibility

The KYA (Know Your Agent) framework is designed to let AI agents participate as first-class investors. KYA verification would establish the agent's operating principal (a verified human or institutional KYB-passed entity) and the agent's permission scope. It is a design and is not built. The operating bond denominated in $OMNI is Phase 2; the $OMNI token is not live and no bond can be posted. No agent has been onboarded as an investor.

What exists today is the agent payment rail on Base Sepolia testnet: an HTTP 402 challenge, an EIP-3009 signed authorization, verification by a self-hosted facilitator, on-chain settlement, and a paid diligence note priced at 0.10 testnet USDC. See KYA Framework for the intended onboarding workflow.

## Verification Process

First-time onboarding carries a target of 2 to 5 days after all documentation is submitted. That is a target, not an observed figure — no investor has been verified. It is reported separately from the settlement cycle. Required documentation, the step-by-step workflow, and document specifications are detailed in Onboarding & KYB.

## Restricted Persons

The eligibility model does not admit:

- Residents of South Korea (the underlying asset jurisdiction; included to avoid potential extraterritorial application of Korean securities law)

- Residents of jurisdictions where the offering of private placement securities to local persons is prohibited

- Persons appearing on OFAC, UN, EU, or MAS sanctions lists

- Persons identified as politically exposed in connection with adverse media risk indicators (subject to enhanced due diligence)

OmniFlow has no compliance function and cannot render an eligibility determination today. For diligence questions, contact partners@omniflow.xyz.
