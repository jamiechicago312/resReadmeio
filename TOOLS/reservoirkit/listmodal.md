---
title: "ListModal"
slug: "listmodal"
excerpt: "Leverage the ListModal to create listings using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:03:29.434Z"
updatedAt: "2023-07-03T15:28:06.176Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# List Modal

ReservoirKit provides a simple to configure modal for facilitating token listing in your react app. Below is an example of a simple ListModal setup.

```typescript
import { useState } from 'react'

const openState = useState(true)

<ListModal
  trigger={
    <button>
      List Item
    </button>
  }
  collectionId="0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"
  tokenId="1"
  currencies={[
    {
      contract: '0x0000000000000000000000000000000000000000',
      symbol: 'ETH',
    },
    {
      contract: '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
      symbol: 'USDC',
      decimals: 6
    },
  ]}
  openState={openState}
  nativeOnly={false}
  oracleEnabled={false}
  onGoToToken={() => console.log('Awesome!')}
  onListingComplete={(data) => {
    console.log('Listing Complete', data)
  }}
  onListingError={(error, data) => {
    console.log('Transaction Error', error, data)
  }}
  onClose={(data, stepData, currentStep) => {
    console.log('ListModal Closed')
  }}
/>
```

Let's dive into the parameters:

| Prop                       | Description                                                                                                                                                                                                                                                                                          | Required |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**                | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                                            | Y        |
| **collectionId**           | The collection id of the token you wish to list. Can be undefined until the data is ready.                                                                                                                                                                                                           | Y        |
| **tokenId**                | The token id of the token you wish to list. Can be undefined until the data is ready.                                                                                                                                                                                                                | Y        |
| **currencies**             | If there are multiple currencies supplied the user will be able to select from them, otherwise it will be selected by default. If no currencies are supplied the modal will default to ETH.                                                                                                          | N        |
| **nativeOnly**             | A boolean parameter that removes all non native (opensea, x2y2, looks rare etc) marketplace options.                                                                                                                                                                                                 | N        |
| **openState**              | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                                               | N        |
| **normalizeRoyalties**     | Use this to ensure that royalties are added to the stats and market pricing information. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.                                              | N        |
| **oracleEnabled**          | Use this to create oracle powered listings which can be cancelled without paying a gas cost.                                                                                                                                                                                                         | N        |
| **enableOnChainRoyalties** | Use this to enable on chain royalties. Instead of the ListModal displaying royalties from Reservoir's api it pulls the data from the manifold royalty registry contract. It will also override the execute/list royalties and apply the ones from the registry. This only applies to seaport orders. | N        |
| **copyOverrides**          | An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/list/ListModal.tsx#L55) for which tokens map to what copy.                                        | N        |
| **feesBps**                | A list of fee strings representing a recipient and the fee in <<glossary:bps>> delimited by a colon: ["0xabc:100"].                                                                                                                                                                                  | N        |
| **onListingComplete**      | Triggered when the listing was completed successfully, returns some useful data about the listing.                                                                                                                                                                                                   | N        |
| **onListingError**         | Triggered when the listing resulted in an error, returns the error and the listing data.                                                                                                                                                                                                             | N        |
| **onClose**                | Triggered when the modal was closed. Returns some useful data about the listing as well as the step data and the current step.                                                                                                                                                                       | N        |

# Conditional Rendering

ReservoirKit doesn't take care of conditionally showing the button based on if the item is listable, we leave that logic up to the developer. You'll need to conditionally render your button based on multiple data points. Below are the requirements for listing and how to go about getting that data:

- The user needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.
- The user **must be the owner** of the token, you can check this by comparing the current address and the address of the owner.

# Custom ListModal

The ListModal also comes with a custom renderer which can be used to just get the data layer that the ListModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { ListModal, ListStep } from '@reservoir0x/reservoir-kit-ui'

<ListModal.Custom
  collectionId="0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"
  tokenId="1"
>
    {({
        token,
        collection,
        ethUsdPrice,
        listStep,
        expirationOption,
        expirationOptions,
        marketplaces,
        unapprovedMarketplaces,
        localMarketplace,
        syncProfit,
        listingData,
        transactionError,
        stepData,
        setListStep,
        listToken,
        setMarketPrice,
        toggleMarketplace,
        setSyncProfit,
        setExpirationOption,
      }) => {
        { Your Custom React Elements }
    })}
</ListModal.Custom>
```

The custom ListModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom ListModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `ListStep` here which is used to manage the internal state of the ListModal's logic. You can decide to use all or some of the data passed into your custom implementation.

> 👍 Great!
> 
> Now that we've added a ListModal to your dApp, let's [customize the theme to match your brand](/docs/reservoir-kit-theming-and-customization).