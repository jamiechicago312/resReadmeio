---
title: "BidModal"
slug: "bidmodal"
excerpt: "Leverage the BidModal to create bids using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:31:31.838Z"
updatedAt: "2023-07-07T16:53:59.660Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# BidModal

ReservoirKit provides a simple to configure modal for facilitating token bidding in your react app. Below is an example of a simple BidModal setup.

```typescript
import { BidModal } from '@reservoir0x/reservoir-kit-ui'
import { useState } from 'react'

const openState = useState(true)

<BidModal
  trigger={
    <button>
      Place Bid
    </button>
  }
  collectionId="0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"
  tokenId="1469875"
  openState={openState}
  attribute={{
   key: "Fur",
   value: "Gold"
  }}
  currencies={[
    contract: "0x0000000000000000000000000000000000000000",
    symbol: "ETH",
    decimals: 18, //Optional
    coinGeckoId: "ethereum" //Optional
  ]}
  onBidComplete={(data) => {
    console.log('Bid Complete', data)
  }}
  onBidError={(error, data) => {
    console.log('Bid Transaction Error', error, data)
  }}
  onClose={(data, stepData, currentStep) => {
    console.log('BidModal Closed')
  }}
/>
```

Let's dive into the parameters:

| Prop                   | Description                                                                                                                                                                                                                                                 | Required |
| :--------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**            | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                   | Y        |
| **collectionId**       | The collection id of the token you wish to bid on. Can be undefined until the data is ready.                                                                                                                                                                | Y        |
| **tokenId**            | The token id of the token you wish to bid on. Can be undefined until the data is ready. This is not required when making a collection wide bid.                                                                                                             | N        |
| **attribute**          | An object with a key and a value representing an attribute. This is used to prefill the modal with an attribute in the case of a collection offer.                                                                                                          | N        |
| **openState**          | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                      | N        |
| **normalizeRoyalties** | Use this to ensure that royalties are added to the stats and market pricing information. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.     | N        |
| **oracleEnabled**      | Use this to create oracle powered bids which can be cancelled without paying a gas cost.                                                                                                                                                                    | N        |
| **currencies**         | Use this to supply an array of currencies to select when making the bid. You can use any ERC-20 that Reservoir supports indexing wallet balances. This is chain dependent.                                                                                  | N        |
| **copyOverrides**      | An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/bid/BidModal.tsx#L61) for which tokens map to what copy. | N        |
| **feesBps**            | A list of fee strings representing a recipient and the fee in <<glossary:bps>> delimited by a colon: ["0xabc:100"]                                                                                                                                          | N        |
| **onBidComplete**      | Triggered when the bid was placed successfully, returns some useful data about the bid.                                                                                                                                                                     | N        |
| **onBidError**         | Triggered when the bid resulted in an error, returns the error and the bid data.                                                                                                                                                                            | N        |
| **onClose**            | Triggered when the modal was closed. Returns some useful data about the bid as well as the step data and the current step.                                                                                                                                  | N        |

# Conditional Rendering

ReservoirKit's BidModal doesn't take care of conditionally showing the button/modal, we leave that logic up to the developer. The user also needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.

# Custom BidModal

The BidModal also comes with a custom renderer which can be used to just get the data layer that the BidModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { BidModal, BidStep } from '@reservoir0x/reservoir-kit-ui'

<BidModal.Custom
  open={open}
  tokenId={tokenId}
  collectionId={collectionId}
  attribute={attribute}
  normalizeRoyalties={normalizeRoyalties}
  oracleEnabled={oracleEnabled}
  currencies={currencies}>
  {({
    token,
    collection,
    attributes,
    bidStep,
    expirationOption,
    expirationOptions,
    wrappedBalance,
    wrappedContractName,
    wrappedContractAddress,
    bidAmountPerUnit,
    totalBidAmount,
    totalBidAmountUsd
    quantity,
    setQuantity,
    hasEnoughNativeCurrency,
    hasEnoughWrappedCurrency,
    amountToWrap,
    balance,
    convertLink,
    canAutomaticallyConvert,
    transactionError,
    stepData,
    bidData,
    isBanned,
    currencies,
    currency,
    feeBps,
    setCurrency,
    setBidAmountPerUnit,
    setExpirationOption,
    setBidStep,
    setTrait,
    trait,
    placeBid,
  }) => {
    { Your Custom React Elements }
  })}
</BidModal.Custom>
```

The custom BidModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom BidModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `BidStep` here which is used to manage the internal state of the BidModal's logic. You can decide to use all or some of the data passed into your custom implementation. `placeBid` is the function used to trigger the main action of placing a bid, it also accepts an object of options of which you can pass the quantity.

> 👍 Nice job!
> 
> Now that we've added a bid modal to your dApp, let's [customize the theme to match your brand](/docs/reservoir-kit-theming-and-customization).