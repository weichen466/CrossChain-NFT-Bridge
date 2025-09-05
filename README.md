# 🌉 CrossChain NFT Bridge

**ChainLinker NFT Bridge** - A comprehensive project demonstrating cross-chain NFT transfers using Chainlink CCIP (Cross-Chain Interoperability Protocol).

This project implements two different approaches for transferring NFTs between different blockchain networks: Lock-and-Release and Burn-and-Mint mechanisms.

## 🎯 Project Overview

This project showcases:

- **Cross-chain NFT transfers** between Sepolia and Amoy testnets
- **Two transfer mechanisms**: Lock-and-Release and Burn-and-Mint
- **Chainlink CCIP integration** for secure cross-chain messaging
- **Hardhat development environment** with deployment scripts and tasks

## 🏗️ Architecture

### 🌉 ChainLinker NFT Bridge Overview

The **ChainLinker NFT Bridge** serves as a decentralized gateway for transferring NFTs across different blockchain networks, leveraging Chainlink's robust CCIP infrastructure for secure and reliable cross-chain communication.

### Core Components

1. **MyNFT.sol** - Original NFT contract with standard ERC721 functionality
2. **WrappedNFT.sol** - Wrapped version of the NFT for cross-chain operations
3. **NFTPoolLockAndRelease.sol** - Handles NFT locking on source chain and releasing on destination chain
4. **NFTPoolBurnAndMint.sol** - Handles NFT burning on source chain and minting on destination chain
5. **CCIPSimulator.sol** - Local simulator for CCIP functionality during development

### Transfer Mechanisms

#### 🔒 Lock-and-Release

- **Source Chain**: NFT is locked in the pool contract
- **Destination Chain**: Wrapped NFT is minted to the user
- **Return Journey**: Wrapped NFT is burned, original NFT is unlocked

#### 🔥 Burn-and-Mint

- **Source Chain**: Wrapped NFT is burned
- **Destination Chain**: New NFT is minted to the user
- **Return Journey**: NFT is burned, new wrapped NFT is minted

## 🚀 Quick Start

### Prerequisites

- Node.js (v16+)
- npm or yarn
- Hardhat
- Environment variables for testnet access

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd CrossChain-NFT-Bridge

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your private keys and RPC URLs
```

### Environment Configuration

Create a `.env` file with the following variables:

```env
PRIVATE_KEY=your_private_key_here
SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/your_project_id
AMOY_RPC_URL=https://polygon-amoy.g.alchemy.com/v2/your_api_key
```

## 🔧 Available Scripts

### Deployment

```bash
# Deploy all contracts to local network
npx hardhat deploy --network localhost

# Deploy to Sepolia testnet
npx hardhat deploy --network sepolia

# Deploy to Amoy testnet
npx hardhat deploy --network amoy
```

### NFT Operations

```bash
# Mint a new NFT
npx hardhat mint-nft --network localhost

# Check NFT ownership
npx hardhat check-nft --network localhost

# Check wrapped NFT
npx hardhat check-wrapped-nft --network localhost
```

### Cross-Chain Transfers

```bash
# Lock and cross NFT (using deployed contracts)
npx hardhat lock-and-cross --tokenid 0 --network sepolia

# Burn and cross NFT (using deployed contracts)
npx hardhat burn-and-cross --tokenid 0 --network sepolia

# Specify custom destination
npx hardhat lock-and-cross --tokenid 0 --chainselector 16281711391670634445 --receiver 0x... --network sepolia
```

### Testing

```bash
# Run unit tests
npx hardhat test

# Run tests with coverage
npx hardhat coverage

