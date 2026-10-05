# Web3 Wallet & Trading Dashboard

Frontend-focused Web3 dashboard for wallet connectivity, on-chain portfolio data, smart contract interactions, market data synchronization, and transaction lifecycle management.

## Overview

This project explores the integration between modern frontend engineering and Web3 infrastructure.

The application connects browser wallets to an EVM-compatible environment, reads on-chain data, combines blockchain state with off-chain market information, and manages transaction flows through a responsive React and TypeScript interface.

The main goal is to demonstrate practical experience with wallet integration, on-chain data, smart contract interaction, asynchronous state, testing, performance, and production-oriented frontend workflows.

## Architecture

React + TypeScript → wagmi → viem → Wallet / RPC → Ethereum / EVM

Off-chain market data is fetched separately and synchronized with wallet and blockchain state through TanStack Query.

## Features

- Wallet connectivity with MetaMask and WalletConnect
- Account and network state management
- Supported network detection
- Network switching
- Native token balance reads
- ERC-20 token balance reads
- On-chain portfolio data
- Off-chain market data integration
- Smart contract reads and interactions
- Transaction signing
- Transaction lifecycle handling
- Loading, error, and rejected transaction states
- RPC error handling
- Address and network validation
- Query caching and refetching
- Unit, component, and end-to-end testing
- CI validation through GitHub Actions
- Production deployment

## Tech Stack

- React
- TypeScript
- wagmi
- viem
- MetaMask
- WalletConnect
- Ethereum / EVM
- TanStack Query
- Vitest
- React Testing Library
- Playwright
- GitHub Actions
- REST APIs

## How It Works

1. A user connects a compatible browser wallet.
2. The application retrieves the connected account and current network.
3. wagmi manages wallet connection and reactive blockchain state.
4. viem handles low-level EVM interactions and contract calls.
5. The application reads native and ERC-20 balances from the blockchain.
6. External market data is fetched through an API.
7. TanStack Query manages caching, refetching, retries, and synchronization.
8. On-chain balances and market prices are combined to calculate portfolio values.
9. Smart contract interactions can trigger wallet transaction requests.
10. The interface tracks transaction states until confirmation or failure.

## Wallet Integration

The wallet layer is responsible for:

- connecting and disconnecting wallets
- tracking account changes
- detecting the active chain
- validating supported networks
- switching networks
- reacting to wallet state changes

Supported wallet integrations include:

- MetaMask
- WalletConnect

## On-Chain Data

The application uses wagmi and viem to retrieve blockchain data such as:

- native token balances
- ERC-20 balances
- token metadata
- smart contract state
- transaction data

Typical on-chain flow:

```text
Connected Wallet
      ↓
Account Address
      ↓
Network Validation
      ↓
RPC Request
      ↓
Blockchain Data
      ↓
Frontend State
```

## Portfolio Data

The portfolio layer combines two different data sources.

Blockchain data provides:

- wallet ownership
- token balances
- contract state

External APIs provide:

- token prices
- market information
- percentage changes

The application combines both sources to produce derived portfolio values.

Example:

```text
ETH Balance
+
ETH Market Price
↓
Portfolio Value
```

## State Management

The project distinguishes between different types of state.

### Wallet State

Managed through wagmi:

- connection status
- account
- chain
- wallet connector

### On-Chain State

Includes:

- balances
- contract reads
- transaction state

### Server State

Managed through TanStack Query:

- market data
- caching
- refetching
- retries
- stale data

### Derived State

Calculated from existing data:

- portfolio value
- asset allocation
- formatted balances
- transaction summaries

## State Synchronization

The application reacts to changes across wallet, blockchain, and market state.

Examples:

```text
Wallet Connected
↓
Fetch Balances
```

```text
Network Changed
↓
Invalidate On-Chain Queries
↓
Fetch New Network Data
```

```text
Transaction Confirmed
↓
Refetch Balance
↓
Update Portfolio
```

```text
Wallet Disconnected
↓
Clear Wallet-Dependent Data
```

## Smart Contract Interaction

The application supports interaction with EVM smart contracts through wagmi and viem.

Examples include:

- reading contract state
- ERC-20 token interactions
- transaction requests
- network-aware contract calls

Contract interactions require:

- contract address
- ABI
- function name
- function arguments
- connected wallet
- supported network

## Transaction Lifecycle

Transaction flows are treated as explicit application states.

