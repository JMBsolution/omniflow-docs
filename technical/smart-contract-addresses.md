# Smart Contract Addresses

This page lists the deployed smart contract addresses for OmniFlow's protocol. Addresses are published immediately upon deployment and verified on the respective block explorers. Investors and integrators should verify any address against this page before transacting.

## Status

**Status:** Pre-deployment. **Target deployment:** Phase 1, [TBD — to be confirmed at audit completion]. **Last updated:** [TBD]

OmniFlow's mainnet contracts are deployed in a single coordinated event following completion of audits, regulatory approvals, and partner integrations. Until that point, all addresses below are placeholders and no production contracts exist on-chain.

## Mainnet Contract Registry

### Core Protocol — Ethereum Mainnet

| **Contract** | **Address** | **Source Commit** | **Deployed At** |
| --- | --- | --- | --- |
| Identity Registry | [TBD] | [TBD] | [TBD] |
| Compliance Module | [TBD] | [TBD] | [TBD] |
| Korea Jurisdiction Module | [TBD] | [TBD] | [TBD] |
| Deposit Receipt (ERC-4626) | [TBD] | [TBD] | [TBD] |
| RWA Token Factory (ERC-3643) | [TBD] | [TBD] | [TBD] |
| Yield Distribution Contract | [TBD] | [TBD] | [TBD] |
| NAV Oracle | [TBD] | [TBD] | [TBD] |
| Risk Oracle | [TBD] | [TBD] | [TBD] |
| Reserve Attestation | [TBD] | [TBD] | [TBD] |
| Governance Multi-sig (5/9) | [TBD] | [TBD] | [TBD] |
| Governance Timelock | [TBD] | [TBD] | [TBD] |

### Per-Product RWA Tokens — Ethereum Mainnet

| **Product** | **Token Symbol** | **Address** | **Issuance Date** | **Status** |
| --- | --- | --- | --- | --- |
| Korea Listed REIT Income (T1) — Series A | [TBD] | [TBD] | [TBD] | Pre-issuance |
| Korea Logistics Income (T2) — Series A | [TBD] | [TBD] | [TBD] | Pre-issuance |
| Korea Senior Development Credit (T3) — Series A | [TBD] | [TBD] | [TBD] | Pre-issuance |

Additional product series will be added to this registry at the time of issuance. Each series corresponds to a discrete subscription window and a specific underlying asset pool.

### Stablecoin Settlement Addresses

The following addresses are used by OmniFlow's MPI partner for stablecoin deposit receipt across supported chains. These are MPI partner-controlled wallets, not OmniFlow protocol contracts.

| **Chain** | **Stablecoin** | **Receiving Address** | **Verification Source** |
| --- | --- | --- | --- |
| Ethereum | USDT | [TBD] | MPI partner attestation [TBD] |
| Ethereum | USDC | [TBD] | MPI partner attestation [TBD] |
| Ethereum | USD1 | [TBD] | MPI partner attestation [TBD] |
| TRON | USDT | [TBD] | MPI partner attestation [TBD] |
| Base | USDT | [TBD] | MPI partner attestation [TBD] |
| Base | USDC | [TBD] | MPI partner attestation [TBD] |
| Arbitrum | USDT | [TBD] | MPI partner attestation [TBD] |
| Arbitrum | USDC | [TBD] | MPI partner attestation [TBD] |
| Solana | USDT | [TBD] | MPI partner attestation [TBD] |
| Solana | USDC | [TBD] | MPI partner attestation [TBD] |

Investors must confirm the current receiving address with their relationship manager before each subscription. Addresses may rotate periodically per MPI partner security policy.

## Testnet Deployments

Pre-production testing is conducted on Ethereum Sepolia testnet. Testnet addresses are made available to integration partners and audit firms upon request. Testnet contracts are not for use with real funds and may be redeployed at any time without notice.

### Sepolia Testnet — Current Test Build

| **Contract** | **Address** | **Source Commit** | **Deployed At** |
| --- | --- | --- | --- |
| Identity Registry | [TBD] | [TBD] | [TBD] |
| Compliance Module | [TBD] | [TBD] | [TBD] |
| Korea Jurisdiction Module | [TBD] | [TBD] | [TBD] |
| Deposit Receipt (test) | [TBD] | [TBD] | [TBD] |
| RWA Token Factory (test) | [TBD] | [TBD] | [TBD] |
| NAV Oracle (test) | [TBD] | [TBD] | [TBD] |

To request testnet access, contact engineering@omniflow.xyz with the integration use case.

## Verification Standard

All mainnet contracts are:

- Deployed with verified source code on the relevant block explorer (Etherscan, BaseScan, etc.)

- Audited by at least two independent firms (see Smart Contract Audits)

- Tagged with a permanent reference to the audited source commit

- Published with the deployment transaction hash for chain-of-custody verification

## Programmatic Address Resolution

The canonical list of OmniFlow contract addresses is also available in machine-readable form, signed by the OmniFlow operations team:

GET https://api.omniflow.xyz/v1/contract-addresses

The endpoint returns the same address list as this page, plus an EIP-191 signature from the OmniFlow operations key. Integration partners and agents are encouraged to verify the signature before consuming the address list programmatically.

## Address Update Policy

Address list updates are signed transactions executed by the governance multi-signature. New deployments (additional jurisdiction modules, additional product variants) extend the list. Address removals or replacements occur only in the case of contract migration and are subject to the standard 72-hour governance timelock and advance notification to all token holders.

## Address Authority Notice

The canonical list of OmniFlow contract addresses is maintained on this page. Addresses claimed to be associated with OmniFlow but not listed here have not been verified by OmniFlow. Investors and integrators should verify any address against this page before transacting.

If you encounter an address claimed to be OmniFlow's that does not appear here, contact security@omniflow.xyz immediately.
