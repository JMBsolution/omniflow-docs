# Risk Oracle Standard

The Risk Oracle is a proposed standard for publishing risk metrics as machine-consumable structured data, so that an AI agent can perform suitability assessment and ongoing monitoring without parsing human-readable reports.

**The Risk Oracle is not built.** No oracle contract is deployed, no oracle code exists, and no metric has ever been published. There is no NAV history to compute volatility from, no secondary market to score liquidity against, and no portfolio to measure concentration in. This page is a schema, not a service.

What does exist is narrower and worth being precise about: a single paid diligence note, served over the agent rail at 0.10 testnet USDC, containing the gross-to-net yield bridge for the one live product with each line's source or stated assumption attached. That is machine-readable analysis an agent can pay for and consume. It is not a risk oracle, it is not updated on a cadence, and it covers one product. See [MCP Server](mcp-server-and-sdk.md).

## Proposed Metric Schema

The intended metric set for each RWA token:

| **Metric** | **Description** | **Update Frequency** |
| --- | --- | --- |
| volatility_30d | 30-day annualized NAV volatility | Daily |
| liquidity_score | 0-100 score reflecting secondary market depth and bid-ask spreads | Daily |
| concentration_risk | Largest single-asset concentration as fraction of fund | At NAV update |
| counterparty_risk | Credit rating of largest counterparties (issuer, guarantor) | At underwriting; reviewed quarterly |
| underlying_ltv | Loan-to-value ratio for credit positions | At NAV update |
| stress_drawdown_p95 | 95th percentile drawdown under stress scenario | Quarterly |
| lockup_remaining_days | Days remaining until the issuer-imposed transfer restriction lapses on the oldest restricted parcel | Daily |
| duration_remaining_days | Days until product maturity | Daily |
| nav_last_updated | Timestamp of most recent NAV attestation | Per NAV update |

The update frequencies in the table are design targets for a service that does not run. No metric is being updated at any frequency.

## Unresolved Design Questions

Two problems have to be answered before any of this is worth building, and neither is answered today.

**Who attests.** A metric an agent consumes is only as good as the signature on it. Attestation by the issuer alone is self-certification. Independent attestation requires a valuation provider and a fund manager, and none is engaged — so there is no attestation scheme to describe, and describing a multi-party signing arrangement between parties that do not exist would be the wrong thing to publish.

**What the early metrics would mean.** Volatility computed from a short NAV history understates volatility. A liquidity score computed from a market with no participants is not a measurement. The metrics that are cheapest to publish first are the ones that carry the least information, and publishing them early would misrepresent their reliability.

## Limitations

Were the Oracle built, its metrics would be estimates subject to model risk:

- **Volatility metrics** depend on NAV update history and may understate true volatility in early product life.

- **Liquidity scores** depend on observed secondary market activity and may not reflect liquidity under stress.

- **Stress drawdown estimates** are scenario-based and do not bound actual losses.

- **Counterparty risk ratings** depend on third-party providers and may lag actual creditworthiness changes.

Agents and human investors are responsible for their own suitability assessment. A standardized metric feed would be an input to due diligence, never a substitute for it.
