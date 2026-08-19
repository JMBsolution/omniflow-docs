# Risk Disclosure

Last updated: [TBD]

Document version: [TBD]

**This Risk Disclosure is subject to legal review and has not been reviewed by counsel.**

**No OmniFlow product is currently open for subscription.** OmniFlow holds no licence, manages no fund, and holds no assets. What exists is a testnet demonstration on Base Sepolia. The risks below are therefore written for a product that does not yet exist; they describe what an investor would be exposed to if it did.

The most immediate risk is not on this list at all: this is a pre-funding company with no licence and no appointed counterparties, and the structure described throughout this documentation may never be built.

This Risk Disclosure is not exhaustive.

**You should not invest in any product of this kind unless you can afford to lose your entire investment.**

## 1. General Investment Risks

### 1.1 Risk of Loss

Investment in products of this kind carries material risk of partial or total loss of principal. Risk rises across the product ladder, and Tier 4 (Opportunistic Credit) sits at the top of it. Only Tier 2 (Korea Logistics Income) is live, on testnet; Tiers 1, 3 and 4 are not open, and no yield target is published for Tier 3 or Tier 4.

### 1.2 No Guaranteed Returns

The 3.43% net distribution yield published for Tier 2 is illustrative — a derivation from a stated cap rate, debt cost, fee assumption and treaty withholding rate, not an observed return. It may not be achieved. Actual returns would vary with underlying asset performance, market conditions, currency movements, operating expenses, and other factors.

### 1.3 No Performance History

OmniFlow has no performance history of any kind. No product has been operated, no distribution has been paid, and no asset has been held. There is nothing to report and no track record to evaluate.

## 2. Real Estate and Asset Risks

### 2.1 Real Estate Market Risk

Underlying real estate values fluctuate based on macroeconomic conditions, interest rates, supply and demand dynamics, regulatory changes, and other factors. Declines in real estate values reduce NAV and may reduce or eliminate distributions.

### 2.2 Tenant and Occupancy Risk

Income from real estate assets depends on tenant performance and occupancy levels. Tenant defaults, vacancies, or rent renegotiations reduce income.

### 2.3 Construction and Project Risk (Tier 3 Products)

PF loans are exposed to construction completion risk, cost overruns, project delays, and force majeure events. Repayment depends on completion guarantees from construction firms, the financial condition of which may deteriorate during the loan term.

### 2.4 Subordination Risk (Tier 4 Products)

Tier 4 products may include junior or mezzanine positions that absorb losses before senior creditors. In distressed scenarios, junior positions may receive nothing while senior creditors are made whole.

### 2.5 Recovery Risk on NPL (Tier 4 Products)

NPL acquisitions rely on recovery through asset auction or restructuring. Actual recovery may fall below modeled levels, potentially resulting in partial or total loss.

### 2.6 Concentration Risk

Every tier OmniFlow documents is concentrated in Korean real estate; no product is open for subscription. Were one opened, adverse developments in Korean real estate markets or Korean macroeconomic conditions would disproportionately affect investors. Future asset categories may reduce but will not eliminate geographic concentration.

## 3. Currency and Settlement Risks

### 3.1 FX Risk

Distributions and redemption proceeds would be converted from Korean won to USD and delivered in stablecoin. KRW/USD movements affect distribution amounts measured in USD or stablecoin terms. **The published 3.43% yield is stated unhedged and excludes any currency hedge carry**; no hedging arrangement is in place, and residual currency risk is borne by investors. A one-standard-deviation KRW move exceeds the entire published yield.

### 3.2 Stablecoin Risk

The intended settlement currency is a third-party stablecoin, carrying the risk of de-pegging, issuer failure, regulatory action against the issuer, or freezing of transfers. Today the deal's settlement token is a mock deployed by OmniFlow on testnet and is not a stablecoin at all; the separate agent-payment fee leg uses Circle's Base Sepolia testnet USDC, which carries no value.

### 3.3 Settlement Risk

Cross-border settlement would involve SWIFT messaging, correspondent banking, and currency conversion, none of which is arranged. The published settlement cycle target — 12 to 19 calendar days from payment received to token issued, with first-time onboarding of 2 to 5 days reported separately — is a target, not an observed time. No settlement has been performed with real money.

## 4. Smart Contract and Technology Risks

### 4.1 Smart Contract Risk

OmniFlow's smart contracts are subject to bugs, vulnerabilities, and unforeseen interactions.

**No smart contract audit has been performed.** No formal verification has been done and no bug bounty programme exists. The contracts have been exercised end to end on testnet by their own authors and nothing more. At least one gap is known and disclosed: `RwaToken.issue()` carries no access control, so an eligible wallet holding a subscription certificate could mint itself fund tokens without the off-chain workflow having completed. Step ordering is enforced by the off-chain operator record, not by the contracts.

An independent audit is required before these contracts handle anything of value.

### 4.2 Blockchain Risk

Base Sepolia, and any network OmniFlow may later deploy to, are subject to consensus failures, congestion, hard forks, and other systemic events that may temporarily or permanently disrupt the Services.

