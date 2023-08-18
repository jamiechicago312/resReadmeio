---
title: "Flagged Token Status"
slug: "flagged-tokens"
excerpt: "Track and exclude NFTs that are flagged on OpenSea from Reservoir endpoints"
hidden: false
createdAt: "2022-12-23T19:02:02.847Z"
updatedAt: "2023-06-14T17:51:55.802Z"
---
Reservoir offers a range of APIs to help developers to track and exclude NFTs that are flagged on OpenSea:

- View the "non-flagged" collection floor price ([on-demand](https://docs.reservoir.tools/reference/getcollectionsv5) or [historical](https://docs.reservoir.tools/reference/geteventscollectionsflooraskv1))
- [Show a list of Tokens](https://docs.reservoir.tools/reference/gettokensv6), with flagged tokens filtered or indicated
- [Fetch all Token IDs](https://docs.reservoir.tools/reference/gettokensidsv1) in a collection that are flagged
- Exclude flagged tokens when [placing collection offers](https://docs.reservoir.tools/reference/postexecutebidv4)
- [View changes in flag status](https://docs.reservoir.tools/reference/gettokensflagchangesv1), to keep your own DB in sync
- [Oracle for excluding flagged tokens](https://docs.reservoir.tools/reference/getoracletokensstatusv2) in on-chain applications

### Relevant Fields

- `isFlagged` = whether or not the token is flagged (0 or 1)
- `lastFlagChange` = date that the flag status last changed
- `lastFlagUpdate` = date that the flag status was last checked

### Freshness

We strive to have the freshest possible data using the following methods:

- Automated re-checks popular collections and floor tokens
- Crowd-sourced re-checks from users of the Reservoir SDK, as they view tokens

That said, there is always a risk of us not being perfectly in sync. If you only need data for a single token, it is always safer to check OpenSea directly. In fact, there is a method in the Reservoir SDK that makes this easy to add to your app, and report back to our API if it notices a discrepancy, crowd-sourcing better results for everyone. 

### Non-Tradeable Tokens

The strict definition of a "flagged" token is that it is "not tradeable on OpenSea". Unfortunately, there are other reasons that a token might not be tradeable, other than being reported stolen, and it's not possible to differentiate these. For example:

- NFTs that pre-date ERC-721 (e.g. CryptoPunks)
- Tokens that can be staked without lockup (e.g. Moonbirds & The Potatoez & DeGods)

For these collections, all tokens or a large number of tokens will be marked as "flagged". We are actively working on a potential solution, but don't have one yet.