# Settlement Layer

The Settlement Layer enables AI agents to pay for OmniFlow protocol services autonomously — without per-transaction human signing, without manually refilled gas balances, and without exposing private keys for each micropayment. It combines three Ethereum-aligned standards: **x402** (HTTP-native stablecoin payments), **ERC-4337** (account abstraction with paymasters), and **ERC-7710** (smart contract delegation).

This page describes why Settlement is a distinct layer in OmniFlow's Agent Stack, how the three standards combine in OmniFlow's design, and how the layer rolls out across Phase 1, Phase 1.5, and Phase 2.

## Why Settlement Is a Distinct Layer

Permissioning (Layer 2) establishes what an agent is allowed to do. Execution (Layer 5) provides the interface through which agents call OmniFlow services. Between these two, a gap exists in most agent frameworks: an agent may have authority and may have an interface, but cannot pay for the API call autonomously. A human must pre-fund the agent's wallet, refresh gas balances, and approve token allowances out-of-band.

This gap is the practical limit of "agent autonomy" in earlier protocols. An agent that requires a human to refill its balance every Tuesday is not autonomous in any meaningful sense.

The Settlement Layer closes this gap. It provides:

- **Pull-based pricing.** OmniFlow services advertise their price through the HTTP 402 status code (x402). An agent receives the price requirement and decides — within its delegated payment scope — whether to pay.

- **Session-key execution.** A session key (ERC-4337 + ERC-7710 combined) carries permission, payment ceiling, and duration in a single cryptographic primitive. The principal grants a session key once; the agent uses it for hundreds or thousands of micropayments without touching the principal's primary key.

- **Atomic permission-payment validation.** Permission and payment are validated in a single check. An agent cannot exceed payment scope by racing two separate checks (Time-of-Check-to-Time-of-Use safety).

Layer 4 (Settlement) and Layer 5 (Execution) operate as paired layers. Settlement happens within the Execution request-response cycle through HTTP 402 negotiation — the server responds with 402 carrying payment requirements, the agent answers with a payment header, the server returns the resource. The two layers are conceptually distinct but cycle-coupled in operation.

## The Three Standards

OmniFlow's Settlement Layer is built on three standards. Each addresses a different part of agent payment.

**x402.** The HTTP 402 Payment Required status code, dormant in the HTTP specification since 1996, was operationalized by the x402 protocol in 2025. A server requesting payment returns 402 with a `PAYMENT-REQUIRED` header containing chain, token, amount, and recipient. The client constructs a stablecoin transaction and resubmits with a `PAYMENT-SIGNATURE` header. The server validates and serves the resource. The x402 Foundation, launched in April 2026 by Coinbase and the Linux Foundation with founding members including Stripe, Cloudflare, AWS, Google, Microsoft, Visa, and Mastercard, stewards the protocol as an open standard.

**ERC-4337 (Account Abstraction).** ERC-4337 enables smart contract wallets to validate transactions through arbitrary logic, including session keys with restricted authority. The paymaster pattern allows a third party to sponsor gas, eliminating the need for the agent to hold the native gas token. Multiple production paymaster providers operate as of April 2026, including Coinbase CDP, Circle, Crossmint, Biconomy, Stackup, and ZeroDev.

**ERC-7710 (Smart Contract Delegation).** ERC-7710 defines an interface for one smart contract to delegate capability to another. In OmniFlow's Settlement Layer, ERC-7710 expresses the principal's grant of a payment scope to a session key. Combined with ERC-4337's signature validation, this enables a single session key to carry permission, payment ceiling, and duration. ERC-7710 remains in **Draft status as of May 2026**; OmniFlow tracks its progression toward Final status and will adapt to interface changes during finalization.

The three together solve what x402 alone cannot: how an agent makes thousands of micropayments without exposing the principal's key for each one. x402 alone would require the agent to hold its own EOA — a key-exposure surface that is unacceptable for institutional principals.

## How Settlement Works on OmniFlow

A typical agent payment on OmniFlow follows this flow:

1. **Session key issuance.** During KYA onboarding, the principal grants the agent a session key with explicit payment scope: `{daily_limit: 50,000 USDC, per_call_limit: 500 USDC, valid_until: 2026-12-31, permitted_recipient: omniflow_facilitator}`. The session key is signed by the principal's primary signer through an ERC-4337 user operation that combines ERC-7710 delegation.

2. **Service discovery.** The agent queries an OmniFlow endpoint (e.g., `GET /api/v1/risk-oracle/{assetId}`).

3. **Payment requirement.** OmniFlow's facilitator returns HTTP 402 with the `PAYMENT-REQUIRED` header: chain (Base), token (USDC), amount ($0.10), recipient (OmniFlow facilitator), nonce, and expiration timestamp.

