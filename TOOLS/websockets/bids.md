---
title: "Bids (Offers)"
slug: "bids"
hidden: false
createdAt: "2023-05-31T14:11:47.109Z"
updatedAt: "2023-08-17T00:47:10.125Z"
---
Subscribe to `bid` events to get real-time access to new bids or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value             | Description                                                                       |
| :---------- | :---------------- | :-------------------------------------------------------------------------------- |
| **Event**   | bid.created       | When a new bid is created                                                         |
|             | bid.updated       | When an existing bid updates (status, quantityRemaining, price, etc)              |
|             | bid.\*            | All bid events (created and updated)                                              |
| **Filters** | contract          | Filter to one or more contracts (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) |
|             | source            | Filter to one or more source (e.g. opensea.io)                                    |
|             | taker             | Filter to one or more takers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)    |
|             | maker             | Filter to one or more takers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)    |
| **Changed** | status            |                                                                                   |
|             | expiration        |                                                                                   |
|             | quantityFilled    |                                                                                   |
|             | quantityRemaining |                                                                                   |
|             | validFrom         |                                                                                   |
|             | validUntil        |                                                                                   |

## Update Types

Bids can update with the following state changes:

| Key               | Value     | Description                                                                                                                                          |
| :---------------- | :-------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| status            | active    | Fillable                                                                                                                                             |
| status            | inactive  | Temporarily unfillable, due to balance / approval                                                                                                    |
| status            | expired   | Permanently unfillable, due to expiry                                                                                                                |
| status            | cancelled | Permanently unfillable, due to cancellation (by user or protocol)                                                                                    |
| status            | filled    | Permanently unfillable, because it's been completely filled                                                                                          |
| quantityRemaining | \*        | When multi-quantity orders (e.g. 1155 or collection offers) are partially filled, the quantityRemaining will reduce, while the status remains active |
| price             | \*        | Dutch auctions and erc20 orders are periodically updated to reflect their relevant price in the chains native currency                               |

## Example `bid.created` Payload

```json
{
	"event": "bid.created",
	"tags": {
		"contract": "0xc7e4d1dfb2ffda31f27c6047479dfa7998a07d47",
		"source": "opensea.io",
		"maker": "0x4fcdd456e0c8de4b6ac51d1b269e7fb40f54d9e4",
		"taker": "0x0000000000000000000000000000000000000000"
	},
	"data": {
		"id": "0x1374ca1fe7a0b25f7ba17f5114c399b2fc1a889c3161c2a8285cd34bbaf772a5",
		"kind": "seaport-v1.5",
		"side": "buy",
		"status": "active",
		"tokenSetId": "token:0xc7e4d1dfb2ffda31f27c6047479dfa7998a07d47:7194",
		"tokenSetSchemaHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"nonce": 0,
		"contract": "0xc7e4d1dfb2ffda31f27c6047479dfa7998a07d47",
		"maker": "0x4fcdd456e0c8de4b6ac51d1b269e7fb40f54d9e4",
		"taker": "0x0000000000000000000000000000000000000000",
		"price": {
			"currency": {
				"contract": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
				"name": "Wrapped Ether",
				"symbol": "WETH",
				"decimals": 18
			},
			"amount": {
				"raw": "109600000000000000",
				"decimal": 0.1096,
				"usd": 205.46733,
				"native": 0.1096
			},
			"netAmount": {
				"raw": "98081040000000000",
				"decimal": 0.09808,
				"usd": 183.87272,
				"native": 0.09808
			}
		},
		"validFrom": 1687531974,
		"validUntil": 1687534074,
		"quantityFilled": 0,
		"quantityRemaining": 1,
		"criteria": {
			"kind": "token",
			"data": {
				"token": {
					"tokenId": "7194",
					"name": "Aopanda-Gold#7194",
					"image": "https://i.seadn.io/gae/T47gfxgdphXMdw0sQsP86tx8WVFyOgWauv69jYdwW1TkWwE7JPtq0GKyeDFzR-3kmQahFOozffzoIADDGz_Sp_SgyUd1uWpf46M0RQ?w=500&auto=format"
				},
				"collection": {
					"id": "0xc7e4d1dfb2ffda31f27c6047479dfa7998a07d47",
					"name": "Aopanda Party",
					"image": "https://i.seadn.io/gcs/files/a44dcb92b2224fe3daccb6d310a785a3.gif?w=500&auto=format"
				}
			}
		},
		"source": {
			"id": "0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
			"domain": "opensea.io",
			"name": "OpenSea",
			"icon": "https://raw.githubusercontent.com/reservoirprotocol/indexer/v5/src/models/sources/opensea-logo.svg",
			"url": "https://opensea.io/assets/ethereum/0xc7e4d1dfb2ffda31f27c6047479dfa7998a07d47/7194"
		},
		"feeBps": 1051,
		"feeBreakdown": [{
			"bps": 51,
			"kind": "marketplace",
			"recipient": "0x0000a26b00c1f0df003000390027140000faa719"
		}, {
			"bps": 1000,
			"kind": "royalty",
			"recipient": "0x62314d5a0f7cbed83df49c53b9f2c687d2c18289"
		}],
		"expiration": 1687534074,
		"isReservoir": null,
		"isDynamic": false,
		"createdAt": "2023-06-23T14:52:59.256Z",
		"updatedAt": "2023-06-23T14:52:59.256Z",
		"rawData": {
			"kind": "single-token",
			"salt": "0x17917e7e05c0df83e63ee78d50e345e6",
			"zone": "0x004c00500000ad104d7dbd00e3ae0a5c00560c00",
			"offer": [{
				"token": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
				"itemType": 1,
				"endAmount": "109600000000000000",
				"startAmount": "109600000000000000",
				"identifierOrCriteria": "0"
			}],
			"counter": "0",
			"endTime": 1687534074,
			"offerer": "0x4fcdd456e0c8de4b6ac51d1b269e7fb40f54d9e4",
			"partial": true,
			"zoneHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
			"orderType": 0,
			"startTime": 1687531974,
			"conduitKey": "0x0000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f0000",
			"consideration": [{
				"token": "0xc7e4d1dfb2ffda31f27c6047479dfa7998a07d47",
				"itemType": 2,
				"endAmount": "1",
				"recipient": "0x4fcdd456e0c8de4b6ac51d1b269e7fb40f54d9e4",
				"startAmount": "1",
				"identifierOrCriteria": "7194"
			}, {
				"token": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
				"itemType": 1,
				"endAmount": "558960000000000",
				"recipient": "0x0000a26b00c1f0df003000390027140000faa719",
				"startAmount": "558960000000000",
				"identifierOrCriteria": "0"
			}, {
				"token": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
				"itemType": 1,
				"endAmount": "10960000000000000",
				"recipient": "0x62314d5a0f7cbed83df49c53b9f2c687d2c18289",
				"startAmount": "10960000000000000",
				"identifierOrCriteria": "0"
			}]
		}
	},
	"offset": "341150000",
	"published_at": 1687531979865,
	"type": "event",
	"status": "success"
}
```

