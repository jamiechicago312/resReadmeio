---
title: "Tokens"
slug: "token"
hidden: false
createdAt: "2023-06-09T16:19:08.802Z"
updatedAt: "2023-07-19T18:03:59.709Z"
---
Subscribe to `token` events to get real-time access to tokens (created/updated) or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value                                        | Description                                                                       |
| :---------- | :------------------------------------------- | :-------------------------------------------------------------------------------- |
| **Event**   | token.created                                | When a token is created (minted).                                                 |
|             | token.updated                                | When a token is updated                                                           |
|             | token.\*                                     | All token events (created and updated)                                            |
| **Filters** | contract                                     | Filter to one or more contracts (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) |
| **Changed** | name                                         |                                                                                   |
|             | description                                  |                                                                                   |
|             | image                                        |                                                                                   |
|             | media                                        |                                                                                   |
|             | collection.id                                |                                                                                   |
|             | market.floorAsk.id                           |                                                                                   |
|             | market.floorAsk.price.gross.amount           |                                                                                   |
|             | token.rarity                                 |                                                                                   |
|             | token.rarityRank                             |                                                                                   |
|             | token.isFlagged                              |                                                                                   |
|             | token.lastFlagUpdate                         |                                                                                   |
|             | token.lastFlagChange                         |                                                                                   |
|             | market.floorAskNormalized.id                 |                                                                                   |
|             | market.floorAskNormalized.price.gross.amount |                                                                                   |
|             | token.supply                                 |                                                                                   |
|             | token.remainingSupply                        |                                                                                   |

## Update Types

Any time any field in the response is updated, a `token.updated` event will be emitted. That includes flag status, image urls, metadata changes, etc. Below are some example of what can change.

| Key                | Value   | Description                                                                       |
| :----------------- | :------ | :-------------------------------------------------------------------------------- |
| isFlagged          | true    | OpenSea has marked this token as flagged (untradable, staked, suspicious, stolen) |
| isFlagged          | false   | OpenSea has marked this token as tradable.                                        |
| lastFlagUpdate     | date    | Last time checked for flag status; can be null.                                   |
| lastFlagChange     | date    | Last time the flag status changes; can be null.                                   |
| image              | url     | Metadata can be updated to reflect new imageUrl and more.                         |
| rarity             | float   | A score for it's rarity.                                                          |
| rarityRank         | integer | A rank in rarity against other tokens.                                            |
| floorAsk           |         | When the floor ask changes.                                                       |
| floorAskNormalized |         | When the floor ask (including royalties) changes.                                 |

## Example `token.created` Payload

```json
{
	"event": "token.created",
	"tags": {
		"contract": "0xb42fa25733457b093890fc96343329d971481c0d"
	},
	"data": {
		"token": {
			"contract": "0xb42fa25733457b093890fc96343329d971481c0d",
			"tokenId": "1882",
			"name": null,
			"description": null,
			"media": null,
			"kind": "erc721",
			"isFlagged": false,
			"lastFlagUpdate": null,
			"lastFlagChange": null,
			"rarity": null,
			"rarityRank": null,
			"collection": {
				"id": "0xb42fa25733457b093890fc96343329d971481c0d",
				"name": "PFP Duck",
				"slug": "pfp-duck"
			}
		},
		"market": {
			"floorAsk": null,
			"floorAskNormalized": null
		}
	},
	"published_at": 1686359537710,
	"type": "event",
	"status": "success"
}
```

## Example `token.updated` Payload

```json
{
	"event": "token.updated",
	"tags": {
		"contract": "0xeaa708c29ffce22db864385f0c6509907af45c03"
	},
  "changed": ["rarity_score", "rarity_rank"],
	"data": {
		"token": {
			"contract": "0xeaa708c29ffce22db864385f0c6509907af45c03",
			"tokenId": "2038",
			"name": "Asuki #2038",
			"description": null,
			"image": "https://i.seadn.io/gae/X5M2eLkz_gVXSn4ILelu5pVo-hP6SnZhbrUAnSM8ucK0ZFe_3a89wCSw9l0e_fwOd-NfDV5cawNrvIa8pBdIrv_unu8dMeRu52SfpAA?w=500&auto=format",
			"media": null,
			"kind": "erc721",
			"isFlagged": false,
			"lastFlagUpdate": "2023-02-02T17:59:53.894Z",
			"lastFlagChange": null,
			"rarity": 13.842,
			"rarityRank": 2915,
			"collection": {
				"id": "0xeaa708c29ffce22db864385f0c6509907af45c03",
				"name": "WeAsuki",
				"image": "https://i.seadn.io/gcs/files/121bf29dcb4d3998171e9eb1f1e33b0d.gif?w=500&auto=format",
				"slug": "we-asuki"
			}
		},
		"market": {
			"floorAsk": {
				"id": "0xca479582f12ea50bff2b813ab0c9543be73ef907d1997affda5c2ce955529e5a",
				"price": {
					"currency": {
						"contract": "0x0000000000000000000000000000000000000000",
						"name": "Ether",
						"symbol": "ETH",
						"decimals": 18
					},
					"amount": {
						"raw": "50000000000000000",
						"decimal": 0.05,
						"usd": 92.3015,
						"native": 0.05
					}
				},
				"maker": "0x6f3339eac0deb3dbc78e628c174737046498cda4",
				"validFrom": 1686346978,
				"validUntil": 1686368978,
				"source": {
					"id": "0x5924a28caaf1cc016617874a2f0c3710d881f3c1",
					"domain": "looksrare.org",
					"name": "LooksRare",
					"icon": "https://raw.githubusercontent.com/reservoirprotocol/indexer/v5/src/models/sources/looksrare-logo.svg",
					"url": "https://looksrare.org/collections/0xeaa708c29ffce22db864385f0c6509907af45c03/2038"
				}
			},
			"floorAskNormalized": {
				"id": "0xca479582f12ea50bff2b813ab0c9543be73ef907d1997affda5c2ce955529e5a",
				"price": {
					"currency": {
						"contract": "0x0000000000000000000000000000000000000000",
						"name": "Ether",
						"symbol": "ETH",
						"decimals": 18
					},
					"amount": {
						"raw": "52500000000000000",
						"decimal": 0.0525,
						"usd": 96.91657,
						"native": 0.0525
					}
				},
				"maker": "0x6f3339eac0deb3dbc78e628c174737046498cda4",
				"validFrom": 1686346978,
				"validUntil": 1686368978,
				"source": {
					"id": "0x5924a28caaf1cc016617874a2f0c3710d881f3c1",
					"domain": "looksrare.org",
					"name": "LooksRare",
					"icon": "https://raw.githubusercontent.com/reservoirprotocol/indexer/v5/src/models/sources/looksrare-logo.svg",
					"url": "https://looksrare.org/collections/0xeaa708c29ffce22db864385f0c6509907af45c03/2038"
				}
			}
		}
	},
	"published_at": 1686359663537,
	"type": "event",
	"status": "success"
}
```