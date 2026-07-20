# Cross-Chain Architecture

OmniFlow's cross-chain design is one of the most consequential architectural decisions in the protocol. This page explains the design and the reasoning behind it.

It is a design. The contracts are deployed on **Base Sepolia testnet** and nowhere else, and the multi-chain deposit rails described below have not been built. What follows is the architecture we have committed to, and the reasoning for it, not a description of live infrastructure.

## The Bridge Problem

Between 2022 and 2024, more than USD 2 billion was lost across cross-chain bridge exploits — Ronin (USD 625M), Wormhole (USD 325M), Nomad (USD 190M), Multichain (USD 230M), Harmony (USD 100M), and others. Every one of these incidents shared the same structural pattern: assets were locked on a source chain, and synthetic representations of those assets were minted on a destination chain. When the lock contract or its keys were compromised, attackers minted unbacked synthetics, draining liquidity and destroying user holdings.

For RWA assets, this attack pattern is unacceptable. An RWA token represents legal rights to off-chain assets — real estate, credit positions, fund interests. If a bridge exploit allows attackers to mint unbacked RWA tokens, the resulting damage is not limited to crypto-native losses; it cascades into legal disputes over ownership of the underlying assets, regulatory consequences for the protocol, and potential systemic risk to the entire RWA category.

OmniFlow rejects the lock-and-mint bridge architecture entirely.

## OmniFlow's Approach: Single Source of Truth + Multi-Chain Deposit Rails

```
BRIDGE-BASED RWA (REJECTED)
Chain A                                    Chain B
┌────────┐                                ┌────────┐
│ RWA    │                                │ wRWA   │
│ Token  │                                │ Token  │
│ (real) │  ◄──── lock-and-mint ────►   │(synth) │
└────────┘                                └────────┘
│                                          │
▼                                          ▼
Locked in     ◄── exploit risk ──►       Minted from
bridge                                    bridge state
contract                                  attestation
OMNIFLOW APPROACH (CHOSEN)
RWA Token
(single chain)
▲
│
│ minted only after off-chain
│ settlement is recorded
│
┌───────────┐    ┌─────┴─────┐    ┌───────────┐
│ Chain A   │    │           │    │ Chain B   │
│ USDT/USDC │    │  Issuance │    │ USDT/USDC │
│ deposit   ├───►│  Chain    │◄───┤ deposit   │
│ rail      │    │           │    │ rail      │
└───────────┘    └───────────┘    └───────────┘
│
│
Multi-chain deposit rails
```

feed a single issuance chain.

No RWA token ever crosses

chain boundaries.

## How It Works

OmniFlow RWA tokens exist exclusively on a single primary issuance chain — **Base**, chosen for its institutional adoption trajectory, native USDC support, and a cost profile compatible with agent micropayments. Today that means Base Sepolia testnet; there is no mainnet deployment. The protocol retains the option to extend issuance to Ethereum mainnet or other networks where ERC-7943 compliance infrastructure is mature.

The design provides for investors to deposit stablecoins from other chains through a payments partner that aggregates those deposits into a single fiat settlement, with RWA tokens minted only on the issuance chain regardless of where the deposit originated. No such partner is engaged and no deposit rail has been built. On testnet, deposits are made in a mock settlement token on Base Sepolia itself.

The property this buys is structural: no OmniFlow RWA token exists on more than one chain simultaneously, and no synthetic representation of one is minted on any chain. The token is single-chain native by design, and adding deposit rails would not change that.

## Why This Architecture Has No Bridge Exposure

Bridge exploits exploit the gap between two synchronization mechanisms — the lock event on the source chain and the mint event on the destination chain. If the synchronization is compromised (whether through key theft, oracle manipulation, or smart contract bug), unbacked synthetics can be minted.

OmniFlow has no such gap, because it has no bridge. There is no cross-chain message, no bridge oracle, and no lock contract whose compromise could trigger a mint on another chain. This holds today and would continue to hold with deposit rails added, since a deposit rail carries value in one direction and mints nothing.

Deposit chains are intended to function as fiat-equivalent rails: value arrives, a payments partner settles it in fiat, and tokens are minted on the issuance chain only against that settled position. From the protocol's perspective this is no different from receiving a bank wire — a compromise of the source rail does not threaten the integrity of issued tokens.

What this argument does **not** cover is authorization of the mint itself. On the deployed testnet contracts, `RwaToken.issue()` has no access control: any eligible wallet holding a deposit certificate can mint itself fund tokens. The discipline that keeps issuance tied to settlement is off-chain workflow, not on-chain enforcement. Restricting issuance to an authorized issuer role is required work before any deployment outside testnet. Absence of bridge risk is a real property of this architecture; it is not a claim that the mint path is fully constrained.

## Trade-Offs Accepted

This architecture accepts certain trade-offs that other RWA platforms have chosen differently:

**Single-chain liquidity.** Any secondary trading of OmniFlow RWA tokens would occur on the issuance chain, and holders wanting to use the token in DeFi protocols on other chains would have no synthetic version available. We believe this trade-off is appropriate for RWA assets: the alternative, multi-chain synthetics, reintroduces bridge attack surface. No secondary market exists today.

**Deposit-side dependence on a payments partner.** The set of chains from which investors could deposit would be bounded by the chains the payments partner supports. Adding a deposit rail is a partner integration, not a protocol modification — which also means the capability does not exist until such a partner is engaged, and none is.

**Migration friction if changing issuance chain.** Should OmniFlow ever migrate the issuance chain, the migration is a coordinated burn-and-reissue with all token holders notified and ample time provided. This is more disruptive than a chain-agnostic token, but ensures supply integrity at every step. The deployed contracts have no burn or redemption function, so this path is not yet implemented, and the multi-signature control it assumes does not exist — the testnet contracts are owned by a single key.

## Future Considerations: ZK-Verified Cross-Chain Transfer

As zero-knowledge proof infrastructure matures, technical paths exist to enable cross-chain RWA token movement without the lock-and-mint pattern — for example, using zk-SNARKs to prove that a token has been burned on the source chain and the corresponding mint on the destination chain is therefore valid.

OmniFlow is monitoring this space but has no current plans to deploy cross-chain RWA token transfer until (a) the underlying ZK infrastructure has independent operational track record at scale, (b) regulatory clarity exists on the legal effect of ZK-verified cross-chain mint events, and (c) the engineering economics justify the additional complexity. Investors and integrators should not expect cross-chain RWA token transfer in the near-to-medium term.