# Run staging tests
npx hardhat test test/staging/
```

## 📋 Contract Addresses (Testnet)

### Sepolia (Chain ID: 11155111)

- **Router**: `0x0BF3dE8c5D3e8A2B34D2BEeB17ABfCeBaf363A59`
- **LINK Token**: `0x779877A7B0D9E8603169DdbD7836e478b4624789`
- **Chain Selector**: `16015286601757825753` (for Amoy)

### Amoy (Chain ID: 80002)

- **Router**: `0x9C32fCB86BF0f4a1A8921a9Fe46de3198bb884B2`
- **LINK Token**: `0x0Fd9e8d3aF1aaee056EB9e802c3A762a667b1904`
- **Chain Selector**: `16281711391670634445` (for Sepolia)

## 🔗 Network Configuration

The project supports cross-chain operations between:

- **Sepolia** (Ethereum testnet)
- **Amoy** (Polygon testnet)

Configure networks in [`hardhat.config.js`](hardhat.config.js:30-49) and [`helper-hardhat-config.js`](helper-hardhat-config.js:2-16).

## 🧪 Testing

The project includes comprehensive tests in [`test/unit/cross-chain-nft.test.js`](test/unit/cross-chain-nft.test.js:1-85):

1. **NFT Minting Test**: Verifies NFT can be minted successfully
2. **Lock-and-Transfer Test**: Tests NFT locking and cross-chain transfer
3. **Burn-and-Mint Test**: Tests wrapped NFT burning and return transfer

### Test Coverage

- ✅ NFT minting and ownership
- ✅ Cross-chain transfer initiation
- ✅ Token locking mechanism
- ✅ Wrapped NFT minting
- ✅ Token burning and unlocking

## 📁 Project Structure

```
CrossChain-NFT-Bridge/
├── contracts/                 # Smart contracts
│   ├── MyNFT.sol             # Original NFT contract
│   ├── WrappedNFT.sol        # Wrapped NFT for cross-chain
│   ├── NFTPoolLockAndRelease.sol  # Lock-and-release pool
│   ├── NFTPoolBurnAndMint.sol     # Burn-and-mint pool
│   └── CCIPSimulator.sol     # Local CCIP simulator
├── deploy/                   # Deployment scripts
│   ├── 00_deploy_local_ccip.js
│   ├── 01_deploy_nft.js
│   ├── 02_deploy_lnu_pool.js
│   ├── 03_deploy_wrapped_nft.js
│   └── 04_deploy_mnb_pool.js
├── task/                     # Hardhat tasks
│   ├── mint-nft.js          # Mint NFT task
│   ├── lock-and-cross.js    # Lock and cross-chain transfer
│   ├── burn-and-cross.js    # Burn and cross-chain transfer
│   ├── check-nft.js         # Check NFT ownership
│   └── check-wrapped-nft.js # Check wrapped NFT
├── test/                     # Test files
│   ├── unit/                # Unit tests
│   └── staging/             # Staging tests
├── utils/                    # Utility functions
└── hardhat.config.js        # Hardhat configuration
```

## 🔐 Security Considerations

⚠️ **Important**: This is educational code and should not be used in production without proper security audits.

Key security features implemented:

- Owner-only functions for administrative operations
- Allowlist mechanisms for cross-chain operations
- Proper access control for NFT transfers
- Validation of chain selectors and sender addresses

## 🛠️ Development

### Adding New Networks

1. Add network configuration to [`helper-hardhat-config.js`](helper-hardhat-config.js:2-16)
2. Update [`hardhat.config.js`](hardhat.config.js:30-49) with network settings
3. Deploy contracts to the new network

### Custom Tasks

Create new Hardhat tasks in the [`task/`](task/) directory and register them in [`task/index.js`](task/index.js:1-5).

## 📚 Learning Resources

- [Chainlink CCIP Documentation](https://docs.chain.link/ccip)
- [Hardhat Documentation](https://hardhat.org/docs)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)
- [Cross-Chain NFT Standards](https://docs.chain.link/ccip/tutorials/cross-chain-nft)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your changes
4. Add tests for new functionality
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ⚠️ Disclaimer

This code is for educational purposes only. Always conduct thorough testing and security audits before deploying to mainnet. The authors are not responsible for any losses or damages resulting from the use of this code.

---

**Happy Cross-Chaining!** 🚀
