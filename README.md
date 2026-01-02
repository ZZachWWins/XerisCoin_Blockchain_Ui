Xeris Command Center (Alpha V1)
The Official GUI Dashboard for the Xeris Network Testnet.

This release marks the first public availability of the Xeris Command Center (XCC), a high-performance desktop interface built in Rust. It provides a seamless, zero-latency HUD for managing identities, monitoring network telemetry, and interacting with the Xeris Blockchain.

Release Highlights
Signed, Notarized, & Stapled (macOS)
Certified Security: This application has been cryptographically signed by Xeris Web Co. and notarized by Apple.

Gatekeeper Ready: Install and run immediately without "Unidentified Developer" warnings.

Offline Capable: The notarization ticket is stapled to the binary, allowing first-launch even without an internet connection.

Asynchronous "Zero-Freeze" Architecture
Non-Blocking Core: Key generation and RPC polling now run on dedicated background threads. The UI remains responsive at 60 FPS even during heavy cryptographic operations.

Real-Time Telemetry: Live "Heartbeat" graph visualizes network TPS and block variance in real-time.

Miner & Node Integration
Identity Management: Generate Ed25519 keypairs instantly.

One-Click Export: New "Save as miner.json" button automatically formats your credentials for the Xeris CLI Node.

Miner Tracking: The dashboard automatically detects blocks proposed by your active address and updates your "Mined Blocks" counter.

Dual-Mode Connectivity
Remote Mode: Connects by default to the official Seed Node (138.197...) for instant network visibility.

Localhost Mode: Toggle switch to connect to a local node (127.0.0.1) for zero-latency monitoring of your own infrastructure.

Installation Guide
For macOS Users:
Download release.zip from the Assets below.

Double-click to unzip.

Drag Xeris Command Center into your Applications folder.

Launch the app.

For Windows Users:
Download the Windows version, unzip it, run the exe. 

Alpha Disclaimers
Network Status: This client connects to Testnet V1. Coins have no real-world value and network resets may occur.

Data Persistence: Your generated keys are held in memory until you click "Save". Ensure you back up your miner.json immediately after generation.
