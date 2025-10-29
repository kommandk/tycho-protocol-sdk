# Shibaswap V2 Substream

This substream extracts data from Shibaswap V2 on Shibarium blockchain.

## Overview

Shibaswap V2 is a clone of Uniswap V3 deployed on the Shibarium network. This substream tracks:
- Pool creation events
- Pool state changes (liquidity, tick, sqrt_price)
- Balance changes via various events (Mint, Burn, Swap, Collect, etc.)
- Token reserves and balances

## Contract Addresses

- **Factory**: `0x2996B636663ddeBaE28742368ed47b57539C9600`
- **NonFungiblePositionManager**: `0x8Ab443Be082105AE444337b49E1FD8D23c2631Dc`
- **SwapRouter**: `0xd0d020fd91aB1Ab2CbbdbfBde2Fd9C5e4D5896b8`
- **Quoter**: `0x9dab43E3DbEF5241f491818077E12E21b02D7035`
- **V2Migrator**: `0xf2eA936961c29d6737bF7DF61cC3134684447045`

## Initial Block

The substream starts tracking from block **4734209** on the Shibarium network.

## Modules

The substream contains five main modules:

1. **map_pools_created**: Extracts pool creation events from the Factory contract
2. **store_pools**: Stores pool information for quick lookup
3. **map_balance_changes**: Tracks balance deltas from all pool events
4. **store_pools_balances**: Accumulates balance changes over time
5. **map_pool_events**: Combines all events and state changes

## Building

To build the substream, run:

```bash
make
```

This will compile the Rust code to WASM targeting `wasm32-unknown-unknown`.

## Protocol Details

- **Protocol Version**: Uniswap V3 / Shibaswap V2
- **Financial Type**: Swap (Concentrated Liquidity)
- **Implementation Type**: Custom
- **Fee Tiers**: Multiple fee tiers (0.01%, 0.05%, 0.3%, 1%)

## Events Tracked

- **PoolCreated**: Emitted when a new liquidity pool is created
- **Initialize**: Pool initialization with starting price
- **Mint**: Adding liquidity to a position
- **Burn**: Removing liquidity from a position
- **Swap**: Token swaps
- **Collect**: Collecting fees from positions
- **Flash**: Flash loans
- **SetFeeProtocol**: Protocol fee changes
- **CollectProtocol**: Protocol fee collection

## Attributes

### Static Attributes
- `fee`: Trading fee tier in basis points
- `tick_spacing`: Minimum tick spacing for the pool
- `pool_address`: Address of the pool contract

### Dynamic Attributes  
- `liquidity`: Current liquidity in the pool
- `tick`: Current tick
- `sqrt_price_x96`: Current sqrt price (X96 format)

## Testing

Integration tests can be configured in `integration_test.tycho.yaml`.

