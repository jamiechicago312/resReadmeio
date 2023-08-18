---
title: "How are flagged tokens handled?"
slug: "how-are-flagged-tokens-handles"
excerpt: "How do you handle suspicious tokens flagged by OpenSea?"
hidden: true
createdAt: "2023-03-28T17:17:33.419Z"
updatedAt: "2023-05-02T13:18:31.066Z"
---
If a token on OpenSea is flagged for suspicious activity, Reservoir's `tokens` endpoint will return a `isflagged` boolean to assist developers in quickly identifying flagged tokens. This feature is useful for those who want to avoid purchasing potentially fraudulent or problematic assets. You can learn more about this feature on Reservoir's documentation page about [flagged tokens](https://docs.reservoir.tools/docs/flagged-tokens).

Reservoir is an open infrastructure designed for trading NFTs across major marketplaces and chains. With a set of developer tools, Reservoir enables users to construct custom marketplaces, integrate buying and selling into their applications, and obtain liquidity distribution for their protocol, among other use cases.