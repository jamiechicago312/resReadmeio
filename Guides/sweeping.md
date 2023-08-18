---
title: "How to Add Sweeping to Your Marketplace"
slug: "sweeping"
excerpt: "Learn how to sweep multiple tokens using the Reservoir SDK."
hidden: false
createdAt: "2022-06-21T14:09:55.996Z"
updatedAt: "2023-06-14T17:54:09.743Z"
---
This guide focuses on sweeping or purchasing multiple tokens using the Reservoir SDK. If you want you can skip ahead to the [sandbox demo](https://codesandbox.io/s/github/reservoirprotocol/sandbox/tree/main/sweep).

## Prerequisites ⚙️

First start by installing and configuring the [Reservoir SDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode)

There are a couple of additional prerequisites we'll need to set up before being able to process a transaction. You'll need to fetch tokens and have a few selected to purchase. The most straightforward way is to use the [tokens](ref:gettokensv5) API endpoint. Once you have the tokens selected you'll also need to calculate the total. Although this isn't necessarily required it's best practice to prevent price mismatches when the market is changing quickly.

You'll also need to make sure you're connecting a wallet to process transactions, in our demo we use [wagmi](https://wagmi.sh/) and [viem](https://viem.sh/) to create a simple component that connects your wallet to the sandbox.

## Ready for takeoff 🚀

Now that we have all the required pieces we are ready to use the `buyToken` method from the sdk. Let's dive into some parameters that the `buyToken` method expects.

```typescript
import { getClient } from '@reservoir0x/reservoir-sdk'

getClient()
      .actions.buyToken({
        tokens: tokens,
        signer: signer,
        expectedPrice: sweepTotal,
        onProgress: (steps: Execute["steps"]) => {
          if (!steps) {
            return;
          }

          const currentStep = steps.find(
            (step) => step.status === "incomplete"
          );
          if (currentStep) {
            progressCallback(currentStep.message || "");
          }
        },
      })
```

The first parameter is `tokens`, this is an array of tokens to purchase which require at least a tokenId and a contract property in each token object.

Next is the `expectedPrice`, that's referring to the total price of all the tokens we'll be sweeping. The sdk uses this to ensure that there are no price mismatch errors. As previously stated we can omit this but we'll lose the functionality for price protection.

The `onProgress` callback function is used to update the caller of the `buyToken` method. It passes in a set of steps that the SDK is following to process the transaction. It's useful for determining what step we're currently on and displaying a message to the user.

The returned object is a promise that you can optionally chain with `.then()` for the success and `.catch()` for any errors. Click here to learn more about the [buyToken](https://docs.reservoir.tools/reference/buytoken) method.

> 👍 Ready to sweep?
> 
> Play around in the [sandbox](https://codesandbox.io/s/github/reservoirprotocol/sandbox/tree/main/sweep).

[block:html]
{
  "html": "<iframe src=\"https://codesandbox.io/embed/github/reservoirprotocol/sandbox/tree/main/sweep?fontsize=14&hidenavigation=1&theme=dark&view=preview\"\n     style=\"width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;\"\n     title=\"sweep\"\n     allow=\"accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking\"\n     sandbox=\"allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts\"\n   ></iframe>"
}
[/block]