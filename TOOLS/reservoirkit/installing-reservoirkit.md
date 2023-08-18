---
title: "Installing ReservoirKit"
slug: "installing-reservoirkit"
hidden: false
createdAt: "2023-04-18T20:30:38.456Z"
updatedAt: "2023-08-01T19:53:05.315Z"
---
ReservoirKit is a React library that makes it easy to add marketplace functionality and UI into your project. If you are not using React and need a custom solution you can use the [Reservoir SDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode).

# Installing ReservoirKit

```shell
yarn add @reservoir0x/reservoir-kit-ui
```

Also make sure to install the peer dependencies required by ReservoirKit if your application doesn't already include them:

```shell
yarn add wagmi viem react react-dom
```

ReservoirKit UI relies on [wagmi@v1.0.0](mailto:wagmi@v1.0.0), [react@18.0](mailto:react@18.0) and viem. 

If your application uses [radix-ui](https://www.radix-ui.com/docs/primitives) you'll need to ensure that the radix ui components version match what `reservoir-kit-ui` is using. Deviating from that version may cause issues.

### ethers support

If your application uses ethers and you're not ready to upgrade to viem yet we the wagmi team has created an [ethers adapter](https://wagmi.sh/react/ethers-adapters) to help bridge the gap. _Note: you'll still need to install viem._

# Configuring ReservoirKit UI

```typescript
import {
  ReservoirKitProvider,
  darkTheme,
} from '@reservoir0x/reservoir-kit-ui'
import { WagmiConfig } from 'wagmi'

const wagmiClient = ...

const theme = darkTheme({
  headlineFont: "Sans Serif",
  font: "Serif",
  primaryColor: "#323aa8",
  primaryHoverColor: "#252ea5",
})

<ReservoirKitProvider
  options={{
    chains: [{
      id: 1,
      baseApiUrl: "https://api.reservoir.tools",
      active: true,
      apiKey: "YOUR_KEY"
    }],
    source: "YOUR_SOURCE"
    ...
  }}
  theme={theme}
>
  <WagmiConfig client={wagmiClient}>

   { Your App }

  </WagmiConfig>
</ReservoirKitProvider>
```

The sample code above is all you need to get started with ReservoirKit. Let's break it down step by step. Start by importing the `ReservoirKitProvider` which is needed for configuring ReservoirKit. Also import a theme of your choice, we provide a lightTheme and a darkTheme. Next we import the `WagmiConfig`, Wagmi is a peer dependency of ReservoirKit.

Now that we have all the imports ready we can continue by supplying some options. You'll need to supply an array with at least one Reservoir chain. Read more below about the Reservoir chain object.

Now we create a theme. As mentioned previously we have a few preloaded themes with the ability to override some variables, like colors and fonts. Learn more about theming options [here](https://docs.reservoir.tools/reference/theming).

Next we wrap our app with the `ReservoirKitProvider` and pass it some options. Below is a list of ReservoirKit UI options:

[block:parameters]
{
  "data": {
    "h-0": "Option",
    "h-1": "Description",
    "0-0": "**chains**",
    "0-1": "An array of at least one chain. A Reservoir chain consists of an id (e.g. 1 for mainnet), a `baseApiUrl` and a boolean indicating if it's the active chain. The`baseApiUrl` which can be any of our [hosted reservoir indexer endpoints](https://docs.reservoir.tools/reference/overview) or you can host one yourself. Optionally a chain can have an `apiKey`, while optional it will raise the rate limit for your application. We recommend getting a [free instant key](https://docs.reservoir.tools/reference/getting-started) before deploying to production. If you'd like to read more about the chain configuration in depth, [click here](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode#configuring-the-reservoir-sdk).**This is the only required option**",
    "1-0": "**disablePoweredByReservoir**",
    "1-1": "Used to disable the powered by Reservoir footers.",
    "2-0": "**normalizeRoyalties**",
    "2-1": "Global setting to add royalties on top of orders that do not include royalties.",
    "3-0": "**coinGecko**",
    "3-1": "An optional object representing additional configuration for coingecko.  \n**proxy**: You can configure a  proxy url, in case you have your api key behind a proxy url.  \n**apiKey**:You can also just directly configure an API key, we don't recommend this as this will leak your key but it is the easiest way to configure a coingecko api key.  \n**coinIds**: An object mapping symbols to coingecko coin ids. Refer to the [coingecko api](https://api.coingecko.com/api/v3/coins/list) to manually map a coingecko coin id to a symbol in the case of a conflict. If there is a conflict ReservoirKit will not display a usd price unless a coingecko id is manually set.",
    "4-0": "_ReservoirKit Client options_",
    "4-1": "[More options ](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode#configuring-the-reservoir-sdk)can be configured for the underlying client instance."
  },
  "cols": 2,
  "rows": 5,
  "align": [
    "left",
    "left"
  ]
}
[/block]

You can also pass in `swrOptions` which allow you to further [configure swr](https://swr.vercel.app/docs/global-configuration) at a global level.

We also pass in the theme we previously set up. Now we need to make sure we wrap our application in the `WagmiConfig`. Follow the instructions in their docs to set up the `WagmiClient` and then pass it into the `WagmiConfig`. Finally nest your application code within the `ReservoirKitProvider` and the `WagmiConfig`.

Everything is now correctly configured and ready to go. One last thing you may want to set up for your domain is [custom source metadata](https://docs.reservoir.tools/docs/marketplace-source-attribution-copy)  which ReservoirKit as well as the [Indexer](doc:indexer) use to dynamically keep a catalog of all marketplace source metadata.

If you're having any trouble consult the [troubleshooting guide](https://docs.reservoir.tools/reference/troubleshooting) before reaching out to support.

> 👍 Great job!
> 
> Now that we've installed and configured ReservoirKit lets [add a buy modal](ref:buymodal-1).