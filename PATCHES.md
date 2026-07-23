# Patches Applied to Upstream jsvm.d.ts

## `$http.send()` return type

Upstream types `$http.send()` as returning a Promise-like object with `.catch()`. In PocketBase 0.29.x Goja, `$http.send()` returns synchronously — calling `.catch()` on the result throws `TypeError`. The return type should be treated as a synchronous response object.

**Workaround:** Wrap `$http.send()` in a try/catch block instead of chaining `.catch()`:

```js
function postJson(url, body) {
  try {
    var resp = $http.send({
      url: url,
      method: 'POST',
      headers: { 'content-type': 'application/json' },
      body: JSON.stringify(body),
      timeout: 5
    });
  } catch (err) {
    /* fire-and-forget */
  }
}
```

## `store<T=any>()` return type

```
store<T=any>(): (store.Store<T>)
```

## `expandRecords` return type

```
expandRecords(records: Array<(Record | undefined)>, expands: Array<string>, optFetchFunc?: ExpandFetchFunc): _TygojaDict
```

## `MetaConfig` fields

```
MetaConfig
  appURL: string
  appUrl: string
```

## Handler scope isolation

PocketBase JSVM executes each hook handler in its own isolated context. Functions declared at module (file) scope are **not** visible inside handler callbacks. This is a documented PB behavior but a common trap for new hook authors.

**Wrong** — helpers at module scope are invisible inside the handler:

```js
function readConfig() { /* ... */ }

const handler = (e) => {
  var cfg = readConfig(); // ReferenceError: readConfig is not defined
  e.next();
};

onRecordsListRequest(handler);
```

**Correct** — declare helpers inside the handler, or use a factory function:

```js
function makeHandler() {
  function readConfig() { /* ... */ }

  return (e) => {
    var cfg = readConfig();
    e.next();
  };
}

const handler = makeHandler();
onRecordsListRequest(handler);
```

## ES2022+ methods not available

Goja targets ECMAScript 2021. The following ES2022+ methods are **not available** and will throw at runtime:

- `.at()` — use bracket indexing (`arr[arr.length - 1]`)
- `.findLast()` / `.findLastIndex()` — reverse-loop manually
- `Array.fromAsync()` — use Promise.all + map
- `Object.hasOwn()` — use `Object.prototype.hasOwnProperty.call()`
- `Error.cause` — use a wrapper Error class
- Top-level `await` — wrap in async IIFE

**Example:**

```js
// WRONG — throws ReferenceError in Goja
while (host.length > 0 && host.at(-1) === '/') {
  host = host.slice(0, -1);
}

// CORRECT
while (host.length > 0 && host[host.length - 1] === '/') {
  host = host.slice(0, -1);
}
```
