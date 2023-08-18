---
title: "Collections"
slug: "collection"
hidden: false
createdAt: "2023-06-19T19:55:51.269Z"
updatedAt: "2023-08-01T15:23:01.781Z"
---
Subscribe to `collection` events to get real-time access to collections (created/updated) or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value                    | Description                                                                            |
| :---------- | :----------------------- | :------------------------------------------------------------------------------------- |
| **Event**   | collection.created       | When a collection is created (first token minted)                                      |
|             | collection.updated       | When a collection is updated.                                                          |
|             | collection.\*            | All collection events (created and updated)                                            |
| **Filters** | id                       | Filter to one or more collection-ids (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) |
| **Changed** | slug                     |                                                                                        |
|             | name                     |                                                                                        |
|             | metadata                 |                                                                                        |
|             | royalties                |                                                                                        |
|             | tokenSetId               |                                                                                        |
|             | rank.1day                |                                                                                        |
|             | rank.7day                |                                                                                        |
|             | rank.30day               |                                                                                        |
|             | rank.allTime             |                                                                                        |
|             | volume.1day              |                                                                                        |
|             | volume.7day              |                                                                                        |
|             | volume.30day             |                                                                                        |
|             | volume.allTime           |                                                                                        |
|             | volumeChange.1day        |                                                                                        |
|             | volumeChange.7day        |                                                                                        |
|             | volumeChange.30day       |                                                                                        |
|             | floorSale.1day           |                                                                                        |
|             | floorSale.7day           |                                                                                        |
|             | floorSale.30day          |                                                                                        |
|             | tokenCount               |                                                                                        |
|             | ownerCount               |                                                                                        |
|             | floorAsk.id              |                                                                                        |
|             | floorAsk.price           |                                                                                        |
|             | floorAskNormalized.id    |                                                                                        |
|             | floorAskNormalized.price |                                                                                        |
|             | floorAskNonFlagged.id    |                                                                                        |
|             | floorAskNonFlagged.price |                                                                                        |
|             | topBid.id                |                                                                                        |
|             | topBid.value             |                                                                                        |

## Update Types

Any time any field in the response is updated, a `token.updated` event will be emitted. That includes image urls, metadata changes, etc. Below are some example of what can change.

| Key                | Value   | Description                                                         |
| :----------------- | :------ | :------------------------------------------------------------------ |
| metadata           |         | Metadata can be updated to reflect new imageUrl and more.           |
| tokenCount         | integer | Token count can change to reflect minted or burned tokens.          |
| royalties          |         | The royalty amount (bps) or recipient can change over time.         |
| topBid             |         | Every time the topBid value changes.                                |
| rank               |         | When the rank changes for 1day, 7day, 30day, or allTime.            |
| volume             |         | When the volume changes for 1day, 7day, 30day, or allTime.          |
| volumeChange       |         | When the volumeChange changes for 1day, 7day, 30day, or allTime.    |
| floorSale          |         | When the floorSale changes for 1day, 7day, 30day, or allTime.       |
| floorSaleChange    |         | When the floorSaleChange changes for 1day, 7day, 30day, or allTime. |
| ownerCount         | integer | When the owner county increases or decreases.                       |
| floorAsk           |         | When the floor ask changes.                                         |
| floorAskNormalized |         | When the floor ask (including royalties) changes.                   |
| floorAskNonFlagged |         | When the floor ask for a non-flagged token changes.                 |

## Example `collection.created` Payload

