# Trust & Security

OmniFlow is designed around five layers of trust. Each layer addresses a specific class of risk and is independently verifiable. We document each layer here so that institutional allocators, partner protocols, and AI agent operators can independently assess our integrity before committing capital.

## Layer 1 — Regulatory Trust

OmniFlow operates within Singapore's Monetary Authority of Singapore (MAS) regulatory framework. The protocol relies on licensed counterparties at each step:

- **Fund Operations**: Conducted by an MAS-licensed Capital Markets Services (CMS) Licensed Fund Management Company (LFMC). During Phase 1, fund operations are conducted under partnership with an established LFMC. OmniFlow's own CMS A/I LFMC application is targeted for Phase 2.

- **Stablecoin Settlement**: Conducted by an MAS Major Payment Institution (MPI) holding a Digital Payment Token (DPT) license. Phase 1 settlement uses a licensed MPI partner; OmniFlow's own MPI license is targeted for Phase 2.

- **Korean Asset Management**: Real estate assets are held through Korean Real Estate Funds (REFs) operated by partner Korean Asset Management Companies (AMCs). OmniFlow targets the acquisition of its own AMC in Phase 3.

The protocol issues securities to qualified investors only. Eligibility is governed by the Singapore Securities and Futures Act (SFA) §274 and §275 — the institutional investor (II) and accredited investor (AI) exemptions. All token transfers are gated at the smart contract level to enforce these eligibility rules.

## Layer 2 — Asset Trust

Underlying assets are sourced, audited, and valued by independent third parties:

- **Sourcing**: All deals are originated through Korean partner AMCs and validated through OmniFlow's investment committee.

- **Valuation**: Independent valuations are conducted by globally recognized firms (CBRE, JLL, Cushman & Wakefield).

- **Audit**: Annual audits are conducted by Big 4 accounting firms.

- **Title and Lease Verification**: Korean property registry, building registry, and lease documents are verified at acquisition and re-verified at NAV update intervals.

NAV updates are published on a defined schedule (monthly or event-based, depending on the product) and are attested on-chain via multi-signature Proof-of-Reserve.

## Layer 3 — Technical Trust

OmniFlow's smart contracts implement transfer restrictions, eligibility verification, and yield distribution at the protocol level. Key technical commitments:

- **Audits**: All production smart contracts are audited by at least two independent firms before mainnet deployment. See Smart Contract Audits.

- **Bug Bounty**: A continuous bug bounty program is operated through Immunefi.

- **Upgradeability**: Contract upgrades are governed by multi-signature with mandatory timelock. Critical parameters (token supply invariants, eligibility rules, KYC gating) are protected by constitutional limits and cannot be unilaterally modified.

## Layer 4 — Cryptographic Trust

OmniFlow does not rely on centralized claims for any verifiable property. Reserves, NAV updates, eligibility status, and supply totals are anchored on-chain through cryptographic attestations. Investors and AI agents can independently verify these properties without trusting OmniFlow.

## Layer 5 — Reputational Trust

OmniFlow's leadership, partners, and advisors are publicly identified. Partner LFMC, MPI, and AMC entities are disclosed in the Legal Structure page. Counterparty changes are announced in advance.
