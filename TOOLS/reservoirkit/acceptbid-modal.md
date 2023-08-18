---
title: "AcceptBidModal"
slug: "acceptbid-modal"
excerpt: "Leverage the AcceptBidModal to accept bids using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:32:12.634Z"
updatedAt: "2023-06-26T22:08:25.554Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# AcceptBidModal

ReservoirKit provides a simple to configure modal for facilitating accepting bids in your react app. Below is an example of a simple AcceptBidModal setup.

```typescript
import { AcceptBidModal } from '@reservoir0x/reservoir-kit-ui'

<AcceptBidModal
  trigger={
    <button>
      Accept Bid
    </button>
  }
  tokens={[{
    tokenId: "1469875"
    collectionId: "0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"
    bidIds: ["0x4518b3a90ae5873ee3031904b74366b0316329c2f5ef81ec30480c562a30be9c"] //Optional
  }]}
  onBidAccepted={(data) => {
    console.log('Bid Accepted', data)
  }}
  onBidAcceptError={(error, data) => {
    console.log('Bid Acceptance Error', error, data)
  }}
  onClose={(data, stepData, currentStep) => {
    console.log('AcceptBidModal Closed')
  }}
/>
```

Let's dive into the parameters:

| Prop                   | Description                                                                                                                                                                                                                                                                                                   | Required |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------- |
| **trigger**            | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                                                     | Y        |
| **tokens**             | An array of token objects which consist of a `collectionId` and a `tokenId`. You can also optionally define a bidId if you know the bidId ahead of time. Can be set to `undefined` until the data is ready.                                                                                                   | Y        |
| **openState**          | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                                                        | N        |
| **normalizeRoyalties** | Use this to ensure that royalties are added to the order. If royalties are missing from the order then the correct royalties are added on top. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided. | N        |
| **copyOverrides**      | An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/acceptBid/AcceptBidModal.tsx#L49) for which tokens map to what copy.                                       | N        |
| **onBidAccepted**      | Triggered when the bid was accepted successfully, returns some useful data about the bid.                                                                                                                                                                                                                     | N        |
| **onBidAcceptError**   | Triggered when accepting the bid resulted in an error, returns the error and the bid data.                                                                                                                                                                                                                    | N        |
| **onClose**            | Triggered when the modal was closed. Returns some useful data about the bid as well as the step data and the current step.                                                                                                                                                                                    | N        |

# Conditional Rendering

ReservoirKit's AcceptBidModal doesn't take care of conditionally showing the button/modal based on if the item has a bid, we leave that logic up to the developer. Below are the requirements for accepting a bid and how to go about getting that data:

- The user needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.
- The token must have a **valid offer**, you can check if the `token.market.topBid.price.amount.decimal` is available for that token using the [Tokens](ref:gettokensv5) api endpoint. If not valid offer is detected the modal will handle this accordingly by displaying a message to the user that the offer was not found.

# Custom AcceptBidModal

The AcceptBidModal also comes with a custom renderer which can be used to just get the data layer that the AcceptBidModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { AcceptBidModal, AcceptBidStep } from '@reservoir0x/reservoir-kit-ui'

<AcceptBidModal.Custom
  open={open}
  tokens={tokens}>
  {({
        loading,
        acceptBidStep,
        transactionError,
        txHash,
        usdPrices,
        prices,
        tokensData,
        address,
        blockExplorerBaseUrl,
        stepData,
        acceptBid,
        setAcceptBidStep
  }) => {
    { Your Custom React Elements }
  })}
</AcceptBidModal.Custom>
```

The custom AcceptBidModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom AcceptBidModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `AcceptBidStep` here which is used to manage the internal state of the AcceptBidModal logic. You can decide to use all or some of the data passed into your custom implementation.

> 👍 Nice job!
> 
> Now that we've added an accept bid modal to your dApp, let's [customize the theme to match your brand](/docs/reservoir-kit-theming-and-customization).