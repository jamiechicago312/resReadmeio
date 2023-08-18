---
title: "How to directly fill orders from OpenSea Stream API"
slug: "how-to-fill-orders-with-opensea-stream-api"
hidden: true
createdAt: "2023-05-26T19:38:23.760Z"
updatedAt: "2023-06-06T20:51:22.014Z"
---
> 🚧 We recommend using the ReservoirSDK
> 
> This is an advanced guide that will require using the Reservoir [buy tokens API](ref:postexecutebuyv7) and iterating through the steps on your own. For most use cases we recommend using the [ReservoirSDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) instead. To learn more about the our trading APIs, please check out [NFT Trading Overview](ref:creating-and-filling-orders).

This guide will explain how to fill orders with the Reservoir [buy tokens API](https://docs.reservoir.tools/reference/postexecutebuyv7) using `protocol_data` retrieved from [OpenSea's Stream API](https://docs.opensea.io/reference/stream-api-overview). By using this method, you'll avoid any latency caused by Reservoir's order validation process.

**Note:** Using this method can cause more errors as this will bypass Reservoir's system that checks to make sure orders are valid and fillable. There is a chance the order you're trying to fill will either be filled already or an invalid order (unavailable).

This guide is specifically for OpenSea Stream API; if you'd like a guide on directly filling Blur orders check out [this guide](doc:how-to-directly-fill-orders-from-blur).

## Retrieve OpenSea's `protocol_data`

Connect to [OpenSea's Stream API websocket](https://docs.opensea.io/reference/stream-api-overview) and subscribe to [onItemListed](https://docs.opensea.io/reference/stream-api-event-example-payloads#item-listed-payload) to recieve events for new listings. The payload of these events includes `protocol_data` which can be passed as a rawOrder object to the Reservoir [buy tokens API](https://docs.reservoir.tools/reference/postexecutebuyv7).

_Example of `protocol_data`_

```json JSON
{
                        "data":{
                "parameters": {
                    "offerer": "0xd65c62324bab3613feb93aee9bc56140c3b447cc",
                    "offer": [
                        {
                            "itemType": 3,
                            "token": "0x449f661c53aE0611a24c2883a910A563A7e42489",
                            "identifierOrCriteria": "66",
                            "startAmount": "500",
                            "endAmount": "500"
                        }
                    ],
                    "consideration": [
                        {
                            "itemType": 0,
                            "token": "0x0000000000000000000000000000000000000000",
                            "identifierOrCriteria": "0",
                            "startAmount": "4500000000000000000",
                            "endAmount": "4500000000000000000",
                            "recipient": "0xd65C62324baB3613fEB93aEe9bc56140C3B447cc"
                        },
                        {
                            "itemType": 0,
                            "token": "0x0000000000000000000000000000000000000000",
                            "identifierOrCriteria": "0",
                            "startAmount": "125000000000000000",
                            "endAmount": "125000000000000000",
                            "recipient": "0x0000a26b00c1F0DF003000390027140000fAa719"
                        },
                        {
                            "itemType": 0,
                            "token": "0x0000000000000000000000000000000000000000",
                            "identifierOrCriteria": "0",
                            "startAmount": "375000000000000000",
                            "endAmount": "375000000000000000",
                            "recipient": "0xE98bC415F305E94E7fB82e8c5a366D0168b416C3"
                        }
                    ],
                    "startTime": "1673922180",
                    "endTime": "1674354180",
                    "orderType": 3,
                    "zone": "0x004C00500000aD104D7DBd00e3ae0A5C00560C00",
                    "zoneHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "salt": "0x360c6ebe0000000000000000000000000000000000000000c35e1224f23c604c",
                    "conduitKey": "0x0000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f0000",
                    "totalOriginalConsiderationItems": 3,
                    "counter": 0
                },
                "signature": "0x8a994f939949205853f171e289050be83449a2b063f64d501c56618d334c98fa0509e2cbad6f7555b0417d43a273bdb1aab6c3aa90d455b893b78d12ae315b4b1c"
            },
```

## Filling the Order

To fill the order, call `execute/buy/` and pass the `protocol_data` in the rawOrder object with `kind` as `opensea`.

_Example of `execute/buy/` request_

```json
{
                "taker": "0xD5c0D17cCb9071D27a4F7eD8255F59989b9aee0d",
                "skipBalanceCheck": false,
                "quantity": 1,
                "normalizeRoyalties": false,
                "allowInactiveOrderIds": false,
                "rawOrders": [
                    {
                        "data":{
                "parameters": {
                    "offerer": "0xd65c62324bab3613feb93aee9bc56140c3b447cc",
                    "offer": [
                        {
                            "itemType": 3,
                            "token": "0x449f661c53aE0611a24c2883a910A563A7e42489",
                            "identifierOrCriteria": "66",
                            "startAmount": "500",
                            "endAmount": "500"
                        }
                    ],
                    "consideration": [
                        {
                            "itemType": 0,
                            "token": "0x0000000000000000000000000000000000000000",
                            "identifierOrCriteria": "0",
                            "startAmount": "4500000000000000000",
                            "endAmount": "4500000000000000000",
                            "recipient": "0xd65C62324baB3613fEB93aEe9bc56140C3B447cc"
                        },
                        {
                            "itemType": 0,
                            "token": "0x0000000000000000000000000000000000000000",
                            "identifierOrCriteria": "0",
                            "startAmount": "125000000000000000",
                            "endAmount": "125000000000000000",
                            "recipient": "0x0000a26b00c1F0DF003000390027140000fAa719"
                        },
                        {
                            "itemType": 0,
                            "token": "0x0000000000000000000000000000000000000000",
                            "identifierOrCriteria": "0",
                            "startAmount": "375000000000000000",
                            "endAmount": "375000000000000000",
                            "recipient": "0xE98bC415F305E94E7fB82e8c5a366D0168b416C3"
                        }
                    ],
                    "startTime": "1673922180",
                    "endTime": "1674354180",
                    "orderType": 3,
                    "zone": "0x004C00500000aD104D7DBd00e3ae0A5C00560C00",
                    "zoneHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "salt": "0x360c6ebe0000000000000000000000000000000000000000c35e1224f23c604c",
                    "conduitKey": "0x0000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f0000",
                    "totalOriginalConsiderationItems": 3,
                    "counter": 0
                },
                "signature": "0x8a994f939949205853f171e289050be83449a2b063f64d501c56618d334c98fa0509e2cbad6f7555b0417d43a273bdb1aab6c3aa90d455b893b78d12ae315b4b1c"
            },
                        "kind": "opensea-v1.5"
                    }
                    ]
}
```