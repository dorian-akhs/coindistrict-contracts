# Coin District - Real-World Asset Tokenization Platform

## Overview

**Coin District** is a platform for the tokenization of real-world assets. We make it possible to buy, sell, and invest in tokenized real estate, commodities, and other physical assets through blockchain technology.

This repository contains our smart contract suite built on the [ERC-3643 standard](https://eips.ethereum.org/EIPS/eip-3643) for permissioned tokens, enabling compliant security token issuance and management.

## Technology Stack

- **Solidity**: Smart contract development
- **Hardhat**: Development environment and testing framework
- **OpenZeppelin**: Secure smart contract libraries
- **ERC-3643**: Permissioned token standard
- **pnpm**: Package manager

## Key Features

- **Agent-based access control** for secure token management
- **Global identity registry** for KYC/AML compliance
- **Modular compliance engine** for regulatory adherence
- **Upgradeable contracts** via proxy pattern
- **Permissioned ERC-20 tokens** with transfer restrictions

## Getting Started

### Prerequisites

- Node.js (v16 or higher)
- pnpm package manager

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-org/coindistrict-contracts.git
   cd coindistrict-contracts
   ```

2. Install dependencies:

   ```bash
   pnpm install
   ```

3. Compile the contracts:

   ```bash
   pnpm hardhat compile
   ```

4. Run tests:
   ```bash
   pnpm hardhat test
   ```

### Development

- **Compile**: `pnpm hardhat compile`
- **Test**: `pnpm hardhat test`
- **Deploy**: `pnpm hardhat deploy`
- **Verify**: `pnpm hardhat verify`

## Documentation

For detailed specifications and implementation details, see [SPECIFICATIONS.md](./spec/SPECIFICATIONS.md).

## License

This project is licensed under the [GNU General Public License v3.0](./LICENSE.md).

---