Typical lifecycle:

```text
Idle
↓
Awaiting Wallet Signature
↓
Pending
↓
Confirmed
```

Possible failure states include:

```text
User Rejected
Wrong Network
Insufficient Funds
RPC Error
Contract Revert
```

The UI should provide clear feedback for each stage rather than treating transactions as a single asynchronous action.

## Error Handling

The project handles Web3-specific failure scenarios such as:

- wallet connection failure
- user-rejected requests
- unsupported networks
- malformed addresses
- invalid contract addresses
- insufficient funds
- RPC failures
- RPC timeouts
- reverted transactions
- market API failures

Errors are surfaced through user-facing states instead of relying only on console logs.

## Security

Security considerations include:

- no private keys stored in the application
- no seed phrase handling
- no recovery phrase handling
- address validation
- network validation
- contract address verification
- explicit transaction information before signing
- environment-based configuration
- no secrets committed to GitHub
- safe wallet interaction patterns

The application never requests or stores private wallet credentials.

## Performance

Frontend performance practices include:

- controlled query refetching
- reduced unnecessary RPC calls
- caching through TanStack Query
- render optimization
- lazy loading where justified
- code splitting
- efficient derived calculations

Performance optimizations are introduced only when technically justified.

## Testing

The project uses multiple testing layers.

### Unit Testing

Vitest is used for:

- utilities
- formatting
- transaction-state logic
- derived calculations

### Component Testing

React Testing Library is used for:

- connected and disconnected wallet states
- network warnings
- loading states
- transaction feedback
- error states

### End-to-End Testing

Playwright is used for user flows such as:

- wallet connection states
- navigation
- transaction-related UI flows
- error handling

Wallet-dependent behavior may use mocked providers where necessary.

## Running Locally

### Prerequisites

Make sure you have installed:

- Node.js
- npm
- Git
- a compatible browser wallet such as MetaMask

### Installation

```bash
git clone https://github.com/igor-souza-engineer/web3-wallet-dashboard.git
cd web3-wallet-dashboard
npm install
```

### Environment Variables

Create a local environment file:

```bash
cp .env.example .env
```

Configure the required values according to the integrations used by the project.

Example:

```env
VITE_WALLETCONNECT_PROJECT_ID=
VITE_RPC_URL=
VITE_MARKET_API_URL=
```

Do not commit real credentials or private configuration values.

### Start the Application

```bash
npm run dev
```

Open the local URL displayed by the development server.

## Usage

1. Open the application.
2. Connect MetaMask or another supported wallet.
3. Confirm the connected account and network.
4. Switch to a supported network if necessary.
5. View native and ERC-20 balances.
6. Review portfolio values calculated from on-chain and market data.
7. Interact with supported smart contract actions.
8. Review transaction details before signing.
9. Confirm the transaction through the connected wallet.
10. Follow the transaction state until confirmation or failure.

## CI/CD

GitHub Actions is used to automate project validation.

Typical pipeline:

```text
Push / Pull Request
↓
Install Dependencies
↓
Lint
↓
Typecheck
↓
Unit / Component Tests
↓
Build
↓
End-to-End Validation
```

## Deployment

The frontend is designed for deployment through a modern hosting platform such as Vercel.

Production configuration should include:

- secure environment variables
- production RPC endpoints
- valid WalletConnect configuration
- supported network configuration
- production build validation
- HTTPS

## Repository Structure

```text
web3-wallet-dashboard/
├── src/
│   ├── components/
│   ├── features/
│   │   ├── wallet/
│   │   ├── portfolio/
│   │   ├── market/
│   │   └── transactions/
│   ├── hooks/
│   ├── lib/
│   ├── services/
│   ├── types/
│   └── utils/
├── tests/
├── docs/
├── .github/
│   └── workflows/
├── .env.example
├── README.md
└── package.json
```

The repository structure should evolve with the project and avoid unnecessary abstractions.

## Project Goals

This project was built to demonstrate practical experience with:

- frontend engineering
- React and TypeScript
- Web3 wallet integration
- wagmi
- viem
- MetaMask
- WalletConnect
- Ethereum / EVM
- on-chain data
- smart contract interactions
- transaction lifecycle management
- TanStack Query
- asynchronous state
- testing
- performance
- Web3 security fundamentals
- CI/CD
- production deployment

## License

This project is intended for educational and portfolio purposes.
