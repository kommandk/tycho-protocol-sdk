# Ethereum Shibaswap V2 Substreams

This substreams package indexes [Shibaswap V2](https://shibaswap.com) - a decentralized exchange that is a clone of Uniswap V3 with minor modifications.

## Overview

Shibaswap V2 is a concentrated liquidity AMM (Automated Market Maker) protocol that operates identically to Uniswap V3. This substreams package tracks:

- Pool creation events
- Liquidity provision (mint/burn)
- Swaps
- Fee collection
- Pool state changes

## Configuration

### Network
- **Chain**: Ethereum Mainnet (Chain ID: 1)
- **Factory Address**: `0xD9CE49caf7299DaF18ffFcB2b84a44fD33412509`
- **Deployment Block**: `21036458`

### Key Ecosystem Tokens
- **SHIB** (Shiba Inu): `0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE`
- **BONE** (Bone ShibaSwap): `0x9813037ee2218799597d83D4a5B6F3b6778218d9`
- **TREAT**: `0xa02C49Da76A085e4E1EE60A6b920dDbC8db599F4`
- **LEASH**: `0x27C70Cd1946795B66be9d954418546998b546634`

## Building

To build the substreams package:

```bash
# Using Make
make build

# Or directly with cargo
cargo build --target wasm32-unknown-unknown --release
```

## Modules

### 1. `map_pools_created`
- **Type**: Map
- **Input**: Ethereum blocks
- **Output**: Pool creation events with initial state
- **Description**: Tracks `PoolCreated` events from the Shibaswap V2 factory

### 2. `store_pools`
- **Type**: Store
- **Input**: `map_pools_created`
- **Description**: Maintains a registry of all Shibaswap V2 pools

### 3. `map_balance_changes`
- **Type**: Map
- **Input**: Ethereum blocks, `store_pools`
- **Output**: Token balance changes
- **Description**: Tracks all token balance changes in pools

### 4. `store_pools_balances`
- **Type**: Store  
- **Input**: `map_balance_changes`
- **Description**: Maintains cumulative balance state for all pools

### 5. `map_pool_events`
- **Type**: Map
- **Input**: Ethereum blocks, `map_pools_created`, `store_pools`, `store_pools_balances`
- **Output**: Complete pool state changes
- **Description**: Main output module providing comprehensive pool events and state

## Protocol Type

The protocol type identifier is: `shibaswap_v2_pool`

## Differences from Uniswap V3

While Shibaswap V2 is functionally identical to Uniswap V3, the main differences are:
- Different factory contract address
- Deployed on Ethereum mainnet at a later date
- Focused on Shiba Inu ecosystem tokens

## Development Notes

This package is based on the `ethereum-uniswap-v3` substreams package, with the following changes:
- Updated factory address
- Updated deployment block number
- Changed protocol type name
- Updated proto package namespace

## Testing

Integration tests can be run using the `integration_test.tycho.yaml` configuration.

## License

See the main repository LICENSE file.

