# Patches

`jsvm.d.ts` is the `types.d.ts` that PocketBase generates, with these fixes applied by [`scripts/patch.mjs`](./scripts/patch.mjs):

| Patch | Why |
| --- | --- |
| `store<T = any>(): store.Store<string, T>` | Lets callers type the values they keep in the app store, e.g. `$app.store<Cache>()` |
| `expandRecords(..., optFetchFunc?: ExpandFetchFunc)` | The fetch function is optional at runtime but generated as required |
| `MetaConfig.appUrl` alongside `appURL` | Older code reads `appUrl` |
| `declare namespace` for top-level namespaces | Without `declare`, TypeScript reports TS1046 for the whole file |
| `rootFS extends Omit<Root, ...>` | `rootFS` overrides `Root` methods with different signatures (TS2430) |
| `fieldWithType extends Omit<Field, 'type'>` | Its `type` is a string, while `Field.type` is a method (TS2430) |

The script fails if a patch no longer matches. When that happens, check whether upstream fixed it (then delete the patch) or changed its shape (then update the pattern).
