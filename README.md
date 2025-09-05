# 🎨 Solana NFT Marketplace

A full-stack NFT marketplace built on Solana blockchain with React frontend, Node.js API, and Anchor smart contracts. This project enables users to mint, buy, sell, and bid on NFTs with a complete marketplace experience.

## 🌟 Features

- **NFT Minting**: Create and mint new NFTs with custom metadata
- **Marketplace Trading**: Buy and sell NFTs with SOL payments
- **Bidding System**: Place bids on NFTs for auction-style sales
- **Wallet Integration**: Connect with Solana wallets for transactions
- **Modern UI**: Clean and responsive React frontend
- **RESTful API**: TypeScript-based backend with Express.js
- **Docker Support**: Containerized deployment for easy setup
- **Comprehensive Testing**: Full test suite for smart contracts

## 🏗️ Architecture

This project consists of three main components:

### 1. Solana Program (`programs/nft-marketplace/`)
- **Language**: Rust with Anchor framework
- **Program ID**: `4PYm9iCSmNQokAATfDdAsHzQsiXkcCSNTUzQU8MisNTK`
- **Network**: Solana Devnet
- **Features**:
  - NFT minting with Metaplex metadata
  - NFT selling with SOL transfers
  - Bidding system for auctions
  - Token account management

### 2. Backend API (`api/`)
- **Language**: TypeScript with Express.js
- **Port**: 8080
- **Features**:
  - RESTful endpoints for marketplace operations
  - Solana blockchain integration
  - CORS enabled for frontend communication
  - TypeORM for database operations

### 3. Frontend Application (`app/`)
- **Language**: React with JavaScript
- **Port**: 3000
- **Features**:
  - Modern React UI components
  - Wallet connection interface
  - NFT gallery and marketplace views
  - Transaction management

## 🚀 Quick Start

### Prerequisites

- Node.js (v16 or higher)
- Rust (latest stable)
- Solana CLI
- Docker and Docker Compose
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd nft-marketplace
   ```

2. **Install dependencies**
   ```bash
   # Install root dependencies
   npm install
   
   # Install API dependencies
   cd api && npm install && cd ..
   
   # Install frontend dependencies
   cd app && npm install && cd ..
   
   # Install native Solana dependencies
   cd native-sol && npm install && cd ..
   ```

3. **Set up Solana environment**
   ```bash
   # Configure Solana CLI for devnet
   solana config set --url devnet
   
   # Create a new keypair (if needed)
   solana-keygen new --outfile wallet/keypair.json
   
   # Fund your wallet with devnet SOL
   solana airdrop 2 <your-wallet-address>
   ```

4. **Build and deploy the Solana program**
   ```bash
   # Build the program
   anchor build
   
   # Deploy to devnet
   anchor deploy
   ```

5. **Run the application**
   ```bash
   # Using Docker Compose (recommended)
   docker-compose up
   
   # Or run individually:
   # Backend API
   cd api && npm run dev
   
   # Frontend
   cd app && npm start
   ```

## 📁 Project Structure

```
nft-marketplace/
├── programs/nft-marketplace/     # Solana smart contracts
│   ├── src/
│   │   ├── lib.rs               # Main program entry point
│   │   ├── mint.rs              # NFT minting logic
│   │   ├── sell.rs              # NFT selling logic
│   │   └── bid.rs               # Bidding system
│   └── Cargo.toml
├── api/                         # Backend API
│   ├── src/
│   │   ├── server.ts            # Express server setup
│   │   ├── controller.ts        # API endpoints
│   │   └── service.ts           # Business logic
│   └── package.json
├── app/                         # React frontend
│   ├── src/
│   │   ├── App.js               # Main React component
│   │   └── index.js             # React entry point
│   └── package.json
├── native-sol/                  # Native Solana integration
│   ├── app.ts                   # Native Solana client
│   └── package.json
├── tests/                       # Test files
│   ├── test.ts                  # Main test suite
│   ├── test-mint.ts             # Minting tests
│   ├── test-sell.ts             # Selling tests
│   └── test-bid.ts              # Bidding tests
├── assets/                      # NFT metadata and images
├── docker-compose.yml           # Docker configuration
├── Anchor.toml                  # Anchor configuration
└── Cargo.toml                   # Rust workspace configuration
```

## 🔧 API Endpoints

### NFT Operations
- `GET /mint-new` - Mint a new random NFT from collection
- `GET /get-nfts-minted` - Retrieve all minted NFTs
- `GET /get-nfts-owned/:publicKey` - Get NFTs owned by specific wallet
- `POST /bid-on-nft` - Place a bid on an NFT
- `POST /sell-nft` - Sell an NFT to highest bidder

### Request/Response Examples

**Mint New NFT**
```bash
curl -X GET http://localhost:8080/mint-new
```

**Place Bid**
```bash
curl -X POST http://localhost:8080/bid-on-nft \
  -H "Content-Type: application/json" \
  -d '{
    "mintAddress": "NFT_MINT_ADDRESS",
    "lamports": 1000000000
  }'
