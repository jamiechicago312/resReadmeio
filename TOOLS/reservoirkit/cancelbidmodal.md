---
title: "CancelBidModal"
slug: "cancelbidmodal"
excerpt: "Leverage the CancelBidModal to cancel bids using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:37:45.127Z"
updatedAt: "2023-06-14T05:44:33.809Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# CancelBidModal

ReservoirKit provides a simple to configure modal for canceling a valid bid in your react app. Below is an example of a simple CancelBidModal setup.

```typescript
import { CancelBidModal } from '@reservoir0x/reservoir-kit-ui'

<CancelBidModal
  trigger={
    <button>
      Cancel Bid
    </button>
  }
  bidId="0x26546d77a4511a2c0c2ab24970cdad886fad35f9f875bbb524f1d92775115153"
  onCancelComplete={(data: any) => {
    console.log('Bid Canceled', data)
  }}
  onCancelError={(error: any, data: any) => {
    console.log('Bid Cancel Error', error, data)
  }}
  onClose={(data, currentStep) => {
    console.log('CancelBidModal Closed')
  }}
/>
```

Let's dive into the parameters:

| Prop                   | Description                                                                                                                                                                                                                                                                                                                | Required |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**            | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                                                                  | Y        |
| **bidId**              | An order id representing the bid. It can be set to undefined until the data is ready                                                                                                                                                                                                                                       | Y        |
| **normalizeRoyalties** | Use this to ensure that royalties are added to the bid data displayed. If royalties are missing from the order then the correct royalties are added on top. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided. | N        |
| **openState**          | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                                                                     | N        |
| **copyOverrides**      | An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/cancelBid/CancelBidModal.tsx#L15) for which tokens map to what copy.                                                    | N        |
| **onCancelComplete**   | Triggered when cancelling was completed successfully, returns some useful data about the bid and the cancel step.                                                                                                                                                                                                          | N        |
| **onCancelError**      | Triggered when the cancel resulted in an error, returns the error and the bid data.                                                                                                                                                                                                                                        | N        |
| **onClose**            | Triggered when the modal was closed. Returns some useful data about the bid as well as the step data and the current step.                                                                                                                                                                                                 | N        |

## Conditional Rendering

ReservoirKit's CancelBidModal doesn't take care of conditionally showing the button/modal based on if the item is cancelable by the user, we leave that logic up to the developer. Below are the requirements for canceling a bid and how to go about getting that data:

- The user needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.
- The user must be the maker of the bid, you can check this by comparing maker in the bid object to the connected wallet address. You can get a full list of a wallet's bids by using the [useBids](https://docs.reservoir.tools/reference/reservoirkit-hooks#usebids) hook or the underlying api.

# Custom CancelBidModal

The CancelBidModal also comes with a custom renderer which can be used to just get the data layer that the CancelBidModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { CancelBidModal, CancelBidStep } from '@reservoir0x/reservoir-kit-ui'

<CancelBidModal.Custom
    open={open}
    bidId="0x26546d77a4511a2c0c2ab24970cdad886fad35f9f875bbb524f1d92775115153"
  >
    {({
      loading,
      bid,
      tokenId,
      cancelStep,
      transactionError,
      stepData,
      totalUsd,
      blockExplorerBaseUrl,
      cancelOrder,
    }) => {
  { Your Custom React Elements }
})}
</CancelBidModal.Custom>
```

The custom CancelBidModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom CancelBidModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `CancelBidStep` here which is used to manage the internal state of the CancelBidModal's logic. You can decide to use all or some of the data passed into your custom implementation.

> 👍 Nice job!
> 
> Now that we've added a cancel bid modal to your dApp, let's [customize the theme to match your brand](https://docs.reservoir.tools/reference/theming).