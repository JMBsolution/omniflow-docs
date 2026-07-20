# Trust & Security

OmniFlow is designed around five layers of trust. Each layer addresses a specific class of risk. We document each layer here so that institutional allocators, partner protocols, and AI agent operators can assess what has been built and, just as importantly, what has not.

Read this page against a single fact: OmniFlow is pre-funding. Everything deployed on chain is a Base Sepolia testnet demonstration. There is no licence, no fund, no asset, no investor and no appointed counterparty. The layers below describe an intended structure and the small part of it that currently exists.

## Layer 1 — Regulatory Trust

OmniFlow holds no licence of any kind and is not regulated by the Monetary Authority of Singapore. The structure is designed around licensed counterparties at each step, and none has been engaged:

- **Fund Operations**: designed to be conducted by an MAS-licensed Capital Markets Services (CMS) Licensed Fund Management Company (LFMC). No LFMC has been appointed.

- **Stablecoin Settlement**: designed to be conducted by an MAS Major Payment Institution (MPI) holding a Digital Payment Token (DPT) license. No MPI has been appointed.

- **Korean Asset Management**: real estate assets would be held through Korean Real Estate Funds (REFs) operated by a partner Korean Asset Management Company (AMC). No AMC has been appointed.

The eligibility model is drawn from the Singapore Securities and Futures Act (SFA) §274 and §275 — the institutional investor (II) and accredited investor (AI) exemptions. Nothing has been offered or issued to anyone under those exemptions.

On testnet, the token contract does enforce the eligibility gate it describes: every transfer is checked against an on-chain eligibility registry, and a transfer from or to an ineligible address reverts.

## Layer 2 — Asset Trust

OmniFlow holds no assets. No valuation has been commissioned, no independent valuer has been engaged, and no accounting firm audits anything. The intended process, for when assets exist, is:

- **Sourcing**: deals originated through a partner AMC and validated through an investment committee.

- **Valuation**: independent valuation by an appointed third-party valuation firm.

- **Audit**: annual audit of the fund vehicle by an appointed auditor.

- **Title and Lease Verification**: Korean property registry, building registry, and lease documents verified at acquisition and re-verified at NAV update intervals.

No NAV has been published, because there is nothing to value.

## Layer 3 — Technical Trust

The smart contracts are deployed on Base Sepolia testnet and have been exercised end to end. They implement transfer restrictions, eligibility verification, and a 180-day lock-up from issuance at the contract level. The token implements ERC-7943 (uRWA), which supplies the permissioned controls a restricted asset needs: eligibility gating, freezing, and issuer-forced transfers.

Three things are honest to state plainly:

- **No audit has been performed.** No smart-contract audit firm has reviewed this code. Independent audit before any mainnet deployment is a requirement, not an accomplishment.

- **No bug bounty exists.** There is no Immunefi program or any other bounty.

- **There is an open access-control gap.** The demo agent stops at workflow step 04 because steps 04 to 06 require human counterparties, and it will not write an outcome it cannot source. That halt is enforced by the off-chain operator workflow tracker and the demo script — it is **not** enforced by the contracts. `RwaToken.issue()` has no access control, so a certificate-holding eligible wallet could in principle mint itself fund tokens on chain. Closing that gap is future work.

Upgrade governance by multi-signature with a mandatory timelock is a design commitment for production deployment, not a property of the current testnet contracts.

## Layer 4 — Cryptographic Trust

What is on chain can be verified without trusting OmniFlow: contract bytecode, eligibility state, supply totals, lock-up timestamps and the full event history are readable at the deployed Base Sepolia addresses by anyone. That is the limit of what cryptography can attest to here. There are no reserves, no NAV attestation and no proof-of-reserve, because there is nothing off chain to prove.

## Layer 5 — Reputational Trust

No LFMC, MPI or AMC partner is disclosed, because none has been engaged. When counterparties are appointed, they will be named, and any subsequent change announced in advance.
