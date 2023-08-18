---
title: "How to Add a Custom ERC-20"
slug: "adding-support-for-custom-erc-20-token"
excerpt: "Add a custom ERC-20 support to Reservoir"
hidden: false
createdAt: "2023-01-20T19:08:51.545Z"
updatedAt: "2023-05-18T14:43:41.608Z"
---
> 📘 Please Check Coingecko
> 
> If your custom ERC-20 is available and traded on [CoinGecko](https://www.coingecko.com/), you do not need to complete the steps here. Please reference the [How to list in different ERC-20's](doc:how-to-list-in-different-erc20s) guide to get started with alternative currency.

Reservoir enables users to create and fill orders in any ERC-20 token. If your token has liquidity and is available on [CoinGecko](https://www.coingecko.com/) it will be supported out of the box.

If your token does not have liquidity and is not available on CoinGecko, it will require special handling in our indexer outlined below.

Please note that if your ERC-20 does not have liquidity on CoinGecko, the conversion from your token to USD might not be accurate. This conversion happens because we have to assign a USD to ERC-20 rate since this isn't available from CoinGecko.

# How to add custom ERC-20 support to Reservoir

To add support for your custom ERC-20 Token follow these steps below:

1. Add your custom token details [here](https://github.com/reservoirprotocol/indexer/blob/9bea88db12f3a012aa6558942635b4ee39ff83e2/src/config/network.ts#L126)

```c Example
[
            "0xceb726e6383468dd8ac0b513c8330cc9fb4024a8", // MUST BE LOWERCASE
            {
              contract: "0xceb726e6383468dd8ac0b513c8330cc9fb4024a8",
              name: "Worms",
              symbol: "WORMS",
              decimals: 18,
              metadata: { // OPTIONAL
                image:
                  "{ICON_URL}", 
              },
            },
          ]
```

2. Submit a PR and add the reservoirprotocol/backend team as a reviewer.
3. Once our team has reviewed and merged the PR, the token will be supported.