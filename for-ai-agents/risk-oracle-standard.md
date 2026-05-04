# Risk Oracle Standard

The OmniFlow Risk Oracle publishes standardized risk metrics for every OmniFlow asset, formatted as machine-consumable structured data. The Oracle is designed to enable AI agents to perform automated suitability assessment, portfolio construction, and ongoing monitoring without parsing human-readable reports.

## What the Oracle Publishes

For each OmniFlow RWA token, the Risk Oracle publishes the following standardized metrics:

| **Metric** | **Description** | **Update Frequency** |
| --- | --- | --- |
| volatility_30d | 30-day annualized NAV volatility | Daily |
| liquidity_score | 0-100 score reflecting secondary market depth and bid-ask spreads | Daily |
| concentration_risk | Largest single-asset concentration as fraction of fund | At NAV update |
| counterparty_risk | Credit rating of largest counterparties (issuer, guarantor) | At underwriting; reviewed quarterly |
| underlying_ltv | Loan-to-value ratio for credit positions | At NAV update |
| stress_drawdown_p95 | 95th percentile drawdown under stress scenario | Quarterly |
| lockup_remaining_days | Days remaining until SFA §275 lockup expires | Daily |
| duration_remaining_days | Days until product maturity | Daily |
| nav_last_updated | Timestamp of most recent NAV attestation | Per NAV update |

## Access Patterns

The Risk Oracle is available through three access patterns:

**On-chain query.** Direct contract call to RiskOracle.getMetrics(assetAddress). Returns the structured metrics on-chain. Suitable for smart contract integrations and on-chain agents.

**REST API.** HTTP GET to /api/v1/risk-oracle/{assetId}. Returns JSON with the same metrics plus historical time series. Suitable for off-chain agent runtimes.

**MCP Server.** The OmniFlow MCP server exposes the Risk Oracle as a callable tool for LLM-based agents. Suitable for natural-language agent interfaces.

## Methodology and Attestation

Risk metrics are computed by OmniFlow's risk team in coordination with the partner LFMC, and are independently reviewed at the standard NAV attestation cadence (monthly or quarterly depending on the product).

Each Oracle update is signed by the LFMC, OmniFlow risk team, and the partner valuation provider through a 3-of-3 multi-signature attestation. The attestation is recorded on-chain alongside the metric values, enabling agents to verify the integrity of metrics they consume.

## Phase Evolution

The Risk Oracle's scope expands across Phases:

- **Phase 1.** Basic metrics (volatility, lockup, duration, NAV timestamp) with monthly updates. Stress and concentration metrics published quarterly.

- **Phase 2.** Full standard metric set with daily updates where applicable. Integration with external rating providers for counterparty risk.

- **Phase 3.** Cross-asset correlation matrix, agent-readable factor decomposition, scenario analysis API.

The current Oracle status and metric availability per asset are published on the Smart Contract Addresses page.

## Limitations

Risk metrics are estimates and are subject to model risk. Specifically:

- **Volatility metrics** depend on the NAV update history and may underestimate true volatility in early product life when limited NAV updates are available.

- **Liquidity scores** depend on observed secondary market activity and may not reflect liquidity under stress conditions.

- **Stress drawdown estimates** are scenario-based and do not bound actual losses. Actual losses may exceed stress estimates under conditions not modeled.

- **Counterparty risk ratings** rely on third-party rating providers and may lag actual creditworthiness changes.

Agents and human investors are responsible for their own suitability assessment. The Risk Oracle is a standardized input, not a substitute for due diligence.
