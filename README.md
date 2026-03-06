# The Xeris Command Center

The Official Node Client and Interface for the XerisCoin Triple Consensus Blockchain.

The Xeris Command Center (XCC) is a high-performance desktop environment engineered in Rust. The XCC connects to existing Trusted XerisCoin Validators to ensure your participation in the network.

It serves as the primary operational interface for the XerisCoin Ecosystem, providing institutional-grade network telemetry, identity management, zero-knowledge privacy, post-quantum cryptography, AI agent delegation, and direct participation in the Xeris Triple Consensus Protocol.


## What's New in v0.3.0

This release introduces three new cryptographic systems to the Xeris Command Center, all verified and running on testnet.

Zero-Knowledge Privacy allows you to send XRS with the amount completely hidden from on-chain observers. The new ZK Privacy tab lets you send private transfers where the amount is concealed inside a cryptographic commitment. Observers see a 32-byte hash on the explorer instead of the actual value.

Post-Quantum Cryptography protects your account against future quantum computer attacks. The new Quantum Shield tab generates a CRYSTALS-Dilithium keypair (NIST FIPS 204, the same algorithm recommended by the NSA for quantum migration) and registers it on-chain. You can then send transfers signed with a lattice-based signature that the chain verifies using the actual NIST reference library.

AI Agent Delegation lets you register autonomous AI agents with protocol-enforced spending limits. The new AI Agents tab lets you register an agent with a daily budget and per-transaction cap, restrict which contracts it can call, and revoke all authority with a single click. The chain enforces the guardrails at the consensus level rather than in application code.


## Our Network Architecture: Triple Consensus

XerisCoin utilizes a proprietary Triple-Layer Hybrid Consensus Mechanism designed to solve the blockchain trilemma by integrating Proof of Work, Proof of Stake, and Proof of History into a single, unified protocol.

By running the Xeris Command Center, you transform your local machine into an active participant in this novel architecture. By simply remaining online, your XCC client contributes to all three layers simultaneously.

Proof of Work (PoW): Computational Availability. For our mainnet roll-out, we have chosen to develop a light mining client. Unlike legacy chains that require wasteful energy consumption, the XCC utilizes a "Light-PoW" model. Your client contributes "Work" by providing uptime, bandwidth, and computational resources to verify block headers and propagate the ledger. The longer your node remains active, the more Validation Power (VP) it accumulates.

Proof of Stake (PoS): Economic Security. To prevent Sybil attacks and ensure honest behavior, the network requires economic collateral. Users must stake a minimum balance (100 XRS) to activate the XCC mining client. The probability of receiving block rewards is algorithmically weighted by this stake, incentivizing long-term holding and network alignment.

Proof of History (PoH): Cryptographic Sequencing. The Xeris Command Center itself acts as a timekeeper. It continuously synchronizes with the network's global state, cryptographically verifying the passage of time between blocks. This ensures the integrity of the ledger's sequence without requiring the XCC to have heavy peer-to-peer communication overhead.


## System Features

### The XCC Node Operations Console (Active Mining)

The Xeris Command Center features a fully integrated light mining client that operates silently in the background.

Automatic Validation: The client connects to the validator mesh and verifies incoming blockhashes. Successful attestations earn 0.01 XRS per verified block, rate-limited to one reward per ten blocks.

Validation Power (VP) Metrics: A Xeris Technologies proprietary metric that quantifies your node's contribution based on the synergy of your Stake (PoS) and Uptime (PoW).

Real-Time Contribution Graph: Visualizes your node's network weight and activity live.


### ZK Privacy (New in v0.3.0)

The ZK Privacy tab provides a private transfer interface where the transfer amount is hidden from all on-chain observers.

When you send a private transfer, the XCC generates a random 32-byte blinding factor, computes a SHA-256 binding commitment that locks in the exact amount, creates a balance proof that cryptographically proves you have sufficient funds without revealing your balance, and derives a nullifier that prevents double-spending the same commitment.

On-chain, the explorer shows a cryptographic hash where the amount would normally appear. Only you and the recipient know the value. The chain verifies the proofs and executes the transfer. The nullifier is recorded permanently to prevent reuse.


### Quantum Shield (New in v0.3.0)

The Quantum Shield tab protects your account against quantum computer attacks using CRYSTALS-Dilithium, the lattice-based signature algorithm standardized by NIST as FIPS 204 in August 2024.

Clicking "Enable Quantum Protection" generates a real Dilithium3 keypair with 128-bit post-quantum security. The 1,952-byte public key is registered on-chain alongside your existing Ed25519 key. The 4,016-byte secret key is saved to encrypted local storage.

Once protected, you can send transfers signed with your Dilithium key. The chain verifies both the Ed25519 transport signature and the Dilithium transfer signature. Both must be valid. Even if Ed25519 is broken by a quantum computer in the future, your Dilithium-signed transfers remain secure.

The Quantum Shield tab also shows network-wide PQ adoption statistics including total registered keys and total PQ-signed transactions.


### AI Agents (New in v0.3.0)

The AI Agents tab provides a delegation interface for autonomous AI systems operating on the XerisCoin network through the Xeris Ari Protocol.

