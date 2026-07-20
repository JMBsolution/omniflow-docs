# Smart Contract Addresses

This page lists OmniFlow's deployed smart contract addresses. Every contract below is deployed on **Base Sepolia testnet** and nowhere else. Integrators should verify any address against this page before transacting.

## Status

**Status:** Testnet only. No mainnet deployment exists, and no address on this page controls real assets.

The contracts below are a working testnet demonstration: they have been deployed and exercised end to end on Base Sepolia. The settlement asset is a mock token minted for the demonstration, not Circle USDC. There is no fund, no register of members and no licensed issuer behind these contracts.

## Base Sepolia Testnet — Current Deployment

Network: Base Sepolia (chain ID 84532). Verify on [BaseScan Sepolia](https://sepolia.basescan.org).

| **Contract** | **Address** | **Notes** |
| --- | --- | --- |
| MockUSDC | `0x0f77b3a298c6c1b6940a6147b536cbe687aa98ef` | Mock settlement token, 6 decimals. Not Circle USDC. |
| EligibilityRegistry | `0x814D7F34D0259b725B4857c09650Cd328324295e` | Allow-list consulted by the token's transfer checks |
| DepositCertificate | `0xd5252fd4c9a6fdd683bce0356b044a0fe9912bd9` | ERC-4626, non-transferable. Symbol `ofDC-KLI1` |
| RwaToken | `0xb88d9fb681ab743e5b3701b2c8102baa79446c32` | ERC-20 plus ERC-7943 (uRWA). Symbol `ofKLI1` |

The implemented permissioned-token standard is **ERC-7943 (uRWA)**, not ERC-3643. `RwaToken` advertises the ERC-7943 fungible interface id `0x3edbb4c4` and reverts at deployment if that id drifts from the interface definition.

### Subscription Account

| **Role** | **Address** | **Notes** |
| --- | --- | --- |
| Subscription account | `0xb61bAf800658Dd6Fbe3287287Bc1b04f7357C5f9` | Demonstration wallet that receives the mock settlement asset when a certificate is exchanged. Not a treasury, not a custodian, not a segregated account. |

### Deployed Parameters

| **Parameter** | **Value** |
| --- | --- |
| Certificate | `OmniFlow Deposit Certificate — Korea Logistics Income Fund I` (`ofDC-KLI1`) |
| Fund token | `OmniFlow Korea Logistics Income Fund I (Testnet Demo)` (`ofKLI1`) |
| Settlement asset | `mUSDC`, 6 decimals |
| Transfer restriction | 15,552,000 seconds — 180 days from issuance |

The lock-up is enforced on chain as a FIFO queue of per-parcel lots: each issuance creates a lot with its own unlock date, lots are consumed oldest-first, and a later acquisition does not re-lock units already seasoned. `lotsOf(address)` returns the live lots for any holder and `unrestrictedBalanceOf(address)` returns the seasoned total.

## Known Limitation — Issuance Access Control

`RwaToken.issue()` has no access control. Any wallet that holds a deposit certificate and passes the eligibility registry can call it and mint itself fund tokens on chain.

In the demonstration, the workflow does not reach that point: the agent halts at workflow step 04 because steps 04 to 06 require human counterparties, and it will not write an outcome it cannot source. That halt is enforced by the off-chain operator workflow tracker and by the demo script — **it is not enforced by the smart contracts**. Closing this gap on chain is future work.

## Verification

Each contract above is deployed with source available for verification on BaseScan Sepolia. Contracts are unaudited — see [Smart Contract Audits](smart-contract-audits.md).

Testnet contracts may be redeployed at any time without notice. Nothing on this page should be used with real funds.

## Address Authority Notice

The canonical list of OmniFlow contract addresses is maintained on this page. Addresses claimed to be associated with OmniFlow but not listed here have not been verified by OmniFlow.

If you encounter an address claimed to be OmniFlow's that does not appear here, contact archiyong217@gmail.com.
