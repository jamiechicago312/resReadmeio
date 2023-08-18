---
title: "How is the washTradingScore determined?"
slug: "how-is-washtradingscore-determined"
hidden: false
createdAt: "2023-05-17T20:53:18.674Z"
updatedAt: "2023-05-19T20:42:50.663Z"
---
The `washTradingScore` is a metric used to determine the likelihood of wash trading activity for a particular transaction. Wash trading refers to the practice of artificially inflating trading volume by simultaneously buying and selling the same asset. 

In the Reservoir Indexer, the `washTradingScore` is calculated by checking wallets that trade back and forth. We also manual blocklist collections and wallets with high wash trading. Treat the score as a rough estimation. The score returned will be either 0 or 1.

Please note a `washTradingScore` of 1 does not guarantee wash trading occurred, but the transaction exhibits a high likelihood of wash trading. It serves as an indicator to flag potentially suspicious trading activity for further analysis.