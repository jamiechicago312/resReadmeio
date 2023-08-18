---
title: "Reservoir SDK (Typescript)"
slug: "reservoir-sdk-jstsnode"
excerpt: "ReservoirSDK wraps the trading APIs into convenient methods for use in typescript"
hidden: false
createdAt: "2023-04-06T16:13:31.000Z"
updatedAt: "2023-08-15T19:56:58.634Z"
---
### Reservoir SDK

The Reservoir SDK is the underlying package that [ReservoirKit UI](https://docs.reservoir.tools/reference/reservoirkit) uses behind the scenes to execute core functionality (listing, bidding, buying and selling). The Reservoir SDK can be used if you are using another **JavaScript framework**, executing orders via a **Nodejs server** or building a custom experience.

If you're using [ReservoirKit UI](https://docs.reservoir.tools/reference/reservoirkit) then you're already using the SDK, and you have access to the `useReservoirClient` hook to retrieve the SDK in a react context and use it. If you aren't using the UI package then you'll need to follow these steps to get the SDK up and running.

### Installing Reservoir SDK:

Make sure that you've got version 18+ of node installed.

```shell
yarn add @reservoir0x/reservoir-sdk
```

The Reservoir SDK also requires viem to be installed, make sure that's added to your package.json if it isn't already.

```shell
yarn add viem
```

### ethers support

If your application uses ethers and you're not ready to upgrade to viem yet we offer an [ethers adapter](https://github.com/reservoirprotocol/reservoir-kit/tree/main/packages/ethers-wallet-adapter) package to help bridge the gap. Learn more about adapters [here](https://docs.reservoir.tools/reference/adapters).

### Configuring the Reservoir SDK

To configure the SDK we first need to create a global instance of it:

```typescript
import { createClient } from "@reservoir0x/reservoir-sdk"

createClient({
  chains: [{
    id: 1,
    baseApiUrl: 'https://api.reservoir.tools',
    active: true,
    apiKey: "YOUR_KEY"
  }],
  source: "YOUR.SOURCE
});
```

We start by importing the `createClient` function and then call that function to create a global client, passing in the required parameters.  

| Option                 | Description                                                                                                                                                                                                                                                          |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **chains**             | An array of chain objects representing reservoir chains that your application supports. Below we'll breakdown the properties of the chain object.                                                                                                                    |
| **source**             | The `source` parameter can be any valid domain (e.g. `reservoir.market`). It's used to attribute orders to your particular marketplace and to scrape [custom metadata](https://docs.reservoir.tools/docs/marketplace-source-attribution-copy) from your marketplace. |
| **marketplaceFees**    | A list of fee strings representing a recipient and the fee in <<glossary:bps>> delimited by a colon: ["0xabc:100"] used when creating an order (listing or bid)                                                                                                      |
| **automatedRoyalties** | If true, royalties will be automatically included, defaults to true. Only relevant for creating orders (listing and bidding)                                                                                                                                         |
| **normalizeRoyalties** | Global setting to add royalties on top of orders that do not include royalties.                                                                                                                                                                                      |

Let's dive into the properties that make up a reservoir chain:

| Property   | Description                                                                                                                                                                                  |
| :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id         | The id of the chain (e.g. 1 for mainnet)                                                                                                                                                     |
| baseApiUrl | Can be one of our [hosted api](https://docs.reservoir.tools/reference/supported-chains) endpoints or any instance of the Reservoir indexer.                                                  |
| active     | Only one chain can be the default at a time. This is used in the SDK when determining which default chain to select.                                                                         |
| apiKey     | The apiKey is not required but should be passed in as it allows for higher rate limits. Read more about the [API Keys & Rate Limits](ref:getting-started) and how to instantly generate one. |

Once the client has been created there are 5 core actions available to you:

[buyToken](/docs/buytoken)  
[listToken](/docs/listtoken)  
[placeBid](/docs/placebid)  
[acceptOffer](/docs/acceptoffer)  
[cancelOrder](/docs/cancelorder)

Please note that the SDK can only have a single chain at a time. You can put a new instance of the `createClient` before a core action if you need to switch chains.

**Events**

The Reservoir SDK also comes with an event system to detect results from the actions above. This can be useful to display a toast message to your users, refresh some data within your application, or track the data. You can find the [supported events](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/utils/events.ts#L4) here. Here's an example of how you would listen to events:

```
import { getClient } from "@reservoir0x/reservoir-sdk";

getClient()?.addEventListener((event, chainId) => {
  switch (event.name) {
    case 'purchase_error': {
      //Handle the error
      console.log(event.data);
      break;
    }
    case 'purchase_complete': {
      //Handle the success
      console.log(event.data);
      break;
    }
})
```

> 👍 Nice!
> 
> Now that the Reservoir SDK is up and running lets [add sweeping](/docs/sweeping) to our javascript application.