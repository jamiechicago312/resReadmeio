---
title: "Security and Smart Contract Audits"
slug: "security-and-smart-contract-audits"
hidden: false
createdAt: "2022-09-21T16:58:38.260Z"
updatedAt: "2023-03-30T17:54:26.795Z"
---
### Summary

At Reservoir we take smart contract security very seriously to ensure the protection of our developers and their users. Below is a breakdown of the smart contracts used within the Reservoir ecosystem and their security/audit status.

### Aggregation

Reservoir aggregates different NFT exchange protocols, allowing you to access them all through a single, simplified interface. All supported protocols have undergone extensive audits:

- [Seaport](https://github.com/ProjectOpenSea/seaport) (used by OpenSea)
- [0xV4](https://s3.us-east-2.amazonaws.com/zeips.0x.org/audits/abdk-consulting/ABDK_0x_Solidity_v_1_0.pdf) (used by Coinbase)
- [Blur](https://docs.blur.foundation/contracts)
- [LooksRare](https://github.com/trailofbits/publications/blob/master/reviews/LooksRare.pdf)
- [X2Y2](https://docs.x2y2.io/assets/files/X2Y2_Protocol_Report-93b524ab7d8e9a000efcfeec12fc4aa4.pdf)

Full list of aggregated marketplaces can be found [here](https://docs.reservoir.tools/docs/supported-marketplaces).

### Creating Orders

When you create an order through a Reservoir-powered marketplace, the listing or bid happens through one of the above protocols. By default, Seaport is used, but each team who deploys a marketplace chooses which to use.

To list, you must approve the exchange contract to transfer your tokens. This is exactly the same as if you listed directly on another marketplace. In fact, if you have already approved a particular exchange contract through OpenSea, Coinbase or LooksRare, you don’t need to do it again on a Reservoir-powered marketplace. You’re approving the underlying exchange, not Reservoir.

### Purchasing

Single item sales are executed via the order's native exchange contract. Multi-item sales are executed through Reservoir’s Router contract, enabling users to purchase items from different marketplaces in one transaction.

Reservoir's Router contract has had the following audits:

- V3 internally audited by multiple teams, including Art Blocks and Coinbase
- V4 & V5 are minor edits to V3, based on audit feedback
- V6 audited by Consensys Dilligence ([report](https://consensys.net/diligence/audits/private/2mas58hvaujkby/reservoir-audit-2022-08.pdf) and [response](https://acrobat.adobe.com/link/review?uri=urn:aaid:scds:US:8859bea5-3770-3053-9f14-51e6d78edaa6))

_Note: V6 is currently live on Mainnet and being used by our hosted APIs._

This contract does not hold any user funds or have permission to spend user funds. All actions must be directly approved by the user, on a per transaction basis. This gives it a very different security profile to the exchange contracts above, or DeFi protocols.

### Deployed Contracts

- Mainnet: [0xc2c862322e9c97d6244a3506655da95f05246fd8](https://etherscan.io/address/0xC2c862322E9c97D6244a3506655DA95F05246Fd8#code)
- Goerli: [0xc2c862322e9c97d6244a3506655da95f05246fd8](https://goerli.etherscan.io/address/0xc2c862322e9c97d6244a3506655da95f05246fd8#code)
- Polygon: [0xc2c862322e9c97d6244a3506655da95f05246fd8](https://polygonscan.com/address/0xc2c862322e9c97d6244a3506655da95f05246fd8#code)
- Arbitrum: [0xc2c862322e9c97d6244a3506655da95f05246fd8](https://arbiscan.io/address/0xc2c862322e9c97d6244a3506655da95f05246fd8#code)
- Optimism: [0xc2c862322e9c97d6244a3506655da95f05246fd8](https://optimistic.etherscan.io/address/0xc2c862322e9c97d6244a3506655da95f05246fd8#code)

### Source Code

- [Router Contract](https://github.com/reservoirprotocol/core/blob/main/packages/contracts/contracts/router/ReservoirV6_0_0.sol)
- [Router API](https://github.com/reservoirprotocol/indexer/blob/v5/src/api/endpoints/execute/get-execute-buy/v6.ts)
- [ReservoirKit](https://github.com/reservoirprotocol/reservoir-kit)
- [Marketplace UI](https://github.com/reservoirprotocol/marketplace)