# KYA Framework

KYA — Know Your Agent — is OmniFlow's proposed verification framework for AI agents that participate as investors. It is parallel to KYC and shares the same objectives: establishing accountable identity, screening for sanctions and prohibited activity, and creating an audit trail.

**KYA is a design. It is not built.** No agent has been verified, no principal has been onboarded, no bond has been posted in any denomination, and no slashing or kill-switch contract exists. The only related component deployed is an eligibility register on Base Sepolia testnet, which gates transfers of the RWA token; entries in it are workflow decisions recorded for the demonstration, not verifications of identity.

KYA is also OmniFlow's own framework, not a regulatory standard adopted by MAS or any other authority. OmniFlow holds no licence of any kind. The framework is drafted with MAS PSN02 AML/CFT objectives in mind, but it has not been reviewed by a regulator or by counsel.

The rest of this page describes the intended design.

## KYA Principles

OmniFlow's KYA framework rests on three principles:

**Principle 1 — Agents Have Principals.** Every agent would have a verified principal — a human individual or institutional entity that has passed KYC or KYB — legally and operationally accountable for the agent's actions. No "anonymous agent" tier.

**Principle 2 — Authority Is Scoped Cryptographically.** The intent is that an agent's position limit, asset class restrictions, and rate limits are enforced on chain rather than merely declared, so that they hold even if the agent's runtime is compromised. No such enforcement exists today. The deployed contracts do not check agent authority at all: `RwaToken.issue()` carries no access control, so an eligible wallet holding a subscription certificate could in principle mint itself fund tokens. Closing that gap is outstanding work.

**Principle 3 — Misbehavior Is Bonded.** The design calls for an operating bond posted by the principal, with defined classes of misbehavior resulting in slashing. No bond mechanism is implemented. The $OMNI token, in which a bond would eventually be denominated, is Phase 2+ and is not active.

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

In the design, each tier is independently verifiable on chain, and the Principal can revoke Custodial authority — and Custodial the Agent's — through signed revocation transactions. None of the three tiers is implemented.

## KYA Onboarding Workflow

| **Step** | **Activity** | **Required Inputs** |
| --- | --- | --- |
| 1 | Principal KYC/KYB | Standard institutional or accredited investor onboarding (see Onboarding & KYB) |
| 2 | Custodial Designation | Wallet address, custody arrangement (self-custody, MPC, qualified custodian) |
| 3 | Agent Registration | Agent code repository or hash, runtime environment description, intended strategy |
| 4 | Permission Scoping | Position limits, asset class restrictions, rate limits, kill switch threshold |
| 5 | Bond Posting | Operating bond deposit, sized to agent's authorized position limit |
| 6 | Permission Grant | Principal signs grant transaction; Agent receives scoped authority |

No step of this workflow is implemented, and no processing time is quoted because none has been observed.

## Operating Bond

The design calls for an operating bond posted by the principal and sized as a percentage of the agent's authorized position limit, held in a non-custodial slashing contract with the principal retaining ownership.

Bond sizing parameters, the notice period for withdrawal, and the denomination are not settled and are therefore not published. No slashing contract has been written.

## Slashing Conditions

The design contemplates slashing under the following misbehavior conditions:

- **Unauthorized asset class.** Agent attempts to execute a transaction outside its permitted asset classes.

- **Position limit breach.** Agent attempts to exceed its authorized position limit.

- **Rate limit breach.** Agent exceeds its authorized transactions-per-period limit.

- **Compliance gating bypass attempt.** Agent attempts to transfer to a wallet that has not passed AI/II eligibility.

- **Sanctioned counterparty interaction.** Agent attempts to interact with a wallet on the protocol-maintained sanctions list.

Under the design, slashing executes when violation conditions are detected on chain, and severe or repeated violations revoke agent permissions in addition to slashing. Detection, slashing, and the destination of slashed amounts are all unimplemented.

## Kill Switch

The design includes a kill switch — a signed transaction the Principal can submit to revoke the agent's authority, after which the agent cannot execute new transactions while existing positions remain manageable by the Principal directly. No kill switch is implemented, and no execution latency is quoted because none has been measured.

## Compliance and Audit Trail

The design records agent actions on chain with attribution to the agent and, transitively, to the Principal, aggregated into a transaction summary, a violation log, a slashing history, and a permission grant and revocation history.

What exists today is narrower: the demonstration keeps an append-only event log of workflow steps in the off-chain operator application. There is no compliance reporting system, no investor dashboard delivering reports, and no regulatory reporting obligation, because OmniFlow holds no licence and is not a reporting entity.

## Limitations and Honest Acknowledgments

The most important acknowledgment is the one at the top of this page: KYA is a design, and an unbuilt design protects nobody. Assuming it were built, its effectiveness would still depend on:

- **Principal accountability.** A Principal who provides false KYC information undermines the entire chain. Standard KYC controls apply.

- **Correct permission scoping.** A Principal who grants overly broad permissions assumes elevated risk. OmniFlow provides guidance but cannot prevent overly permissive grants.

- **Bond adequacy.** A bond sized to deter misbehavior does not fully indemnify against losses.

- **Detection completeness.** Slashing depends on detecting violations, and no monitoring system can be assumed to catch every class of misbehavior.

KYA is intended to reduce agent-related risk relative to ungated agent participation in DeFi. It would not be a guarantee of agent good behavior or of investor protection from agent-induced losses, and as an unimplemented design it currently provides neither.