Register Agent: Enter an agent name, public key, maximum XRS per transaction, and maximum daily budget. The chain records these limits and enforces them on every transaction the agent submits.

Revoke Agent: Enter an agent's public key and immediately revoke all delegated authority. The revocation takes effect on the next block.

Agent Registry: View all agents registered under your account with their current status, spending limits, and active or revoked state.

The full agent lifecycle is supported on-chain including identity registration, reputation attestation, capability advertising, task markets, inter-agent messaging, heartbeats, disputes, governance voting, state channels, and oracle data feeds. These are accessible through the JavaScript SDK (xeris-sdk on npm) and will be integrated into the desktop UI in future releases.


### The Asynchronous "Zero-Freeze" Core

XCC is built on a non-blocking Rust architecture. The application handles cryptographic key generation, Dilithium keypair creation, ZK proof computation, RPC polling, and consensus logic on dedicated background threads. This ensures the UI remains fluid at 60 FPS even during periods of heavy network synchronization or proof generation.


### Your XerisCoin Identity and Wallet Management

Ed25519 Key Generation: Create secure cryptographic keypairs locally in milliseconds.

BIP39 Seed Phrases: Generate and verify 12-word recovery phrases with a guided backup flow.

Encrypted Storage: Private keys and Dilithium secret keys remain encrypted on your local device. The application is strictly non-custodial.

Multi-Wallet Support: Create, import, switch between, and delete multiple wallet identities.

Data Export: One-click export functionality formats credentials for backup or use with the Xeris CLI tools.


### DeFi Operations

Token Factory: Create new tokens on the XerisCoin network with custom name, symbol, and supply. Mint tokens to any address. Transfer tokens between accounts.

DEX Trading: Deploy liquidity pools, execute on-chain atomic swaps, and wrap or unwrap XRS for DEX compatibility.

Staking: Lock XRS for Proof of Stake mining eligibility with a minimum of 100 XRS. Unstake with a 7-day unbonding period.


### Network Telemetry

Global Throughput: Monitor the global Transactions Per Second (TPS) across the testnet.

Block Variance: Visualize block production times and network latency.

Chain Economics: View total mined supply, current block reward, halving epoch, and fee collection.

Dual-Mode Connectivity: Toggle instantly between Remote Mode (connecting to the official Seed Nodes) and Localhost Mode (monitoring your own local infrastructure).


## Technical Operation: Probabilistic Reward Distribution

To maintain scalability while allowing thousands of consumer-grade devices to participate as miners, XerisCoin uses a Stochastic Proof-of-Engagement (SPoE) and Proof of Stake Reward Model.

Instead of solving arbitrary hashing problems, the Xeris Command Center runs a local, stake-weighted validation cycle.

Sync: The client verifies it is synchronized with the canonical chain tip through Proof of History.

Verification: The client validates block integrity by checking hash chain linkage, slot ordering, and proposer signatures.

Attestation: If the block passes all checks, the client signs a ValidatorAttestation transaction referencing the verified block's slot and full 32-byte hash.

Settlement: The network verifies the attestation signature, checks the attestor has at least 100 XRS staked, enforces the one-per-ten-blocks rate limit, and distributes 0.01 XRS per valid attestation.

Increasing your staked balance directly increases your Validation Power (VP), thereby increasing the frequency of mining rewards.


## Installation Guide

### macOS

Download the release archive (.zip) from the repository assets. Extract the archive. Move the Xeris Command Center application to your Applications folder. Launch the application.

Security Note: This application is cryptographically signed and notarized by Xeris Technologies LLC. It is fully compliant with Apple Gatekeeper.

### Windows

Download the Windows release archive. Extract the folder to your preferred location. Run the executable file.


## Developer SDK

The JavaScript SDK is available on npm for building wallets, dApps, and AI agents.

```
npm install xeris-sdk
```

The SDK provides full support for all 54 on-chain instruction types including ZK private transfers, PQ key registration, PQ-signed transfers, and the complete AI agent lifecycle. Sending a private transfer is one line of code.

Documentation and test vectors are included in the package. Source code is available at github.com/ZZachWWins/xeris-sdk.


## Important Disclaimers

Network Status: This client currently connects to the XerisCoin Test Network. Digital assets on this network have NO monetary value and the ledger MAY be subject to resets during the alpha and beta phases.

Data Persistence: Generated keys (both Ed25519 and Dilithium) are stored locally on your device. Users must ensure they back up their wallet files immediately after generation. No entity under Xeris Technologies LLC can recover lost private keys.

Post-Quantum Keys: Dilithium secret keys are stored in ~/.xeris/ on your local filesystem. Back up this directory along with your wallet files.


## Network Info

Seed Node: 138.197.116.81. RPC Port: 56001. Explorer Port: 50008. P2P Port: 4000. Block Time: 4 seconds. Decimals: 9 (1 XRS equals 1,000,000,000 lamports). Instruction Variants: 54. Contract Types: 20.


Designed by Xeris Technologies LLC. Copyright 2026 Xeris Technologies LLC. All rights reserved.
