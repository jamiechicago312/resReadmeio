---
title: "Open-Source Marketplace"
slug: "open-source-marketplace"
excerpt: "Fork and customize the Reservoir Open-source Marketplace"
hidden: false
createdAt: "2023-04-21T21:06:57.370Z"
updatedAt: "2023-08-04T17:37:05.005Z"
---
## Introduction

[Reservoir Market v2 ](https://github.com/reservoirprotocol/marketplace-v2)is an open source marketplace built with Reservoir APIs that enables access to instant liquidity aggregated from major marketplace. We encourage developers to use this project as a reference for their own implementation or even fork the project and make their own meaningful changes. The project is lightly configurable refer to the configuration variables below. If you're looking for a no-code solution check out our [v1 marketplace](https://github.com/reservoirprotocol/marketplace-v1). this marketplace isn't merely a demonstration but an actionable, scalable, and customizable blueprint. It's designed to help you create your own NFT marketplace or trading experiences, matching and even surpassing the sophistication of mainstream marketplaces like Opensea or Looksrare.

## Features

- **Open-source**: The marketplace’s open-source nature allows you to understand, modify, and enhance the code to suit your unique requirements.

- **Liquidity and Order Execution**: Our developer tools also allow for seamless liquidity management and efficient execution of orders in the NFT marketplaces. Access all listings from all marketplaces including [Opensea](https://opensea.io/), [Blur](https://blur.io/), [LookRare](https://looksrare.org/), [X2Y2 ](https://x2y2.io/)& [150 more](https://docs.reservoir.tools/reference/supported-marketplaces-1).

- **Feature rich**: Built to cater to marketplaces of all sizes, our platform is has many of the beloved features including a collection ranking, sweeping & a portfolio.

- **Customizable**: The Open-source Marketplace is a boilerplate, meaning it's designed to be tailored according to your specific needs and preferences. You can include as little or as many built in features as you want while also being able to integrate custom features of your own

## Benefits

- **Fast-Track Development**: Leverage the Open-source Marketplace as a boilerplate to jumpstart your own platform, significantly reducing the time to market & simplifies the process of interacting with other marketplaces, making it accessible even to those new to the space. As well as reduce the cost associated with building a marketplace from scratch and maintaining data servers, order management systems, and liquidity pools.

- **No compromise innovation**: As an open-source platform, you have the freedom to modify the platform to suit your needs, giving you more control over your platform's functionality. Doing so without compromising industry standard features mainstream marketplaces currently have, you're starting with a strong foundation based on industry best practices.

- **Learning Opportunity**: This Open-source Marketplace serves as a practical learning resource for developers looking to understand the intricacies of building a feature-rich NFT marketplace.

## Getting Started

### Prerequisites

1. Install [Node.js and NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
2. Install [Yarn](https://classic.yarnpkg.com/en/docs/install)
3. Request free [Reservoir API key](https://reservoir.tools/request-api-key)

### Built With

- [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit)
- [Reservoir Protocol and API](https://reservoirprotocol.github.io/)
- [Next.js](https://nextjs.org/)
- [React.js](https://reactjs.org/)
- [Ethers.io](https://ethers.io/)
- [WAGMI](https://wagmi.sh/)
- [Stitches](https://stitches.dev/docs/variants)

### Installation

Fork this repo and follow these instructions to install dependencies.

With yarn:

```bash
$ yarn install
```

With NPM:

```bash
$ npm install
```

> 📘 [Learn how to protect your API key](https://docs.reservoir.tools/docs/how-to-protect-your-api-key)
> 
> Here are some best practices to secure your API key from unauthorized access.

### Configuration

Reservoir Market v2 is lightly configurable with the configurations below. You can either add these to a `.env.production` and `.env.development` or add env variables to a deployment platform like [vercel](https://vercel.com/).

**Environment Variables**  

| Environment Variable                  | Required | Description                                                                                                                                                                                     | Example                                                          |
| :------------------------------------ | :------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------- |
| NEXT_PUBLIC_HOST_URL                  | `true`   | The domain that the deployed project is hosted on.                                                                                                                                              | <http://localhost:3000>                                          |
| NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID | `true`   | Follow the steps [here](https://docs.walletconnect.com/2.0/web/sign/installation#1-obtain-project-id) to create a wallet connect project and retrieve the id.                                   | 0e11adav112d76d4de6f631dsa12b7321                                |
| RESERVOIR_API_KEY                     | `false`  | Reservoir API key. [Sign up here get a free API key.](https://reservoir.tools/)                                                                                                                 | 123e4567-e89b-12d3-a456-426614174000                             |
| NEXT_PUBLIC_ALCHEMY_ID                | `false`  | Alchemy API key required for removing rate limiting restrictions. Sometimes used to fetch Wallet token balance.                                                                                 | 123e4567-e89b-12d3-a456-426614174000                             |
| NEXT_PUBLIC_ETH_COLLECTION_SET_ID     | `false`  | Use this to configure a community marketplace. This will only impact the mainnet network. [Generate your collection set ID here.](https://docs.reservoir.tools/reference/postcollectionssetsv1) | f566ba09c14f56aedeed3f77e3ae7f5ff28b9177714d3827a87b7a182f8f90ff |
| NEXT_PUBLIC_GOERLI_COLLECTION_SET_ID  | `false`  | Use this to configure a community marketplace. This will only impact the goerli network. [Generate your collection set ID here.](https://docs.reservoir.tools/reference/postcollectionssetsv1)  | f566ba09c14f56aedeed3f77e3ae7f5ff28b9177714d3827a87b7a182f8f90ff |
| NEXT_PUBLIC_POLYGON_COLLECTION_SET_ID | `false`  | Use this to configure a community marketplace. This will only impact the polygon network. [Generate your collection set ID here.](https://docs.reservoir.tools/reference/postcollectionssetsv1) | f566ba09c14f56aedeed3f77e3ae7f5ff28b9177714d3827a87b7a182f8f90ff |
| NEXT_PUBLIC_ETH_COMMUNITY             | `false`  | Use this to configure a community marketplace. Note: Community IDs are only available for certain communities. This will only impact the mainnet network.                                       | artblocks                                                        |
| NEXT_PUBLIC_GOERLI_COMMUNITY          | `false`  | Use this to configure a community marketplace. Note: Community IDs are only available for certain communities. This will only impact the goerli network.                                        | artblocks                                                        |
| NEXT_PUBLIC_POLYGON_COMMUNITY         | `false`  | Use this to configure a community marketplace. Note: Community IDs are only available for certain communities. This will only impact the polygon network.                                       | artblocks                                                        |
| NEXT_PUBLIC_NORMALIZE_ROYALTIES       | `false`  | Enables royalty normalization. [Refer to docs for more info.](https://docs.reservoir.tools/docs/normalized-royalties)                                                                           | `true`, `false`                                                  |
| NEXT_PUBLIC_DATADOG_CLIENT_TOKEN      | `false`  | Datadog client token for configuring analytics.                                                                                                                                                 | pubdaddswww4dad449dadas12ada123bae                               |
| NEXT_PUBLIC_DATADOG_APPLICATION_ID    | `false`  | Datadog application id for configuring analytics.                                                                                                                                               | 123cccbb-1234-1111-4411-abc12345612afgds                         |
| NEXT_PUBLIC_MARKETPLACE_SOURCE        | `false`  | Marketplace source, used to attribute a source to orders. Must be a valid domain                                                                                                                | reservoir.tools                                                  |

In addition to the configuration above we've also added comments prefixed with `CONFIGURABLE:` throughout the app pointing out some pieces of code where you could customize functionality. After cloning the app make sure to search the repo for the aforementioned prefix.

### Deeplinking to Actions

The open source marketplace supports deeplinking to purchase actions. Deeplinking to these pages require the user to log in and if they are not on the right chain, chain switching will be prompted if necessary. Note that deeplinking to minting only works if the collection is actively minting. Below are the list of actions and how to deeplink to them:

| Action    | Url Sample                                                                                              |
| :-------- | :------------------------------------------------------------------------------------------------------ |
| **Buy**   | <https://explorer.reservoir.tools/ethereum/asset/0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:2823/buy>   |
| **Sweep** | <https://explorer.reservoir.tools/ethereum/collection/0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d/sweep> |
| **Mint**  | <https://testnets.reservoir.tools/goerli/collection/0xfa1b1b13da7d697f0c350a3b04491839954714a2/mint>    |

### Run the App

Once you have your setup ready, run:

With yarn:

```
$ yarn dev
```

With npm:

```
$ npm run dev
```

### Deploy with Vercel

This is a Next.js app that can be easily deployed using [Vercel](https://vercel.com/). For more information on how to deploy your Github repository with Vercel visit their [docs](https://vercel.com/docs/concepts/projects/overview).