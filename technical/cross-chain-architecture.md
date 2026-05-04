# Cross-Chain Architecture

OmniFlow's cross-chain design is one of the most consequential architectural decisions in the protocol. This page explains the design and the reasoning behind it.

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
│ minted only after settlement
│ from VCC sub-register
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

OmniFlow RWA tokens exist exclusively on a single primary issuance chain — Ethereum during the protocol's mainnet phase, with the option to migrate or extend to specific Layer-2 networks (Base, Arbitrum) where ERC-3643 compliance infrastructure is mature.

Investors can deposit stablecoins from any chain that the OmniFlow MPI partner supports — Ethereum, TRON, Base, Arbitrum, Solana (subject to MPI partner availability). The MPI partner aggregates deposits from all chains into a single USD settlement that funds the underlying asset purchase. RWA tokens are minted only on the issuance chain, regardless of which chain the investor's deposit originated from.

There is no scenario in which an OmniFlow RWA token exists on more than one chain simultaneously. There is no scenario in which a synthetic representation of an OmniFlow RWA token is minted on any chain. The token is single-chain native by design.

## Why This Architecture Is Immune to Bridge Exploits

Bridge exploits exploit the gap between two synchronization mechanisms — the lock event on the source chain and the mint event on the destination chain. If the synchronization is compromised (whether through key theft, oracle manipulation, or smart contract bug), unbacked synthetics can be minted.

OmniFlow has no such gap. The RWA token's mint event is gated solely on settlement of the underlying asset purchase, attested by the LFMC and verified against the VCC sub-register. There is no cross-chain message, no bridge oracle, and no lock contract whose compromise could trigger an unauthorized mint.

The deposit chains are merely fiat-equivalent rails. The investor sends USDT on TRON; the MPI partner credits USD on the OmniFlow Singapore account. From the protocol's perspective, this is no different than receiving a SWIFT wire from a bank — the source rail's compromise (an exchange hack, a wallet theft) does not threaten the integrity of the issued RWA tokens, because the RWA tokens are minted only after settled USD funds the underlying asset purchase.

## Trade-Offs Accepted

This architecture accepts certain trade-offs that other RWA platforms have chosen differently:

**Single-chain liquidity.** Secondary market trading of OmniFlow RWA tokens occurs on the issuance chain. Investors who want to use OmniFlow tokens in DeFi protocols on other chains do not have a synthetic version available. We believe this trade-off is appropriate for RWA assets: composability with permissioned DeFi within the issuance chain provides meaningful flexibility, while the alternative (multi-chain synthetics) reintroduces bridge attack surface.

**Deposit-side dependence on MPI partner chain coverage.** The set of chains from which investors can deposit is bounded by the chains the OmniFlow MPI partner supports. Adding deposit rail support for an additional chain is a partner integration, not a protocol modification.

**Migration friction if changing issuance chain.** Should OmniFlow ever migrate the issuance chain (for example, from Ethereum mainnet to a specific L2), the migration is a coordinated burn-and-reissue executed under governance and multi-signature control, with all token holders notified and ample time provided. This is more disruptive than a chain-agnostic token, but ensures supply integrity at every step.

## Future Considerations: ZK-Verified Cross-Chain Transfer

As zero-knowledge proof infrastructure matures, technical paths exist to enable cross-chain RWA token movement without the lock-and-mint pattern — for example, using zk-SNARKs to prove that a token has been burned on the source chain and the corresponding mint on the destination chain is therefore valid.

OmniFlow is monitoring this space but has no current plans to deploy cross-chain RWA token transfer until (a) the underlying ZK infrastructure has independent operational track record at scale, (b) regulatory clarity exists on the legal effect of ZK-verified cross-chain mint events, and (c) the engineering economics justify the additional complexity. Investors and integrators should not expect cross-chain RWA token transfer in the near-to-medium term.