## Example `bid.updated` payload

```json
 {
    "event": "bid.updated",
    "tags": {
        "contract": "0x790b2cf29ed4f310bf7641f013c65d4560d28371"
    },
    "data": {
        "id": "0x5c35dbeaa306e80c541219e010b6444c2ece23e41305e47986595b211fe689c7",
        "kind": "seaport-v1.4",
        "side": "buy",
        "status": "expired",
        "tokenSetId": "token:0x790b2cf29ed4f310bf7641f013c65d4560d28371:26615",
        "tokenSetSchemaHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "contract": "0x790b2cf29ed4f310bf7641f013c65d4560d28371",
        "maker": "0x91e4510bba1e3776824a4f2b2f7c197a1bdc9119",
        "taker": "0x0000000000000000000000000000000000000000",
        "price": {
            "currency": {
                "contract": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
                "name": "Wrapped Ether",
                "symbol": "WETH",
                "decimals": 18
            },
            "amount": {
                "raw": "1301700000000000000",
                "decimal": 1.3017,
                "usd": 2419.36455,
                "native": 1.3017
            },
            "netAmount": {
                "raw": "1204072500000000000",
                "decimal": 1.20407,
                "usd": 2237.91221,
                "native": 1.20407
            }
        },
        "validFrom": 1681175092,
        "validUntil": 1681176892,
        "quantityFilled": 0,
        "quantityRemaining": 1,
        "criteria": {
            "kind": "token",
            "data": {
                "token": {
                    "tokenId": "26615"
                }
            }
        },
        "source": {
            "id": "0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
            "domain": "opensea.io",
            "name": "OpenSea",
            "icon": "https://raw.githubusercontent.com/reservoirprotocol/indexer/v5/src/models/sources/opensea-logo.svg",
            "url": "https://opensea.io/assets/0x790b2cf29ed4f310bf7641f013c65d4560d28371/26615"
        },
        "feeBps": 750,
        "feeBreakdown": [{
            "bps": 500,
            "kind": "royalty",
            "recipient": "0xa858ddc0445d8131dac4d1de01f834ffcba52ef1"
        }, {
            "bps": 250,
            "kind": "marketplace",
            "recipient": "0x0000a26b00c1f0df003000390027140000faa719"
        }],
        "expiration": 1681176892,
        "isReservoir": null,
        "isDynamic": false,
        "createdAt": "2023-04-11T01:05:29.296Z"
    },
    "type": "event",
    "status": "success"
 }
```

## Backfilling

If you need to backfill historical data, or catch up events missed due to disconnection, you can leverage the [Bids API](/reference/getordersbidsv6).