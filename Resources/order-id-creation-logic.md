---
title: "Order ID Creation Logic"
slug: "order-id-creation-logic"
excerpt: "See the table below to see the logic behind `orderId` creation."
hidden: false
createdAt: "2023-05-18T16:58:42.708Z"
updatedAt: "2023-05-18T16:59:40.612Z"
---
[block:parameters]
{
  "data": {
    "h-0": "Protocol",
    "h-1": "`id` Logic",
    "h-2": "`orderKind`",
    "0-0": "Alienswap",
    "0-1": "Order Hash",
    "0-2": "`alienswap`",
    "1-0": "Blur",
    "1-1": "Order hash for listings/  \n [Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/blur/index.ts#L305-L307) for bids",
    "1-2": "`blur`",
    "2-0": "Cryptopunks",
    "2-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/cryptopunks/index.ts#L43-L44)",
    "2-2": "`cryptopunks`",
    "3-0": "Element",
    "3-1": "Order Hash",
    "3-2": "`element`",
    "4-0": "Flow",
    "4-1": "Order Hash",
    "4-2": "`flow`",
    "5-0": "Foundation",
    "5-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/foundation/index.ts#L42-L44)",
    "5-2": "`foundation`",
    "6-0": "Looks Rare V2",
    "6-1": "Order Hash",
    "6-2": "`looks-rare-v2`",
    "7-0": "Manifold",
    "7-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/manifold/index.ts#L38-L46)",
    "7-2": "`manifold`",
    "8-0": "NFTX",
    "8-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/nftx/index.ts#L43-L48)",
    "8-2": "`nftx`",
    "9-0": "Rarible",
    "9-1": "Order Hash",
    "9-2": "`rarible`",
    "10-0": "Seaport 1.1",
    "10-1": "Order Hash",
    "10-2": "`seaport`",
    "11-0": "Seaport 1.4",
    "11-1": "Order Hash",
    "11-2": "`seaport-v1.4`",
    "12-0": "Seaport 1.5",
    "12-1": "Order Hash",
    "12-2": "`seaport-v1.5`",
    "13-0": "Sudoswap",
    "13-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/sudoswap/index.ts#L43-L48)",
    "13-2": "`sudoswap`",
    "14-0": "SuperRare",
    "14-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/superrare/index.ts#L45-L46)",
    "14-2": "`superrare`",
    "15-0": "Universe",
    "15-1": "Order Hash",
    "15-2": "`universe`",
    "16-0": "X2Y2",
    "16-1": "Order Hash",
    "16-2": "`x2y2`",
    "17-0": "Zeroex V4",
    "17-1": "Order Hash",
    "17-2": "`zeroex-v4`",
    "18-0": "Zora",
    "18-1": "[Custom](https://github.com/reservoirprotocol/indexer/blob/1e2fb408b6dd1198e68b5957e723eb4ddb2d6295/packages/indexer/src/orderbook/orders/zora/index.ts#L43-L49)",
    "18-2": "`zora`"
  },
  "cols": 3,
  "rows": 19,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]