---
title: "Marketplace Fees & Royalties"
slug: "marketplace-fees-royalties"
hidden: false
createdAt: "2023-03-14T00:19:31.604Z"
updatedAt: "2023-03-14T05:06:20.643Z"
---
Each marketplace that Reservoir supports has different rules around fees and royalties. Below is a summary:

## OpenSea

**Royalties**

| Collection enforces blocklist | Min Royalty                | Max Royalty               |
| :---------------------------- | :------------------------- | :------------------------ |
| Yes                           | Creator configured amount  | Creator configured amount |
| No                            | 0.5%                       | Creator configured amount |

**Marketplace Fee**

| Collection volume | Royalty >= 0.5% | Royalty \< 0.5%    |
| :---------------- | :-------------- | :----------------- |
| Low               | Fee = 0.5%      | Fee = 0.5%         |
| High              | Fee = 0         | Fee = 0.5%-Royalty |

_Note: There are no clear guidelines as to what qualifies as “low volume”, so we lookup and cache the marketplace fee per collection when you use our List API._

## LooksRare

LooksRare has a fixed total fee of 2%. If a collection has royalties configured, 0.5% goes to the creator, and 1.5% to protocol. Otherwise, the whole 2% goes to protocol.

## X2Y2

X2Y2 has a fixed protocol fee of 0.5%, and enforces creator configured royalties. Note that creators need to explicitly set royalties on X2Y2 for them to be applied