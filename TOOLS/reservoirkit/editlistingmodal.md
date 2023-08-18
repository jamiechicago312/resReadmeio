---
title: "EditListingModal"
slug: "editlistingmodal"
excerpt: "Leverage the EditListingModal to edit listings using ReservoirKit"
hidden: false
createdAt: "2023-04-18T21:38:21.429Z"
updatedAt: "2023-06-14T05:44:57.653Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# EditListingModal

ReservoirKit provides a simple to configure modal for editing oracle listings in your react app. Below is an example of a simple EditListingModal setup.

**It is important to note that you can only edit oracle powered listings**  

```typescript
import { EditListingModal } from '@reservoir0x/reservoir-kit-ui'

<EditListingModal
	trigger={
  	<button>
      Edit Listing
    </button>
  }
  listingId="0x99e3ad649dbd9ae2f1a3c9f1331d69021a61ff9a15e1a50550b548c2d502ff05"
	collectionId="0x21227ea09f9e7ec425f59cea621debb52de8bee9"  
  tokenId="1"
  onEditListingComplete={(data: any) => {
		console.log('Listing updated', data)
  }}
  onEditListingError={(error: any, data: any) => {
  	console.log('Edit Listing Error', error, data)
  }}
  onClose={() => {
  	console.log('EditListingModal Closed')
  }}
/>
```

Let's dive into the parameters:

| Prop                      | Description                                                                                                                                                                                                                                                               | Required |
| :------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------- |
| **trigger**               | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                 | Y        |
| **listingId**             | An order id representing the listing. It can be set to undefined until the data is ready                                                                                                                                                                                  | Y        |
| **collectionId**          | The collection id of the token you wish to edit a listing on. Can be undefined until the data is ready.                                                                                                                                                                   | Y        |
| **tokenId**               | The token id of the token you wish to edit a listing on. Can be undefined until the data is ready.                                                                                                                                                                        | Y        |
| **normalizeRoyalties**    | Use this to ensure that royalties are added to the stats and market pricing information. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.                   | N        |
| **openState**             | This is a state tuple from react's [useState](https://reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                    | N        |
| **copyOverrides**         | An object containing copy overrides for titles and ctas contained in the modal. Refer to the ModalCopy [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/editListing/EditListingModal.tsx#L20) for which tokens map to what copy. | N        |
| **onEditListingComplete** | Triggered when editing the listing was completed successfully, returns some useful data about the listing and the cancel step.                                                                                                                                            | N        |
| **onEditListingError**    | Triggered when editing the listing resulted in an error, returns the error and the listing data.                                                                                                                                                                          | N        |
| **onClose**               | Triggered when the modal was closed. Returns some useful data about the listing as well as the step data and the current step.                                                                                                                                            | N        |

# Conditional Rendering

ReservoirKit's EditListingModal doesn't take care of conditionally showing the button/modal based on if the listing is editable by the user, we leave that logic up to the developer. Below are the requirements for editing a listing and how to go about getting that data:

- The user needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.
- The user must be the maker of the listing, you can check this by comparing maker in the listing object to the connected wallet address. You can get a full list of a wallet's listings by using the [useListings](https://docs.reservoir.tools/reference/reservoirkit-hooks#uselistings) hook or the underlying api.
- The listing must be an oracle powered listing. You can check this by verifying that the listing kind returned from the [useListings](https://docs.reservoir.tools/reference/reservoirkit-hooks#uselistings) hook is of type `seaport-v1.4`. You also need to verify that the listing's order zone is included in this [list of zone addresses.](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/constants/zoneAddresses.ts) You can get this info by adding the `includeRawData` flag to the the [useListings](https://docs.reservoir.tools/reference/reservoirkit-hooks#uselistings) hook or the underlying api.

# Custom EditListingModal

The EditListingModal also comes with a custom renderer which can be used to just get the data layer that the EditListingModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { EditListingModal, EditListingStep } from '@reservoir0x/reservoir-kit-ui'

<EditListingModal.Custom
  listingId="0x99e3ad649dbd9ae2f1a3c9f1331d69021a61ff9a15e1a50550b548c2d502ff05"
	collectionId="0x21227ea09f9e7ec425f59cea621debb52de8bee9"  
  tokenId="1"
>
    {({
        loading,
        listing,
        token,
        price,
        currency,
        isOracleOrder,
        quantityAvailable,
        collection,
        quantity,
        expirationOption,
        expirationOptions,
        editListingStep,
        transactionError,
        usdPrice,
        totalUsd,
        royaltyBps,
        stepData,
        setPrice,
        setQuantity,
        setExpirationOption,
        editListing,
      }) => {
        { Your Custom React Elements }
    })}
</EditListingModal.Custom>
```

The custom EditListingModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom EditListingModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `EditListingStep` here which is used to manage the internal state of the EditListingModal's logic. You can decide to use all or some of the data passed into your custom implementation.