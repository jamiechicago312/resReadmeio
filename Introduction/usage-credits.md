---
title: "Usage Credits"
slug: "usage-credits"
excerpt: "What are usage credits and how to use them."
hidden: false
createdAt: "2023-05-15T20:17:39.663Z"
updatedAt: "2023-06-06T21:18:50.271Z"
---
# What are credits?

Credits are a unit of measurement that represent the computational resources your apps are consuming on Reservoir. Not all API queries are equal and some can be far more lightweight than others. Credits allow us to more fairly weigh different queries and actions and ensure you're only paying for what you need. 

To keep things as simple as possible, **most requests cost 1 credit**. Only a handful of computationally heavy endpoints are priced higher (see below).

# What are additional credits?

Each subscription plan offers a certain amount of included credits that resets with each billing cycle. Additional credits can be consumed and will be charged to your account at the end of the billing cycle. For more information about included credit amounts and additional credits costs for each subscription plan, [visit our pricing page](https://reservoir.tools/pricing).

# What are rate limits and how are they measured?

Rate limits are designed to protect the Reservoir network from abuse. Each subscription plan is offered a certain amount of credits that can be consumed every second (credits per second) for each of your apps (api key). For more information about credits per second for each subscription plan, [visit our pricing page](https://reservoir.tools/pricing).

# How do I monitor my usage?

You can monitor your company's credit usage from the current and previous billing cycle in the [Developer Dashboard's usage & billing section](https://dashboard.reservoir.tools/usage-and-billing?tab=usage). 

# Endpoint costs

Each API query uses a different amount of computational resources. See costs breakdown of each API endpoint below:

## Collections

| Route                                                                                                                                         | Base Cost         | Extra Costs |
| :-------------------------------------------------------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/collections/\*](https://docs.reservoir.tools/reference/getcollectionsv5)                                                                    | 1 credits/request |             |
| [/search/collections/\*](https://docs.reservoir.tools/reference/getsearchcollectionsv2)                                                       | 1 credits/request |             |
| [/collections/{collection}/supported-marketplaces/\*](https://docs.reservoir.tools/reference/getcollectionscollectionsupportedmarketplacesv1) | 1 credits/request |             |
| [/users/{user}/collections/\*](https://docs.reservoir.tools/reference/getusersusercollectionsv3)                                              | 1 credits/request |             |
| [/collections/{collection}/community/\*](https://docs.reservoir.tools/reference/putcollectionscollectioncommunityv1)                          | 1 credits/request |             |
| [/collections-sets/\*](https://docs.reservoir.tools/reference/postcollectionssetsv1)                                                          | 1 credits/request |             |
| [/contracts-sets/\*](https://docs.reservoir.tools/reference/postcontractssetsv1)                                                              | 1 credits/request |             |
| [/collections/refresh/\*](https://docs.reservoir.tools/reference/postcollectionsrefreshv2)                                                    | 1 credits/request |             |

## Tokens

| Route                                                                                    | Base Cost         | Extra Costs |
| :--------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/tokens/\*](https://docs.reservoir.tools/reference/gettokensv6)                         | 1 credits/request |             |
| [/tokens/bootstrap/\*](https://docs.reservoir.tools/reference/gettokensbootstrapv1)      | 1 credits/request |             |
| [/tokens/floor/\*](https://docs.reservoir.tools/reference/gettokensfloorv1)              | 1 credits/request |             |
| [/tokens/ids/\*](https://docs.reservoir.tools/reference/gettokensidsv1)                  | 1 credits/request |             |
| [/tokens/flag/changes/\*](https://docs.reservoir.tools/reference/gettokensflagchangesv1) | 1 credits/request |             |
| [/users/{user}/tokens/\*](https://docs.reservoir.tools/reference/getusersusertokensv7)   | 1 credits/request |             |
| [/token-sets/\*](https://docs.reservoir.tools/reference/posttokensetsv2)                 | 1 credits/request |             |
| [/tokens/refresh/\*](https://docs.reservoir.tools/reference/posttokensrefreshv1)         | 1 credits/request |             |

## Orders

| Route                                                                                                  | Base Cost         | Extra Costs |
| :----------------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/orders/asks/\*](https://docs.reservoir.tools/reference/getordersasksv4)                              | 1 credits/request |             |
| [/orders/bids/\*](https://docs.reservoir.tools/reference/getordersbidsv5)                              | 1 credits/request |             |
| [/orders/depth/\*](https://docs.reservoir.tools/reference/getordersdepthv1)                            | 1 credits/request |             |
| [/orders/users/{user}/top-bids/\*](https://docs.reservoir.tools/reference/getordersusersusertopbidsv4) | 1 credits/request |             |

## Events

| Route                                                                                                     | Base Cost         | Extra Costs |
| :-------------------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/events/asks/\*](https://docs.reservoir.tools/reference/geteventsasksv3)                                 | 1 credits/request |             |
| [/events/bids/\*](https://docs.reservoir.tools/reference/geteventsbidsv3)                                 | 1 credits/request |             |
| [/events/collections/floor-ask/\*](https://docs.reservoir.tools/reference/geteventscollectionsflooraskv2) | 1 credits/request |             |
| [/events/collections/top-bid/\*](https://docs.reservoir.tools/reference/geteventscollectionstopbidv2)     | 1 credits/request |             |
| [/events/tokens/floor-ask/\*](https://api.reservoir.tools/events/tokens/floor-ask/v4)                     | 1 credits/request |             |

## Execute (Buy & Sell)

| Route                                                                                                    | Base Cost          | Extra Costs |
| :------------------------------------------------------------------------------------------------------- | :----------------- | :---------- |
| [/execute/ask/\*](https://docs.reservoir.tools/reference/postexecutelistv5)                              | 1 credits/request  |             |
| [/execute/bid/\*](https://docs.reservoir.tools/reference/postexecutebidv5)                               | 1 credits/request  |             |
| [/execute/cancel/\*](https://docs.reservoir.tools/reference/postexecutecancelv3)                         | 1 credits/request  |             |
| [/execute/buy/\*](https://docs.reservoir.tools/reference/postexecutebuyv7)                               | 10 credits/request |             |
| [/execute/sell/\*](https://docs.reservoir.tools/reference/postexecutesellv7)                             | 10 credits/request |             |
| [/order/\*](https://docs.reservoir.tools/reference/postorderv4)                                          | 1 credits/request  |             |
| [/cross-posting-orders/\*](https://docs.reservoir.tools/reference/getcrosspostingordersv1)               | 1 credits/request  |             |
| [/transactions/{txHash}/synced/\*](https://docs.reservoir.tools/reference/gettransactionstxhashsyncedv1) | 1 credits/request  |             |

## Activity

| Route                                                                                          | Base Cost         | Extra Costs |
| :--------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/activity/\*](https://docs.reservoir.tools/reference/getactivityv5)                           | 1 credits/request |             |
| [/collections/activity/\*](https://docs.reservoir.tools/reference/getcollectionsactivityv6)    | 1 credits/request |             |
| [/tokens/{token}/activity/\*](https://docs.reservoir.tools/reference/gettokenstokenactivityv5) | 1 credits/request |             |
| [/users/activity/\*](https://docs.reservoir.tools/reference/getusersactivityv6)                | 1 credits/request |             |

## Sales & Transfers

| Route                                                                           | Base Cost         | Extra Costs |
| :------------------------------------------------------------------------------ | :---------------- | :---------- |
| [/sales/\*](https://docs.reservoir.tools/reference/getsalesv5)                  | 1 credits/request |             |
| [/transfers/\*](https://docs.reservoir.tools/reference/gettransfersv3)          | 1 credits/request |             |
| [/transfers/bulk/\*](https://docs.reservoir.tools/reference/gettransfersbulkv1) | 1 credits/request |             |

## Owners

| Route                                                                                                                                                        | Base Cost         | Extra Costs |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/owners/\*](https://docs.reservoir.tools/reference/getownersv2)                                                                                             | 1 credits/request |             |
| [/owners/common-collections/\*](https://docs.reservoir.tools/reference/getownerscommoncollectionsv1)                                                         | 1 credits/request |             |
| [/owners/cross-collections/\*](https://docs.reservoir.tools/reference/getownerscrosscollectionsv1)                                                           | 1 credits/request |             |
| [/collections/{collection}/owners-distribution/\*](https://docs.reservoir.tools/reference/getcollectionscollectionownersdistributionv1)                      | 1 credits/request |             |
| [/collections-sets/{collectionsSetId}/owners-distribution/\*](https://docs.reservoir.tools/reference/getcollectionssetscollectionssetidownersdistributionv1) | 1 credits/request |             |

## Stats

| Route                                                                                                | Base Cost         | Extra Costs |
| :--------------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/stats/\*](https://docs.reservoir.tools/reference/getstatsv2)                                       | 1 credits/request |             |
| [/collections/daily-volumes/\*](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) | 1 credits/request |             |
| [/liquidity/users/\*](https://docs.reservoir.tools/reference/getliquidityusersv2)                    | 1 credits/request |             |

## Sources

| Route                                                              | Base Cost         | Extra Costs |
| :----------------------------------------------------------------- | :---------------- | :---------- |
| [/sources/\*](https://docs.reservoir.tools/reference/getsourcesv1) | 1 credits/request |             |

## Oracle

| Route                                                                                                     | Base Cost         | Extra Costs |
| :-------------------------------------------------------------------------------------------------------- | :---------------- | :---------- |
| [/oracle/collections/floor-ask/\*](https://docs.reservoir.tools/reference/getoraclecollectionsflooraskv5) | 1 credits/request |             |
| [/oracle/collections/top-bid/\*](https://docs.reservoir.tools/reference/getoraclecollectionstopbidv2)     | 1 credits/request |             |
| [/oracle/tokens/status/\*](https://docs.reservoir.tools/reference/getoracletokensstatusv2)                | 1 credits/request |             |

## Utility

| Route                                                                                                   | Base Cost         | Extra Costs |
| :------------------------------------------------------------------------------------------------------ | :---------------- | :---------- |
| [/api-keys/{key}/rate-limits](https://docs.reservoir.tools/reference/getapikeyskeyratelimits)           | 1 credits/request |             |
| [/tokens/flag/\*](https://docs.reservoir.tools/reference/posttokensflagv1)                              | 1 credits/request |             |
| [/management/orders/simulate/\*](https://docs.reservoir.tools/reference/postmanagementorderssimulatev1) | 1 credits/request |             |
| [/execute/auth-signature/\*](https://docs.reservoir.tools/reference/postexecuteauthsignaturev1)         | 1 credits/request |             |
| [/execute/cancel-signature/\*](https://docs.reservoir.tools/reference/postexecutecancelsignaturev1)     | 1 credits/request |             |