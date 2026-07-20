# Custody & Reserves

OmniFlow does not custody any assets. There are no reserves, and there are no attestations to publish.

## Current Status

The demonstration runs end to end on Base Sepolia testnet, using test tokens that have no value:

- **MockUSDC** is a mock stablecoin minted for the demonstration. It is not Circle USDC and is not redeemable for anything.
- **DepositCertificate** is a non-transferable ERC-4626 vault that holds demonstration deposits on testnet.
- The **subscription account** that receives demonstration payments is a demo wallet. It is not a treasury and not a client money account.

No fiat is held at any point. No bank, custodian, trust company or digital asset custody provider has been appointed — in Singapore, in Korea, or anywhere else. The settlement chain described in the workflow model is a design, not an operating arrangement.

## Reserves

There are no reserves.

No real assets have been acquired, no fund vehicle exists, and no investor funds have been received. There is therefore no reserve balance to attest to, and no register to reconcile against on-chain token supply.

No proof-of-reserve mechanism is deployed. The testnet deployment contains no reserve attestation contract and no safety reserve contract.

## Insurance

No insurance is in place. No custody, professional liability, property or cyber policy has been bound.

## What Comes Later

Custody arrangements, a reserve verification process and a disclosure cadence become relevant only once a vehicle holds real assets on behalf of investors. None of that is built. This page will describe the actual arrangements, and publish actual attestations, once they exist.
