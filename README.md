# @iasd/bun-bake

Minimal wrapper around the [`Bun.build`](https://bun.sh/docs/bundler) API to support generating bundles as well as `.d.ts` type definitions. This library solves a very specific problem for a select group of developers.

> See: [https://github.com/oven-sh/bun/issues/5141](https://github.com/oven-sh/bun/issues/5141)

## Installing

```bash
# Install via bun
$ bun add @iasd/bun-bake,
```

> Note: You can also just copy the [./index.ts](./index.ts) file into your project.

> Note: This is a pure `bun` package, that is not useable with `NodeJs`.

## Usage

The package exposes the `build` object as well as the `Builder` class. The `build` object can be used to bundle using minimal configuration.

```ts
// .build.ts
import { build } from "@iasd/bun-bake";
import pkg from "./package.json";

await build.for('bun').from({
    // The provided package.json should have a 
    // main + module field that is used as output 
    // location for the bundle.
    ...pkg, 
    entry: './src/index.ts'
})
```

If you need to provide more configuration, you can import the `Builder` class and configure the build object yourself.

```ts
// .build.ts
import { Builder } from "@iasd/bun-bake";
import pkg from "./package.json";

const build = new Builder({ watch: false, clean: false })
await build.for('bun').from({
    ...pgk, 
    entry: './src/index.ts'
})
```

The library will generate `esm` and `cjs` as well as a `.d.ts` file by default.

To learn more about different ways to configure the builder, take a look at [the source](./index.ts).
