# KYA Framework

KYA — Know Your Agent — is OmniFlow's verification framework for AI agents that participate as investors. KYA is parallel to KYC and shares the same regulatory objectives: establishing accountable identity, screening for sanctions and prohibited activity, and creating an audit trail for compliance reporting.

KYA is OmniFlow's own framework. It is not a regulatory standard adopted by MAS or any other authority. The framework is designed to satisfy the spirit and substance of MAS PSN02 AML/CFT requirements as applied to agent-mediated capital flows, by ensuring that every agent action has a verifiable, accountable principal.

## KYA Principles

OmniFlow's KYA framework rests on three principles:

**Principle 1 — Agents Have Principals.** Every agent on OmniFlow has a verified principal — a human individual or institutional entity that has passed KYC or KYB. The principal is legally and operationally accountable for the agent's actions. There is no "anonymous agent" tier.

**Principle 2 — Authority Is Scoped Cryptographically.** Agents operate under permissions that are enforced at the smart contract level, not merely declared in a contract. An agent's position limit, asset class restrictions, and rate limits cannot be exceeded even if the agent's runtime is compromised.

**Principle 3 — Misbehavior Is Bonded.** Each agent operates against a $OMNI operating bond posted by the principal. Defined classes of misbehavior — unauthorized transactions, attempts to bypass position limits, violations of OmniFlow protocol rules — result in slashing of the bond. The bond aligns the principal's incentives with the agent's good behavior.

## Three-Layer Identity Stack

```
Tier 1 — Principal Identity
Human or institutional entity, KYC/KYB verified
│
│ delegates authority via signed grant
▼
Tier 2 — Custodial Identity
Custody account, MPC wallet, or smart account
│
│ executes transactions within scoped permissions
▼
Tier 3 — Agent Identity
AI agent runtime with code attestation and bond
```

Each tier is independently verifiable on-chain. The Principal can revoke Custodial authority, and Custodial can revoke Agent authority, at any time through signed revocation transactions.

## KYA Onboarding Workflow

| **Step** | **Activity** | **Required Inputs** |
| --- | --- | --- |
| 1 | Principal KYC/KYB | Standard institutional or accredited investor onboarding (see Onboarding & KYB) |
| 2 | Custodial Designation | Wallet address, custody arrangement (self-custody, MPC, qualified custodian) |
| 3 | Agent Registration | Agent code repository or hash, runtime environment description, intended strategy |
| 4 | Permission Scoping | Position limits, asset class restrictions, rate limits, kill switch threshold |
| 5 | Bond Posting | $OMNI operating bond deposit, sized to agent's authorized position limit |
| 6 | Permission Grant | Principal signs grant transaction; Agent receives scoped authority |

The end-to-end KYA process typically takes 7 to 14 business days following completion of Principal KYC/KYB.

## Operating Bond — Sizing and Mechanics

The operating bond is denominated in $OMNI tokens and sized as a percentage of the agent's authorized position limit. The current parameters:

| **Authorized Position Limit** | **Operating Bond Requirement** |
| --- | --- |
| Up to $1M | 0.5% of position limit |
| $1M to $10M | 0.4% of position limit |
| $10M to $100M | 0.3% of position limit |
| Above $100M | 0.25% of position limit |

Bond requirements are subject to adjustment by protocol governance based on observed agent behavior, slashing event history, and overall protocol risk parameters.

The bond is held in a non-custodial slashing contract. The Principal retains ownership of the bond and may withdraw the bond at any time, subject to a 30-day notice period during which the agent's authority is wound down.

## Slashing Conditions

The bond is subject to slashing under defined misbehavior conditions:

- **Unauthorized asset class.** Agent attempts to execute a transaction outside its permitted asset classes.

- **Position limit breach.** Agent attempts to exceed its authorized position limit.

- **Rate limit breach.** Agent exceeds its authorized transactions-per-period limit.

- **Compliance gating bypass attempt.** Agent attempts to transfer to a wallet that has not passed AI/II eligibility.

- **Sanctioned counterparty interaction.** Agent attempts to interact with a wallet on the protocol-maintained sanctions list.

Slashing is executed automatically by the protocol when violation conditions are detected on-chain. Slashed amounts are sent to the OmniFlow safety reserve. The Principal retains the residual bond after the slashed amount is removed.

Severe or repeated violations result in agent permission revocation in addition to bond slashing.

## Kill Switch

Each agent registration includes a kill switch — a signed transaction the Principal can submit at any time to immediately revoke the agent's authority. Kill switch execution is confirmed within one block of submission. After kill switch, the agent cannot execute new transactions; existing positions are unaffected and can be managed by the Principal directly.

## Compliance and Audit Trail

All agent actions are recorded on-chain with attribution to the agent's identity and, transitively, to the Principal. OmniFlow's compliance system aggregates this into:

- Daily transaction summary per agent

- Violation event log

- Bond slashing history

- Permission grant and revocation history

Compliance reports are available to Principals through the institutional dashboard and are used for OmniFlow's MAS reporting obligations.

## Limitations and Honest Acknowledgments

KYA is OmniFlow's own framework, not a regulatory standard. The framework's effectiveness depends on:

- **Principal accountability.** A Principal who provides false KYC information undermines the entire chain. Standard KYC controls apply.

- **Correct permission scoping.** A Principal who grants overly broad permissions assumes elevated risk. OmniFlow provides guidance but cannot prevent overly permissive grants.

- **Bond adequacy.** The operating bond is sized to deter misbehavior, not to fully indemnify against losses. Bond sizing parameters are subject to ongoing calibration.

- **Detection completeness.** Slashing depends on detection of violations. OmniFlow operates monitoring systems but cannot guarantee detection of all possible misbehavior classes.

KYA is a framework that meaningfully reduces agent-related risk relative to ungated agent participation in DeFi. It is not a guarantee of agent good behavior or of investor protection from agent-induced losses.