```json
{
	"event": "collection.created",
	"tags": {
		"id": "0xb614c578062a62714c927cd8193f0b8bfb90055c:410000000:410999999"
	},
	"data": {
		"id": "0xb614c578062a62714c927cd8193f0b8bfb90055c:410000000:410999999",
		"slug": "art-blocks-v3-core-staging-goerli",
		"name": "Jenim by Orr Kislev & Alona Rodeh",
		"metadata": {
			"imageUrl": "https://media.artblocks.io/410000000.png",
			"description": "Initially worn by miners and cowboys, roughly half of the world’s population wears denim on a given day, and the range of styles is–literally–endless. A new pair of jeans might be acid bleached, sandblasted, stonewashed, or tie-dyed; it can have hand-sanded rips and tears, followed by visible mendings, patches, intentional paint stains, and more. In an epic attempt to crack the genetic code of denim, Jenim playfully but carefully observes and translates the warp and weft of denim into generative code, weaving unique iterations of irregular, distorted, or hyper-realistic textile crops.\n\nIronically, imitating aging, a pair of jeans produced today generates more pollution and labor than most average garments. In response, Jenim’s minted iterations go beyond wearables and into infinity. Each year that passes, the color might fade slightly; the rips might expand. Who knows what these artworks will look like ten or even fifty years from now?",
			"externalUrl": null,
			"safelistRequestStatus": "not_requested"
		},
		"tokenCount": "59",
		"primaryContract": "0xb614c578062a62714c927cd8193f0b8bfb90055c",
		"tokenSetId": "range:0xb614c578062a62714c927cd8193f0b8bfb90055c:410000000:410999999",
		"royalties": {
			"bps": 500,
			"recipient": "0x73b2e8e8faf8613cde07712c3f1cadbcda9900b2"
		},
		"topBid": {
			"id": null,
			"value": null,
			"maker": null,
			"validFrom": null,
			"validUntil": null
		},
		"rank": {
			"1day": null,
			"7day": null,
			"30day": null,
			"allTime": null
		},
		"volume": {
			"1day": 0,
			"7day": 0,
			"30day": 0,
			"allTime": 0
		},
		"volumeChange": {
			"1day": null,
			"7day": null,
			"30day": null
		},
		"floorSale": {
			"1day": null,
			"7day": null,
			"30day": null
		},
		"floorSaleChange": {
			"1day": null,
			"7day": null,
			"30day": null
		},
		"ownerCount": 1,
		"floorAsk": {
			"id": null,
			"price": null,
			"maker": null,
			"validFrom": 2147483647,
			"validUntil": null
		},
		"floorAskNormalized": {
			"id": null,
			"price": null,
			"maker": null,
			"validFrom": 2147483647,
			"validUntil": null
		},
		"floorAskNonFlagged": {
			"id": null,
			"price": null,
			"maker": null,
			"validFrom": 2147483647,
			"validUntil": null
		}
	},
	"published_at": 1688430574778,
	"type": "event",
	"status": "success"
}
```

## Example `collection.updated` Payload

