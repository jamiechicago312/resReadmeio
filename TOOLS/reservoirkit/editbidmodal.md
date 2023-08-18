---
title: "EditBidModal"
slug: "editbidmodal"
excerpt: "Leverage the EditBidModal to edit bids using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:39:30.737Z"
updatedAt: "2023-06-14T05:45:32.821Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit). 

# EditBidModal

ReservoirKit provides a simple to configure modal for editing oracle bids in your react app. Below is an example of a simple EditBidModal setup.

**It is important to note that you can only edit oracle powered bids**

```typescript
import { EditBidModal } from '@reservoir0x/reservoir-kit-ui'

<EditBidModal
	trigger={
  	<button>
      Edit Bid
    </button>
  }
  bidId="0x99e3ad649dbd9ae2f1a3c9f1331d69021a61ff9a15e1a50550b548c2d502ff05"
	collectionId="0x21227ea09f9e7ec425f59cea621debb52de8bee9"  
  tokenId="1"
  onEditBidComplete={(data: any) => {
		console.log('Bid updated', data)
  }}
  onEditBidError={(error: any, data: any) => {
  	console.log('EditBid Transaction Error', error, data)
  }}
  onClose={() => {
  	console.log('EditBidModal Closed')
  }}
/>
```

Let's dive into the parameters:

| Prop                   | Description                                                                                                                                                                                                                                                       | Required |
| :--------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**            | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                         | Y        |
| **bidId**              | An order id representing the bid. It can be set to undefined until the data is ready                                                                                                                                                                              | Y        |
| **collectionId**       | The collection id of the token you wish to edit a bid on. Can be undefined until the data is ready.                                                                                                                                                               | Y        |
| **tokenId**            | The token id of the token you wish to edit a bid on. Can be undefined until the data is ready.                                                                                                                                                                    | Y        |
| **normalizeRoyalties** | Use this to ensure that royalties are added to the stats and market pricing information. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.           | N        |
| **openState**          | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                            | N        |
| **copyOverrides**      | An object containing copy overrides for titles and ctas contained in the modal. Refer to the ModalCopy [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/editBid/EditBidModal.tsx#L37) for which tokens map to what copy. | N        |
| **onEditBidComplete**  | Triggered when editing the bid was completed successfully, returns some useful data about the bid and the cancel step.                                                                                                                                            | N        |
| **onEditBidError**     | Triggered when editing the bid resulted in an error, returns the error and the bid data.                                                                                                                                                                          | N        |
| **onClose**            | Triggered when the modal was closed. Returns some useful data about the bid as well as the step data and the current step.                                                                                                                                        | N        |

## Conditional Rendering

ReservoirKit's EditBidModal doesn't take care of conditionally showing the button/modal based on if the bid is editable by the user, we leave that logic up to the developer. Below are the requirements for editing a bid and how to go about getting that data:

- The user needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.
- The user must be the maker of the bid, you can check this by comparing maker in the bid object to the connected wallet address. You can get a full list of a wallet's bids by using the [useBids](https://docs.reservoir.tools/reference/reservoirkit-hooks#usebids) hook or the underlying api.
- The bid must be an oracle powered bid. You can check this by verifying that the bid kind returned from the [useBids](https://docs.reservoir.tools/reference/reservoirkit-hooks#usebids) hook is of type `seaport-v1.4`. You also need to verify that the bid's order zone is included in this [list of zone addresses.](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/constants/zoneAddresses.ts) You can get this info by adding the `includeRawData` flag to the the [useBids](https://docs.reservoir.tools/reference/reservoirkit-hooks#usebids) hook or the underlying api.

# Custom EditBidModal

The EditBidModal also comes with a custom renderer which can be used to just get the data layer that the EditBidModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { EditBidModal, EditBidStep } from '@reservoir0x/reservoir-kit-ui'

<EditBidModal.Custom
  bidId="0x99e3ad649dbd9ae2f1a3c9f1331d69021a61ff9a15e1a50550b548c2d502ff05"
	collectionId="0x21227ea09f9e7ec425f59cea621debb52de8bee9"  
  tokenId="1"
>
    {({
				loading,
        bid,
        attributes,
        trait,
        tokenId,
        contract,
        isOracleOrder,
        isTokenBid,
        bidAmount,
        bidAmountUsd,
        token,
        currency,
        collection,
        editBidStep,
        transactionError,
        hasEnoughNativeCurrency,
        hasEnoughWrappedCurrency,
        balance,
        wrappedBalance,
        wrappedContractName,
        wrappedContractAddress,
        amountToWrap,
        convertLink,
        canAutomaticallyConvert,
        royaltyBps,
        expirationOptions,
        expirationOption,
        usdPrice,
        steps,
        stepData,
        setTrait,
        setBidAmount,
        setExpirationOption,
        setEditBidStep,
        editBid,
      }) => {
        { Your Custom React Elements }
    })}
</EditBidModal.Custom>
```

The custom EditBidModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom EditBidModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `EditBidStep` here which is used to manage the internal state of the EditBidModal's logic. You can decide to use all or some of the data passed into your custom implementation.