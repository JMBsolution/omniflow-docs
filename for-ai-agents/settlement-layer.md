# Settlement Layer

The Settlement Layer lets AI agents pay for OmniFlow protocol services autonomously on the **Base Sepolia testnet**, against a testnet fee token — without per-transaction human signing and without the agent holding the gas token. It is built on **x402** (HTTP-native stablecoin payments), with **ERC-4337** (account abstraction with paymasters) and **ERC-7710** (smart contract delegation) as committed extensions that are not implemented.

## What Is Built Today

Being precise about this matters more than the roadmap, so it comes first.

**Working now, on Base Sepolia.** An agent requests a paid resource and receives HTTP 402 carrying the price it did not know in advance. It signs an EIP-3009 `transferWithAuthorization` — an EIP-712 signature over a value, a recipient, a validity window and a single-use nonce — and retries. OmniFlow's facilitator recovers the signer, checks the authorization against the stated requirements, and relays it on chain, paying the gas itself. The agent never holds the gas token and never signs a raw transaction. Settlement is a real transfer of testnet USDC, visible on the block explorer.

**Not built yet, and therefore not claimed.** There are no ERC-4337 smart accounts, no session keys, and no ERC-7710 delegation instruments in the current implementation. The agent signs with an ordinary key. What a session key would add — a standing payment ceiling, a validity period and a permitted-recipient list enforced cryptographically rather than by the facilitator's checks — is described below as a Phase 2 design, not as a present capability.

The practical difference: today each payment is authorised individually and the ceiling is enforced by OmniFlow's own verification. Under the Phase 2 design the ceiling would travel with the key itself, so the agent could not exceed it even if OmniFlow's checks were wrong.

This page describes why Settlement is a distinct layer in OmniFlow's Agent Stack, how the three standards combine in OmniFlow's design, and how the layer rolls out across Phase 1, Phase 1.5, and Phase 2.

## Why Settlement Is a Distinct Layer

Permissioning (Layer 2) establishes what an agent is allowed to do. Execution (Layer 5) provides the interface through which agents call OmniFlow services. Between these two, a gap exists in most agent frameworks: an agent may have authority and may have an interface, but cannot pay for the API call autonomously. A human must pre-fund the agent's wallet, refresh gas balances, and approve token allowances out-of-band.

This gap is the practical limit of "agent autonomy" in earlier protocols. An agent that requires a human to refill its balance every Tuesday is not autonomous in any meaningful sense.

The Settlement Layer closes this gap. One of the three pieces below is built:

- **Pull-based pricing — built, on testnet.** OmniFlow services advertise their price through the HTTP 402 status code (x402). An agent receives the price requirement and decides whether to pay.

- **Session-key execution — design.** A session key (ERC-4337 + ERC-7710 combined) would carry permission, payment ceiling, and duration in a single cryptographic primitive, granted once by the principal and used for many micropayments without touching the principal's primary key. Not implemented.

- **Atomic permission-payment validation — design.** Validating permission and payment in a single check would remove the Time-of-Check-to-Time-of-Use gap between them. Not implemented; today the facilitator's checks are what enforce scope.

Layer 4 (Settlement) and Layer 5 (Execution) operate as paired layers. Settlement happens within the Execution request-response cycle through HTTP 402 negotiation — the server responds with 402 carrying payment requirements, the agent answers with a payment header, the server returns the resource. The two layers are conceptually distinct but cycle-coupled in operation.

## The Three Standards

OmniFlow's Settlement Layer is built on three standards. Each addresses a different part of agent payment.

**x402.** The HTTP 402 Payment Required status code, dormant in the HTTP specification since 1996, was operationalized by the x402 protocol in 2025. A server requesting payment returns 402 with a `PAYMENT-REQUIRED` header containing chain, token, amount, and recipient. The client constructs a stablecoin transaction and resubmits with a `PAYMENT-SIGNATURE` header. The server validates and serves the resource. The protocol is stewarded as an open standard by a foundation rather than by a single vendor, which is why OmniFlow adopts it rather than defining a payment scheme of its own.

**ERC-4337 (Account Abstraction).** ERC-4337 enables smart contract wallets to validate transactions through arbitrary logic, including session keys with restricted authority. The paymaster pattern allows a third party to sponsor gas, eliminating the need for the agent to hold the native gas token. Multiple production paymaster providers operate as of April 2026, including Coinbase CDP, Circle, Crossmint, Biconomy, Stackup, and ZeroDev.

**ERC-7710 (Smart Contract Delegation).** ERC-7710 defines an interface for one smart contract to delegate capability to another. In OmniFlow's Settlement Layer, ERC-7710 expresses the principal's grant of a payment scope to a session key. Combined with ERC-4337's signature validation, this enables a single session key to carry permission, payment ceiling, and duration. ERC-7710 remains in **Draft status as of May 2026**; OmniFlow tracks its progression toward Final status and will adapt to interface changes during finalization.

The three together solve what x402 alone cannot: how an agent makes thousands of micropayments without exposing the principal's key for each one. x402 alone would require the agent to hold its own EOA — a key-exposure surface that is unacceptable for institutional principals.

