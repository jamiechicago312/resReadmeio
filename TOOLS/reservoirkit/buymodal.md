---
title: "BuyModal"
slug: "buymodal"
excerpt: "Leverage the BuyModal to purchase a token using ReservoirKit"
hidden: false
createdAt: "2023-04-18T20:49:02.417Z"
updatedAt: "2023-08-03T20:27:52.916Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# BuyModal

ReservoirKit provides a simple to configure modal for facilitating token purchases in your react app. Below is an example of a simple BuyModal setup.

```typescript TypeScript
import { BuyModal } from '@reservoir0x/reservoir-kit-ui'

<BuyModal
  trigger={
    <button>
      Buy Token
    </button>
  }
  collectionId="0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"
  tokenId="1236715"
  onPurchaseComplete={(data) => console.log('Purchase Complete')}
  onPurchaseError={(error, data) => console.log('Transaction Error', error, data)}
  onClose={(data, stepData, currentStep) => console.log('Modal Closed')}

/>
```

Let's dive into the parameters:

| **Prop**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Required |
| :--------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| **trigger**            | A react node that will be presented to the user, usually a button or something clickable.                                                                                                                                                                                                                                                                                                                                                                                                                                | Y        |
| **collectionId**       | The collection id of the token you wish to purchase. Can be undefined until the data is ready.                                                                                                                                                                                                                                                                                                                                                                                                                           | Y        |
| **tokenId**            | The token id of the token you wish to purchase. Can be undefined until the data is ready.                                                                                                                                                                                                                                                                                                                                                                                                                                | Y        |
| **feesOnTopBps**       | Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee separated by a colon: `['0xabc:250']`. The fee is in bps. The fee currency will follow the default rules for the execute buy endpoint `feesOnTop` parameter. This takes precedence over the `feesOnTopFixed`.                                                                                                                                                          | N        |
| **feesOnTopUsd**       | Used to conditionally apply a referral fee on top of an order when purchasing. The parameter is an array of strings with the referrer and the fee separated by a colon: `['0xabc:1000000']`. The fee is a flat fee in the atomic unit of usd (6 decimals). It will then be converted to the purchase currency to match the same value in USD. So for example if you have 1000000 configured (1 usd) and the total price is in ETH the fee applied will be ~0.00054 ETH (or whatever is equivalent to 1 usd in realtime). | N        |
| **normalizeRoyalties** | Use this to ensure that royalties are added to the order. If royalties are missing from the order then the correct royalties are added on top. If unspecified then the [global setting](https://docs.reservoir.tools/reference/installing-reservoirkit#configuring-reservoirkit-ui) will be used if provided.                                                                                                                                                                                                            | N        |
| **openState**          | This is a state tuple from react's [useState](https://legacy.reactjs.org/docs/hooks-state.html), you can use this to programmatically open or close the modal. The modal will use this state when determining if the modal is open or closed.                                                                                                                                                                                                                                                                            | N        |
| **copyOverrides**      | An object containing copy overrides for titles and ctas contained in the modal. Refer to the `ModalCopy` [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/modal/buy/BuyModal.tsx#L39) for which tokens map to what copy.                                                                                                                                                                                                                                                              | N        |
| **onPurchaseComplete** | Triggered when the purchase was completed successfully, returns some useful data about the purchase.                                                                                                                                                                                                                                                                                                                                                                                                                     | N        |
| **onPurchaseError**    | Triggered when the purchase resulted in an error, returns the error and the purchase data.                                                                                                                                                                                                                                                                                                                                                                                                                               | N        |
| **onClose**            | Triggered when the modal was closed. Returns some useful data about the purchase as well as the step data and the current step.                                                                                                                                                                                                                                                                                                                                                                                          | N        |

# Conditional Rendering

ReservoirKit's BuyModal doesn't take care of conditionally showing the button/modal based on if the item is purchasable, we leave that logic up to the developer. Below are the requirements for purchasing and how to go about getting that data:

- The user needs to have a connected wallet. You can check this by looking for a signer from the useSigner wagmi hook.
- The user cannot be the owner of the token, you can check this by comparing the current address and the address of the owner.
- The token must have a valid listing, you can check if the floorAskPrice is available for that token using the Tokens api endpoint.

# Custom BuyModal

The BuyModal also comes with a custom renderer which can be used to just get the data layer that the BuyModal uses internally to handle the underlying business logic. With the renderer you can rebuild the UI completely to your liking. Below is an example of how it works in practice.

```typescript
import { BuyModal, BuyStep } from '@reservoir0x/reservoir-kit-ui'

<BuyModal.Custom
  open={open}
  tokenId={tokenId}
  collectionId={collectionId}>
  {({
    loading,
    token,
    collection,
    listing,
    quantityAvailable,
    quantity,
    averageUnitPrice,
    currency,
    mixedCurrencies,
    totalPrice,
    feeOnTop,
    buyStep,
    transactionError,
    hasEnoughCurrency,
   	addFundsLink,
    steps,
    stepData,
    feeUsd,
    totalUsd,
    usdPrice,
    isBanned,
    balance,
    address,
    blockExplorerBaseUrl,
    setQuantity,
    setBuyStep,
    buyToken,
  }) => {
    { Your Custom React Elements }
  })}
</BuyModal.Custom>
```

The custom BuyModal takes a few parameters like before with one additional one being the open parameter. This is because there is no trigger, you have control over what sort of modal you want this to eventually live in and how to trigger that modal. You'll have the ability to add a custom button with a custom handler, etc. The custom BuyModal then passes some key data into the children which we parse above and use in our custom UI. It's also important to note the BuyStep here which is used to manage the internal state of the BuyModal's logic. You can decide to use all or some of the data passed into your custom implementation.

> 👍 Now that we've added a buy modal to your dApp, let's [customize the theme to match your brand](https://docs.reservoir.tools/reference/theming).