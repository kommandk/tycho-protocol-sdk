# Shibaswap V1 Substream

This substream extracts data from Shibaswap V1 on Shibarium blockchain.

## Overview

Shibaswap V1 is a clone of Uniswap V2 deployed on the Shibarium network. This substream tracks:
- Pool creation events
- Pool state changes (via Sync events)
- Token reserves and balances

## Contract Addresses

- **Factory**: `0xc2b4218F137e3A5A9B98ab3AE804108F0D312CBC`
- **Router**: `0xEF83bbB63E8A7442E3a4a5d28d9bBf32D7c813c8`

## Initial Block

The substream starts tracking from block **4734209** on the Shibarium network.

## Modules

The substream contains three main modules:

1. **map_pools_created**: Extracts pool creation events from the Factory contract
2. **store_pools**: Stores pool information for quick lookup
3. **map_pool_events**: Tracks pool state changes via Sync events

## Building

To build the substream, run:

```bash
make
```

This will compile the Rust code to WASM targeting `wasm32-unknown-unknown`.

## Protocol Details

- **Trading Fee**: 0.3% (30 basis points) - hardcoded, same as Uniswap V2
- **Protocol Type**: `shibaswap_v1_pool`
- **Financial Type**: Swap
- **Implementation Type**: Custom

## Events Tracked

- **PairCreated**: Emitted when a new liquidity pool is created
- **Sync**: Emitted on every reserve-altering operation (mint, burn, swap)

## Attributes

### Static Attributes
- `fee`: Trading fee in basis points (30 for 0.3%)
- `pool_address`: Address of the pool contract

### Dynamic Attributes  
- `reserve0`: Reserve amount of token0
- `reserve1`: Reserve amount of token1

## Testing

Integration tests can be configured in `integration_test.tycho.yaml`.