## How Settlement Works on OmniFlow

A typical agent payment on OmniFlow follows this flow:

The numbered flow below describes the **Phase 2 design**, in which the payment scope is carried by a session key. Steps 2 through 6 are implemented today; step 1 is not, and in the current implementation the agent signs each authorization with an ordinary key while OmniFlow's facilitator enforces the scope.

1. **Session key issuance — Phase 2, not yet built.** During KYA onboarding, the principal grants the agent a session key with explicit payment scope: `{daily_limit: 50,000 USDC, per_call_limit: 500 USDC, valid_until: 2026-12-31, permitted_recipient: omniflow_facilitator}`. The session key is signed by the principal's primary signer through an ERC-4337 user operation that combines ERC-7710 delegation.

2. **Service discovery.** The agent requests the one priced resource on the agent rail — the diligence note, over HTTP or through the paid MCP tool. There is no general-purpose REST API and no risk-oracle endpoint; see [MCP Server & SDK](mcp-server-and-sdk.md) for the full endpoint list.

3. **Payment requirement.** OmniFlow's facilitator returns HTTP 402 carrying the payment requirements: chain (Base Sepolia testnet), token (Circle's testnet USDC), amount (0.10 testnet USDC), recipient, nonce, and validity window.

4. **Check and payment.** The agent signs an EIP-3009 authorization over the stated value, recipient, validity window and a single-use nonce, and retries the request carrying it. OmniFlow's facilitator recovers the signer and checks recipient, amount, validity window, nonce reuse and payer balance before relaying anything on chain — a failed check is a refusal with a stated reason, not a reverted transaction. Under the Phase 2 design the ceiling and duration would additionally be enforced by the session key itself, so a scope breach would be impossible rather than merely rejected.

5. **Resource delivery.** OmniFlow validates the payment and returns the requested resource (HTTP 200).

6. **Settlement.** Payments accrue to a subscription account on Base Sepolia — a demo wallet, not a treasury. Issuance and settlement share the same chain, so no cross-chain settlement leg exists.

## Priced Resources

One resource is priced today: the diligence note, at 0.10 testnet USDC, reachable over HTTP or through the paid MCP tool. That is the entire fee surface.

The intended commercial shape is that machine-channel access is priced per call while human-facing subscription and redemption carry no platform fee, with monetization concentrated in the machine channel and recurring fund economics. No fee other than the diligence note has been implemented, no fee has ever been charged in anything but testnet tokens, and there is no revenue.

## Single-Chain Alignment

OmniFlow's architectural commitment is that an issued RWA token resides on a single chain. Today that chain is **Base Sepolia testnet**; there is no mainnet deployment.

- **Issuance and settlement on one chain.** Subscriptions, certificate issuance, and per-call x402 micropayments all execute on Base Sepolia. OmniFlow operates as its own facilitator — no third-party facilitator dependency.
- **Deposit rails.** A multi-chain deposit design is described elsewhere in this documentation; it is not built, and no deposit rail partner is engaged.

This keeps the issued token single-chain while giving agents micropayment economics that a mainnet-issuance design could not offer.

## Phase Rollout

The Settlement Layer rolls out in three milestones.

**Phase 1 — x402 payment, protocol-fee scope (current, on testnet).** An agent can discover a paid resource, receive a price over HTTP 402, sign an EIP-3009 authorization and have OmniFlow's facilitator settle it on chain. Payment scope is restricted to OmniFlow's own resources; the permitted recipient is fixed in the payment requirements the server issues, and external payments to non-OmniFlow services are not enabled. Gas is paid by OmniFlow's facilitator, which holds no authority over any OmniFlow contract — it can relay a signed authorization and nothing else, and its key is deliberately not the deployer key that owns eligibility, pause, and forced transfer.

**Phase 1.5 — Paymaster.** OmniFlow would operate its own ERC-4337 paymaster and activate gas sponsorship for distribution claims. No paymaster exists today, of any kind, third-party or otherwise — the facilitator simply pays gas when it relays. An independent security audit is intended before this phase; no audit has been performed and no audit firm has been engaged.

**Phase 2 — $OMNI bond and external facilitator.** An operating bond denominated in $OMNI would be introduced. No bond exists today in any denomination, and the $OMNI token is not issued (see [The OMNI Token](../trust-and-transparency/omni-token.md)). Fee discount tiers tied to $OMNI staking would be activated. External facilitator partnerships would be evaluated, enabling agents to settle payments to non-OmniFlow services within the same session-key scope, subject to per-jurisdiction legal review.

## Phase 1 Scope Limit

In Phase 1, the Settlement Layer's payment scope is restricted to **OmniFlow protocol fees only**. No session key exists to carry a broader scope — OmniFlow issues none — and external payments to non-OmniFlow services are not enabled.

The immediate reason is simply that nothing else is built: the permitted recipient is fixed in the payment requirements the server issues, and there is one priced resource.

The restriction is also deliberate, because external P2P agent payments — an agent paying a third-party data API, say — raise questions that would need answering first:

