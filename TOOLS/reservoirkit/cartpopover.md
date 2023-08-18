---
title: "CartPopover"
slug: "cartpopover"
excerpt: "Add cart UX to your app with the CartPopover using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:33:20.631Z"
updatedAt: "2023-08-03T20:29:27.742Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# Cart Provider

ReservoirKit provides a cart for you to quickly get a functional, persistent cart into your react application. The first step to configuring your cart is to add the `CartProvider` to your application. Ensure that it's wrapped by the ReservoirKitProvider as well as Wagmi

```typescript
import { CartProvider } from '@reservoir0x/reservoir-kit-ui'

<WagmiConfig ...>
 ...
  <ReservoirKitProvider ...>
 ...
    <CartProvider>
      {YOUR APP COMPONENTS}
    </CartProvider>
  </ReservoirKitProvider>
</WagmiConfig>
```

Let's dive into the parameters. You'll need to provide an element to trigger the modal, this can be any valid html element. Next you'll want to provide a `collectionId` and a `tokenId`. These can be set to undefined until the data is ready. 

There are also some additional _optional_ props:

| Prop             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **feesOnTopBps** | A list of fee strings representing a recipient and the fee in <<glossary:bps>> delimited by a colon: ["0xabc:100"] used when creating an order (listing or bid). This will override the global configuration. The fee currency will follow the default rules for the [execute buy endpoint](/reference/postexecutebuyv6) feesOnTop parameter.                                                                                                                                                                            |
| **feesOnTopUsd** | Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee separated by a colon: `['0xabc:1000000']`. The fee is a flat fee in the atomic unit of usd (6 decimals). It will then be converted to the purchase currency to match the same value in USD. So for example if you have 1000000 configured (1 usd) and the total price is in ETH the fee applied will be ~0.00054 ETH (or whatever is equivalent to 1 usd in realtime). |
| **persist**      | Use this to disable the cart's persistence. This is true by default.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

# CartPopover

After setting up the CartProvider, you can now use the CartPopover to display your cart in your app. The cart automatically validates the cart whenever it's opened and allows the user to check out or edit their cart.

```typescript
import { CartPopover } from '@reservoir0x/reservoir-kit-ui'

<CartPopover 
  trigger={<button>Open the Cart</button>}
  side={'bottom'}
  openState={openState}
  tokenUrl={'https://reservoir.market/${contract}/${tokenId}'}
  onConnectWallet={() => {}} />
```

Let's go over the options you can provide to the CartPopover:

| Prop                | Description                                                                                                                                                                                                                                                                                                                 | Required |
| :------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**         | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                                                                   | Y        |
| **side**            | The preferred side of the anchor to render against when open. This maps to the side property in [radix](https://www.radix-ui.com/docs/primitives/components/popover#content).                                                                                                                                               | N        |
| **openState**       | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                                                                      | N        |
| **tokenUrl**        | You can configure the token url schema that the CartPopover uses to route users to the token page when clicking on an item in the cart. By default the CartPopover will detect the token url schema based on the reservoir [custom source metatags](https://docs.reservoir.tools/docs/marketplace-source-attribution-copy). | N        |
| **onConnectWallet** | This is a required parameter to handle scenarios when the user needs to connect their wallet. Either prompt a custom modal for the user to connect their wallet or prompt metamask/the wallet of your choice.                                                                                                               | N        |

# Conditional Rendering

ReservoirKit's CartPopover doesn't take care of conditionally showing the button/modal based on if the user has a connected wallet, we leave that logic up to the developer. You can decide to show the button all the time and allow users to add/remove items from the cart but you need to handle validation when they connect their wallet.

# Custom CartPopover

The CartPopover also comes with a custom renderer which can be used to just get the data layer that the CartPopover uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { CartPopover, CheckoutStatus } from '@reservoir0x/reservoir-kit-ui'

<CartPopover open={open}>
    {({
      loading,
      items,
      flaggedItems,
      unavailableItems,
      priceChangeItems,
      totalPrice,
      feeOnTop,
      usdPrice,
      hasEnoughCurrency,
      balance,
      currency,
      transaction,
      blockExplorerBaseUrl,
	    cartChain,
      remove,
      clear,
      checkout,
    }) => {
  { Your Custom React Elements }
  })}
</CartPopover.Custom>
```

The custom CartPopover takes one parameter, the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom CartPopover then passes some key data into the children which we parse above and use in our custom UI. Out of the box, the cart will use the listing's currency in the cart; once multiple listings have been added with multiple different currencies, the total cart currency will default to the chain's native currency. It's also important to note the `CheckoutStatus` here which is used to manage the internal state of the `CartPopover`'s logic. You can decide to use all or some of the data passed into your custom implementation.

In addition to the components mention above there is also a [hook](https://docs.reservoir.tools/reference/reservoirkit-hooks#usecart) for interacting with the cart context. You can use it to add items, remove items, validate the cart etc.