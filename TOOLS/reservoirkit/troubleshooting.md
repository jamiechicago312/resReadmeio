---
title: "Troubleshooting"
slug: "troubleshooting"
excerpt: "Having issues with ReservoirKit? Make sure to check this guide first."
hidden: false
createdAt: "2023-04-18T20:48:54.253Z"
updatedAt: "2023-08-15T18:02:19.103Z"
---
# Nextjs commonjs module error

`SyntaxError: Named export 'Arrow' not found. The requested module '@radix-ui/react-popover' is a CommonJS module, which may not support all module.exports as named exports.
CommonJS modules can always be imported via the default export, for example using:`

ReservoirKit UI 0.7+ uses esmodules and drops commonjs module support in order to support wagmi 0.8+. The error message may vary but will always suggest importing the package differently. This is an issue when using ReservoirKit UI in a nextjs application. This issue is not specific to the ReservoirKit UI package and is impacting many other [projects](https://github.com/ant-design/ant-design-mobile/blob/3c87f1c5b16c39c70e494159732f6bb1f0a08c01/docs/guide/ssr.en.md) that have switched to esmodules. Thankfully there are a couple of solutions to solve the issue above:

**Next 13+**

```
// next.config.js
const nextConfig = {
  experimental: {
    transpilePackages: ['@reservoir0x/reservoir-kit-ui'],
  },
};

module.exports = nextConfig;
```

This solution uses the experimental nextjs flag to transpile packages to whatever nextjs's packager is expecting. Add the flag to your next.config.js file.

<https://beta.nextjs.org/docs/api-reference/next.config.js#transpilepackages>

**Nextjs 12 and below:**  
`yarn add -D next-transpile-modules`

```
const withTM = require('next-transpile-modules')([
  '@reservoir0x/reservoir-kit-ui',
]);

module.exports = withTM({
  // other Next.js configuration in your project
});
```

Older versions of Nextjs don't have the luxury of a simple flag, instead you need to install the `next-transpile-modules` plugin and add the following code to your next.config.js file.

# TypeScript `skipLibCheck`

***

**`reservoir-sdk` & `reservoir-kit-ui` Dependency Notice**

`reservoir-sdk` & `reservoir-kit-ui` both integrate types from their child-dependencies. Unfortunately, some of these dependencies have .d.ts files with potentially inaccurate or incorrect type declarations. As a result, when our libraries import these types, discrepancies and build errors can arise.

To mitigate this, please set `skipLibCheck: true` in your `tsconfig.json` file. This will skip the type checking of those child dependencies .d.ts files and resolve the errors.  Here's an example of two errors that might be emitted due to these type declaration inconsistencies: 

`node_modules/viem/dist/types/actions/wallet/writeContract.d.ts:12:683 - error TS2536: Type '"value"' cannot be used to index type 'SendTransactionParameters<TChain, TAccount, TChainOverride>'.` 

`node_modules/@stitches/react/types/stitches.d.ts:53:79 - error TS2503: Cannot find namespace 'React'.53    string extends Composers[K] ? Composers[K] \: Composers[K] extends string | React.ComponentType<any> | Util.Function ? Composers[K] \: RemoveIndex<CSS> & {`

To learn more about the `skipLibCheck` compiler option checkout [TypeScripts documentation](https://www.typescriptlang.org/tsconfig#skipLibCheck).