- **Travel Rule applicability.** Singapore MAS PSN02 exempts micropayments below SGD 1,500 individually, but cumulative agent transactions per principal could reach reportable thresholds. A single-recipient scope keeps aggregation tractable.
- **STR (Suspicious Transaction Report) chain of responsibility.** Agent-initiated external payments raise the question of who the reporting entity is. OmniFlow is not a reporting entity — it holds no licence — so this question would have to be resolved before any such expansion, not assumed away.
- **Cross-jurisdiction risk.** Agent payment to a Korean-hosted API may raise Korean Capital Markets Act questions.

These are open questions, not resolved positions. No counsel has reviewed them.

## MCP Transport Compatibility

The x402 protocol operates over HTTP. OmniFlow's MCP server uses the **Streamable HTTP transport** — the standard remote-MCP transport since November 2025 — which is fully x402-compatible.

The legacy MCP-over-stdio transport, used in some local development environments, does not support x402 natively. Agents using stdio-mode MCP must either use a separate payment mechanism (typically EIP-712 signed permits resolved out-of-band) or run the MCP server in HTTP mode.

OmniFlow's MCP server operates in Streamable HTTP mode, stateless, on the `/mcp` path of the agent rail. See [MCP Server & SDK](mcp-server-and-sdk.md) for the endpoint list and tool surface.

## Compliance Notes

The Settlement Layer extends the [KYA Framework](kya-framework.md)'s principal-agent accountability model to agent payments. Several aspects warrant explicit acknowledgment.

**KYA payment scope is OmniFlow's framework, not a regulatory standard** — and it is not built. The [KYA Framework](kya-framework.md) is a design; no principal has granted a payment scope to any agent. OmniFlow's position, that such a grant would constitute pre-authorization of in-scope payments, is its own and has not been adopted by MAS or reviewed by counsel.

**No compliance perimeter exists.** There is no Travel Rule aggregation system, no STR review process, and no compliance function. Those are things a licensed operator would need, and OmniFlow holds no licence. They are listed here as work required before real value moves, not as controls in place.

**Legal review required throughout.** External agent payment, $OMNI fee discount classification under securities law, and cross-jurisdiction payment scope all require legal review that has not been obtained.

## Standards Status (May 2026)

OmniFlow tracks the maturity of each Settlement Layer dependency:

| **Standard** | **Status** | **OmniFlow Posture** |
| --- | --- | --- |
| x402 | Production; x402 Foundation launched April 2026 | Adopt; OmniFlow operates own facilitator |
| EIP-3009 | Long-standing; implemented by Circle's USDC | **In use today** — the signed authorization x402's `exact` scheme settles with |
| ERC-4337 | Production; multiple paymaster providers operating | **Not yet implemented.** Committed for Phase 2 session keys |
| ERC-7710 | Draft EIP, pending Final | **Not yet implemented.** Tracked; adapt to finalization changes |
| MCP Streamable HTTP | Standard remote transport since November 2025 | **In use today** — stateless, on the agent rail's `/mcp` path |

Where a dependency is in Draft, OmniFlow uses the current Draft interface and commits to migrating to Final upon standardization.

## Limitations and Honest Acknowledgments

The Settlement Layer reduces but does not eliminate agent payment risk:

- **Agent key compromise.** In the current implementation the agent signs with an ordinary key, so a compromised agent runtime can sign payments up to the payer's balance. The only enforced ceilings are the per-request amount stated in the payment requirements and whatever the payer's wallet actually holds — so an agent wallet should be funded with the float it needs and no more. The session-key model described above is what removes this exposure, and it is not built yet.

- **Facilitator availability.** There is one facilitator, run by OmniFlow, and it is a single point of failure. If it is down or its key is unfunded, no payment settles.

- **Replay protection depends on facilitator correctness.** The facilitator rejects a reused nonce before relaying, and the token itself enforces single use on chain. The off-chain check is a clean refusal rather than a reverted transaction; the on-chain enforcement is what the guarantee actually rests on. Neither has been audited.

- **Cross-rail settlement attack surface.** A future multi-chain expansion would introduce the possibility of an agent exceeding a daily limit by settling on several chains in parallel. Defending that requires a unified counter across rails. No such counter exists, because there are no daily limits and no second rail.

For settlement-related risks disclosed to investors, see [Risk Disclosure](../legal/risk-disclosure.md).

## Open Items for Future Phases

The following Settlement Layer enhancements are planned but not in current scope:

- **KYA payment scope slashing conditions.** The [KYA Framework](kya-framework.md)'s slashing conditions are a design and none is implemented; payment-scope violations would be added to them.

- **Settlement Layer audit.** No security audit has been performed on any part of this system, and no audit firm has been engaged. An independent audit is required before any of this handles real value. See [Smart Contract Audits](../technical/smart-contract-audits.md).

- **External facilitator partnerships.** Phase 2 evaluation of third-party x402 facilitators for cross-jurisdiction payment scope expansion. Subject to legal review per jurisdiction.

- **Integration with $OMNI staking fee discounts.** Phase 2 activation of staked-$OMNI fee discount tiers. Detailed in [The OMNI Token](../trust-and-transparency/omni-token.md).
