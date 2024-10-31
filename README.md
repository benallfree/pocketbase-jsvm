# TypeScript Typings for PocketBase JSVM

This package provides TypeScript typings for the PocketBase JavaScript Virtual Machine (JSVM), based on Goja and Goja-Node.

## Usage

Install the package:

```bash
npm install pocketbase-jsvm
```

### For PocketBase version matching the package version:

In your `tsconfig.json`:

```json
{
  "compilerOptions": {
    "types": ["pocketbase-jsvm"],
    "moduleResolution": "node"
  }
}
```

### For Legacy PocketBase Versions or Specific Versions

For older PocketBase versions, use triple-slash directives instead of the `types` field:

```typescript
/// <reference path="./node_modules/pocketbase-jsvm/index-v22.d.ts" />  // For v0.22
```

## Important Notes

- **Limited APIs:** The JSVM supports [most of ECMAScript 2020](https://github.com/dop251/goja/issues/608) and includes some custom PocketBase bindings and Goja-Node features like `require()` and `process.env`. It does **not** include Web/Browser APIs, most Node.js APIs, or anything related to the event loop such as `async`, `Promise`, or `setTimeout`.

- **Version Matching:** Package versions follow PocketBase versions. Since the JSVM API isn't stable yet, use the exact package version that matches your PocketBase version.

- **Avoid Unavailable Typings:** Do not use `@types/node` or include typings for unavailable APIs. Be cautious with `typeRoots` in your TypeScript configuration.

- **Independent Typings:** This package lets you reference JSVM types without relying on PocketBase's `jsvm.d.ts` in `pb_hooks`.

## Example

```typescript
// Using Goja-Node bindings
const myModule = require('myModule')
const apiKey = process.env.API_KEY

// ECMAScript 2020 features are supported
const myFunc = () => {
  // Your code here
}
```

## Versioning Strategy

`pocketbase-ejs` uses [Upstream Anchoring](https://gist.github.com/benallfree/6baa35e925df06b35b2df755f5776cc7).

- **Our Version** = `Upstream MAJOR.MINOR.(Upstream PATCH × 10000 + Our Revision Number)`

Example:

- **Upstream Version**: `0.22.22`
- **Our First Revision**: `0.22.220001`

This keeps our fork aligned with upstream releases and allows us to manage our own revisions effectively.

## Updating this fork

```bash
git fetch --all
git checkout main
```

Then, copy the latest `jsvm.d.ts` and update the version number using the Upstream Anchoring technique described above.
