# BitStitch 🔗

> Modular Bitcoin Collateral Layer for Stable Liquidity and Yield

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Clarity](https://img.shields.io/badge/Clarity-v3-blue.svg)](https://clarity-lang.org)
[![Stacks](https://img.shields.io/badge/Stacks-Blockchain-orange.svg)](https://stacks.org)

## Overview

BitStitch is a decentralized, composable financial layer that transforms native Bitcoin into programmable liquidity. By locking BTC as over-collateral, users can mint stablecoins and interact with an automated liquidity pool designed for low-slippage swaps and yield generation.

### Core Features

- 🏦 **BTC-backed Stablecoin Issuance** - Mint stablecoins with Bitcoin collateral enforcement
- 🔄 **Dynamic AMM-based Liquidity** - Automated market maker for liquidity provision and redemption
- 📊 **Oracle-driven Price Feeds** - Real-time price data with validity gating
- 🛡️ **Safety-first Design** - Liquidation thresholds and comprehensive access controls
- 🧩 **Composable Architecture** - Built for cross-chain extensibility and protocol integration

## Architecture

BitStitch consists of several key components:

### Collateral Vaults

- Minimum 150% collateralization ratio
- 130% liquidation threshold
- Minimum deposit: 0.01 BTC
- Real-time collateral ratio monitoring

### Automated Market Maker (AMM)

- 0.3% trading fee
- Dynamic liquidity pool management
- LP token rewards system
- Low-slippage swap mechanisms

### Oracle System

- Price validation and gating
- Maximum price limits for safety
- Owner-controlled price updates
- Integration-ready design

## Use Cases

### For Stablecoin Ecosystems

- Leverage Bitcoin's security and liquidity
- Enhance collateral diversity
- Reduce counterparty risk

### For Protocol Builders

- Build Bitcoin-native DeFi applications
- Access composable liquidity infrastructure
- Integrate with existing Stacks ecosystem

### For Liquidity Providers

- Earn yield on Bitcoin holdings
- Participate in diversified liquidity pools
- Benefit from trading fee revenue

## Getting Started

### Prerequisites

- [Clarinet](https://docs.hiro.so/stacks/clarinet) (v2.0+)
- [Node.js](https://nodejs.org/) (v18+)
- Basic understanding of Clarity smart contracts

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/adamu-williams/bit-stitch.git
   cd bit-stitch
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Verify contract syntax**

   ```bash
   clarinet check
   ```

### Development Setup

1. **Start Clarinet console**

   ```bash
   clarinet console
   ```

2. **Run tests**

   ```bash
   npm test
   ```

3. **Run tests with coverage**

   ```bash
   npm run test:report
   ```

4. **Watch mode for development**

   ```bash
   npm run test:watch
   ```

## Contract Functions

### Core Operations

#### Initialization

```clarity
(contract-call? .bit-stitch initialize u50000000) ;; Initialize with $50 BTC price
```

#### Vault Management

```clarity
;; Deposit Bitcoin collateral
(contract-call? .bit-stitch deposit-collateral u100000000) ;; 1 BTC

;; Mint stablecoins (requires sufficient collateral)
(contract-call? .bit-stitch mint-stablecoin u30000000) ;; $30 USD

;; Burn stablecoins to reduce debt
(contract-call? .bit-stitch burn-stablecoin u10000000) ;; $10 USD
```

#### Liquidity Operations

```clarity
;; Add liquidity to the pool
(contract-call? .bit-stitch add-liquidity u50000000 u2500000000) ;; 0.5 BTC + $2500 USD

;; Remove liquidity from the pool
(contract-call? .bit-stitch remove-liquidity u1000000) ;; LP tokens
```

### Read-Only Functions

```clarity
;; Get vault details for a user
(contract-call? .bit-stitch get-vault-details 'SP1234...)

;; Check collateral ratio
(contract-call? .bit-stitch get-collateral-ratio 'SP1234...)

;; Get pool statistics
(contract-call? .bit-stitch get-pool-details)

;; Get liquidity provider details
(contract-call? .bit-stitch get-lp-details 'SP1234...)
```

## Protocol Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Minimum Collateral Ratio | 150% | Required over-collateralization |
| Liquidation Threshold | 130% | Automatic liquidation trigger |
| Minimum Deposit | 0.01 BTC | Smallest collateral deposit |
| Pool Fee Rate | 0.3% | Trading fee for liquidity pool |
| Price Precision | 6 decimals | Oracle price accuracy |
| Maximum Price | $1M USD | Safety limit for price feeds |

## Error Codes

| Code | Error | Description |
|------|-------|-------------|
| u1000 | ERR-NOT-AUTHORIZED | Unauthorized access attempt |
| u1001 | ERR-INSUFFICIENT-BALANCE | Insufficient token balance |
| u1002 | ERR-INVALID-AMOUNT | Invalid amount specified |
| u1003 | ERR-INSUFFICIENT-COLLATERAL | Below minimum collateral ratio |
| u1004 | ERR-POOL-EMPTY | Liquidity pool has no reserves |
| u1005 | ERR-SLIPPAGE-TOO-HIGH | Slippage exceeds tolerance |
| u1006 | ERR-BELOW-MINIMUM | Amount below minimum threshold |
| u1007 | ERR-ABOVE-MAXIMUM | Amount exceeds maximum limit |
| u1008 | ERR-ALREADY-INITIALIZED | Contract already initialized |
| u1009 | ERR-NOT-INITIALIZED | Operation requires initialization |
| u1010 | ERR-INVALID-PRICE | Invalid price data |

## Testing

The project includes comprehensive test coverage using Vitest and the Clarinet SDK:

```bash
# Run all tests
npm test

# Run tests with coverage and cost analysis
npm run test:report

# Watch mode for continuous testing
npm run test:watch

# Check contract syntax
clarinet check
```

## Security Considerations

### Collateralization

- Minimum 150% collateral ratio enforced
- Automatic liquidation at 130% ratio
- Real-time collateral monitoring

### Access Controls

- Owner-only functions for critical operations
- Proper authorization checks throughout
- Safe mathematical operations

### Oracle Security

- Price validation and bounds checking
- Maximum price limits
- Controlled price update mechanism

## Deployment

### Testnet Deployment

```bash
clarinet integrate --testnet
```

### Mainnet Deployment

```bash
clarinet integrate --mainnet
```

## Contributing

We welcome contributions to BitStitch! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Write tests** for your changes
4. **Ensure all tests pass** (`npm test`)
5. **Check contract syntax** (`clarinet check`)
6. **Commit your changes** (`git commit -m 'Add amazing feature'`)
7. **Push to the branch** (`git push origin feature/amazing-feature`)
8. **Open a Pull Request**

### Development Guidelines

- Follow Clarity best practices
- Maintain comprehensive test coverage
- Document all public functions
- Use meaningful variable names
- Include error handling for edge cases

## Roadmap

### Phase 1: Core Protocol ✅

- [x] Basic collateral management
- [x] Stablecoin minting/burning
- [x] AMM liquidity pools
- [x] Oracle price feeds

### Phase 2: Enhanced Features 🚧

- [ ] Advanced liquidation mechanisms
- [ ] Multi-asset collateral support
- [ ] Governance token integration
- [ ] Cross-chain bridge compatibility

### Phase 3: Ecosystem Integration 📋

- [ ] DEX aggregator integration
- [ ] Yield farming strategies
- [ ] Insurance protocol partnerships
- [ ] Mobile application interface

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built on the [Stacks blockchain](https://stacks.org)
- Powered by [Clarity smart contracts](https://clarity-lang.org)
- Developed with [Clarinet](https://docs.hiro.so/stacks/clarinet)
