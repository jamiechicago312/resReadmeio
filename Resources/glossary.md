---
title: "Glossary"
slug: "glossary"
hidden: false
createdAt: "2022-06-24T14:04:02.521Z"
updatedAt: "2023-04-12T16:25:18.165Z"
---
### Order

An NFT order is an agreement to either buy or sell a token or token set under predetermined conditions. Orders are matched together and sent to an on-chain exchange where the trade is executed. 

### Ask (Listing)

An ask, also known as a listing, is a signed sell-side order determining the conditions under which the owner would  be willing to sell a token. 

### Offer (Bid)

An offer, also known as a bid, is a signed buy-side order determining the conditions under which a buyer would be willing to purchase a token. 

### Liquidity

Liquidity refers to the ability to instantly buy and sell assets at a fair price. Having NFT liquidity requires sufficient asks and offers so that someone can easily enter or exit the market at a reasonable price. 

### Exchange

An NFT exchange is an on-chain smart contract that executes trades between matching orders. You can view the Seaport Exchange [here](https://etherscan.io/address/0x00000000006c3852cbef3e08e8df289169ede581).

### EOA

Externally Owned Accounts (EOAs) are regular Ethereum addresses that are controlled by private keys and managed by individuals or entities outside of smart contracts. These accounts are also commonly referred to as regular wallets or user accounts.

### Aggregation 

Aggregation refers to the collection and normalization of NFT orders from disparate sources. Reservoir aggregates orders from major marketplaces into a single source liquidity. 

### Collection

A collection is a group of tokens. In 99% of cases, a collection is defined as all tokens within a contract, and the contract address is used as the Collection ID. However, in some cases, such as Art Blocks, there are multiple collections within a shared contract. In these cases, the Collection ID will be represented as a range, e.g. for Fidenza, the ID is `0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270:78000000:78999999`. 

### Collection Bid

A collection bid is an offer that can be filled by any token in the specified collection. 

### Attribute Bid

An attribute bid is an offer that can be filled by any token with a particular attribute in a specific collection.

### Collection Set

A collection set is grouping of more than one related collections. Practically collection sets can be created to group collections into larger communities or families. Collection sets are identified by a collection set id. You can make a collection set [here](/reference/postcollectionssetsv1)

### Token Set

A token set is a set of token ids that group the tokens together by a single identifier. Practically token sets can be created to place orders across many tokens. User can use a token set to create orders that apply to an arbitrary set of token ids. Token sets are identified by a token set id. You can create a token set [here](/reference/posttokensetsv1)

### Oracle

An oracle is a verifiable source of external data. Oracles enable on-chain applications to be connected to data that lives off-chain.