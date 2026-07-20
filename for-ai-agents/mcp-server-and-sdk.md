# MCP Server & SDK

OmniFlow's agent interface is a single small HTTP service — the agent rail — running against Base Sepolia testnet. It exposes free discovery endpoints, one payment-gated resource, an MCP (Model Context Protocol) server, and a self-hosted x402 facilitator.

**There is no SDK.** No TypeScript package, no Python package, and no published client library exist. There is also no general-purpose REST API beyond the endpoints listed below, and no sandbox environment separate from the testnet deployment — the deployment *is* the sandbox. Everything below is exercised against a mock settlement token and a fictional fund.

## HTTP Endpoints

| **Method** | **Path** | **Cost** |
| --- | --- | --- |
| GET | `/v1/products` | Free |
| GET | `/v1/contract-addresses` | Free |
| GET | `/v1/deals/{symbol}/diligence` | **Paid** — 0.10 testnet USDC via x402 |
| POST | `/mcp` | MCP Streamable HTTP, stateless |
| POST | `/facilitator/verify` | Free — payment verification, no gas spent |
| POST | `/facilitator/settle` | Free — relays a verified authorization on chain |

There is no API key and no authentication. Discovery is public, and the only gate anywhere on the rail is payment. Nothing on the rail writes to a chain except the facilitator's settlement call, which relays an authorization the payer signed.

The paid resource is the one endpoint worth describing in full. Requested without payment it answers HTTP 402 carrying the price, the asset, the recipient, and a validity window. The agent signs an EIP-3009 `transferWithAuthorization` and retries with an `X-PAYMENT` header. The facilitator verifies it against eight conditions — scheme or network mismatch, recipient mismatch, insufficient value, not yet valid, expired, bad signature, nonce already used, and insufficient payer balance — and settles on chain before the resource is returned. A failed check is a refusal with a stated reason, not a reverted transaction. See [Settlement Layer](settlement-layer.md).

The fee is denominated in Circle's Base Sepolia USDC rather than the deal's mock settlement token, because x402's `exact` scheme settles by calling `transferWithAuthorization` on the token itself and the mock token does not implement EIP-3009.

## MCP Server

The MCP server exposes the rail as tools callable by an LLM client over the Streamable HTTP transport. It is stateless: every request is independent, and nothing is kept between calls.

**Four tools. Three free, one paid.**

- `list_products` — available products with their standards, restrictions, and contract addresses. Free.

- `check_eligibility` — points at the eligibility register contract for a given address. Free. The tool does not proxy chain reads; it returns the registry address for the client to call directly. A positive result records a workflow decision and is not a verification of identity.

- `describe_workflow` — the 00–08 settlement workflow, including which steps an agent can execute and which resolve at human counterparties. Free.

- `get_diligence_note` — **paid.** The tool does not settle a payment itself, because MCP has no payment semantics and inventing one would be a private protocol wearing a standard's name. It returns the same x402 payment requirements the HTTP resource would, and the client settles over HTTP against the resource URL.

The MCP server enforces no KYA permissions, because no KYA permissions exist. It enforces payment on one tool and nothing else.

## What the Agent Does Not Do

The demo agent halts at workflow step 04. Steps 04 through 06 — FX and deposit, remittance, and the capital call and foreign investment filing — resolve at human counterparties that are not engaged, and the agent will not write an outcome it cannot source into an append-only record.

That halt is a design decision enforced by the off-chain operator workflow tracker and by the demo script. **It is not enforced by the smart contracts.** `RwaToken.issue()` has no access control, so a certificate-holding eligible wallet could in principle mint itself fund tokens on chain. The agent does not advance past step 04; it is not that it could not. Closing that on-chain gap is outstanding work.

## Source

The agent rail is roughly 900 lines of TypeScript with no database, no session state, and no framework. No licence has been chosen and no package is published.
