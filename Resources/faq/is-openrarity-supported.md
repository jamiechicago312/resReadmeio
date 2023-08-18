---
title: "Is OpenRarity supported?"
slug: "is-openrarity-supported"
hidden: false
createdAt: "2023-03-28T17:15:30.150Z"
updatedAt: "2023-05-02T16:18:34.461Z"
---
No, Reservoir does not support OpenRarity ranks at this time. For a rarity score, we use PopRank's NFT rankings that you can learn more about [here](https://www.npmjs.com/package/@poprank/rankings).

We return both `rarity` and `rarityRank` in the tokens API (`GET /tokens/v5`). 

- `rarity` is a score based on the frequencies of each trait given to each token within a collection. 
- `rarityRank` is a rank given to each token within a collection based on their `rarity`. In most cases, we recommend using `rarityRank`. 

Please note that as `rarity` is based on trait frequency, collections with few or no traits will not provide accurate `rarity` or `rarityRank` data.