### 4.3 Wallet Security Risk

Loss of private keys, compromise of wallet infrastructure, or unauthorized transfers from your wallet are not recoverable through OmniFlow. Investors are solely responsible for wallet security.

### 4.4 Oracle Risk

The intended structure relies on oracle attestations for NAV, risk metrics, and reserve verification. No oracle is built and no attestation has ever been produced, so there is nothing to verify a NAV against today. Once built, oracle compromise or attestation error could result in incorrect on-chain state or NAV manipulation.

### 4.5 Cross-Chain Risk

A multi-chain deposit rail is described elsewhere in this documentation as an intended design. It is not built and no deposit rail partner is engaged. Were it built, compromise of a rail could affect an investor's deposit before settlement is confirmed, without affecting issued RWA tokens.

### 4.6 Layer 2 Sequencer Risk

OmniFlow's issuance chain is Base — currently Base Sepolia testnet — an Ethereum Layer 2 operated with a centralized sequencer. Sequencer downtime may temporarily delay transaction inclusion, including subscriptions, transfers, and distribution claims. Base provides an L1 escape hatch for forced transaction inclusion via Ethereum; however, during sequencer outages, timely execution is not guaranteed. Sequencer decentralization is on the Base roadmap but has not been realized as of this writing.

## 5. Regulatory and Legal Risks

### 5.1 Regulatory Change

The regulatory framework applicable to RWA tokens, stablecoin settlement, and cross-border tokenized fund structures is evolving in Singapore, Korea, and primary investor jurisdictions. Regulatory changes may affect product availability, tax treatment, or investor rights.

### 5.2 License Risk

**OmniFlow holds no licence of any kind, and no licensed partner is engaged.** The intended structure depends on a licensed fund manager, a payment institution, and a Korean asset manager, none of which has been appointed. Securing those relationships is a precondition to operating, and there is no assurance any of them will be secured, on any timeline or at all. This is the single largest regulatory risk in the structure.

### 5.3 Tax Treaty Risk

Distributions are modelled on the Korea–Singapore tax treaty's 15% withholding rate. The treaty's lower 10% tier requires a corporate holder of at least 25% of the capital of a company and is not expected to be available to a fund holding a Korean real estate fund interest. Treaty rates are inclusive of Korean local income tax.

Treaty benefits are not automatic. Relief depends on beneficial ownership, current certification of tax residence, filing before the payment date, and satisfying anti-treaty-shopping tests. Where Korean look-through rules apply to a foreign collective vehicle, relief may depend on documenting the residence of each underlying investor at each payment date; any portion that cannot be certified is taxed at the domestic rate. If relief is unavailable the domestic rate of 22% applies, inclusive of local income tax.

Separately, and frequently missed: proceeds on disposal of an interest deriving its value principally from Korean immovable property are taxable in Korea and are **not** capped by the treaty. Any model showing a tax-free exit is incorrect.

### 5.4 Cross-Border Securities Law Risk

The intended structure relies on the position that VCC sub-fund interests issued in Singapore to non-Korean investors are not subject to Korean securities law. No VCC sub-fund has been established and this position has not been tested or reviewed by counsel. Adverse determination by Korean authorities or courts would require structural modifications.

The global track is not available to Korean entities or residents. A Korean track is dated to the commencement of Korea's token-securities regime on 2027-02-04 and is not built.

### 5.5 Sanctions and AML Risk

Changes in sanctions designations, AML rules, or regulatory enforcement may require OmniFlow to suspend specific investors, freeze tokens, or restructure operations.

## 6. Counterparty Risks

### 6.1 Counterparty Appointment Risk

The intended structure operates through licensed partners in a fund management role, a payment institution role, and a Korean asset management role. **None is appointed.** The primary counterparty risk today is that these relationships may not be secured at all. Once appointed, failure, fraud, or regulatory action against a partner could disrupt operations or require migration.

### 6.2 Banking Counterparty Risk

The intended structure holds USD and KRW with banking partners during settlement; no banking relationship exists. Were one in place, bank failure or regulatory action could delay or impair settlement.

### 6.3 Service Provider Risk

The intended structure relies on KYC, document forensics, and audit service providers. None is engaged, and no KYC has been performed on anyone. Failure or compromise of such a provider, once engaged, could affect operations and result in compliance gaps.

## 7. Liquidity Risks

### 7.1 Lock-Up Period

Newly issued RWA units carry a 180-day transfer restriction from issuance, imposed by the issuer and not required by statute. During that period the affected parcel cannot be transferred.

**The restriction attaches per parcel, not per account.** Each issuance creates its own lot with its own unlock date, and a later subscription does not re-restrict units already seasoned. Parcels are spent oldest-first, so selling and repurchasing destroys seasoning rather than preserving it. Units acquired in a secondary transfer from another holder arrive unrestricted, because the restriction attaches to newly issued units and not to the act of receiving them.

