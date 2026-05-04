# Smart Contract Audits

This page lists the security audits conducted on OmniFlow's smart contracts. Audit reports are published in full alongside the audited source code commit, in perpetuity.

## Audit Policy

OmniFlow's audit policy commits the protocol to:

- **At least two independent audits** for each contract before mainnet deployment

- **Formal verification** of critical invariants (supply integrity, compliance gating)

- **Public disclosure** of complete audit reports, including findings and remediation status

- **Re-audit** of any contract that undergoes substantive modification post-launch

- **Continuous bug bounty** through Immunefi, with payouts proportional to finding severity

## Audit Engagement Status

**Status:** Pre-deployment audit engagements scheduled. **Target audit completion:** Phase 1, [TBD]. **Last updated:** [TBD]

The following audit engagements are confirmed for the pre-deployment phase. Auditor selections will be finalized and disclosed at the time of contract signing.

| **Engagement** | **Auditor** | **Scope** | **Engagement Status** | **Target Completion** |
| --- | --- | --- | --- | --- |
| Audit 1 — Core Protocol | Trail of Bits or equivalent | Identity Registry, Compliance Module, RWA Token, Deposit Receipt | [TBD — letter of engagement pending] | [TBD] |
| Audit 2 — Core Protocol | OpenZeppelin or equivalent | Same scope, independent review | [TBD — letter of engagement pending] | [TBD] |
| Audit 3 — Oracle Layer | [TBD — auditor selection in progress] | NAV Oracle, Risk Oracle, Reserve Attestation | [TBD] | [TBD] |
| Audit 4 — Governance | [TBD — auditor selection in progress] | Multi-sig, Timelock, Constitutional Limits enforcement | [TBD] | [TBD] |
| Formal Verification | Certora or equivalent | Supply invariant, compliance gating, lock-up enforcement | [TBD — letter of engagement pending] | [TBD] |

Auditor selections will be confirmed and disclosed on this page at the time of engagement signing. Audit reports will be published in full upon completion.

## Audit Report Archive

Completed audit reports are linked here as they become available. Reports are preserved in perpetuity; corrections or updates are issued as supplementary documents with explicit references to the original report.

### Mainnet Audits

| **Report** | **Auditor** | **Audit Period** | **Source Commit** | **Findings Summary** | **Report Link** |
| --- | --- | --- | --- | --- | --- |
| [TBD] | [TBD] | [TBD] | [TBD] | [TBD] | [TBD] |

*No reports available — protocol is in pre-deployment audit preparation.*

### Re-Audit and Update History

| **Report** | **Auditor** | **Trigger** | **Audit Period** | **Source Commit** | **Report Link** |
| --- | --- | --- | --- | --- | --- |
| [TBD] | [TBD] | [TBD] | [TBD] | [TBD] | [TBD] |

*No re-audits performed — initial audit cycle has not yet completed.*

## Findings Disclosure Standard

For each completed audit, the following information is disclosed in full on this page:

- **Severity distribution**: Count of findings at each severity level (Critical / High / Medium / Low / Informational)

- **Each finding's status**: Fixed / Acknowledged / Mitigated / Won't Fix, with explanation for non-fixed findings

- **Remediation source commits**: Specific commits that address each fixed finding

- **Auditor sign-off on remediation**: Where the auditor has reviewed remediation, the auditor's confirmation is included

This standard follows the disclosure practices of established institutional-grade RWA protocols and is intended to enable independent verification of OmniFlow's security posture.

## Bug Bounty Program

A continuous bug bounty program operates through Immunefi from the moment of mainnet deployment. The bounty scope covers all production smart contracts and the on-chain components of the oracle and governance layers.

### Severity and Payout

| **Severity** | **Maximum Payout** | **Examples** |
| --- | --- | --- |
| Critical | USD 500,000 | Unauthorized minting, theft of underlying funds, compliance gating bypass |
| High | USD 100,000 | Unauthorized state changes, oracle manipulation, governance bypass |
| Medium | USD 25,000 | Denial of service, gas griefing, partial functionality compromise |
| Low | USD 5,000 | Minor logic errors, documentation gaps, gas optimization opportunities |

Bounty determinations follow Immunefi's standard severity classification and dispute resolution process. Detailed scope, exclusions, and submission procedure are published on the Immunefi page upon program launch.

**Bug bounty program status:** Pre-launch. Program activation is targeted for Phase 1 mainnet deployment. **Immunefi page:** [TBD — link will be posted upon program activation]

## Coordinated Disclosure

OmniFlow follows the standard coordinated disclosure model for security findings. Researchers who identify vulnerabilities are encouraged to report through the bug bounty channel (Immunefi) or directly to security@omniflow.xyz. OmniFlow commits to:

- Acknowledging valid reports within 48 hours

- Providing status updates at least every 7 days during active triage

- Crediting researchers (with permission) in any public disclosure

- Not pursuing legal action against researchers who follow coordinated disclosure

The coordinated disclosure policy is detailed at omniflow.xyz/security.

## Security Incident Disclosure

In the event of a security incident affecting OmniFlow's smart contracts, oracle layer, or governance system, OmniFlow commits to disclosing:

- The nature and scope of the incident

- The time of detection and the time of remediation

- The impact on user funds, if any

- The remediation actions taken

- The lessons learned and any architectural changes adopted

Incident disclosures are posted on this page in a dedicated section and remain visible permanently. As of the latest update, **no security incidents have occurred** because the protocol is in pre-deployment status.

### Incident History

| **Incident Date** | **Description** | **Severity** | **Resolution** | **Disclosure Link** |
| --- | --- | --- | --- | --- |
| — | No incidents to date | — | — | — |
