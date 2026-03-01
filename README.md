The Xeris Command Center

The Official Node Client and Interface for the XerisCoin Triple Consensus Blockchain.

The Xeris Command Center (XCC) is a high-performance desktop environment engineered in Rust. The XCC connects to existing Trusted XerisCoin Validators to ensure your participation in the network.

It serves as the primary operational interface for the XerisCoin Ecosystem, providing institutional-grade network telemetry, identity management, and direct participation in the Xeris Triple Consensus Protocol.

Our Network Architecture: Triple Consensus

XerisCoin utilizes a proprietary Triple-Layer Hybrid Consensus Mechanism designed to solve the blockchain trilemma by integrating Proof of Work, Proof of Stake, and Proof of History into a single, unified protocol.

By running the Xeris Command Center, you transform your local machine into an active participant in this novel architecture. By simply remaining online, your XCC client contributes to all three layers simultaneously through:

1. Proof of Work (PoW): Computational Availability
   
For our mainnet roll-out, we have chosen to develop a light mining client. Unlike legacy chains that require wasteful energy consumption (we're looking at you, BTC), the XCC utilizes a "Light-PoW" model. Your client contributes "Work" by providing uptime, bandwidth, and computational resources to verify block headers and propagate the ledger. The longer your node remains active, the more Validation Power (VP) it accumulates.

2. Proof of Stake (PoS): Economic Security


To prevent Sybil attacks and ensure honest behavior, the network requires economic collateral. Users must stake a minimum balance (100 XRS) to activate the XCC mining client. The probability of receiving block rewards is algorithmically weighted by this stake, incentivizing long-term holding and network alignment.

3. Proof of History (PoH): Cryptographic Sequencing

The Xeris Command Center itself acts as a timekeeper. It continuously synchronizes with the network's global state, cryptographically verifying the passage of time between blocks. This ensures the integrity of the ledger's sequence without requiring the XCC to have heavy peer-to-peer communication overhead.

System Features
The XCC Node Operations Console (Active Mining)

The Xeris Command Center features a fully integrated light mining client that operates silently in the background.

Automatic Validation: The client connects to the validator mesh and verifies incoming blockhashes.

Validation Power (VP) Metrics: A Xeris Technologies proprietary metric that quantifies your node's contribution based on the synergy of your Stake (PoS) and Uptime (PoW).

Real-Time Contribution Graph: Visualizes your node's network weight and activity live.

The Asynchronous "Zero-Freeze" Core

XCC is built on a non-blocking Rust architecture. The application handles cryptographic key generation, RPC polling, and consensus logic on dedicated background threads. This ensures the UI remains fluid at 60 FPS even during periods of heavy network synchronization.

Your XerisCoin "Identity" and Wallet Management

Ed25519 Key Generation: Create secure cryptographic keypairs locally in milliseconds.

Encrypted Storage: Private keys remain encrypted on your local device. The application is strictly non-custodial.

Data Export: One-click export functionality formats credentials (called miner.json) for backup or use with the Xeris CLI tools.

Network Telemetry

Global Throughput: Monitor the global Transactions Per Second (TPS) across the testnet/mainnet.

Block Variance: Visualize block production times and network latency.

Dual-Mode Connectivity: Toggle instantly between Remote Mode (connecting to the official Seed Nodes) and Localhost Mode (monitoring your own local infrastructure).

Technical Operation: Probabilistic Reward Distribution

To maintain scalability while allowing thousands of consumer-grade devices to participate as miners (yes, even a smart fridge if you can get it to run Windows), XerisCoin currently uses a Stochastic Proof-of-Engagement (SPoE) & Proof of Stake Reward Model.

Instead of solving arbitrary hashing problems, the Xeris Command Center runs a local, stake-weighted validation cycle:

Sync: The client verifies it is synchronized with the canonical chain tip (Proof of History).

Calculation: A local process calculates a reward eligibility score based on the user's Staked Balance (Proof of Stake) and Connection Stability (Proof of Work).

Attestation: If the node meets the protocol threshold, it signs a heartbeat transaction referencing the latest Testnet/Mainnet Blockhash.

Settlement: The network verifies the signature and distributes the block reward.

Note: Increasing your staked balance directly increases your Validation Power (VP), thereby increasing the frequency and magnitude of mining rewards.

Installation Guide

macOS
Download the release archive (.zip) from the repository assets.

Extract the archive.

Move the Xeris Command Center application to your Applications folder.

Launch the application.

Security Note: This application is cryptographically signed and notarized by Xeris Web Co. It is fully compliant with Apple Gatekeeper.

Windows
Download the Windows release archive.

Extract the folder to your preferred location.

Run the executable file.

Important Disclaimers

Network Status: This client currently connects to the XerisCoin Test Network. Digital assets on this network have NO monetary value and the ledger MAY be subject to resets during the alpha/beta phases.

Data Persistence: Generated keys are held in volatile memory until saved. Users must ensure they back up their miner.json file immediately after generation. No entity under the Xeris Network Foundation can recover lost private keys.

Designed by Xeris Web Co. Copyright 2026 Xeris Technologies, Xeris Network Foundation. All rights reserved.
