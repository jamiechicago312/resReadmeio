---
title: "SweepModal"
slug: "sweepmodal"
excerpt: "Leverage the SweepModal to sweep tokens using ReservoirKit"
hidden: false
createdAt: "2023-04-20T21:19:38.275Z"
updatedAt: "2023-07-18T22:10:32.559Z"
---
> 🚧 The SweepModal was deprecated in v1.3
> 
> Please use the [CollectModal](https://docs.reservoir.tools/reference/collectmodal-mint-sweep) if using v.1.3 or higher.

# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# SweepModal

ReservoirKit provides a simple to configure modal for facilitating sweeping tokens in your react app. Below is an example of a simple SweepModal setup.

```typescript
import { SweepModal } from '@reservoir0x/reservoir-kit-ui'

<SweepModal
	trigger={
    <button>
    	Sweep
    </button>
        }
  collectionId={collectionId}
  onSweepComplete={(data) => {
    console.log('Sweep Complete', data)
  }}
  onSweepError={(error, data) => {
    console.log('Sweep Error', error, data)
  }}
  onClose={() => {
    console.log('SweepModal Closed')
  }}
/>
```

Let's dive into the parameters:

| **Prop**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                              | Required |
| :--------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**            | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                                                                                                                                                                    | Y        |
| **collectionId**       | The collection id of the token you wish to purchase. Can be undefined until the data is ready.                                                                                                                                                                                                                                                                                                                               | Y        |
| **feesOnTopBps**       | Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee seperated by a colon: `['0xabc:250']`. The fee is in bps. The fee currency will follow the default rules for the execute buy endpoint `feesOnTop` parameter. This takes precedence over the `feesOnTopFixed`.                                                              | N        |
| **feesOnTopFixed**     | Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee seperated by a colon: `['0xabc:10000000000000000']`. The fee is a flat fee in the atomic unit of whatever the listing currency will be in (for ether this will be wei). The fee currency will follow the default rules for the execute buy endpoint `feesOnTop` parameter. | N        |
| **normalizeRoyalties** | Use this to ensure that royalties are added to the order. If royalties are missing from the order then the correct royalties are added on top. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.                                                                                                                | N        |
| **openState**          | This is a state tuple from react's [useState](https://legacy.reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                                                                                                                                                                | N        |
| **copyOverrides**      | An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/sweep/SweepModal.tsx#L43) for which tokens map to what copy.                                                                                                                                                              | N        |
| **onSweepComplete**    | Triggered when the purchase was completed successfully, returns some useful data about the purchase.                                                                                                                                                                                                                                                                                                                         | N        |
| **onSweepError**       | Triggered when the purchase resulted in an error, returns the error and the purchase data.                                                                                                                                                                                                                                                                                                                                   | N        |
| **onClose**            | Triggered when the modal was closed. Returns some useful data about the purchase as well as the step data and the current step.                                                                                                                                                                                                                                                                                              | N        |

# Conditional Rendering

ReservoirKit's SweepModal doesn't take care of conditionally showing the button/modal, we leave that logic up to the developer. The user also needs to have a **connected wallet**. You can check this by looking for a signer from the [useWalletClient](https://wagmi.sh/react/hooks/useWalletClient) wagmi hook.

## Custom SweepModal

The SweepModal also comes with a custom renderer which can be used to just get the data layer that the SweepModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { SweepModal, SweepStep } from '@reservoir0x/reservoir-kit-ui'

<SweepModal.Custom
  open={open}
  collectionId={collectionId}>
  {({
     loading,
     address,
     selectedTokens,
     itemAmount,
     setItemAmount,
     ethAmount,
     setEthAmount,
     isItemsToggled,
     setIsItemsToggled,
     maxInput,
     currency,
     chainCurrency,
     isChainCurrency,
     total,
     totalUsd,
     feeOnTop,
     feeUsd,
     usdPrice,
     currentChain,
     availableTokens,
     balance,
     hasEnoughCurrency,
     blockExplorerBaseUrl,
     transactionError,
     stepData,
     sweepStep,
     sweepTokens,
  }) => {
    { Your Custom React Elements }
  })}
</SweepModal.Custom>
```

The custom SweepModal takes a few parameters like before with one additional one being the `open` parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom SweepModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the `SweepStep` here which is used to manage the internal state of the SweepModal's logic. You can decide to use all or some of the data passed into your custom implementation.

> 👍 Nice job!
> 
> Now that we've added a sweep modal to your dApp, let's [customize the theme to match your brand](https://docs.reservoir.tools/reference/theming).