# pocketbase-jsvm

## 0.40.60001

### Minor Changes

- Updated to the PocketBase 0.40.6 JSVM types
- `$app.store<T>()` now returns `store.Store<string, T>`, following upstream's new two-parameter `Store`
- Fixed the errors TypeScript reported inside `jsvm.d.ts` (TS1046 and TS2430), so it typechecks without `skipLibCheck`
- Added `scripts/patch.mjs`, which applies PATCHES.md to a freshly generated `types.d.ts`

## 0.25.10001

### Patch Changes

- e27054a: Updated to v25 JSVM
- e27054a: Removed legacy JSVM versions
- e27054a: Started a PATCHES.md to manually track patches not present in upstream

## 0.23.10002

### Patch Changes

- Support v22 and lower

## 0.23.00001

- Definitions for v23

## 0.22.20002

- b2187cd: Genericized $app.store<T>() for better cache typing

## 0.22.20001

- Converted to version anchoring
- bcfb813: Initial release

## 0.22.20-rev.1

- Initial release
