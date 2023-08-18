---
title: "top-bid.changed"
slug: "top-bids"
hidden: false
createdAt: "2023-05-04T12:55:52.927Z"
updatedAt: "2023-06-16T14:13:28.273Z"
---
The top-bid.changed websocket is designed to send push notifications to users when there is a notable new event. This notification can be pushed to a wallet or portfolio to let the user know they have a new top bid on one of their NFTs. 

Notes:

- The owners are cached for 60s in order to reduce the overhead of calculation.
- The same top bid event might trigger multiple ws events with a different list of owners. This is done in order to keep the we event payload size small.

```json
{
  "type": "event",
	"event": "top-bid.changed",
  "status": "success",
	"tags": {
		"contract": "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258"
	},
	"data": {
		"order": {
			"id": "0x9040b290745bd0360e66f75ea079dbda7f28f81758c5ce01329f6afc723f84f2",
			"contract": "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258",
			"maker": "0xecd6cc64107957affb297ed36ca4c5a26f1ad2e4",
			"createdAt": "2023-04-03T13:50:14.351Z",
			"validFrom": 1680529790,
			"validUntil": 1680531565,
			"source": {
				"id": "0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
				"domain": "opensea.io",
				"name": "OpenSea",
				"icon": "https://raw.githubusercontent.com/reservoirprotocol/indexer/v5/src/models/sources/opensea-logo.svg"
			},
			"price": {
				"currency": {
					"contract": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
					"name": "Wrapped Ether",
					"symbol": "WETH",
					"decimals": 18
				},
				"amount": {
					"raw": "6114400000000000000",
					"decimal": 6.1144,
					"usd": 10981.02281,
					"native": 6.1144
				},
				"netAmount": {
					"raw": "6083828000000000000",
					"decimal": 6.08383,
					"usd": 10926.1177,
					"native": 6.08383
				},
				"normalizedNetAmount": {
					"raw": "5808680000000000000",
					"decimal": 5.80868,
					"usd": 10431.97167,
					"native": 5.80868
				}
			},
			"criteria": {
				"kind": "attribute",
				"data": {
					"collection": {
						"id": "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258"
					},
					"attribute": {
						"key": "Artifact",
						"value": "Koda Pickaxe"
					}
				}
			}
		},
		"owners": ["0xc0738649740929ef714cc5c0229a1d5fa8138c29", "0xa2efa94766ee867c91f71e8020a3c97ae687e5c3", "0x8764393bb2da999d056f524307ca58c6849db81a", "0xf0713fe8fd952a464e68e6123d7fca2675c3dee5", "0x652702f27c56eedc17ecebb4e10f39070d68fc29", "0xa26dc8ed1f0ae2808597f2e629c1514946e33c93", "0x8681e8985a0cb9da47b6529955bedad5e6656972", "0x9ad38c3498636e06202b660d8d9b7a6766768a51", "0x6b2e1b4717d336af0839db550b3e95c0b7359750", "0x85e59a136696fa544714eb32625f2f56f3b1c96d", "0x354737082cd7631e3cf6b3218e55f319cd1d0285", "0x9fe9e92012e97f6f0c884fee5436d4f07b505517", "0xe858900bfe2d28eb7e18929428381d156941f5aa", "0xff21d5c231fc37066dbf181c69abbd0c3a564965", "0xcb415344cd0fc552ce7b48ee9375991ff5865895", "0x37f6db41ccafa7b4137f53387b861edb165470b5", "0xdf127d8d4393c89ac2db1109adff4971bf780bc1", "0xd3a1ab87c8ab81cb093ef5430a387d127ac523a0", "0x8937c6f6764e15b0172282a14d00076d47b89124", "0x78b2b89855960ffbb6b9071a50d02ff0875063aa", "0x1e692a6ef09ae411e9190bf2add391285b5d9d76", "0x461f4e27d93f30821a866f87d55aaa6fb03fd3d6", "0xf4893542e4ec7c33356579f91bf22e8fa7cd06dc", "0x87f9a31024ae7bd0a0b82071e7b2244b8280043f", "0x63809d09938a5770228db86baad44844d541fcf7", "0xb84580a14e42c74efa1213ab2fb9f98da33452ee", "0x0cb634e90f6e2c0baacbfea1fc7780c715f2857b", "0xa8189c566c8b602e23b016da819c11dae50160d6", "0xd37533b4a6e8bbabf344b557173f48a7eb1ec937", "0x9f9dc1c37b06f565644085a828b16dbc100bc6c5", "0x33d4b1c41ba877e97cb366e4c53e426cc898896b", "0xe66b2cf097c0f898047d89eb2f59107637b09f0e", "0x2c419c8b207b10b39673482d83caa3e11f3604c5", "0x8315df0d961906301ef7715f8415b29d0d4a2a9e", "0x2fff0f98909bae74d00583e65db3ade8a4f634ca", "0x1e12f89f1ff0c72938fc1e211e2b0360dae2ec5e", "0x64f7de90dc79d775703bbec66a1591c7a26a22f0", "0xe8bb5796e841e2814266e1bd04f02edd8fb5ea29", "0xe4fb812f2c715e581e45763a6a744f4f92da6854", "0xddd3d68c069e2260aa425220b090fcf6e985edda", "0x28a341684fda2f78e19beb0ef3732a5b6b41927a", "0x1f77687df949341a0fd8f69a3b557a26e13efc8f", "0xf24649899edb01a223a8d4c899b66d35f655a735", "0x2bca9da6cd1a0b58449eacf80379ad3a5f2c77c4", "0xf90abb155a076abd146e0add3a99d3c92c42ca37", "0x1655406778522ee038efaa2f1dd12acdf75eb240", "0x4072d2c6e58c9a3d43d692c0dba81ec0eeeed15d", "0xe3636d969fe448ae835c8984d6c3a4e1ace27232", "0xeb6bace57477f64633a0b143d37938051184e331", "0xaa621b960f22911462550c078df678493c22b2ae", "0x04f5df957ce0405ba0264eca6130161cfaa12571", "0xb47c55f00a31deda8415e67d587168e05d41f92c", "0x08632358d3f5781cb2bae28da286aaf4ccacaaa0", "0xab58f3de07fb3455d218438a99d69b3f06f23c49", "0xc0d92f633ee8c8439783f5d2c06aafdb70e781b8", "0x459d1e0ede6a531ef6aa48d8309bb7984736299e", "0xdf61927b4485be10c8b72e885aab37a53d4a77b1", "0x14210914d6a65fa2c7747579a7aa287b027fd092", "0xb9187bea86318b2062729c9bdea2f1c157308025", "0x720a4fab08cb746fc90e88d1924a98104c0822cf", "0x2fa2231d73b3dfe658273426ed69fec1bf7252f0", "0x0a2a335b7420db3bada6a13e354d465a3d6de2a4", "0x58b21358c660d4a277eefc5a08e72aca52f75fb6", "0xd435b22d96bfe40752e8b01596c1e95b3fef3afa", "0xa858ddc0445d8131dac4d1de01f834ffcba52ef1", "0xc67238599e9fb7e4974e7f9269cd9a4761119e5f", "0xc4c597855146caf762fc850b2a0bbe5c59735637", "0xa4041232f7eeb883425112593c8dd517d0da024f", "0x898b22fda30e044a81ea36af7aff3f13503a7531", "0x45632d932579861ca72dc93b50677795253f9bab", "0x9fa09b6bc07bf4a70357072134130be3d9a4dbcc", "0x17b0a1a7179e6d1bd0b2526fe8d6a39f2657c7be", "0x0385f354f23a28269986507f5dbf13623c069a06", "0x5d9d1eb4f3250a3c5520a65df88d5fe238f90b2e", "0x7eb413211a9de1cd2fe8b8bb6055636c43f7d206", "0xf838d2cf50fab2531fca8b3295806c8fbdd36244", "0x6897625c2da7e985e9c22e0d7b27a960fc81d1d2", "0x02bb854b217682e0db2a7795ba479a9b88711dbb", "0x4d8838d4eeda7f2ced51f817fa03909da34bc834", "0xbf3939431e40d57ec79a8790df41d75ba718ccfa", "0xc4b0d0a7717905d342926958453e0654806850bb", "0x388ebb5528d2c35934063f51a1ec15935a8921f9", "0xc94bb9a7485954e17f589e572346cd8b7deadbe1", "0x3eae39e29af926503e5bc2a4c0c650db9e8091f3", "0xedae46bc4357e4619397ef4e121fc3067d931cd1", "0x3bdaafb9a90e66d6e79867212bff706c68232929", "0x905ace916763b814877123db761c429ce5578a5d", "0xc3daadf40b5ddf466e0cec53b86e8646a345fad5", "0x4b1e684d5143eb7435e5d78385fa8cbdccd8f7ec", "0xe8ef758bbf02f6730234ca504cf094ca647209b5", "0xf34d535fb694cc91157a7eb54b97729c14938876", "0x6a53d1beb2a9c4d86684cb4b62a86c435e8d4455", "0x1df428833f2c9fb1ef098754e5d710432450d706", "0xd7d398542d010d1eb095501c34bedd7cf22c6fd6", "0x856ab52578ecb505ac9d2231dd0033878943b0ba", "0x1b88ff8fcb1b677c3771e9ed56a620df010b5829", "0xef9497439548c5967b179d80a49e829efa2a9300", "0x67ba1c914e6b3b396346a6498c1ef8e59802b1e9", "0xdfd143ae8592e8e3c13aa3e401f72e1ca7deaed0", "0x50505bd07229122e3c139e04bf524138aa936173", "0x599c2b5dbfbc8851e674d3dacbb14a408f7b416c", "0x175dd6b8e32ff64713bbad581236e589b5c32389", "0x7e483230f2a35d0f352a94095ae2a30689021e56", "0xdb0f95806885c2e6b048d2ee62918fcd852c0fcb", "0xcefb579898e907b01cdc9f42a7d5cf265ee6d373", "0x6035d69158dcae6a288c2abb621f38ab462a0007", "0xacdaeeb57ff6886fc8e203b9dd4c2b241df89b7a", "0x31a520c0f66de2258db288ee1c1bcc577fd91652", "0xbe9a3e392cd7d2b855f8c6b414f8f2a99724f831", "0x4042857bbd069ef964d8319c5859ac566fc6e9e4", "0x928b232c055b32c062775a9297d2291788fc80bf"],
		"collection": {
			"id": "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258",
			"slug": "otherdeed",
			"name": "Otherdeed for Otherside",
			"floorAskPrice": 1.73,
			"floorAskPriceNormalized": 1.7655,
      "floorAskPriceNonFlagged": 1.1,
			"floorDifferencePercentage": 280.18
		}
	}
}
```