---
title: "Typescript API Typings"
slug: "typescript-api-typings"
excerpt: "Typescript API Typings Typescript Types that facilitate API interaction"
hidden: false
metadata: 
createdAt: "2023-04-06T16:16:47.592Z"
updatedAt: "2023-06-14T01:37:58.675Z"
---
Reservoir SDK comes with built in API types to facilitate interacting with Reservoir APIs. The API types are useful for parsing API responses and determining what parameters an api accepts. Note that the types are exposed as part of the Reservoir SDK package, leaving where and how you use it up to you. There's no requirement for React, or anything else, except for Typescript. Below we'll dig into some examples:

### Typing out parameters:

```typescript
import { paths } from '@reservoir0x/reservoir-sdk'

const parameters: paths['/tokens/v5']['get']['parameters']['query'] = {
  ...
}

```



With the Typescript types imported you can easily discover what query parameters an api might allow. 

### Parsing API responses:

```typescript
import { paths } from '@reservoir0x/reservoir-sdk'

const res = await fetch('https://api.reservoir.tools/tokens/v5?limit=20&collection=0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d')
const data = (await res.json())

const response = data as paths['/tokens/v5']['get']['responses']['200']['schema']

```



When it comes to converting the data returned by an api request into a typed response you can use the Typescript API types. Here we fetch from the tokens API endpoint and then cast the data into a tokens API response schema. The result is an easy to use, typed, json schema.