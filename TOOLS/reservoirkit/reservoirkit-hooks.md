---
title: "ReservoirKit Hooks"
slug: "reservoirkit-hooks"
excerpt: "ReservoirKit comes with powerful hooks to make accessing Reservoir data simple and efficient."
hidden: false
createdAt: "2023-04-18T20:43:59.421Z"
updatedAt: "2023-06-14T05:35:20.928Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit)

# SWR powered hooks

These hooks use [SWR](https://swr.vercel.app/), a performant lightweight data-fetching hook library. Using SWR means that we can cache requests, batch requests and use powerful features developed and tested by the SWR team. You can utilize hooks across your components without worrying about performance or duplicate network requests. You can also pass in SWR configuration [options](https://swr.vercel.app/docs/options#options) to each SWR powered hook. Below are the properties returned in each SWR powered hook.

**response**: The response returned from the api  
**data**: The data extracted from the response  
**mutate**: SWR's [mutate](https://swr.vercel.app/docs/mutation) function for refreshing data.  
**error**: An api error  
**isValidating**: If there's an ongoing request or revalidation

[useCollections](doc:usecollections)  
[useAttributes](doc:useattributes)

# Infinite Loading Hooks

The following hooks are built with infinite loading in mind. They expose a some useful methods and properties to build an infinite loading UX, in addition to the [properties](https://swr.vercel.app/docs/pagination#return-values) returned by all SWR infinite powered hooks.

**hasNextPage**: If there is more data to load  
**isFetchingInitialData**: If the initial data has been fetched or not  
**isFetchingPage**: If data is currently being fetched  
**fetchNextPage**: A method to fetch the next page, takes no parameters.  
**resetCache**: A method to clear the SWR cache, resets the page to 0. Calling fetchNextPage will behave like the first time the hook was called

<https://swr.vercel.app/docs/pagination#return-values>

[useTokens](https://docs.reservoir.tools/reference/reservoirkit-hooks#usetokens)  
[useListings](https://docs.reservoir.tools/reference/reservoirkit-hooks#uselistings)  
[useOwnerListings](https://docs.reservoir.tools/reference/reservoirkit-hooks#useownerlistings)  
[useBids](https://docs.reservoir.tools/reference/reservoirkit-hooks#usebids)  
[useUserTopBids](https://docs.reservoir.tools/reference/reservoirkit-hooks#useusetopbids)  
[useCollectionActivity](https://docs.reservoir.tools/reference/reservoirkit-hooks#usecollectionactivity)  
[useUsersActivity](https://docs.reservoir.tools/reference/reservoirkit-hooks#useusersactivity)  
[useUserCollections](https://docs.reservoir.tools/reference/reservoirkit-hooks#useusercollections)  
[useUserTokens](https://docs.reservoir.tools/reference/reservoirkit-hooks#useusertokens)  
[useTokenActivity](https://docs.reservoir.tools/reference/reservoirkit-hooks#usetokenactivity)

# Utility Hooks

Just like every good tool belt there are usually some utility hooks included. These hooks don't necessarily fetch Reservoir data but they are quite useful.

[useReservoirClient](https://docs.reservoir.tools/reference/reservoirkit-hooks#usereservoirclient)

# Manually overriding chain endpoint

The hooks above fetch data from the default chain configured in the `ReservoirKitProvider`, read more on that [here](https://docs.reservoir.tools/reference/reservoirkit). You can also manually override the chainId for all of these hooks to fetch specific data. Please note that the manually overridden chain needs to be in the list of chains passed to the provider.

# useTokens

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks) and also handles [infinite loading UX](https://docs.reservoir.tools/reference/reservoirkit-hooks#infinite-loading-hooks). Use this hook to fetch token details, using the [Tokens](ref:gettokensv5) endpoint. It takes a query parameter which maps to the same parameters that the api endpoint uses.

```typescript
import { useTokens } from '@reservoir0x/reservoir-kit-ui'

const { data: tokens } = useTokens({
  tokens: ["0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb:1"],
})
```

# useCollections

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch a collection, using the [Collections](ref:collections) endpoint. It takes a query parameter which maps to the same parameters that the api endpoint uses.

```typescript
import { useCollections } from '@reservoir0x/reservoir-kit-ui'

const { data: collection } = useCollections({
  id: "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb",
})
```

# useCollectionActivity

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch a collection's activity, using the [Collection Activity](https://docs.reservoir.tools/reference/getcollectionsactivityv5) endpoint. It takes the collection ID, as the first parameter, an optional query object which maps to the same parameters that the API endpoint uses, as the second parameter, and an optional [SWR Infinite](https://swr.vercel.app/docs/pagination#useswrinfinite) configuration object, as the third parameter.

```typescript
import { useCollectionActivity } from '@reservoir0x/reservoir-kit-ui'

const { data: activity } = useCollectionActivity(
  "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb"
)
```

# useUsersActivity

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch a single user or multiple user's activity, using the [Users Activity](ref:getusersactivityv5) endpoint. It takes an array of users (i.e. wallet addresses), as the first parameter, an optional query object which maps to the same parameters that the API endpoint uses, as the second parameter, and an optional [SWR Infinite](https://swr.vercel.app/docs/pagination#useswrinfinite) configuration object, as the third parameter.

```typescript
import { useUsersActivity } from '@reservoir0x/reservoir-kit-ui'

const { data: activity } = useUsersActivity(
  ["0xFd03726FD90ccc7386bf62b44Bb594f7cbFB3995"]
)
```

# useTokenActivity

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch a token's activity, using the [Token Activity](https://docs.reservoir.tools/reference/gettokenstokenactivityv4) endpoint. It takes the collection ID appended to the token ID (collectionID:tokenID), as the first parameter, an optional query object which maps to the same parameters that the API endpoint uses, as the second parameter, and an optional [SWR Infinite](https://swr.vercel.app/docs/pagination#useswrinfinite) configuration object, as the third parameter.

```typescript
import { useTokenActivity } from '@reservoir0x/reservoir-kit-ui'

const { data: activity } = useTokenActivity(
  "0x744df993f93c89801cadbea8a4a3fd2b4a443d2c:1793"
)
```

# useListings

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks) and also handles [infinite loading UX](https://docs.reservoir.tools/reference/reservoirkit-hooks#infinite-loading-hooks). Use this hook to fetch listings, using the [Asks (listings)](ref:getordersasksv4) endpoint. It takes a query parameter which maps to the same parameters that the api endpoint uses.

```typescript
import { useListings } from '@reservoir0x/reservoir-kit-ui'

 const {
   data: listings,
   fetchNextPage,
   hasNextPage,
 } = useListings({
    contracts: ['0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb'],
 })
```

To skip this hook, you can pass in false for the enabled parameter. Use the code snippet below:

```typescript
export default function (
  options: AsksQuery,
  swrOptions: SWRInfiniteConfiguration = {},
  enabled: boolean = true,
  chainId?: number
)

useListings(options, swrOptions, enabled, chainId)
```

# useOwnerListings

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks) and also handles [infinite loading UX](https://docs.reservoir.tools/reference/reservoirkit-hooks#infinite-loading-hooks). The hook is an extension of the [useListings](https://docs.reservoir.tools/reference/reservoirkit-hooks#uselistings) hook. It's a convenient way to fetch the listings that belong to the currently connected wallet. The parameters are exactly the same as the aforementioned useListings hook.

```typescript
import { useOwnerListings } from '@reservoir0x/reservoir-kit-ui'

 const {
   data: listings,
   fetchNextPage,
   hasNextPage,
 } = useOwnerListings()
```

# useReservoirClient

This hook exposes the underlying ReservoirKit client which is in charge of making the underlying execute requests and interacting with web3 interfaces. The hook can also be useful to get the underlying global configuration of ReservoirKit (apiBase, apiKey etc).

```typescript
import { useReservoirClient } from '@reservoir0x/reservoir-kit-ui'

const client = useReservoirClient()
console.log(client?.apiBase)
```

It can also be useful to trigger actions in a flexible way. Actions are the underlying execute apis that ReservoirKit's ui triggers. Here's an example of how to trigger the underlying execute/buy api.

```typescript
import { useReservoirClient } from '@reservoir0x/reservoir-kit-ui'

const client = useReservoirClient()
await reservoirClient.actions
      .buyToken({
        ...
      })
      .then(()=> {})
      .catch(() => {})
```

# useAttributes

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch collection attributes, using the [All Attributes](ref:getcollectionscollectionattributesallv2) endpoint. It takes a query parameter which maps to the same parameters that the api endpoint uses.

```typescript
import { useAttributes } from '@reservoir0x/reservoir-kit-ui'

  const attributes = useAttributes(collectionId)
```

# useBids

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks) and also handles [infinite loading UX](https://docs.reservoir.tools/reference/reservoirkit-hooks#infinite-loading-hooks). Use this hook to fetch bids, using the [Bids (offers)](ref:getordersbidsv5) endpoint. It takes a query parameter which maps to the same parameters that the api endpoint uses.

| Parameter      | Type                                                                     |
| :------------- | :----------------------------------------------------------------------- |
| **options**    | [Bids (offers) options](ref:getordersbidsv4)                             |
| **swrOptions** | [SWR Options](https://docs.reservoir.tools/docs/hooks#swr-powered-hooks) |
| **enabled**    | Boolean                                                                  |

```typescript
import { useBids } from '@reservoir0x/reservoir-kit-ui'

 const {
   data: bids,
   fetchNextPage,
   hasNextPage,
 } = useBids({
    contracts: ['0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb'],
 })
```

# useUseTopBids

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks) and also handles [infinite loading UX](https://docs.reservoir.tools/reference/reservoirkit-hooks#infinite-loading-hooks). Use this hook to fetch a single user’s top bids, using the [User Top Bids](https://docs.reservoir.tools/reference/getordersusersusertopbidsv2) endpoint. It takes in a user, as the first parameter, a query object which maps to the same parameters that the API endpoint uses, as the second parameter, and an optional SWR Infinite configuration object, as the third parameter.

| Parameter      | Type                                                                                        |
| :------------- | :------------------------------------------------------------------------------------------ |
| **user**       | string                                                                                      |
| **options**    | [User Top Bids options](https://docs.reservoir.tools/reference/getordersusersusertopbidsv1) |
| **swrOptions** | [SWR Options](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks)  |

```typescript
import { useUserTopBids } from '@reservoir0x/reservoir-kit-ui'

 const {
   data: bids,
   fetchNextPage,
   hasNextPage,
 } = useUserTopBids('0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00', {})
```

# useUserCollections

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch a single user's collections using the [Users Collections](ref:getusersusercollectionsv2) endpoint. It takes an address, as the first parameter, an optional query object which maps to the same parameters that the API endpoint uses, as the second parameter, and an optional [SWR Infinite](https://swr.vercel.app/docs/pagination#useswrinfinite) configuration object, as the third parameter.

```typescript
import { useUserCollections } from '@reservoir0x/reservoir-kit-ui'

const { data: collections } = useUserCollections("0xFd03726FD90ccc7386bf62b44Bb594f7cbFB3995")
```

# useUserTokens

This hook is [SWR powered](https://docs.reservoir.tools/reference/reservoirkit-hooks#swr-powered-hooks). Use this hook to fetch a single user's tokens using the [Users Tokens](https://docs.reservoir.tools/reference/getusersusertokensv6) endpoint. It takes an address, as the first parameter, an optional query object which maps to the same parameters that the API endpoint uses, as the second parameter, and an optional [SWR Infinite](https://swr.vercel.app/docs/pagination#useswrinfinite) configuration object, as the third parameter.

```typescript
import { useUserTokens } from '@reservoir0x/reservoir-kit-ui'

const { data: tokens } = useUserTokens("0xFd03726FD90ccc7386bf62b44Bb594f7cbFB3995")
```

# useCart

Make sure you've installed ReservoirKit and followed the [installation steps](https://docs.reservoir.tools/reference/installing-reservoirkit) for adding a cart to your application.

This hook interacts with the CartProvider to expose the cart state and some useful methods to manage the cart.

```typescript
import { useCart } from '@reservoir0x/reservoir-kit-ui'

  const { data, clear, clearTransaction, validate, remove, add, checkout } =
    useCart((cart) => cart)
```

The hook takes one parameter, which is a selector. To make the hook performant we've given developers the ability to select a piece of state to get updates on. This means that the hook won't trigger unnecessary rerenders. In the example above we select the whole state but if you simply want to just get the items you can do something like this:

```
import { useCart } from '@reservoir0x/reservoir-kit-ui'

  const { data: items } =
    useCart((cart) => cart.items)
```

The code above will just expose the items and only rerender when the items in the cart change. Let's dig into some of the methods returned by the hook:

| Method               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **add**              | You can use this method to add multiple items to the cart. There are two interfaces that the method accepts. An array of tokens matching the interface from the [tokens hook](https://docs.reservoir.tools/reference/reservoirkit-hooks#usetokens) or a simplified interface where the cart needs to fetch the token data asynchronously. This could impact UX but is easier to implement in scenarios where the token info is not already prefetched. The second parameter the function takes is the chain id for the tokens.                                                                           |
| **remove**           | You can use this method for removing an item from the cart. Just pass an array of objects with an id property, which is just a combination of the token collection id and the token id delimited by a colon (`:`).                                                                                                                                                                                                                                                                                                                                                                                       |
| **validate**         | This method validates the cart by checking if all the tokens have valid listings.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **checkout**         | Use this method to checkout valid tokens in the cart. If the transaction fails before being submitted then the tokens will not be removed from the cart. You can pass an object of options that map to the [execute buy endpoint](https://docs.reservoir.tools/reference/postexecutebuyv6). Once this method is called the transaction object will be added to the cart which has information around the transaction hash and the status of the transaction. You can observe and react to this state to give your users an update on the pending transaction. Only one transaction is tracked at a time. |
| **clear**            | Clears all the items in the cart.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **clearTransaction** | Clears the pending transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

```typescript
import { useCart } from '@reservoir0x/reservoir-kit-ui'

  const { data, clear, clearTransaction, validate, remove, add, checkout } =
    useCart((cart) => cart)
  const tokens = useTokens({collection: "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb"})

//add: Simplified interface
add([{id: "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb:1"}], 1)

//add: Optimized interface
add([tokens[0]], 1)

remove(["0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb:1"])
checkout({ ...buyEndpointOptions })
validate()
clear()
clearTransaction()
```

# useDynamicTokens

While you can have a cart and use the [useTokens](https://docs.reservoir.tools/reference/reservoirkit-hooks#usetokens) hook to display a grid of tokens, this hook is specifically designed to make it easier to use the cart in a token grid. The hook handles the following things:

- Sorting the tokens if a token in a dynamically priced pool is in the cart
- Automatically returning cart actions from the [useCart](https://docs.reservoir.tools/reference/reservoirkit-hooks#usecart) hook
- Adding a `isInCart` boolean property to each token to make it easier to display which token is in the cart

```typescript
import { useDynamicTokens } from '@reservoir0x/reservoir-kit-ui'

const { data: tokens, add, remove } = useDynamicTokens({
  collection: "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb",
})

//Display the tokens in your app
```