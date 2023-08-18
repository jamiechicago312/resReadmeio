---
title: "Royalty Enforcement"
slug: "royalties"
excerpt: "Reservoir supports marketplace royalty normalization and onchain royalty enforcement"
hidden: false
createdAt: "2022-11-02T18:19:43.396Z"
updatedAt: "2023-08-18T01:12:03.956Z"
---
Reservoir is committed to preserving creator royalties, and believes that a pragmatic solution is needed to balance the needs of different stakeholders. We support two major mechanisms for royalty enforcement, marketplace royalty normalization and onchain royalty enforcement using ERC721C and payment processor. 

# Marketplace Royalty Normalization

Royalty normalization enable developers to automatically repair aggregated orders from non-royalty compliant marketplaces by calculating the missing royalties and adding them on top.

## How does it work?

For supported exchanges, Reservoir calculates the missing royalty by comparing the royalty fee included in the order to the default royalty. The default royalty is the maximum royalty across all royalty standards supported by Reservoir (e.g., OpenSea off-chain royalties and the royalty registry). If normalizeRoyalties is enabled, Reservoir will automatically return the new price of the token with missing royalties added on top.

Currently, `normalizeRoyalties` affects all non-royalty compliant exchanges, except Blur. When `normalizeRoyalties` is set to true, Blur listings are filtered from endpoints, so that all orders respect royalties. This is a fundamental limitation of Blur's architecture, which you can learn more about [here](https://docs.reservoir.tools/reference/blur-api#blur-limitations). 

## How do I enable Normalized Royalties?

### Via ReservoirKit or ReservoirSDK

If you are using ReservoirKit UI or the Reservoir SDK packages, they can both be configured to `normalizeRoyalties` globally or on a case-by-case basis. These changes will impact everything from the hooks to the execution of orders.

### Via APIs

If you are using Reservoir's APIs, you can add the `normalizeRoyalties` parameter to configure getting orders/pricing information with normalized royalties.

# Onchain Royalty Enforcement (ERC721C & Payment Processor)

Reservoir worked closely with the [LimitBreak team](https://twitter.com/reservoir0x/status/1674522522912722944) to build full support for [ERC-721C and Payment Processor](https://medium.com/limit-break/introducing-erc721-c-payment-processor-a-game-changing-nft-marketplace-protocol-355b840dfd5d). 

## ERC-721C and Payment Processor

ERC-721C is an extension of the ERC-721 standard that introduces a white list for NFT transfers. This standard was built in conjunction with Payment Processor, a novel NFT exchange that is capable of enforcing royalties at the exchange level. In practice what this means is that creators can launch 721C contracts and enforce royalties on all trades. You can learn more about the options[here](https://medium.com/limit-break/introducing-erc721-c-payment-processor-a-game-changing-nft-marketplace-protocol-355b840dfd5d), and create 721C payment processor contracts [here](https://developers.freenft.com/).

## Reservoir Support of ERC-721C and Payment Processor

Reservoir has implemented full support for Payment Processor and ERC-721C, meaning you can enjoy all of Reservoir tools when leveraging 721C. There is no need to do anything differently, simply use Reservoir, as we will route ERC-721C trades through Payment Processor as required.