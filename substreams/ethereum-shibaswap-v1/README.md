# Ethereum Shibaswap v1 Substream

This substream extracts and processes data from Shibaswap v1 pools on Ethereum. Shibaswap v1 is a clone of Uniswap v2 with very minor changes.

## Overview

Shibaswap v1 is an Automated Market Maker (AMM) protocol that allows users to swap tokens and provide liquidity. This substream tracks:

- Pool creation events
- Liquidity changes (Mint/Burn events)
- Swap events
- Reserve updates via Sync events

## Configuration

The substream is configured with the following Shibaswap v1 contract addresses on Ethereum:

- **Factory**: `0x115934131916C8b277DD010Ee02de363c09d037c`
- **Router**: `0x03f7724180AA6b939894B5Ca4314783B0b36b329` (for reference)
- **Deployment Block**: 12771526

Parameters in `ethereum-shibaswap-v1.yaml`:
- `factory_address`: 115934131916C8b277DD010Ee02de363c09d037c (without 0x prefix)
- `protocol_type_name`: shibaswap_v1_pool
- `initialBlock`: 12771526

## Modules

1. **map_pools_created**: Extracts pool creation events from the factory contract
2. **store_pools**: Stores pool data for reference by subsequent modules
3. **map_pool_events**: Processes Sync events to track reserve changes and pool state

## Building

```bash
make build
```

This will compile the Rust code to WebAssembly for use with Substreams.

## Testing

Integration tests can be configured in `integration_test.tycho.yaml`. Add test cases with specific block ranges and expected pool states.

## ABI Files

- `abi/Factory.json`: Shibaswap v1 Factory contract ABI
- `abi/Pool.json`: Shibaswap v1 Pool (Pair) contract ABI

## Protocol Details

- Trading fee: 0.3% (30 basis points) - hardcoded in the pool creation logic
- Uses the same constant product formula (x * y = k) as Uniswap v2
- Sync events are emitted on every reserve-altering operation

## Notes

Since Shibaswap v1 is a clone of Uniswap v2, it maintains the same event signatures and contract interfaces. The main difference is in the factory contract address and any minor modifications made by the Shibaswap team.

