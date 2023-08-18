---
title: "Custom Fees"
slug: "custom-fees"
excerpt: "Create orders with custom marketplace, royalty, and referral fees."
hidden: false
createdAt: "2022-12-23T19:24:41.937Z"
updatedAt: "2023-08-14T18:12:16.534Z"
---
Using Reservoir's API, it's easy to create NFT orders with custom fees on NFT marketplaces. Whether you need to charge marketplace fees, royalty fees, referral fees, or a combination of all three, Reservoir has you covered. With these powerful tools at your disposal, you can create an NFT marketplace that works for you and your users.

# Setting Order Fees

Order fees are fees that are baked into the order. They are set by the user or marketplace that creates the order and will be paid out regardless of where the order is filled. To set an order fee for an order, follow these steps:

1. Create an order using the Reservoir [API](https://docs.reservoir.tools/reference/postexecutelistv5) or [SDK](https://docs.reservoir.tools/reference/listtoken).
2. Set the `fees` field (formatted as feeRecipient:feeBps)to the desired recipient address and fee percentage in basis points (100 basis points = 1%).
3. Submit the order to the Reservoir network.

The order fee will be deducted from the total amount paid by the buyer when the order is filled.

# Setting Royalty Fees

Royalty fees are paid to the creator of an NFT when it is sold on a marketplace. To set a compliant royalty fee when creating an order, follow these steps:

1. Create an order using the Reservoir [API](https://docs.reservoir.tools/reference/postexecutelistv5) or [SDK](https://docs.reservoir.tools/reference/listtoken) with `automatedRoyalties = True` .
2. Submit the order to the Reservoir network.

To set compliant royalties when filling an order you can use our [Normalized Royalties](doc:royalties) feature to add missing royalties on top of non-compliant orders.

# Setting FeesOnTop

Referral fees are fees paid to an individual or entity for facilitating a sale. To set a feesOnTop for an order, follow the steps below. Feel free to check out our [how-to guide](https://docs.reservoir.tools/docs/how-to-add-feesontop).

1. Get an order using the Reservoir [API](https://docs.reservoir.tools/reference/postexecutebuyv7) or [SDK](https://docs.reservoir.tools/reference/buytoken).
2. Set the `feesOnTop` field (formatted as feeRecipient:feeAmount) to the desired recipient address and fee amount in wei (eg. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00:1000000000000000).
3. Execute the order

If the order also has a marketplace fee, both fees will be paid.