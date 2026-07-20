# Agent-Native Overview

OmniFlow is designed for both institutional investors and AI agents that allocate capital autonomously. What is built today runs on Base Sepolia testnet; this page marks each layer accordingly.

## Why AI Agents Matter for RWA

A growing class of capital is allocated by AI agents — autonomous software systems that hold wallets, evaluate opportunities, and execute investment decisions without per-transaction human intervention. These systems are operated by treasury teams, asset managers, and emerging agent-native funds.

For RWA assets, agent participation has been blocked by four structural limitations in existing platforms:

1. **KYC frameworks assume human or corporate counterparties.** Onboarding requires passport photos, selfies, beneficial ownership trees — none of which apply to a software agent.

1. **Token standards assume human wallet operators.** Permission delegation, scoped authority, rate limiting, and kill switches are not part of standard token interfaces.

1. **Risk metrics are formatted for human readers.** Quarterly PDF reports and appraisal documents are not machine-consumable.

1. **Trading interfaces are UI-based.** Subscription, secondary market trading, and yield claiming are designed for clicks, not API calls.

OmniFlow is designed from inception to remove all four limitations.

## What Agent-Native Means at OmniFlow

Agents are treated as first-class participants in OmniFlow's design rather than as a feature bolted onto a human-only platform. Two layers of that design are built and exercised end to end on testnet. The rest is design, and is marked as such.

**Settlement — built, on Base Sepolia testnet.** An agent pays for a priced OmniFlow resource without a human signing each transaction and without holding the gas token. It requests the resource, receives HTTP 402 carrying a price it did not know in advance, signs an EIP-3009 `transferWithAuthorization`, and retries. A self-hosted facilitator recovers the signer, checks the authorization against eight refusal conditions, and relays it on chain while paying the gas itself. Settlement is a real transfer of testnet USDC, visible on the block explorer. See [Settlement Layer](settlement-layer.md).

**Execution — built, on Base Sepolia testnet.** An MCP (Model Context Protocol) server exposes four tools: three free — product listing, eligibility register lookup, and a description of the 00–08 settlement workflow — and one paid, a diligence note priced at 0.10 testnet USDC. See [MCP Server](mcp-server-and-sdk.md).

**Discovery — partial.** The free tools return product metadata, contract addresses, implemented token standards, and the transfer restriction as structured JSON, so an agent does not have to parse a PDF. There is no NAV oracle and no NAV to publish.

**Identity — design only.** KYA (Know Your Agent) is described in [KYA Framework](kya-framework.md) as a design. An eligibility register contract is deployed on testnet and gates transfers of the RWA token; no identity has been verified through it, and no other part of the KYA design is built.

**Permissioning, Risk, and Composition — design only.** Scoped delegation, the Risk Oracle, and permissioned DeFi composition are not implemented. No operating bond exists in any denomination; the $OMNI token is Phase 2+ and is not active.

## The Agent-Native Stack

The diagram below is the target architecture. Layers 4 and 5 are built on testnet; the others are design.

```
┌─────────────────────────────────────────────────────────────┐
│  Layer 7 — Composition                                       │
│  Permissioned DeFi integration, collateralization, vaults    │
├─────────────────────────────────────────────────────────────┤
│  Layer 6 — Risk                                              │
│  OmniFlow Risk Oracle (standardized metrics per asset)       │
├─────────────────────────────────────────────────────────────┤
│  Layer 5 — Execution                                         │
│  REST API, TypeScript/Python SDK, MCP Server                 │
├─────────────────────────────────────────────────────────────┤
│  Layer 4 — Settlement                                        │
│  x402 micropayments + ERC-4337 + ERC-7710 session keys       │
├─────────────────────────────────────────────────────────────┤
│  Layer 3 — Discovery                                         │
│  Machine-readable asset metadata, NAV oracle, attestations   │
├─────────────────────────────────────────────────────────────┤
│  Layer 2 — Permissioning                                     │
│  Scoped delegation, position limits, kill switch (ERC-7710)  │
├─────────────────────────────────────────────────────────────┤
│  Layer 1 — Identity                                          │
│  KYA verification, operator KYC, $OMNI operating bond        │
└─────────────────────────────────────────────────────────────┘
```

Layers 4 (Settlement) and 5 (Execution) operate as paired layers. The Execution interface returns HTTP 402 when payment is required; the Settlement Layer answers with a payment header within the same request-response cycle. The two are conceptually distinct but cycle-coupled in operation.

## What Is Built, What Is Not

| **Layer** | **Status** |
| --- | --- |
| Identity (KYA) | Not built. Eligibility register contract deployed on testnet; no identity verified |
| Permissioning (scoped delegation) | Not built |
| Discovery (metadata) | Built on testnet — structured product metadata over MCP |
| Discovery (NAV oracle) | Not built |
| Execution (MCP server, four tools) | Built on testnet |
| Execution (REST API, SDKs) | Not built |
| Settlement (x402 + EIP-3009 + self-hosted facilitator) | Built on testnet |
| Settlement (ERC-4337 session keys, paymaster) | Not built |
| Risk Oracle | Not built |
| Composition (collateralization) | Not built |

Nothing is deployed to mainnet. There are no real assets, no assets under management, no investors, and no distributions. The whole of the above runs against a mock settlement token and a fictional fund.

## Who Should Read This Section

The pages in this section are written for two audiences:

- **Agent operators** — humans or institutions deploying autonomous systems for capital allocation. Start with KYA Framework for the onboarding workflow.

- **Developers building agent infrastructure** — engineers integrating OmniFlow into agent runtimes, LLM tool interfaces, or autonomous trading systems. Start with MCP Server & SDK.

For institutional human investors, the How It Works section is the primary reference.

Machine-readable delivery of this documentation itself — llms.txt, per-page markdown outputs, a documentation MCP endpoint — is intended, so that agents can ingest these pages without scraping. None of it is published today.
