# Agent-Native Overview

OmniFlow is built for both institutional investors and AI agents that allocate capital autonomously.

## Why AI Agents Matter for RWA

A growing class of capital is allocated by AI agents — autonomous software systems that hold wallets, evaluate opportunities, and execute investment decisions without per-transaction human intervention. These systems are operated by treasury teams, asset managers, and emerging agent-native funds.

For RWA assets, agent participation has been blocked by four structural limitations in existing platforms:

1. **KYC frameworks assume human or corporate counterparties.** Onboarding requires passport photos, selfies, beneficial ownership trees — none of which apply to a software agent.

1. **Token standards assume human wallet operators.** Permission delegation, scoped authority, rate limiting, and kill switches are not part of standard token interfaces.

1. **Risk metrics are formatted for human readers.** Quarterly PDF reports and appraisal documents are not machine-consumable.

1. **Trading interfaces are UI-based.** Subscription, secondary market trading, and yield claiming are designed for clicks, not API calls.

OmniFlow is designed from inception to remove all four limitations.

## What Agent-Native Means at OmniFlow

Agents at OmniFlow are not a feature added on top of a human-only platform. They are first-class participants integrated into the protocol's design.

**Identity.** Agents pass KYA (Know Your Agent) verification, a parallel to KYC tailored to autonomous systems. KYA establishes the agent's operating principal (a verified human or institutional entity), the agent's permission scope, and an operating bond denominated in $OMNI tokens. See KYA Framework.

**Permissioning.** Agent authority is enforced cryptographically through scoped delegation. An agent operating under a $10M position limit cannot exceed that limit at the smart contract level, even if instructed to do so. Rate limits, asset class restrictions, and kill switches are protocol-enforced.

**Discovery.** Asset metadata is published in machine-readable form. An agent can query the available products, their target yields, lock-up status, NAV, and risk metrics through a standardized interface, without parsing PDF reports.

**Execution.** Subscription, redemption, secondary market trading, and yield claiming are accessible through TypeScript and Python SDKs, REST APIs, and a native MCP (Model Context Protocol) server.

**Settlement.** Agents pay for OmniFlow protocol services autonomously through x402-based session keys (ERC-4337 + ERC-7710). Payment scope — daily limits, per-call limits, duration, permitted recipient — is delegated by the principal once and validated atomically with each call, removing the need for per-transaction human signing or pre-funded gas relayers. See [Settlement Layer](settlement-layer.md).

**Risk.** Standardized risk metrics — volatility, liquidity score, concentration risk, counterparty risk, stress-test drawdown — are published per asset through the OmniFlow Risk Oracle. Agents consume these as structured data.

**Composition.** Agents can compose OmniFlow positions with other DeFi primitives within OmniFlow's permissioned environment, including collateralization for stablecoin liquidity (Phase 3+).

## The Agent-Native Stack

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

## What Is Live, What Is Coming

OmniFlow is honest about the current state of the agent stack. Some layers are operational from Phase 1; others are in active development for Phase 2 and beyond.

| **Layer** | **Status** |
| --- | --- |
| Identity (KYA) | Phase 1 — operational |
| Permissioning (ERC-7710 delegation) | Phase 1 — operational |
| Discovery (metadata, NAV oracle) | Phase 1 — operational |
| Execution (REST API, SDK) | Phase 1 — operational |
| Execution (MCP Server) | Phase 1 — operational |
| Settlement (x402 + session keys) | Phase 1 — spec, OmniFlow protocol fee scope; Phase 1.5 — self-paymaster; Phase 2 — external facilitator |
| Risk Oracle (standard metrics) | Phase 1 — basic; Phase 2 — full standard |
| Composition (collateralization) | Phase 3 — planned |

We deliberately avoid claiming production-ready functionality for capabilities not yet deployed. Status above reflects the actual deployment state and is updated with each release.

## Who Should Read This Section

The pages in this section are written for two audiences:

- **Agent operators** — humans or institutions deploying autonomous systems for capital allocation. Start with KYA Framework for the onboarding workflow.

- **Developers building agent infrastructure** — engineers integrating OmniFlow into agent runtimes, LLM tool interfaces, or autonomous trading systems. Start with MCP Server & SDK.

For institutional human investors, the How It Works section is the primary reference.
