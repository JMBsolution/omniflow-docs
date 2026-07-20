# Smart Contract Audits

## Status

**No smart contract audit has been performed.** No audit firm has been engaged, no formal verification has been carried out, and no audit report exists.

The contracts listed on [Smart Contract Addresses](smart-contract-addresses.md) are deployed on Base Sepolia testnet only. They are unaudited testnet code. They hold no real assets and must not be used with real funds.

There is no bug bounty program. OmniFlow has no Immunefi page and no bounty pool.

One known limitation is documented rather than deferred to an audit: `RwaToken.issue()` has no access control, so a certificate-holding eligible wallet could in principle mint itself fund tokens on chain. The demonstration does not reach that step because the agent halts at workflow step 04, but that halt is enforced off chain by the operator workflow tracker and the demo script, not by the contracts. See [Smart Contract Addresses](smart-contract-addresses.md).

## Audit Policy

Before any mainnet deployment, OmniFlow commits to:

- **At least two independent audits** of each contract

- **Formal verification** of critical invariants (supply integrity, compliance gating, lock-up enforcement)

- **Public disclosure** of complete audit reports, including findings and remediation status

- **Re-audit** of any contract that undergoes substantive modification post-launch

These are commitments, not engagements. No auditor has been selected or approached, and no timeline is committed to.

For each completed audit, OmniFlow will disclose the severity distribution of findings, each finding's status (Fixed / Acknowledged / Mitigated / Won't Fix) with an explanation for anything not fixed, the remediation source commits, and the auditor's sign-off on remediation where given.

## Audit Report Archive

No audit reports exist. Completed reports will be published here in full, alongside the audited source commit, as they become available.

## Coordinated Disclosure

Researchers who identify vulnerabilities in the testnet contracts are encouraged to report them to security@omniflow.xyz. OmniFlow will credit researchers, with permission, in any public disclosure, and will not pursue legal action against researchers who follow coordinated disclosure.

## Security Incidents

No security incidents have occurred. Any incident affecting deployed contracts will be disclosed on this page, including its nature and scope, the time of detection and remediation, the impact on any funds, the remediation actions taken, and any resulting architectural changes.
