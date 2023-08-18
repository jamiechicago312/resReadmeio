---
title: "Sales"
slug: "sale"
hidden: false
createdAt: "2023-05-31T14:53:04.873Z"
updatedAt: "2023-07-31T20:46:49.876Z"
---
Subscribe to `sale` events for any new sales, updated sales, or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value                        | Description                                                                                                          |
| :---------- | :--------------------------- | :------------------------------------------------------------------------------------------------------------------- |
| **Event**   | sale.created                 | When a new sale is created                                                                                           |
|             | sale.updated                 | When an existing sale updates data (e.g. updates to the royalties after the sale has been recorded in the database.) |
|             | sale.deleted                 | When a sale is deleted (e.g. a block being reverted)                                                                 |
|             | sale.\*                      | All ask events (created and updated)                                                                                 |
| **Filters** | contract                     | Filter to one or more contracts (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63)                                    |
|             | maker                        | Filter to one or more makers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)                                       |
|             | taker                        | Filter to one or more takers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)                                       |
| **Changed** | washingTradingScore          |                                                                                                                      |
|             | fees.royaltyFeeBps           |                                                                                                                      |
|             | fees.marketplaceFeeBps       |                                                                                                                      |
|             | fees.royaltyFeeBreakdown     |                                                                                                                      |
|             | fees.marketplaceFeeBreakdown |                                                                                                                      |
|             | fees.paidFullRoyalty         |                                                                                                                      |

The `data:id` will be unique for every txn; this is the same as `saleId` in the API.

## Update Types

Any time any field in the response is updated, a `sale.updated` event will be emitted. Typically, what will be updated on a sale is the royalty amount if that was not included in the `sale.created` event.

## Example `sale.created` Payload

```json
{
    "event": "sale.created",
    "tags": {
        "contract": "0x06012c8cf97bead5deae237070f9587f8e7a266d",
        "maker": "0x89cc68f31ae2f49f3ef9be22c881efaec6ac1dcc",
        "taker": "0x7266672ea797ce9b0796e8bf26a564adec6729c3"
    },
    "changed": [],
    "data": {
        "id": "7505b231fafe9d133e156fffe82c63fe5d7a6de25075fadfc9936494e34e48d0",
        "token": {
            "contract": "0x06012c8cf97bead5deae237070f9587f8e7a266d",
            "tokenId": "2019258",
            "name": "Striker",
            "image": "https://i.seadn.io/gae/cBN53ebmNNn0I293FDryFB5pFsR2c4YcSoFymtDxpxmr4x5qMUWoiLNE-Nkgph769dv8nHfQPu9gNNeWvMgp4bSgd3qnQ5HDI1_FK1c?w=500&auto=format",
            "collection": {
                "id": "0x06012c8cf97bead5deae237070f9587f8e7a266d",
                "name": "CryptoKitties"
            }
        },
        "orderId": "0x97a0c4064bb3210e39ca8228237e485bac75e86496f4b3b4ec7d1d8583877726",
        "orderSource": "opensea.io",
        "orderSide": "ask",
        "orderKind": "seaport-v1.5",
        "from": "0x89cc68f31ae2f49f3ef9be22c881efaec6ac1dcc",
        "to": "0x7266672ea797ce9b0796e8bf26a564adec6729c3",
        "amount": "1",
        "fillSource": "opensea.io",
        "block": 17815461,
        "txHash": "0x544bb5a0ae59048f562e4fb2e5d74ee8c1e19d256b3ea1a55900a7d2b57e8507",
        "logIndex": 376,
        "batchIndex": 1,
        "timestamp": 1690836275,
        "price": {
            "currency": {
                "contract": "0x0000000000000000000000000000000000000000",
                "name": "Ether",
                "symbol": "ETH",
                "decimals": 18
            },
            "amount": {
                "raw": "35000000000000000",
                "decimal": 0.035,
                "usd": 65.16545,
                "native": 0.035
            }
        },
        "washTradingScore": 0,
        "createdAt": "2023-07-31T20:44:41.045Z",
        "updatedAt": "2023-07-31T20:44:41.045Z"
    },
    "offset": "26011238",
    "published_at": 1690836281667,
    "type": "event",
    "status": "success"
}
```

## Example `sale.updated` Payload

```json
{
    "event": "sale.updated",
    "tags": {
        "contract": "0x524c08be48e0b414c452da3d142c075444a2bd9e",
        "maker": "0x09846c9ed5d569b3c2429b03997ca9f7bc76393a",
        "taker": "0xef0b56692f78a44cf4034b07f80204757c31bcc9"
    },
    "changed": [
        "fees.royaltyFeeBps",
        "fees.marketplaceFeeBps",
        "fees.royaltyFeeBreakdown",
        "fees.marketplaceFeeBreakdown",
        "fees.paidFullRoyalty"
    ],
    "data": {
        "id": "04f175411b1c129f2ceaddc72893bdfbcc4e98119b72e110e00e57205fec01e3",
        "token": {
            "contract": "0x524c08be48e0b414c452da3d142c075444a2bd9e",
            "tokenId": "2353",
            "name": "krew #2353",
            "image": "https://i.seadn.io/gcs/files/d86a4d34420e9f99c9d4ef85186ddaf3.png?w=500&auto=format",
            "collection": {
                "id": "0x524c08be48e0b414c452da3d142c075444a2bd9e",
                "name": "Hippie Life Krew: The Cloudalia Story"
            }
        },
        "orderId": "0xee6c4c9863258635644c55635d6a49d560872a20627883f15ea14a6bee2b07af",
        "orderSource": "opensea.io",
        "orderSide": "ask",
        "orderKind": "seaport-v1.5",
        "from": "0x09846c9ed5d569b3c2429b03997ca9f7bc76393a",
        "to": "0xef0b56692f78a44cf4034b07f80204757c31bcc9",
        "amount": "1",
        "fillSource": "opensea.io",
        "block": 17815468,
        "txHash": "0x09d4fdf6db7cb63afcae67ea6382730c57b8a5a68fe39335e30e63f0d03d5bb5",
        "logIndex": 159,
        "batchIndex": 1,
        "timestamp": 1690836359,
        "price": {
            "currency": {
                "contract": "0x0000000000000000000000000000000000000000",
                "name": "Ether",
                "symbol": "ETH",
                "decimals": 18
            },
            "amount": {
                "raw": "55500000000000000",
                "decimal": 0.0555,
                "usd": 103.33378,
                "native": 0.0555
            },
            "netAmount": {
                "raw": "51337500000000000",
                "decimal": 0.05134,
                "usd": 95.58375,
                "native": 0.05134
            }
        },
        "washTradingScore": 0,
        "royaltyFeeBps": 500,
        "marketplaceFeeBps": 250,
        "paidFullRoyalty": true,
        "feeBreakdown": [
            {
                "kind": "royalty",
                "bps": 500,
                "recipient": "0xd1d26e8f7c71781fca279fb8d0a374fba9431193",
                "rawAmount": "2775000000000000"
            },
            {
                "kind": "marketplace",
                "bps": 250,
                "recipient": "0x0000a26b00c1f0df003000390027140000faa719",
                "rawAmount": "1387500000000000",
                "source": "opensea.io"
            }
        ],
        "createdAt": "2023-07-31T20:46:03.383Z",
        "updatedAt": "2023-07-31T20:46:06.796Z"
    },
    "offset": "26011262",
    "published_at": 1690836367266,
    "type": "event",
    "status": "success"
}
```

## Backfilling

If you need to backfill historical data, or catch up events missed due to disconnection, you can leverage the [Sales API](/reference/getsalesv5).