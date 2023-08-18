---
title: "Integrate Your Protocol into Reservoir"
slug: "how-to-get-distribution-for-your-protocol-using-reservoir"
excerpt: "Integrate your protocol's liquidity into Reservoir"
hidden: false
createdAt: "2023-04-07T20:03:18.147Z"
updatedAt: "2023-06-01T22:55:28.912Z"
---
For marketplaces and NFT liquidity protocols, order distribution is key. Because Reservoir is open-source, you can integrate your new marketplace or liquidity protocol into Reservoir yourself, and instantly get distribution to across the Reservoir ecosystem, including to [Opensea Pro](https://pro.opensea.io/). 

# Integrating your protocol

There are three major steps to complete you integration:

1. SDK integration
2. Indexer integration
3. Router integration

> 📘 We recommend forking the indexer and working internally before making a one pass PR to the indexer.

## SDK integration

Every exchange that we support needs to have a corresponding SDK implementation. You can checkout the SDK repo [here](https://github.com/reservoirprotocol/indexer/tree/main/packages/sdk).

We need the following (below examples are taken from the LooksRare integration):

- The addresses of any relevant contracts for every supported chain ([example](https://github.com/reservoirprotocol/indexer/blob/main/packages/sdk/src/looks-rare/addresses.ts))
- The ABIs of any relevant contracts ([example](https://github.com/reservoirprotocol/indexer/tree/main/packages/sdk/src/looks-rare/abis))
- Types for the exchange’s order format ([example](https://github.com/reservoirprotocol/indexer/blob/main/packages/sdk/src/looks-rare/types.ts))
- Logic for handling common order operations:
  - [normalization](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/order.ts#L237-L262)
  - [high-level validation](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/order.ts#L22-L42)
  - [hashing and signature generation/validation](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/order.ts#L44-L80)
  - [optional on-chain validation](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/order.ts#L88-L165)
  - [order type detection](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/order.ts#L167-L205)(goes hand in hand with the below builders)
- logic for building/parsing/validating the different kind of available order types (eg. bids/asks, single-token/contract-wide/token-list) ([example](https://github.com/reservoirprotocol/core/tree/main/packages/sdk/src/looks-rare/builders)):
  - [order type validation](https://github.com/reservoirprotocol/indexer/tree/main/packages/sdk/src/looks-rare/builders) - ensuring that an order adheres to some standard format we support and understand
  - [order building](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/builders/single-token/index.ts#L33-L65) - generating a compliant order of a particular type
  - [matching an order](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/looks-rare/builders/single-token/index.ts#L67-L79) - generating any data needed to fill an existing order

The way to check an integration is via automated tests which reside in the `contracts` package.[Here](https://github.com/reservoirprotocol/core/tree/main/packages/contracts/test/sdk/looks-rare) are the tests for the LooksRare integration as an example. Since the tests are run on mainnet forks, make sure to have a `.env` file in the `contracts` package directory containing the following:

```
ALCHEMY_KEY=
BLOCK_NUMBER=
```

## Indexer Integration

Once the SDK integration is done, the next step is to add support for the new exchange at the indexer level (this builds on top of the previous core SDK integration, which the indexer uses as an abstraction for the low-level exchange details).

We need the following (below examples are taken from the LooksRare integration):

- [order parsing/validation logic](https://github.com/reservoirprotocol/indexer/blob/main/packages/indexer/src/orderbook/orders/looks-rare-v2/index.ts) - This implies quite a few checks ensuring that the order is properly formatted and valid - some checks are exchange-independent (like validity times) while other checks are exchange-dependent (like nonce validation))
- [order fillability checking logic](https://github.com/reservoirprotocol/indexer/blob/main/packages/indexer/src/orderbook/orders/looks-rare-v2/check.ts) - the above validation logic will use the fillability checking logic in order to associate an up-to-date status to the order
- event ingestion logic - 
  - [event definitions](https://github.com/reservoirprotocol/indexer/blob/main/packages/indexer/src/sync/events/data/looks-rare.ts)
  - [event handling logic](https://github.com/reservoirprotocol/indexer/blob/main/packages/indexer/src/sync/events/handlers/looks-rare.ts) - the examples are pretty easy to follow along and adjust for any other new exchanges. It involves keeping orders validated based on events happening on-chain like cancels or fills/

To check the indexer part of the integration, it would be useful to write unit/integration tests that check different logic:

- [sales ingestion](https://github.com/reservoirprotocol/indexer/blob/9d961ce154f776995aeec6dd26195e5884095c5b/packages/indexer/src/tests/nftx/nftx.test.ts#L194-L227)
- [liquidity ingestion, order validation, order filling](https://github.com/reservoirprotocol/indexer/blob/main/packages/indexer/src/tests/flow/flow-integration.test.ts)

## Router Integration

In order to support some advanced features (eg. buying listings / filling bids from different protocols) a router module is needed. 

Here are some [examples](https://github.com/reservoirprotocol/indexer/blob/main/packages/contracts/contracts/router/modules/exchanges/LooksRareModule.sol) and [tests](https://github.com/reservoirprotocol/indexer/tree/main/packages/contracts/test/router/looks-rare) to help with module construction.  

Once the module is ready and tested, the next and final step is integrating it within the smart-routing logic which resides in the SDK’s [Router](https://github.com/reservoirprotocol/indexer/blob/main/packages/sdk/src/router/v6/router.ts) class. For integrating listings, you should cover the [fillListingsTx](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/router/v6/router.ts#L144) method while bids are covered by the [fillBidsTx](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/router/v6/router.ts#L2309) method. The smart-routing logic for the new protocol can actually be implemented without a corresponding router module, but in this case the functionality will be severely restricted. Here’s an [example](https://github.com/reservoirprotocol/indexer/blob/65c1da114c24a8de7db002ed2ccfeecb94868f35/packages/sdk/src/router/v6/router.ts#L392-L431) of handling listings of a protocol without a router module.

## Running and testing locally

- Run `docker-compose rm -f && docker-compose up --remove-orphans` to bootstrap a local postgres and redis instance (the Docker daemon must be running in the background)
- Run `yarn && yarn build && yarn start` to install any dependencies, migrate the database, and start the indexer
- Run `yarn test` to trigger the tests
- If needed, it’s also possible to manually trigger syncing data from the blockchain via `curl -X POST -H ‘Content-Type: application/json’ -H ‘X-Admin-Api-Key: admin’ -d ‘{“fromBlock”: 1, “toBlock”: 1}’ http://localhost:3000/admin/sync-events`

# Notes

- It will be useful to take a look at the examples most similar to the protocol being integrated. For example, an off-chain orderbook protocol’s integration should be very similar to eg. LooksRare, Seaport, an on-chain orderbook protocol should be similar to eg. Foundation, while an AMM-like protocol should be similar to eg. Sudoswap, NFTX.

# FAQ

### What's the difference between `price` and `value`?

 For listings `value = price`, for bids `value = price - fees`. Value is basically what the taker needs to pay for listings or what the taker will receive for bids

### What's the difference between `currency_price` and `price`?

`Value` and `Price` are always denominated in ETH (or the native currency of the chain) while `currency value` are the in the currency the order was made in.

### What does `is_reservoir` refer to?

`Is_reservoir` is used to denote Reservoir native orders. You'll want that to be `null/false`

### What does `missing_royalties` refer to?

The missing royalties are the difference between the royalties the order pays and the full royalties the creator configured. For example if an order pays a royalty of 0.5% but the creator set their royalties to 10% the missing royalties will be 9.5%. You shouldn't set that to a negative value, just leave it empty if all royalties are paid (even if more royalties than configured are paid).