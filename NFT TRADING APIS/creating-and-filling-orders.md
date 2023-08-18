---
title: "NFT Trading Overview"
slug: "creating-and-filling-orders"
excerpt: "Leverage Reservoir's Trading APIs to create and fill NFT orders."
hidden: false
createdAt: "2022-07-28T17:47:53.570Z"
updatedAt: "2023-08-15T17:51:31.700Z"
---
Reservoir gives you access to a [Global NFT Orderbook](doc:global-nft-orderbook) of NFT liquidity aggregated from across major marketplaces and chains. The NFT Trading API lets you:

- Create orders (list for sale, make an offer) with custom fees and distribute them to Reservoir ecosystem partners
- Post orders (list for sale, make an offer) on all major NFT marketplaces
- Fill orders aggregated from all major marketplaces with custom fees on top

# Using the Trading API

The Trading API is a set of rest APIs that can be used directly to create and execute liquidity. 

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](https://docs.reservoir.tools/docs/reservoir-sdk) includes helpers that abstract the process of using the Trading API such as iterating through execution steps and returning callbacks that can be used to update your UI. If you are developing in TS/JS we recommend using the ReservoirSDK.

## Step Execution using the API

When executing orders using the API directly, there are often multiple steps, like approving an exchange to access your NFTs, or wrapping WETH for a bid. These steps differ for every different type of liquidity that Reservoir supports. To make this simple, you can use the `Router` endpoints, which return the exact steps that you need to follow, including descriptions that you can display to users.

The flow looks like this:

1. Call the [Router API](https://docs.reservoir.tools/reference/postexecutebuyv7) with the action you want to take (create or fill)
2. Iterate through the steps and the items within a step, taking the necessary actions. Steps with no items, or an empty array of items, should be skipped.

As mentioned above each step contains an array of one or more items. These items need to be iterated and completed depending on the kind of step. There are two kinds of steps:

### 1. Signature

_A message that needs to be signed._ Every signature comes with `sign` data and `post` data. The first action we need to take is to sign the message, keep in mind the `signatureKind` and use the appropriate signing method. Refer to your crypto library of choice on how to sign (viem, web3, etc).

#### Example Signature contents of `signatureKind=eip191`

Creating an `EIP-191` signature involves signing a message. When you receive a `signatureKind: "eip191"` from the API, you will sign the value associated with the `message` property. In the case below, the message `Sign in to Blur...` will be signed and sent back to the API.

```javascript
// Example message returned from API
const message = {
    "signatureKind": "eip191",
    "message": "Sign in to Blur\n\nChallenge: e2483db1d9d66d2b77f47a8dfa13a15a0e7df5aee2287ade4bf313d6d4bdd0e0"
}

const eip191Message = "\x19Ethereum Signed Message:\n" + message.message.length + message.message;
```

#### Example Signature contents of `signatureKind=eip721`

Creating an EIP-721 signature involves signing a structured object composed of a domain, types, and values. When receiving a `signatureKind: "eip712"` from the API, you'll need to structure the signature in `eth_signTypedData_v4` format. Below, you'll find an example that illustrates how the domain, types, and values can be structured to create the signature.

```javascript JavaScript
const data = {
        "signatureKind": "eip712",
        "domain": {
            "name": "Seaport",
            "version": "1.5",
            "chainId": 137,
            "verifyingContract": "0x00000000000000adc04c56bf30ac9d3c0aaf14dc"
        },
        "types": {
            "OrderComponents": [
                {
                    "name": "offerer",
                    "type": "address"
                },
                {
                    "name": "zone",
                    "type": "address"
                },
                {
                    "name": "offer",
                    "type": "OfferItem[]"
                },
                {
                    "name": "consideration",
                    "type": "ConsiderationItem[]"
                },
                {
                    "name": "orderType",
                    "type": "uint8"
                },
                {
                    "name": "startTime",
                    "type": "uint256"
                },
                {
                    "name": "endTime",
                    "type": "uint256"
                },
                {
                    "name": "zoneHash",
                    "type": "bytes32"
                },
                {
                    "name": "salt",
                    "type": "uint256"
                },
                {
                    "name": "conduitKey",
                    "type": "bytes32"
                },
                {
                    "name": "counter",
                    "type": "uint256"
                }
            ],
            "OfferItem": [
                {
                    "name": "itemType",
                    "type": "uint8"
                },
                {
                    "name": "token",
                    "type": "address"
                },
                {
                    "name": "identifierOrCriteria",
                    "type": "uint256"
                },
                {
                    "name": "startAmount",
                    "type": "uint256"
                },
                {
                    "name": "endAmount",
                    "type": "uint256"
                }
            ],
            "ConsiderationItem": [
                {
                    "name": "itemType",
                    "type": "uint8"
                },
                {
                    "name": "token",
                    "type": "address"
                },
                {
                    "name": "identifierOrCriteria",
                    "type": "uint256"
                },
                {
                    "name": "startAmount",
                    "type": "uint256"
                },
                {
                    "name": "endAmount",
                    "type": "uint256"
                },
                {
                    "name": "recipient",
                    "type": "address"
                }
            ]
        },
        "value": {
            "kind": "single-token",
            "offerer": "0xd6044091d0b41efb3402ca05ba4068f969fdd9e4",
            "zone": "0x0000000000000000000000000000000000000000",
            "offer": [
                {
                    "itemType": 1,
                    "token": "0x0d500b1d8e8ef31e21c99d1db9a6444d3adf1270",
                    "identifierOrCriteria": "0",
                    "startAmount": "1000000000000000",
                    "endAmount": "1000000000000000"
                }
            ],
            "consideration": [
                {
                    "itemType": 2,
                    "token": "0x362cc74e031091992cdf0e07be54804c7cce9240",
                    "identifierOrCriteria": "32",
                    "startAmount": "1",
                    "endAmount": "1",
                    "recipient": "0xd6044091d0b41efb3402ca05ba4068f969fdd9e4"
                }
            ],
            "orderType": 0,
            "startTime": 1691165262,
            "endTime": 1691424522,
            "zoneHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "salt": "0x07b88f641d4da48b00000000000000001fc57a14aea256b9eb70bf364ce57c64",
            "conduitKey": "0x0000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f0000",
            "counter": "0",
            "signature": "0x0000000000000000000000000000000000000000000000000000000000000000"
        },
        "primaryType": "OrderComponents"
    }
```

After the message is signed the second action is to submit the `post` body to the `endpoint` provided in the `post` data. You'll also need to provide the signature that was generated from the sign data as a query parameter. If the request is successful we can mark the step item as complete.

The design pattern of this API is completely generic, allowing for automatic support of new types of liquidity without needing to update the app. This data can be fed directly into an Ethereum library such as viem, making it easy to sign and submit the exact data that is needed.

### 1.1 Sign into Blur & OpenSea

This step is a subset of the signature step (it will still have the `signature` kind). Follow the steps above on how to complete it. After completion you'll run into steps without data. These steps need to be refetched from the execute api with a query parameter called `signature` with the value being the signature returned from the Sign into Blur/OpenSea step. Once the execute api returns the next step with data you can continue to process the steps as normal. Note that steps returned before blur auth can be omitted depending on the results of the signature (you may not need to approve access for an exchange for example). Refer to the [executeSteps](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/utils/executeSteps.ts#L151) method in the SDK for more context.

### 2. Transaction

_A transaction that needs to be submitted on-chain._ After this item is complete you can poll the [Transaction Status API](https://docs.reservoir.tools/reference/gettransactionstxhashsyncedv1) to ensure that the transaction was successfully picked up by the indexer. Depending on the router api, if it's a sale or a buy transaction, you can additionally poll the [Sales API](https://docs.reservoir.tools/reference/getsalesv4) to ensure that the sale event was indexed correctly. The step item can then be successfully marked as complete.

#### Reference Material:

[JS SDK](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/utils/executeSteps.ts) 

# Options for filling orders

The listing and bid acceptance APIs (`/execute/buy` and `/execute/sell`) support a few ways of requesting transaction data for filling (any combination of the below options is accepted):

- pass a list of tokens, in which case the API will simply pick the best-priced orders that can get filled on those particular tokens
- pass a list of order ids, in which case the API will use those specific order ids
- pass a list of raw orders, in which case the API will use those specific raw orders

The first two options are self-explanatory, while the 3rd option requires the raw order data to get passed in a certain format, as follows:

- each `rawOrder` object has two fields: `kind` and `data` (the `data` field will get parsed according to the `kind`)
- both of these fields will get returned in various `orders` APIs (`/orders/asks` or `/orders/bids`): `kind` and `rawData`
- the actual schema of each the `data` field can be found in the core SDK source code, in the `order.ts` file corresponding to each [supported exchange](https://github.com/reservoirprotocol/core/tree/main/packages/sdk/src) (the `params` field in the constructor will include it)

Here's some examples:

```
[
   {
      "kind":"looks-rare",
      "data":{
         "r":"0xfa491d0e0a13dccd6467c38c890cc90f89700b587a2e678261df70e91fef0101",
         "s":"0x40ec4ecbcd26902a23325aee0e20364e55b94e42db1d9bf16c201b5bd5a916ab",
         "v":28,
         "kind":"single-token",
         "nonce":"445747",
         "price":"5800000000000000",
         "amount":"1",
         "params":"0x",
         "signer":"0x9044a0bcddbd69822f6b0d0d426ff65bbef8a1bd",
         "endTime":1675948780,
         "tokenId":"281",
         "currency":"0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
         "strategy":"0x579af6fd30bf83a5ac0d636bc619f98dbdeb930c",
         "startTime":1675941580,
         "collection":"0x63c5f88155b22e913cc46ed569edb0133aee503c",
         "isOrderAsk":true,
         "minPercentageToAsk":8500
      }
   },
   {
      "kind":"x2y2",
      "data":{
         "id":50947214,
         "nft":{
            "token":"0xeaa708c29ffce22db864385f0c6509907af45c03",
            "tokenId":"2486"
         },
         "kind":"single-token",
         "type":"sell",
         "maker":"0x6f3339eac0deb3dbc78e628c174737046498cda4",
         "price":"6400000000000000",
         "taker":"0x0000000000000000000000000000000000000000",
         "currency":"0x0000000000000000000000000000000000000000",
         "deadline":1675956570,
         "itemHash":"0xdfda59f7e3687a07b51338bd6a40d30e39c1108d1c179a7a8f9793206fc35bb2",
         "royalty_fee":50000
      }
   },
   {
      "kind":"seaport",
      "data":{
         "kind":"single-token",
         "salt":"0x360c6ebe000000000000000000000000000000000000000015b4c41d94cfd586",
         "zone":"0x004c00500000ad104d7dbd00e3ae0a5c00560c00",
         "offer":[
            {
               "token":"0x8f6a4d8ad2493adfd7d1540ccdba11bde5c7eb9e",
               "itemType":2,
               "endAmount":"1",
               "startAmount":"1",
               "identifierOrCriteria":"3577"
            }
         ],
         "counter":"0",
         "endTime":1691493881,
         "offerer":"0xbb93664780e5e4e22f5255c774bfc455ebfa789e",
         "zoneHash":"0x0000000000000000000000000000000000000000000000000000000000000000",
         "orderType":2,
         "signature":"0xb3277794bf3f113dfbaaa9e4691883a0a7c51cdea56840e906b16c0eb62c052b5a36203276d55d7279397c9a9762638ad369cd2b241da6a7babe8109ceac7979",
         "startTime":1675941882,
         "conduitKey":"0x0000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f0000",
         "consideration":[
            {
               "token":"0x0000000000000000000000000000000000000000",
               "itemType":0,
               "endAmount":"73075000000000000",
               "recipient":"0xbb93664780e5e4e22f5255c774bfc455ebfa789e",
               "startAmount":"73075000000000000",
               "identifierOrCriteria":"0"
            },
            {
               "token":"0x0000000000000000000000000000000000000000",
               "itemType":0,
               "endAmount":"1975000000000000",
               "recipient":"0x0000a26b00c1f0df003000390027140000faa719",
               "startAmount":"1975000000000000",
               "identifierOrCriteria":"0"
            },
            {
               "token":"0x0000000000000000000000000000000000000000",
               "itemType":0,
               "endAmount":"3950000000000000",
               "recipient":"0x5b5173599a2f29973397c34d01a49b3a0ee8963d",
               "startAmount":"3950000000000000",
               "identifierOrCriteria":"0"
            }
         ]
      }
   },
   {
      "kind":"nftx",
      "data":{
         "path":[
            "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
            "0x227c7df69d3ed1ae7574a1a7685fded90292eb48"
         ],
         "pool":"0x227c7df69d3ed1ae7574a1a7685fded90292eb48",
         "extra":{
            "prices":[
               "1260108297127984902",
               "1276394899256615323",
               "1292999305888243388",
               "1309929839687630165",
               "1327195097557417461",
               "1344803961553668927",
               "1362765610311681745",
               "1381089531009513537",
               "1399785531898341045",
               "1418863755430552809"
            ]
         },
         "price":"1260108297127984902",
         "amount":"1",
         "amounts":[
            
         ],
         "vaultId":"392",
         "currency":"0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
         "collection":"0x5af0d9827e0c53e4799bb226655a1de152a425a5",
         "specificIds":[
            "70"
         ]
      }
   },
   {
      "kind":"sudoswap",
      "data":{
         "pair":"0x44d2193a0f966245baa6cb9576d7b675adb5956b",
         "extra":{
            "prices":[
               "1213109641829303257"
            ]
         }
      }
   }
]
```

# Supported Actions

The following actions are possible with the Router API:

- [Buy](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell](https://docs.reservoir.tools/reference/postexecutesellv7)
- [Bid](https://docs.reservoir.tools/reference/postexecutebidv5)
- [List](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Cancel](https://docs.reservoir.tools/reference/getexecutecancelv2)