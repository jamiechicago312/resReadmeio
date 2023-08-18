---
title: "CollectModal (Mint + Sweep)"
slug: "collectmodal-mint-sweep"
excerpt: "Leverage the CollectModal to add minting and sweeping to your app with ReservoirKit."
hidden: false
createdAt: "2023-07-05T17:45:06.804Z"
updatedAt: "2023-08-04T20:42:02.258Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# CollectModal

ReservoirKit provides a simple to configure modal for adding both minting and sweeping to your react app. Below is an example of a simple CollectModal setup.

```typescript
import { CollectModal } from '@reservoir0x/reservoir-kit-ui'

<CollectModal
  trigger={
      <button>
      	Collect
      </button>
    }
  collectionId="0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"
  mode="preferMint"
  onCollectComplete={(data) => {
    console.log('Collect Complete', data)
  }}
  onCollectError={(error, data) => {
    console.log('Collect Error', error, data)
  }}
  onClose={(data, currentStep) => {
    console.log('CollectModal Closed')
  }}
/>
```

Let's dive into the parameters:

[block:parameters]
{
  "data": {
    "h-0": "**Prop**",
    "h-1": "**Description**",
    "h-2": "Required",
    "0-0": "**trigger**",
    "0-1": "A react node that will be presented to the user, usually a button or something clickable.",
    "0-2": "Y",
    "1-0": "**collectionId**",
    "1-1": "The collection id of the collection you wish to mint/sweep. Can be undefined until the data is ready.",
    "1-2": "Y",
    "2-0": "**tokenId**",
    "2-1": "The token id of the token you wish to mint/sweep. Can be undefined until the data is ready.  \n**Note**: You should only pass in a tokenId for ERC1155 collections where you want to mint/sweep a specific token.",
    "2-2": "N",
    "3-0": "**mode**",
    "3-1": "There are three possible modes for the CollectModal:  \n  \n`preferMint`: If minting is available, will use the mint mode. Otherwise, will sweep the cheapest tokens from secondary  \n`mint`: Will only allow minting  \n`trade`: Will only allow sweeping from secondary  \n  \nThe default behavior is `preferMint`",
    "3-2": "N",
    "4-0": "**openState**",
    "4-1": "This is a state tuple from react's [useState](https://legacy.reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.",
    "4-2": "N",
    "5-0": "**copyOverrides**",
    "5-1": "An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/collect/CollectModal.tsx#L22) for which tokens map to what copy.",
    "5-2": "N",
    "6-0": "**feesOnTopBps**",
    "6-1": "Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee separated by a colon: `['0xabc:250']`. The fee is in bps. The fee currency will follow the default rules for the execute buy endpoint `feesOnTop` parameter. This takes precedence over the `feesOnTopFixed`.",
    "6-2": "N",
    "7-0": "**feesOnTopUsd**",
    "7-1": "Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee separated by a colon: `['0xabc:1000000']`. The fee is a flat fee in the atomic unit of usd (6 decimals). It will then be converted to the purchase currency to match the same value in USD. So for example if you have 1000000 configured (1 usd) and the total price is in ETH the fee applied will be ~0.00054 ETH (or whatever is equivalent to 1 usd in realtime).",
    "7-2": "N",
    "8-0": "**normalizeRoyalties**",
    "8-1": "Use this to ensure that royalties are added to the order. If royalties are missing from the order then the correct royalties are added on top. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.",
    "8-2": "",
    "9-0": "**onCollectComplete**",
    "9-1": "Triggered when the mint/sweep was completed successfully, returns some useful data about the transaction.",
    "9-2": "N",
    "10-0": "**onCollectError**",
    "10-1": "Triggered when the mint resulted in an error, returns the error and the mint data.",
    "10-2": "N",
    "11-0": "**onClose**",
    "11-1": "Triggered when the modal was closed. Returns some useful data about the mint as well as and the current step.",
    "11-2": "N"
  },
  "cols": 3,
  "rows": 12,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

# Conditional Rendering

ReservoirKit's CollectModal doesn't take care of conditionally showing the button/modal, we leave that logic up to the developer. The user also needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.

## Custom CollectModal

The CollectModal also comes with a custom renderer which can be used to just get the data layer that the CollectModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { CollectModal, CollectStep } from '@reservoir0x/reservoir-kit-ui'


<CollectModal.Custom
  open={open}
  collectionId={collectionId}>
  {({
     contentMode,
     collection,
     token,
     loading,
     address,
     selectedTokens,
     setSelectedTokens,
     itemAmount,
     setItemAmount,
     maxItemAmount,
     setMaxItemAmount,
     currency,
     chainCurrency,
     isChainCurrency,
     total,
     totalUsd,
     feeOnTop,
     feeUsd,
     usdPrice,
     currentChain,
     mintPrice,
     orders,
     balance,
     contract,
     hasEnoughCurrency,
     addFundsLink,
     blockExplorerBaseUrl,
     transactionError,
     stepData,
     setStepData,
     collectStep,
     setCollectStep,
     collectTokens,
  }) => {
    { Your Custom React Elements }
  })}
</CollectModal.Custom>
```

The custom CollectModal takes a few parameters like before with one additional one being the `open` parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom CollectModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `CollectStep` here which is used to manage the internal state of the CollectModal's logic. You can decide to use all or some of the data passed into your custom implementation.