# 📄 SPECIFICATION.md

> **Version**: 1.0
> **Standard**: [ERC‑3643](https://erc3643.org) — Permissioned Tokens  
> **Project**: Real-World Asset Token Platform  
> **Author**: [Coin District]  
> **Date**: 2025‑08‑01

---

## ✅ Overview

This document specifies the features and behaviors implemented in the **V1 version** of the smart contract suite based on the [ERC‑3643](https://erc3643.org) standard.

This replaces the V0 architecture and introduces:

- **Agent-based access control**
- **Global identity registry**
- **Modular compliance engine**
- **Upgradeable contracts via proxy pattern**
- **Permissioned ERC‑20 tokens**

---

## 🧱 Architecture Summary

### Main Components

| Contract           | Role                                             |
| ------------------ | ------------------------------------------------ |
| `Factory`          | Deploys token instances with ERC‑3643-compliance |
| `Token` (T-REX)    | Permissioned ERC-20 token contract               |
| `IdentityRegistry` | Manages whitelisted identities (KYC-ed)          |
| `Compliance`       | Defines transfer & holding rules                 |

### Agents

| Agent Type        | Permissions                            |
| ----------------- | -------------------------------------- |
| `TokenController` | Mint, burn, pause, forceTransfer       |
| `ComplianceAgent` | Manage compliance rules                |
| `IdentityAgent`   | Approve/revoke identities via registry |

---

## 📦 Functional Coverage

### 🏗️ Token Factory

- [x] Deploys compliant ERC-3643 token contracts
- [x] Assigns initial parameters (name, symbol, decimals, stablecoin, max supply)
- [x] Prevents duplicate token names or symbols
- [x] Stores token instances (via ID → address mapping)
- [x] Validates share implementation version
- [x] Configures supply cap at creation (optional)

---

### 🔐 Agent-Based Access Control

- [x] All admin logic handled through ERC‑3643 **agents**
  - `TokenController`
  - `ComplianceAgent`
  - `IdentityAgent`
- [x] Agents added or removed dynamically via authorized roles
- [x] No legacy `AccessControl` or custom roles

---

### 👤 Identity & Whitelisting

- [x] Uses **global IdentityRegistry**
- [x] Only verified identities can:
  - Buy tokens
  - Send tokens
  - Receive transfers
  - Be minted tokens
- [x] On-chain identity checks integrated in token logic
- [x] Manual identity management via `IdentityAgent`

---

### ⚖️ Compliance Engine

- [x] Pluggable `Compliance` contract per token
- [x] Enforce rules:
  - Holding limits
  - Blacklist
  - Jurisdiction
  - Role-based restrictions
- [x] Updatable at runtime by `ComplianceAgent`

---

### 💵 Token Sales

- [x] Create sales: amount, price, deadline
- [x] Buyers pay in stablecoin (ERC20)
- [x] Amount minted to buyer upon payment
- [x] Track sales data per sale ID
- [x] Reject overselling past supply

---

### 🎯 Token Supply Controls

- [x] Optional cap on total supply (`maxSupply`)
- [x] Expose:
  - `totalSupply()`
  - `getRemainingSupply()`
- [x] Admin burn capability (optional)
- [x] Reject mint if it exceeds max supply

---

### 💰 Treasury Management

- [x] Accept ETH payments (fallback)
- [x] Withdraw stablecoin (ERC20)
- [x] Withdraw ETH

---

### ⚙️ Configuration / Admin

- [x] Update stablecoin address
- [x] Pause/unpause token
- [x] Enable/disable transfer restrictions
- [x] Set compliance contract address
- [x] Set or update `maxHoldingAmount`

---

### 🧾 Views & Helpers

- [x] `getSaleInfo(saleId)`
- [x] `getSupplyInfo()`
- [x] `isBlacklisted(address)` (local/global)
- [x] `isWhitelisted(address)` (IdentityRegistry)
- [x] `getRemainingSupply()`

---

### 🔄 Upgradeability

- [x] Contracts are upgradeable via UUPS or ERC1967
- [x] Upgrades gated via `TokenController` agent
- [x] Proxy pattern via `ERC1967Proxy` (OpenZeppelin)

---

## 📍 Notes & Best Practices

- 🛡️ All permission checks must go through **IdentityRegistry** and **Compliance** contracts.
- 🔄 Agents should be managed through on-chain governance or secure multisigs.
- ✅ Always validate the token implementation version before deploying.
- 👀 For extensibility, keep `__gap` in storage for upgrades.

---

## 📚 References

- [ERC‑3643 Standard](https://erc3643.org/)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)
- [ERC1967 / UUPS Upgradeability](https://docs.openzeppelin.com/contracts/4.x/upgradeable)

---

> This specification is version-controlled and maintained in `main/spec/SPECIFICATION.md`.  
> All contract updates must reflect in this document before merge to main.
