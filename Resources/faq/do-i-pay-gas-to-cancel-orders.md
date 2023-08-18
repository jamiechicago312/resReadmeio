---
title: "Do I pay gas to cancel orders?"
slug: "do-i-pay-gas-to-cancel-orders"
hidden: false
createdAt: "2023-03-29T18:47:30.999Z"
updatedAt: "2023-05-22T19:04:47.137Z"
---
Yes, when you cancel on-chain orders, you must pay gas because orders are signed atomic units that can be copies. If Reservoir simply deleted the user's order from the orderbook, there's no way to know whether someone has a signed copy of the order stored elsewhere. When the user cancel an order, the user is sending a transaction to the on-chain exchange contract tell it to not process your order. Since this step must be done on-chain, the user needs to pay gas.

Reservoir does offer the ability of off-chain cancelation that can be explored more [here](/docs/off-chain-cancellation).