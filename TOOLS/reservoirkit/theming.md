---
title: "Theming"
slug: "theming"
excerpt: "Themes for ReservoirKit"
hidden: false
createdAt: "2023-04-18T20:48:43.889Z"
updatedAt: "2023-04-18T21:56:07.666Z"
---
ReservoirKit provides 2 preconfigured themes, darkMode and lightMode. They can be used as is or configured with some additional overrides:

```typescript
const theme = darkTheme({
  headlineFont: "Sans Serif",
  font: "Serif",
  primaryColor: "#323aa8",
  primaryHoverColor: "#252ea5",
})
```



Click [here](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/ui/src/themes/ReservoirKitTheme.ts#L73) for a full list of overrides.

If that isn't enough customization you can also create a completely custom ReservoirKitTheme.

```typescript
const theme: ReservoirKitTheme = {
  radii: { ... },
  fonts: { ... },
  colors: { ... }
}
```



### Theme Examples

Copy one of the theme objects below as a foundation for personalizing your swap widget's appearance. While doing so, consider incorporating other design elements to enhance the overall look and feel.

***



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cad7f67-midnight_blue.png",
        null,
        "Midnight Blue"
      ],
      "align": "center",
      "sizing": "500px",
      "caption": "Midnight Blue"
    }
  ]
}
[/block]

```typescript
const theme = darkTheme({
    font: 'Inter',
    primaryColor: '#4A90E2',
    primaryHoverColor: '#6EA9F6',
    headerBackground: '#283B5A',
    contentBackground: '#354766',
    footerBackground: '#283B5A',
    textColor: '#C2D2E8',
    borderColor: 'rgba(74, 144, 226, 0.2)',
    overlayBackground: 'rgba(40, 59, 90, 0.85)',
  })
```