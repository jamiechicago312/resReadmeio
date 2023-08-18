---
title: "Transfers"
slug: "transfer"
hidden: false
createdAt: "2023-05-31T19:03:10.752Z"
updatedAt: "2023-07-18T21:49:30.947Z"
---
Subscribe to `transfer` events to get real-time access to new listings or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value            | Description                                                                          |
| :---------- | :--------------- | :----------------------------------------------------------------------------------- |
| **Event**   | transfer.created | When a new transfer is created                                                       |
|             | transfer.updated | When an existing transfer updates (status, quantityRemaining, price, etc)            |
|             | transfer.deleted | When a transfer is deleted (due to a re-organization of blocks)                      |
|             | transfer.\*      | All transfer events (created and updated)                                            |
| **Filters** | address          | Filter to one or more contracts (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63)    |
|             | from             | Filter to one or more `from` maker (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00) |
|             | to               | Filter to one or more `to` takers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)  |

## Example Payload

```json
{
    "event": "transfer.created",
    "tags": {
        "address": "0xbbc86e700e72d50fba598d4e76b1c749291f0cd5",
        "from": "0xcda72070e455bb31c7690a170224ce43623d0b6f",
        "to": "0x6494c47f9bf8aee68ae323d0332fe1de7c8c19a4"
    },
    "data": {
      	"id": "b78a1ed937c7dfddedd27ee13934c7af852e78a119475502b64de96482be90ca",
        "token": {
            "contract": "0xbbc86e700e72d50fba598d4e76b1c749291f0cd5",
            "tokenId": "6"
        },
        "from": "0xcda72070e455bb31c7690a170224ce43623d0b6f",
        "to": "0x6494c47f9bf8aee68ae323d0332fe1de7c8c19a4",
        "amount": "1",
        "block": 17331814,
        "txHash": "0x2a97c308692dd6d88becf501a26c9181ab9557ce32c43f9eab70a0c6670c25b7",
        "logIndex": 247,
        "batchIndex": 1,
        "timestamp": 1684964939
    },
    "published_at": 1684964944109,
    "type": "event",
    "status": "success"
}
```