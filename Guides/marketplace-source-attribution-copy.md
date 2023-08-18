---
title: "How to Set Custom Marketplace Source Metadata"
slug: "marketplace-source-attribution-copy"
hidden: false
createdAt: "2023-04-06T21:32:45.320Z"
updatedAt: "2023-05-05T15:19:59.595Z"
---
By default Reservoir will automatically create source metadata for every new source that creates or fills an order. However it is possible to overwrite these defaults by setting your own custom source metadata using Reservoir meta tags.

The `reservoir:title` meta tag should map to a human readable marketplace name. If nothing is provided then the domain is used instead.

```html
<meta property="reservoir:title" content="Reservoir Marketplace" />
```



Use the `reservoir:icon` meta tag to override the icon that the reservoir orderbook uses to display your marketplace logo. If nothing is provided then the favicon is used by default. The url can either be relative or absolute.

```html
<meta
  property="reservoir:icon"
  content="https://api.reservoir.tools/redirect/sources/reservoir/logo/v2"
/>
```



The `reservoir:token-url-x` meta tag is used to provide a url for the indexer to redirect to the correct token page. It can either be an absolute or a relative url. Replace `x` with the name of your chain (mainnet, goerli etc) and keep the two required keys (`contract` and `tokenId`). These keys are meant to be a placeholder for the indexer to replace when generating the url.  This api redirects to the given url: [Redirect response to the given source token page](ref:getredirectsourcessourcetokenstokenlinkv2)

```html
<meta
  property="reservoir:token-url-mainnet"
  content="https://reservoir.market/${contract}/${tokenId}"
/>

<meta
  property="reservoir:token-url-goerli"
  content="https://dev.reservoir.market/${contract}/${tokenId}"
/>

<meta
  property="reservoir:token-url-polygon"
  content="https://polygon.reservoir.market/${contract}/${tokenId}"
/>
```