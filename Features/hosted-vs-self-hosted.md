---
title: "Self-hosting"
slug: "hosted-vs-self-hosted"
excerpt: "Self-host the Reservoir indexer"
hidden: false
createdAt: "2022-08-27T10:55:51.083Z"
updatedAt: "2023-04-25T22:29:33.959Z"
---
The Reservoir Indexer is completely open-source, which means you can run it yourself if you want to. However, there are some considerations to keep in mind:

- There is a steep learning curve, and we’ve not yet had time to invest in documentation
- The software is still under rapid development, so will require frequent maintenance to get the latest updates and patches
- Running your own indexer is expensive, because you need to index every event for every NFT, which requires a lot of RPC calls and database resources

In 99% of cases, we recommend using the Hosted Indexer provided by the Core Team, and available at <https://api.reservoir.tools>. This is a highly available version of Reservoir that allows you to get started right away, without needing to worry about infrastructure. 

Once the product matures, it’s a high priority to make it simpler to run Reservoir on your own infrastructure, for those who want to do so. However, in the meantime, our focus is on the Hosted Indexer, and we can only offer very basic guidance for self-hosted.

## Bulk Data Access

If your reason for running the Indexer is getting bulk access to data, there might be easier options:

- A number of endpoints (Events, Sales, Transfers, Orders) are specifically designed to allow bulk scraping. Learn more [here](https://docs.reservoir.tools/reference/nft-data-overview).
- Reservoir's dataset is available in Dune Analytics! It's still being tested, but send us a DM and we can give early access. You can learn about how to query Reservoir's Dune tables [here](https://dune.com/reservoir0x/reservoir-dune-docs-dashboard). 
- If you need a dump of a particular dataset, we can probably provide it. Very shortly we will start doing daily dumps to make historical data access much easier. Feel free to reach out if you need more data access. 

## Additional Notes / FAQs

- You will also need to run the metadata service if you want to index token metadata (names, images, etc). This has only been optimized for Ethereum mainnet
- By default, the Indexer only indexes data moving forward. To have complete data, you will need to run backfill jobs