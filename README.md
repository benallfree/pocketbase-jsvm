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
