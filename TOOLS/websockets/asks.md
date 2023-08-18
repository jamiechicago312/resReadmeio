---
title: "Asks (Listings)"
slug: "asks"
hidden: false
createdAt: "2023-05-31T14:11:37.318Z"
updatedAt: "2023-08-15T21:00:25.891Z"
---
Subscribe to `ask` events to get real-time access to new listings or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value              | Description                                                                       |
| :---------- | :----------------- | :-------------------------------------------------------------------------------- |
| **Event**   | ask.created        | When a new ask is created                                                         |
|             | ask.updated        | When an existing ask updates (status, quantityRemaining, price, etc)              |
|             | ask.\*             | All ask events (created and updated)                                              |
| **Filters** | contract           | Filter to one or more contracts (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) |
|             | source             | Filter to one or more source (e.g. opensea.io)                                    |
|             | taker              | Filter to one or more takers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)    |
|             | maker              | Filter to one or more takers (e.g. 0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00)    |
| **Changed** | status             |                                                                                   |
|             | expiration         |                                                                                   |
|             | quantityFilled     |                                                                                   |
|             | quantityRemaining  |                                                                                   |
|             | price.gross.amount |                                                                                   |

## Update Types

Asks can update with the following state changes:

| Key               | Value     | Description                                                                                                                                          |
| :---------------- | :-------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| status            | active    | Fillable                                                                                                                                             |
| status            | inactive  | Temporarily unfillable, due to balance / approval                                                                                                    |
| status            | expired   | Permanently unfillable, due to expiry                                                                                                                |
| status            | cancelled | Permanently unfillable, due to cancellation (by user or protocol)                                                                                    |
| status            | filled    | Permanently unfillable, because it's been completely filled                                                                                          |
| quantityRemaining | \*        | When multi-quantity orders (e.g. 1155 or collection offers) are partially filled, the quantityRemaining will reduce, while the status remains active |
| price             | \*        | Dutch auctions and erc20 orders are periodically updated to reflect their relevant price in the chains native currency                               |

## Example Payload

```json json
{
	"event": "ask.created",
	"tags": {
		"contract": "0x556697ca91476b811f37a851dd2e53ae4c6024db",
		"source": "opensea.io",
		"maker": "0x0d135c0cceea42dff07edb0d890360bb3d12778a",
		"taker": "0x0000000000000000000000000000000000000000"
	},
	"data": {
		"id": "0x15059ad2b857e35fa8dced5f9fe8daeb7a743c8c0ab7386e8815666457086b5f",
		"kind": "seaport-v1.5",
		"side": "sell",
		"status": "active",
		"tokenSetId": "token:0x556697ca91476b811f37a851dd2e53ae4c6024db:942",
		"tokenSetSchemaHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"nonce": 0,
		"contract": "0x556697ca91476b811f37a851dd2e53ae4c6024db",
		"maker": "0x0d135c0cceea42dff07edb0d890360bb3d12778a",
		"taker": "0x0000000000000000000000000000000000000000",
		"price": {
			"currency": {
				"contract": "0x0000000000000000000000000000000000000000",
				"name": "Ether",
				"symbol": "ETH",
				"decimals": 18
			},
			"amount": {
				"raw": "29100000000000000",
				"decimal": 0.0291,
				"usd": 54.53858,
				"native": 0.0291
			},
			"netAmount": {
				"raw": "29100000000000000",
				"decimal": 0.0291,
				"usd": 54.53858,
				"native": 0.0291
			}
		},
		"validFrom": 1687531925,
		"validUntil": 1687535525,
		"quantityFilled": 0,
		"quantityRemaining": 1,
		"criteria": {
			"kind": "token",
			"data": {
				"token": {
					"tokenId": "942",
					"name": "Brawler #942",
					"image": "https://i.seadn.io/gcs/files/36d6957e8ee6b41bd7e343229d678fd1.gif?w=500&auto=format"
				},
				"collection": {
					"id": "0x556697ca91476b811f37a851dd2e53ae4c6024db",
					"name": "Brawler Bearz",
					"image": "https://i.seadn.io/gcs/files/0c60facb88a0601a07de92a59a23ba9a.gif?w=500&auto=format"
				}
			}
		},
		"source": {
			"id": "0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
			"domain": "opensea.io",
			"name": "OpenSea",
			"icon": "https://raw.githubusercontent.com/reservoirprotocol/indexer/v5/src/models/sources/opensea-logo.svg",
			"url": "https://opensea.io/assets/ethereum/0x556697ca91476b811f37a851dd2e53ae4c6024db/942"
		},
		"feeBps": 0,
		"feeBreakdown": [],
		"expiration": 1687535525,
		"isReservoir": null,
		"isDynamic": false,
		"createdAt": "2023-06-23T14:52:07.224Z",
		"updatedAt": "2023-06-23T14:52:07.224Z",
		"rawData": {
			"kind": "single-token",
			"salt": "0x72db8c0b00000000000000000000000000000000000000005ec645e120ffebf5",
			"zone": "0x004c00500000ad104d7dbd00e3ae0a5c00560c00",
			"offer": [{
				"token": "0x556697ca91476b811f37a851dd2e53ae4c6024db",
				"itemType": 2,
				"endAmount": "1",
				"startAmount": "1",
				"identifierOrCriteria": "942"
			}],
			"counter": "0",
			"endTime": 1687535525,
			"offerer": "0x0d135c0cceea42dff07edb0d890360bb3d12778a",
			"partial": true,
			"zoneHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
			"orderType": 0,
			"startTime": 1687531925,
			"conduitKey": "0x0000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f0000",
			"consideration": [{
				"token": "0x0000000000000000000000000000000000000000",
				"itemType": 0,
				"endAmount": "29100000000000000",
				"recipient": "0x0d135c0cceea42dff07edb0d890360bb3d12778a",
				"startAmount": "29100000000000000",
				"identifierOrCriteria": "0"
			}]
		}
	},
	"offset": "341121755",
	"published_at": 1687531927659,
	"type": "event",
	"status": "success"
}
```

## Backfilling

If you need to backfill historical data, or catch up events missed due to disconnection, you can leverage the [Asks API](https://docs.reservoir.tools/reference/getordersasksv4).