4. **Atomic check and payment.** The agent's session key validates the requirement against its payment scope. If within scope, it constructs a payment transaction and submits via the `PAYMENT-SIGNATURE` header. The check (permission + payment ceiling + duration + nonce) is atomic — no race window exists between authorization and execution.

5. **Resource delivery.** OmniFlow validates the payment and returns the requested resource (HTTP 200).

6. **Treasury settlement.** Payments accrue directly to the OmniFlow treasury on Base — issuance and settlement share the same chain, so no cross-chain settlement leg exists.

## Mixed Scale — From Micropayment to Subscription

OmniFlow's services span four payment scales. The Settlement Layer handles each through the same x402 interface but with different settlement parameters.

| **Service** | **Typical Fee** | **Settlement Pattern** |
| --- | --- | --- |
| Risk Oracle query | $0.01–0.10 / query | Real micropayment, settled on Base via x402 |
| MCP tool call (subscription simulation, etc.) | $0.001–0.10 / call | Real micropayment, settled on Base via x402 |
| Distribution claim | Gas-only ($0.05–2) | Paymaster sponsorship; protocol covers under fee discount tier |
| Subscription & redemption | 0% — no platform fee | No fee leg; investor pays network gas only (sponsored where applicable) |

Subscription and redemption carry no platform fee — human-facing entry and exit are free by design, with monetization concentrated in the machine channel (Risk Oracle queries, premium API tiers) and recurring fund economics. Distribution claims are typically gas-only, with the OmniFlow paymaster sponsoring gas to keep claim UX frictionless.

## Single-Chain Alignment

OmniFlow's architectural commitment is that an issued RWA token resides on a single chain — **Base** for Phase 1. With issuance and settlement on the same chain, the Settlement Layer requires no cross-chain legs at all.

- **Issuance, settlement, and treasury: Base.** Subscriptions, redemptions, yield distributions, and per-call x402 micropayments all execute on Base. OmniFlow operates as its own facilitator during Phase 1 — no third-party facilitator dependency.
- **Deposit rails: multi-chain.** Investors may fund from other chains via the MPI partner's deposit rails (see Cross-Chain Architecture); the issued token itself never leaves Base.

This keeps the issued token single-chain while giving agents micropayment economics that a mainnet-issuance design could not offer.

## Phase Rollout

The Settlement Layer rolls out in three milestones.

**Phase 1 — Specification and protocol-fee scope (current).** The Settlement Layer is documented and its API surface is published. Activated payment scope is restricted to OmniFlow protocol fees only. Session keys are issued with `permitted_recipient: omniflow_facilitator`. External P2P payments to non-OmniFlow services are not enabled in Phase 1. Phase 1 uses third-party paymasters during ramp-up.

**Phase 1.5 — Self-paymaster operational.** OmniFlow operates its own ERC-4337 paymaster, replacing the third-party paymaster used in Phase 1. Distribution claim gas sponsorship is activated. Premium feature payments (priority Risk Oracle, advanced MCP tools) are enabled. The Settlement Layer undergoes an independent security audit before Phase 1.5 activation.

**Phase 2 — $OMNI bond and external facilitator.** Operating bonds are converted from Phase 1's stablecoin denomination to $OMNI. Fee discount tiers tied to $OMNI staking are activated (see [The OMNI Token](../trust-and-transparency/omni-token.md)). External facilitator partnerships are evaluated, enabling agents to settle payments to non-OmniFlow services within the same session-key scope, subject to per-jurisdiction legal review.

## Phase 1 Scope Limit

In Phase 1, the Settlement Layer's payment scope is restricted to **OmniFlow protocol fees only**. Agents cannot use OmniFlow-issued session keys to pay external counterparties, even if technically capable.

This restriction is deliberate. External P2P agent payments — for example, an agent paying a third-party data API — raise compliance questions across multiple jurisdictions:

- **Travel Rule applicability.** Singapore MAS PSN02 exempts micropayments below SGD 1,500 individually, but cumulative agent transactions per principal may reach reportable thresholds. Phase 1 limits payment scope to OmniFlow's own facilitator, which simplifies aggregation.
- **STR (Suspicious Transaction Report) chain of responsibility.** Agent-initiated external payments raise the question of who is the reporting entity. Phase 1's restricted scope avoids this question by routing all settlement through OmniFlow's compliance perimeter.
- **Cross-jurisdiction risk.** Agent payment to a Korean-hosted API may trigger Korean Capital Markets Act applicability. OmniFlow's structure assumes Singapore-only regulatory perimeter for Phase 1; external payment expansion requires additional legal review before activation.

Phase 2 expansion is contingent on legal review of agent-initiated external payment under each relevant jurisdiction.