```json
{
    "event": "collection.updated",
    "tags": {
        "id": "0x1e988ba4692e52bc50b375bcc8585b95c48aad77"
    },
    "changed": [
        "floorAskNonFlagged.id",
        "floorAskNonFlagged.price"
    ],
    "data": {
        "id": "0x1e988ba4692e52bc50b375bcc8585b95c48aad77",
        "slug": "bufficornbuidlbrigade",
        "name": "Bufficorn Buidl Brigade",
        "metadata": {
            "imageUrl": "https://i.seadn.io/gae/_Qfw2lI3pYbso5-EKD7VS76UQOd7NTtcaYJ9qSGovG1X0iVm2oJNNgnepXRN5-3dDC3R2OtZQT1TpGgzNr5vp5v53ez84_lQaTjBYyY?w=500&auto=format",
            "bannerImageUrl": "https://i.seadn.io/gae/eF6hA3tRp9M1solLcMrrPgCPc2edxwlsMHOVXwWK1NzsuehZXnTSnU4cEt0AjIHkSMxVoR9Rx9mSULYhsHgHykZizlOmcm2xUXg8lg?w=500&auto=format",
            "discordUrl": "https://discord.gg/SporkDAO",
            "externalUrl": "https://bufficornbuidlbrigade.com/",
            "twitterUsername": "EthereumDenver",
            "description": "REFRESH METADATA BEFORE MAKING OFFERS - BUFFICORN TRAITS MAY HAVE CHANGED SINCE A BBB WAS LISTED\n\nWelcome to the Bufficorn #BUIDL Brigade (B³), a utility-based NFT PFP community brought to you by SporkDAO & ETHDenver, the largest and longest running ETH event in the world.\n\nJoin the community: https://discord.gg/sporkdao\nSwap your Bufficorn's traits: https://swap.bufficorn.com\n\nAs a furtherance of the SporkDAO community's #BUIDLing propensity, B³ is a perfect expression of what it means to \"be a Bufficorn\" and to be passionate about #BUIDLing the decentralized future: You be you and express your inner creativity in a way that creates fulfillment and value for you and the community."
        },
        "tokenCount": "10000",
        "primaryContract": "0x1e988ba4692e52bc50b375bcc8585b95c48aad77",
        "tokenSetId": "contract:0x1e988ba4692e52bc50b375bcc8585b95c48aad77",
        "contractKind": "erc721",
        "openseaVerificationStatus": "verified",
        "royalties": {
            "bps": 200,
            "recipient": "0x11cce80e6ea89c7da94f670977edbf7673fdcef4"
        },
        "topBid": {
            "id": "0x8e7540de36fdd96f9c91a6ff24f27a53eb9e2e2a5682cb398b387b0784b0959f",
            "value": 0.02669,
            "maker": "0xb21a7f37970043e66bf38bd18afaf0c6265735f7",
            "validFrom": 1690600403000,
            "validUntil": 0,
            "source": {
                "id": "0xe864198328af9d2260e4178734190022fe8d79dc",
                "domain": "nftx.io",
                "name": "nftx.io",
                "icon": "https://nftx.io/apple-touch-icon.png"
            }
        },
        "rank": {
            "1day": 1267,
            "7day": 1291,
            "30day": 1262,
            "allTime": 1960
        },
        "volume": {
            "1day": 0.029,
            "7day": 0.11874,
            "30day": 0.51324,
            "allTime": 748.05052
        },
        "volumeChange": {
            "1day": 1.45,
            "7day": 1.4879890982520312,
            "30day": 0.3424222739954596
        },
        "floorSale": {
            "1day": 0.029,
            "7day": 0.025,
            "30day": 0.03
        },
        "floorSaleChange": {
            "1day": 0.6896551724137931,
            "7day": 0.8,
            "30day": 0.6666666666666666
        },
        "ownerCount": 4262,
        "floorAsk": {
            "id": "0x4f16fab5738373356253f637f066a530729526cefc77cb8a3602b755a9e24b75",
            "price": 0.02,
            "maker": "0x047ec60fe3f62009116daded57bf14bb225e0861",
            "validFrom": 1690903321278,
            "validUntil": 0,
            "source": {
                "id": "0xe073a3b3497e2ed4c6110eebbb664a839b168bcb",
                "domain": "blur.io",
                "name": "blur.io",
                "icon": "https://blur.io/favicons/180.png"
            }
        },
        "floorAskNormalized": {
            "id": "0x842bc1d6c14981742b6981ad15498d45b5d3748394c37533c1b3ffa953036239",
            "price": 0.04285,
            "maker": "0xb21a7f37970043e66bf38bd18afaf0c6265735f7",
            "validFrom": 1690600403000,
            "validUntil": 0,
            "source": {
                "id": "0xe864198328af9d2260e4178734190022fe8d79dc",
                "domain": "nftx.io",
                "name": "nftx.io",
                "icon": "https://nftx.io/apple-touch-icon.png"
            }
        },
        "floorAskNonFlagged": {
            "id": "0x4f16fab5738373356253f637f066a530729526cefc77cb8a3602b755a9e24b75",
            "price": 0.02,
            "maker": "0x047ec60fe3f62009116daded57bf14bb225e0861",
            "validFrom": 1690903321278,
            "validUntil": 0,
            "source": {
                "id": "0xe073a3b3497e2ed4c6110eebbb664a839b168bcb",
                "domain": "blur.io",
                "name": "blur.io",
                "icon": "https://blur.io/favicons/180.png"
            }
        }
    },
    "published_at": 1690903321818,
    "type": "event",
    "status": "success"
}
```

## Backfilling

If you need to backfill historical data, or catch up events missed due to disconnection, you can leverage the [Collections API](/reference/getcollectionsv6). You can set `sortBy=createdAt` to find the latest collections.