---
title: "Custom Marketplaces"
slug: "custom-marketplaces"
excerpt: "Leverage Reservoir to build a best-in-class custom NFT marketplace"
hidden: false
createdAt: "2022-12-22T19:08:16.326Z"
updatedAt: "2023-06-14T17:41:26.210Z"
---
Reservoir offers a range of solutions to help teams teams quickly launch custom NFT marketplaces. 

# How to Build a Custom NFT Marketplace

Typically, NFT marketplaces are built on a vertical technology stack, where a single team is responsible for frontend development, orderbook maintenance, aggregation, metadata indexing, and order execution. This leaves little time for the team to focus on the unique value proposition of the business. Reservoir introduces a new paradigm to building custom NFT marketplaces. With Reservoir, you get:

- Access to global NFT market data
- Cross-chain support (see [Supported Chains](doc:supported-chains))
- NFT order creation and execution with custom order and marketplace fees
- Aggregated liquidity from 100+ marketplaces (see [Supported Marketplaces](doc:supported-marketplaces))
- Out of the box order distribution to the Reservoir ecosystem, including OpenSea Pro

In essence, there are three ways to build a custom marketplace using Reservoir:

1. Build a custom marketplace end-to-end by leveraging the ReservoirSDK or ReservoirKit.
2. Fork and customize the Reservoir Open-source Marketplace
3. Partner with one of the white-label marketplace team building on Reservoir

We describe each of these sections in more detail below.

## Build a marketplace end-to-end using the ReservoirSDK or ReservoirKit

To build a custom marketplace end-to-end you can leverage either the Reservoir API or ReservoirKit. If you are building in React we recommend using ReservoirKit:

- [Reservoir API](https://docs.reservoir.tools/reference/overview): The Reservoir API is an all-in-one NFT data and trading API.  The Reservoir API is also wrapped into a [TS/JS SDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) with easy-to-use, performant methods. 
- [ReservoirKit (React)](https://docs.reservoir.tools/reference/reservoirkit): a React library that makes it easy build and customize your marketplace using the ReservoirKit Hooks and UI components. ReservoirKit UI components are headless, meaning you can easily customize checkout modals and more. 

## Fork the Reservoir Open-source Marketplace

[Reservoir's open-source marketplace](https://docs.reservoir.tools/reference/open-source-marketplace) is a NextJS app built using Reservoir tools and is kept up to date with new marketplace integrations and features. Developers are encouraged to use this project as a reference or fork it to make their own changes. The marketplace can be configured using environment variables, and the app can be run with Yarn or NPM. It is built with ReservoirKit, Next.js, React.js, Viem, WAGMI, and Stitches. The app can be easily deployed using Vercel, and customized further.

Learn how to fork and customize the open-source marketplace [here](https://docs.reservoir.tools/reference/open-source-marketplace).

## Partner with one of the teams building white-label NFT marketplaces on Reservoir

There are a number of great that work with Reservoir to build white-label custom NFT marketplaces. If you are interested in partnering with one, please  [reach out to us](https://twitter.com/Reservoir0x) and we can put you in contact!