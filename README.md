# TypeScript Typings for PocketBase JSVM

This package provides TypeScript typings for the PocketBase JavaScript Virtual Machine (JSVM), based on Goja and Goja-Node.

## Usage

Install the package:

```bash
npm install pocketbase-jsvm
```

In your `tsconfig.json`:

```json
{
  "compilerOptions": {
    "types": ["pocketbase-jsvm"],
    "moduleResolution": "node"
  }
}
```

## Important Notes

- **Limited APIs:** The JSVM supports ECMAScript 2020 and includes some custom PocketBase bindings and Goja-Node features like `require()` and `process.env`. It does **not** include Web/Browser APIs or most Node.js APIs.

- **Version Matching:** Package versions follow PocketBase versions. Since the JSVM API isn't stable yet, use the exact package version that matches your PocketBase version.

- **Avoid Unavailable Typings:** Do not use `@types/node` or include typings for unavailable APIs. Be cautious with `typeRoots` in your TypeScript configuration.

- **Independent Typings:** This package lets you reference JSVM types without relying on PocketBase's `jsvm.d.ts` in `pb_hooks`.

## Example

```typescript
// Using Goja-Node bindings
const myModule = require('myModule')
const apiKey = process.env.API_KEY

// ECMAScript 2020 features are supported
const asyncFunction = async () => {
  // Your code here
}
```

## Versioning Strategy

`pocketbase-ejs` uses [Upstream Anchoring](https://gist.github.com/benallfree/6baa35e925df06b35b2df755f5776cc7).

- **Our Version** = `Upstream MAJOR.MINOR.(Upstream PATCH × 1000 + Our Revision Number)`

Example:

- **Upstream Version**: `1.2.4`
- **Our First Revision**: `1.2.4001`

This keeps our fork aligned with upstream releases and allows us to manage our own revisions effectively.

## Updating this fork

```bash
git fetch --all
git checkout main
```

Then, copy the latest `jsvm.d.ts` and update the version number using the Upstream Anchoring technique described above.
