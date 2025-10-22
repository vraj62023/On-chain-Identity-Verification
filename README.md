# 🛡️ On-Chain Identity Verification System

## 🔍 Overview

This project is a **decentralized identity verification platform** built using blockchain technology.  
It allows users to prove their identity through **Verifiable Credentials (VCs)** that are **stored off-chain** (for privacy) and **anchored on-chain** via cryptographic proofs.

The system ensures:
- ✅ Trustless identity verification (no central authority)
- 🔒 Privacy preservation (no personal data on-chain)
- 🧾 Decentralized Identifiers (DIDs)
- 🧠 Zero-Knowledge Proof (zk-SNARK) support (for privacy-preserving claims)

---

## ⚙️ Workflow

### Step 1: Credential Issuance
1. The user submits identity details to a **trusted attester** (e.g., KYC authority).
2. The attester generates a **Verifiable Credential (VC)** JSON.
3. The VC is uploaded to **IPFS**, and a `cidHash` is generated.
4. The attester signs `(subjectAddress, cidHash, expiry)` using its private key.
5. The signature is returned to the user.

### Step 2: On-Chain Attestation
6. The user submits this signed attestation to the **smart contract (`Attestations.sol`)**.
7. The contract verifies the attester’s signature and stores the `cidHash` with metadata.

### Step 3: Verification
8. A verifier queries the contract to check if an attestation is valid (not expired or revoked).
9. The verifier retrieves the VC JSON from IPFS and verifies the attester’s signature.
10. *(Optional)* The user can later prove specific claims using **zero-knowledge proofs**.

---

## 🧱 System Architecture

| Component | Description | Technology |
|------------|--------------|-------------|
| **Smart Contract** | Stores attestations and verifies signatures | Solidity (Hardhat) |
| **Attester Service** | Issues credentials, uploads them to IPFS, and signs attestations | Node.js + Ethers.js + NFT.Storage |
| **Frontend (User + Verifier)** | UI for requesting, submitting, and verifying credentials | React (Vite) + Ethers.js |
| **Storage Layer** | Secure, decentralized VC storage | IPFS (via NFT.Storage) |
| **Blockchain Network** | On-chain registry for attestations | Ethereum Testnet (Hardhat / Sepolia) |

---

## 🧠 Design Choices

### 🪙 Blockchain
- **Ethereum / EVM-based**: mature, testnet-friendly, and widely supported.
- **Alternative**: Polygon for lower gas fees.

### 🧩 Smart Contract Framework
- **Hardhat**  
  - Local development & testing  
  - Built-in Ethers.js support  
  - Clean Solidity debugging and deployment

### 🔐 Libraries
- **OpenZeppelin** for `Ownable` and `ECDSA`
  - Secure cryptographic implementations  
  - Community-audited code

### 🌐 Off-chain Storage
- **IPFS via NFT.Storage**
  - Decentralized and permanent storage  
  - Generates unique CID hashes for every VC  
  - Free tier for development

### 💻 Frontend
- **React (Vite)** for fast, modular UI development  
- **Ethers.js** for wallet and contract interaction

### 🧾 Attester Backend
- **Node.js (Express)** for REST API  
- **dotenv** for private key management  
- **nft.storage** package for uploading to IPFS

### 🧮 Zero-Knowledge Proofs *(Future Integration)*
- **Circom + SnarkJS**  
  - Enables privacy-preserving claims  
  - Example: prove “Age > 18” without revealing DOB


## 🧰 Tech Stack

| Category | Tool / Library |
|-----------|----------------|
| Smart Contracts | Solidity, Hardhat, OpenZeppelin |
| Blockchain Interaction | Ethers.js |
| Backend | Node.js, Express |
| Frontend | React (Vite) |
| Storage | IPFS (NFT.Storage) |
| ZK Proofs (Future) | Circom, SnarkJS |
| Testing | Mocha, Chai |

---

## 🧪 Testing Plan

1. **Smart Contract Unit Tests**
   - Signature validation
   - Attestation storage & retrieval
   - Expiry and revocation logic

2. **Integration Tests**
   - Attester issues credential → `/issue` endpoint
   - User submits attestation on-chain
   - Verifier checks validity and retrieves from IPFS

3. **Frontend Testing**
   - UI interaction with wallet (Metamask)
   - Credential upload and verification flows



## 🚀 Future Improvements

- Implement **DID** method (`did:pkh`, `did:key`)
- Add **zk-proof verification contract**
- **DAO-based attester registration**
- Wallet integration via **RainbowKit / Wagmi**
- **The Graph** integration for indexing attestations


## 📦 Development Setup

### 🪜 Prerequisites
- Node.js v18+
- Git
- Metamask (for testnet)
- Hardhat

### 🛠️ Installation

```bash
# Clone the repository
git clone https://github.com/<your-username>/onchain-identity-verification.git
cd onchain-identity-verification

# Install dependencies
npm install

# Compile contracts
npx hardhat compile

# Run local blockchain
npx hardhat node

# Deploy contracts
npx hardhat run scripts/deploy.js --network localhost

# Start frontend
cd frontend
npm run dev
📄 References
W3C Verifiable Credentials Data Model

EIP-712: Typed Structured Data Hashing

OpenZeppelin Contracts Documentation

NFT.Storage Docs

Circom + SnarkJS Docs

👨‍💻 Author
Vipin Raj
vraj62023@gmail.com

