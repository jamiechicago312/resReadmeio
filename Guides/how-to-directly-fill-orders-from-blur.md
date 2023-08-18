---
title: "How to directly fill orders from Blur"
slug: "how-to-directly-fill-orders-from-blur"
hidden: true
createdAt: "2023-05-26T18:59:59.283Z"
updatedAt: "2023-06-02T14:56:19.535Z"
---
> 🚧 We recommend using the ReservoirSDK
> 
> This is an advanced guide that will require using the Reservoir [buy tokens API](ref:postexecutebuyv7) and iterating through the steps on your own. For most use cases we recommend using the [ReservoirSDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) instead. To learn more about the our trading APIs, please check out [NFT Trading Overview](ref:creating-and-filling-orders).

Below is a guide on how to directly fill orders from Blur. This allows you to reduce latency and have the ability to fill orders faster. This is valuable when every second counts on the trade. 

**Note:** Using this method can cause more errors as this will bypass Reservoir's system that checks to make sure orders are valid and fillable. There is a chance the order you're trying to fill will either be filled already or an invalid order (unavailable).

This guide is specifically for Blur; if you'd like a guide on OpenSea Stream API check out [this guide](doc:how-to-fill-orders-with-opensea-stream-api).

## Filling the Order

You can use the execute API to fill orders with using this method. Please reference [this guide](ref:creating-and-filling-orders#step-execution-using-the-api) on the steps to use the execute API. Below is a sample of using the [Buy Token](ref:postexecutebuyv7) endpoint.

- Set the `kind` to `blur-partial`. 
- Fill out `contract`, `tokenId`, and `price` ; you need these values in order to execute.

**Notes:**

- You must have the token and the correct cost to be able to complete this transaction.
- Even if set to `true`, you cannot `skipBalanceCheck` for Blur orders; the `taker`'s fund must be sufficient for necessary filling data to be returned. 
- Setting the `kind` to `blur` will return an error, you must use `blur-partial` for this direct filling.

```curl
curl --request POST \
     --url https://api.reservoir.tools/execute/buy/v7 \
     --header 'accept: */*' \
     --header 'content-type: application/json' \
     --header 'x-api-key: demo-api-key' \
     --data '
{
  "items": [
    {
      "quantity": 1,
      "rawOrder": {
        "kind": "blur-partial",
        "data": {
          "contract": "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258",
          "tokenId": "1",
          "price": "1500000000000000000"
        }
      }
    }
  ],
  "onlyPath": false,
  "normalizeRoyalties": false,
  "allowInactiveOrderIds": false,
  "partial": false,
  "skipBalanceCheck": false,
  "excludeEOA": false,
  "taker": "0x189B9cBd4AfF470aF2C0102f365FC1823d850000"
}
'
```

> 📘 More About Blur & Reservoir
> 
> To read more about Blur's orders in the Reservoir ecosystem, check out [Blur Limitations](doc:blur-limitations).