---
title: "RenderTokenMedia"
slug: "rendertokenmedia"
excerpt: "Render any token media, supports a wide range of media types using the RenderTokenMedia component"
hidden: false
createdAt: "2023-04-18T21:44:44.371Z"
updatedAt: "2023-07-19T21:56:57.132Z"
---
# Prerequisites ⚙️

[Install and configure ReservoirKit](https://docs.reservoir.tools/reference/installing-reservoirkit).

# RenderTokenMedia

TokenMedia is a component that renders a token in an easy and customizable way. Use this component in various layouts while not having to implement your own rendering logic. Below is a list of component properties:

[block:parameters]
{
  "data": {
    "h-0": "Prop",
    "h-1": "Description",
    "0-0": "**token**",
    "0-1": "This is a token object mapping out to a Token object returned from the [tokensv5 api](/reference/gettokensv5). The only required parameters properties from that object are `image`, `media` and `collection`. Without this property the component will not render",
    "1-0": "**staticOnly**",
    "1-1": "A boolean prop that controls showing a static image preview instead of displaying the token media",
    "2-0": "**imageResolution**",
    "2-1": "`small` `medium` `large`",
    "3-0": "**style**",
    "3-1": "An inline style prop override that's applied to the container of the rendered component",
    "4-0": "**className**",
    "4-1": "A string that applies a class to the container of the rendered component",
    "5-0": "**modelViewerOptions**",
    "5-1": "An object containing additional attributes to control the model-viewer. Refer to the [model-viewer docs](https://modelviewer.dev/docs/index.html#loading-attributes) for more information",
    "6-0": "**videoOptions**",
    "6-1": "An object containing additional HTML5 video attributes. Refer to the [docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video) for more information",
    "7-0": "**audioOptions**",
    "7-1": "An object containing additional HTML5 audio attributes. Refer to the [docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) for more information",
    "8-0": "**iframeOptions**",
    "8-1": "An object containing additional HTML5 iframe attributes. Refer to the [docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) for more information",
    "9-0": "**fallback**",
    "9-1": "A function that passes in a media type and expects a ReactElement or null. Use this prop to override the default fallback per media type. If null is returned then the default fallback if used.",
    "10-0": "**fallbackMode**",
    "10-1": "`default`: Displays the collection image, a 'No content Available' description as well as a button to refresh the metadata.  \n`simple`: Displays an image icon",
    "11-0": "**disableOnChainRendering**",
    "11-1": "If a token's image metadata is missing, the TokenMedia component will call the contract's tokenURI function directly to try and resolve the image before falling back to the fallback. You can disable this logic with the `disableOnChainRendering` prop",
    "12-0": "**onError**",
    "12-1": "A callback whenever an error occurs loading the media or preview.",
    "13-0": "**onRefreshToken**",
    "13-1": "A callback for the default fallback UI that the user decided to refresh the token metadata. You can use this to display a notification and give the user some feedback."
  },
  "cols": 2,
  "rows": 14,
  "align": [
    "left",
    "left"
  ]
}
[/block]

## List of supported media types

- mp4
- wav, mp3
- gltf, glb
- png, jpeg, jpg, gif, svg
- html

## Usage

```typescript
import { TokenMedia, useTokens } from '@reservoir0x/reservoir-kit-ui'

...

  const { data: tokens } = useTokens({
    collection: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"
  })
  

	return (tokens.map((token, i) => (
    <TokenMedia
      key={i}
      token={token?.token}
    />
  )))
```

In the example above we import `TokenMedia` and [useTokens](https://docs.reservoir.tools/reference/reservoirkit-hooks#usetokens) hook. We then use the `useTokens` hook to fetch the token data for a given collection. Finally we iterate over the tokens and use the `TokenMedia` component to render the tokens, passing in the token prop.

## Advanced Usage

In some cases you may want to override one particular media type (video for example) and render it in your own player or layer some additional controls. To support this use case we export a utility function to extract the media type from the token object:

```typescript
import { TokenMedia, useTokens, extractMediaType } from '@reservoir0x/reservoir-kit-ui'

...

  const { data: tokens } = useTokens({
    collection: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"
  })
  

	return (tokens.map((token, i) => {
   	const mediaType = extractMediaType(token) 
    
    if (mediaType === 'mp4') {
      return <CustomVideoComponent/>
    }
    
		return (<TokenMedia
      key={i}
      token={token?.token}
    />)
  }))
```