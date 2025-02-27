# @n1ru4l/in-memory-live-query-store

## 0.7.1

### Patch Changes

- Updated dependencies [fbbee22]
  - @n1ru4l/graphql-live-query@0.8.1

## 0.7.0

### Minor Changes

- e893ecc: Add support for the `@live(throttle:)` directive argument for negotiating a throttle between the server and the client. This is useful for preventing the server to spam the client for data that might be updating too frequently.

  The `InMemoryLiveQueryStore` now accepts a `validateThrottleValue` option that can be used to validate the incoming throttle value sent from clients.

  ```ts
  const store = new InMemoryLiveQueryStore({
    validateThrottleValue: (value /* value as sent by client */) => {
      // value can either be null/undefined or a number
      // returning a string from this function will treat the provided value as invalid
      // and send an error back to the client.
      if (value == null || value > 1000) {
        return "Must provide throttle value in the range from 0-1000";
      }
      // returning a number will replace the user sent throttle value
      if (value === 420) {
        return 690;
      }
      // returning null or undefined will result in no throttle being used.
      return null;
    }
  });
  ```

- 8e14fd2: improve ESM support by using export fields and .mjs file extensions

### Patch Changes

- Updated dependencies [e893ecc]
- Updated dependencies [8e14fd2]
  - @n1ru4l/graphql-live-query@0.8.0

## 0.6.6

### Patch Changes

- e15005f: refactor logic for extracting id schema coordinates

## 0.6.5

### Patch Changes

- a84e469: add InMemoryLiveQueryStore.makeExecute function for ad-hoc execute function composition

## 0.6.4

### Patch Changes

- 41e6c0a: add optional identification field parameter to store configuration
- 916de62: fix: bump upstream issue in @n1ru4l/push-pull-async-iterable-iterator

## 0.6.3

### Patch Changes

- dc5b2cc: Internal refactor: replace usages of graphql-tools wrapSchema with mapSchema.

## 0.6.2

### Patch Changes

- 6be3dc2: browser compat for environment without process.env

## 0.6.1

### Patch Changes

- 4017395: Add `includeIdentifierExtension` option for InMemoryLiveQueryStore constructor.

  Setting the `includeIdentifierExtension` option to `true` will result in all the topics valid for a operation being added as a extensions field to the operation result.

  The option is set to `true` by default if `process.env.NODE_ENV === "development"`.

  ```json
  {
    "data": {
      "post": {
        "id": "1",
        "title": "lel"
      }
    },
    "extensions": {
      "liveResourceIdentifier": ["Query.post", "Query.post(id:\"1\")", "Post:1"]
    },
    "isLive": true
  }
  ```

## 0.6.0

### Minor Changes

- 50ffe13: Allow adding additional resource identifier in user-land via the liveQuery.collectResourceIdentifiers extensions field on schema fields.

## 0.5.5

### Patch Changes

- 88270dc: feat: allow conditional live queries via the if argument on the live directive
- 0caaad0: Ensure compat for non experimental graphql releases without defer and stream support.
- 76c459f: use a resource tracker for more efficient invalidations
- Updated dependencies [88270dc]
  - @n1ru4l/graphql-live-query@0.7.1

## 0.5.4

### Patch Changes

- 6915f6d: fix support safari 14

## 0.5.3

### Patch Changes

- ca21161: Mark live query execution results via the boolean isLive property published by the AsyncIterator. This makes identifying live queries easier. A possible use-case where this is useful might be a wrapper around InMemoryLiveQueryStore.execute that creates patches from the last and next execution result."
- Updated dependencies [ca21161]
- Updated dependencies [f244baa]
  - @n1ru4l/graphql-live-query@0.7.0

## 0.5.2

### Patch Changes

- 8d416b8: make graphql a peer dependency
- 7b37628: Make implementation more compatible with how `graphql-js` behaves.
- c550c40: fix: Don't leak implementation details on the returned AsyncIterableIterator. `InMemoryLiveQueryStore.execute` noe resolves with a generic AsyncIterableIterator.
- Updated dependencies [37f0b6d]
- Updated dependencies [7b37628]
  - @n1ru4l/graphql-live-query@0.6.0

## 0.5.1

### Patch Changes

- c14836a: Fix memory leak cause by not correctly disposing live query records once a live query has finished.

## 0.5.0

### Minor Changes

- 6cfe3e5: Replace `executeLiveQuery` with `execute`.

  Instead of passing two execute functions to the server options, now only a single execute function is passed to the server.

  The `execute` function can now return a `AsyncIterableIterator<ExecutionResult>`.

  `@n1ru4l/socket-io-graphql-server` has no longer a dependency upon `@n1ru4l/graphql-live-query`.

### Patch Changes

- Updated dependencies [6cfe3e5]
  - @n1ru4l/graphql-live-query@0.5.0

## 0.4.0

### Minor Changes

- b086fc8: Shape the API to be more "compatible" with graphql-js.

  **BREAKING CHANG** Rename `InMemoryLiveQueryStore.triggerUpdate` method to `InMemoryLiveQueryStore.invalidate`. `InMemoryLiveQueryStore.invalidate` now also accepts an array of strings.

  **BREAKING CHANGE** `InMemoryLiveQueryStore` no longer implements `LiveQueryStore`. The `LiveQueryStore` interface was removed

  **BREAKING CHANGE** Rename `InMemoryLiveQueryStore.register` to `InMemoryLiveQueryStore.execute`. `InMemoryLiveQueryStore.execute` returns a `AsyncIterableIterator` which publishes the execution results.

### Patch Changes

- Updated dependencies [b086fc8]
  - @n1ru4l/graphql-live-query@0.4.0

## 0.3.0

### Minor Changes

- 6a03905: **BREAKING CHANGE**: Change API of `LiveQueryStore`.

  The register method of the `LiveQueryStore` now has changed:

  ```ts
  import type { DocumentNode, ExecutionResult } from "graphql";

  export type UnsubscribeHandler = () => void;
  export type OperationVariables = { [key: string]: any } | null | undefined;

  export abstract class LiveQueryStore {
    abstract async triggerUpdate(identifier: string): Promise<void>;
    abstract register(
      operationDocument: DocumentNode,
      operationVariables: OperationVariables,
      executeQuery: () => Promise<ExecutionResult>,
      publishUpdate: (executionResult: ExecutionResult, payload: any) => void
    ): UnsubscribeHandler;
  }
  ```

### Patch Changes

- Updated dependencies [6a03905]
  - @n1ru4l/graphql-live-query@0.3.0

## 0.2.0

### Minor Changes

- aa2be73: chore: unify how packages are built.

### Patch Changes

- Updated dependencies [aa2be73]
  - @n1ru4l/graphql-live-query@0.2.0