## MCP Transport Compatibility

The x402 protocol operates over HTTP. OmniFlow's MCP server uses the **Streamable HTTP transport** — the standard remote-MCP transport since November 2025 — which is fully x402-compatible.

The legacy MCP-over-stdio transport, used in some local development environments, does not support x402 natively. Agents using stdio-mode MCP must either use a separate payment mechanism (typically EIP-712 signed permits resolved out-of-band) or run the MCP server in HTTP mode.

OmniFlow's hosted MCP endpoint (`https://mcp.omniflow.xyz`) operates in Streamable HTTP mode by default. See [MCP Server & SDK](mcp-server-and-sdk.md) for connection details.

## Compliance Notes

The Settlement Layer extends the [KYA Framework](kya-framework.md)'s principal-agent accountability model to agent payments. Several aspects warrant explicit acknowledgment.

**KYA payment scope is OmniFlow's framework, not a regulatory standard.** OmniFlow's position — that a principal's grant of a payment scope to an agent constitutes the principal's pre-authorization of in-scope payments — is OmniFlow's own legal position, not adopted by MAS or any other regulator. The position is designed to satisfy the spirit of MAS PSN02 AML/CFT requirements as applied to autonomous payment flows, by ensuring every agent-initiated payment has a verifiable, accountable principal.

**Travel Rule cumulative aggregation.** Per-call micropayments below the SGD 1,500 individual threshold are aggregated per principal across calendar periods to detect cumulative reportable activity. Aggregation is computed automatically and reported to compliance daily.

**STR responsibility.** Suspicious patterns in agent payment activity — sudden spikes, repeated near-ceiling payments, payments to flagged recipients — trigger STR review by OmniFlow compliance. The principal remains the underlying responsible party.

**Lawyer review required for Phase 2 expansion.** External agent payment, $OMNI fee discount classification under securities law, and cross-jurisdiction payment scope all require additional legal review before Phase 2 activation.

## Standards Status (May 2026)

OmniFlow tracks the maturity of each Settlement Layer dependency:

| **Standard** | **Status** | **OmniFlow Posture** |
| --- | --- | --- |
| x402 | Production; x402 Foundation launched April 2026 | Adopt; OmniFlow operates own facilitator |
| ERC-4337 | Production; multiple paymaster providers operating | Adopt; Phase 1 third-party paymaster, Phase 1.5 self-paymaster |
| ERC-7710 | Draft EIP, pending Final | Track; adapt to finalization changes |
| MCP Streamable HTTP | Standard remote transport since November 2025 | In production at `mcp.omniflow.xyz` |

Where a dependency is in Draft, OmniFlow uses the current Draft interface and commits to migrating to Final upon standardization.

## Limitations and Honest Acknowledgments

The Settlement Layer reduces but does not eliminate agent payment risk:

- **Session key compromise.** An agent runtime compromise within the session key's scope still allows in-scope payments to drain. The kill switch (Layer 1) revokes session-key authority within one block. Payment scope sizing — daily and per-call limits — should reflect the principal's risk tolerance.

- **Paymaster availability.** Phase 1 uses a third-party paymaster. Paymaster outage temporarily disables sponsored transactions for affected agents. Phase 1.5 self-paymaster reduces external dependency but introduces OmniFlow's own paymaster as a single point of failure.

- **Replay protection depends on facilitator correctness.** OmniFlow's facilitator strictly enforces nonce-bound payment headers. Replay attempts are rejected; this protection depends on facilitator implementation correctness, which is in scope for the Phase 1.5 audit.

- **Cross-rail settlement attack surface.** Phase 2's multi-chain expansion introduces the possibility of an agent attempting to exceed its daily limit by settling on multiple chains in parallel. OmniFlow's session key validates against a unified daily counter visible across rails.

For settlement-related risks disclosed to investors, see [Risk Disclosure](../legal/risk-disclosure.md).

## Open Items for Future Phases

The following Settlement Layer enhancements are planned but not in current scope:

- **KYA payment scope formal slashing conditions.** Phase 1.5 will extend the [KYA Framework](kya-framework.md)'s slashing conditions (currently five) to include payment-scope violations.

- **Audit 5: Settlement Layer.** The Settlement Layer will undergo independent security audit before Phase 1.5 self-paymaster activation. Audit firm selection in progress; results will be published in [Smart Contract Audits](../technical/smart-contract-audits.md).

- **External facilitator partnerships.** Phase 2 evaluation of third-party x402 facilitators for cross-jurisdiction payment scope expansion. Subject to legal review per jurisdiction.

- **Integration with $OMNI staking fee discounts.** Phase 2 activation of staked-$OMNI fee discount tiers. Detailed in [The OMNI Token](../trust-and-transparency/omni-token.md).