```

## 🧪 Testing

Run the comprehensive test suite:

```bash
# Run all tests
yarn test

# Run specific test suites
yarn test-mint    # Test NFT minting
yarn test-sell    # Test NFT selling
yarn test-bid     # Test bidding system
```

## 🐳 Docker Deployment

The project includes Docker configuration for easy deployment:

```bash
# Build and run all services
docker-compose up --build

# Run specific services
docker-compose up frontend backend

# Run program building (separate profile)
docker-compose --profile program up
```

## 🔑 Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
# Solana Configuration
SOLANA_NETWORK=devnet
WALLET_PATH=./wallet/keypair.json

# API Configuration
API_PORT=8080
FRONTEND_PORT=3000

# Database Configuration (if using TypeORM)
DATABASE_URL=your_database_url
```

### Anchor Configuration

The `Anchor.toml` file contains:
- Program ID: `4PYm9iCSmNQokAATfDdAsHzQsiXkcCSNTUzQU8MisNTK`
- Network: Devnet
- Wallet path configuration

## 🛠️ Development

### Smart Contract Development

1. **Modify contracts** in `programs/nft-marketplace/src/`
2. **Build and test**:
   ```bash
   anchor build
   anchor test
   ```
3. **Deploy changes**:
   ```bash
   anchor deploy
   ```

### Frontend Development

1. **Start development server**:
   ```bash
   cd app && npm start
   ```
2. **Modify components** in `app/src/`
3. **Hot reload** is enabled for development

### API Development

1. **Start API server**:
   ```bash
   cd api && npm run dev
   ```
2. **Modify endpoints** in `api/src/controller.ts`
3. **Add business logic** in `api/src/service.ts`

## 📚 Smart Contract Details

### Mint Function
- Creates new NFT with custom metadata
- Integrates with Metaplex Token Metadata program
- Generates master edition for uniqueness
- Mints single token to creator's wallet

### Sell Function
- Transfers SOL from buyer to seller
- Creates buyer's token account
- Transfers NFT ownership
- Handles all token account operations

### Bid Function
- Creates bid account for NFT
- Stores bid amount and bidder information
- Uses program-derived addresses for security

## 🔒 Security Considerations

- All transactions are signed by appropriate parties
- Program uses Anchor's security features
- Token accounts are properly validated
- Bidding system uses program-derived addresses

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Anchor Framework](https://project-serum.github.io/anchor/) for Solana development
- [Metaplex](https://metaplex.com/) for NFT metadata standards
- [Solana Web3.js](https://solana-labs.github.io/solana-web3.js/) for blockchain interaction
- [React](https://reactjs.org/) for frontend framework

## 📞 Support

For support and questions:
- Create an issue in the repository
- Check the [Solana documentation](https://docs.solana.com/)
- Review [Anchor documentation](https://project-serum.github.io/anchor/)

---

**Built with ❤️ on Solana**