Because the restriction is contractual rather than statutory it could in principle be varied by the issuer, and investors should not rely on it as a protection.

### 7.2 Secondary Market Liquidity

**There is no secondary market.** None has been established and no venue is engaged. Were one to exist, liquidity would depend on the number of qualified investors actively trading, and in early product stages or stressed conditions depth may be insufficient to exit positions at NAV-comparable prices. An investor should assume today that a position cannot be exited before maturity.

### 7.3 Maturity Redemption Timing

Maturity redemption depends on the underlying asset's realization schedule. Asset sale delays, refinancing failures, or other events may delay redemption beyond the scheduled maturity.

### 7.4 No Buyback

OmniFlow operates no issuer buyback programme and holds no treasury capable of funding one. No redemption guarantee and no price floor exists or is implied anywhere in this documentation.

## 8. Operational Risks

### 8.1 Operational Errors

Operational errors in fund accounting, distribution calculation, or cross-border settlement may occur. No fund administrator is appointed and no audit function exists, so the controls that would ordinarily catch such errors are not in place. Material errors would be corrected upon discovery, but corrections may delay or modify distributions.

### 8.2 Cybersecurity Risk

OmniFlow's systems are exposed to cybersecurity threats, and no defense is perfect. No security audit or penetration test has been performed. Successful attacks could disrupt operations, expose personal data, or affect on-chain state.

### 8.3 Key Personnel Risk

OmniFlow is a pre-funding company and its dependence on a very small number of people is correspondingly acute. It has no compliance, legal, or asset management function to lose; it has yet to build one. Loss of key personnel could halt the project entirely.

## 9. AI Agent Risks (Where Applicable)

### 9.1 Agent Behavior Risk

AI Agents may behave unexpectedly, including making suboptimal allocation decisions, exceeding authority through bugs, or failing to respond to changing conditions. The Principal bears full responsibility for agent behavior within authorized scope.

### 9.2 KYA Is Not Built

The KYA framework is a design. No agent has been verified, no bond mechanism exists, and no slashing or kill-switch contract has been written. It currently mitigates nothing. Were it built, it would reduce but not eliminate agent-related risk.

### 9.3 Agent Software Compromise

Compromise of an Agent's runtime environment may result in unauthorized transactions. The kill switch and revocation mechanisms that would mitigate this are not implemented.

### 9.4 Agent Key Compromise (Settlement Layer)

Settlement Layer payments are authorized by an ordinary agent key, not a session key. **No session key, payment ceiling, or duration limit is enforced cryptographically.** A compromised agent runtime can sign payments up to the payer's wallet balance; the only real ceilings are the per-request amount stated in the payment requirements and whatever that wallet actually holds. An agent wallet should therefore be funded with the float it needs and no more. The session-key model described in the [Settlement Layer](../for-ai-agents/settlement-layer.md) is what would remove this exposure and it is not built.

### 9.5 Facilitator Availability Risk

There is one facilitator, operated by OmniFlow, and it is a single point of failure. If it is unavailable or its gas key is unfunded, no payment settles. No ERC-4337 paymaster exists, of any kind.

### 9.6 Settlement Replay Risk

Replay is prevented by single-use nonces, checked off chain by the facilitator and enforced on chain by the token itself. The on-chain enforcement is what the guarantee rests on; the facilitator's check only converts a revert into a stated refusal. Neither has been audited.

### 9.7 No Travel Rule or Reporting Capability

There is no Travel Rule aggregation system, no Suspicious Transaction Report process, and no compliance perimeter. OmniFlow holds no licence and is not a reporting entity. These capabilities would have to be built and a licence obtained before agent payments carry real value.

## 10. $OMNI Token Risks (Phase 2+)

**The $OMNI token does not exist.** It is not issued, not live, and not available in any form. There is no private sale and no public sale. The Cayman Foundation associated with it in the intended structure is likewise not established. The risks below would apply only if the token were ever issued.

### 10.1 Token Volatility

The token's market value would fluctuate and may decline materially. Any operating bond denominated in it would be subject to that volatility.

### 10.2 Token Liquidity

Secondary market liquidity may be limited, particularly in early phases.

### 10.3 Regulatory Classification Risk

OmniFlow's own analysis treats the token as a non-security under Singapore law. That analysis has not been reviewed by counsel or confirmed by any regulator. Adverse classification by MAS or others could materially affect its status, transferability, and value.

## 11. Force Majeure

OmniFlow is not liable for failures or delays caused by events outside our reasonable control, including natural disasters, war, pandemic, governmental action, regulatory shutdown of underlying infrastructure, or large-scale failure of public blockchain networks.

## 12. No Investment Advice

This Risk Disclosure and OmniFlow's other documentation do not constitute investment, legal, tax, or other professional advice. You should consult your own advisors prior to investing.

## 13. Acknowledgment

No product is currently open for subscription, so no acknowledgment is being collected. Were a product opened, subscription would be conditioned on the investor acknowledging that they have read this Risk Disclosure, understand the risks described, and accept them — and that it is not exhaustive.
