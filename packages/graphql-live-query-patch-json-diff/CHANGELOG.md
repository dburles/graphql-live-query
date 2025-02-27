# @n1ru4l/graphql-live-query-patch-jsondiffpatch

## 0.6.1

### Patch Changes

- 6f86843: ensure unmodified properties are not removed when applying patches
- Updated dependencies [6f86843]
  - @n1ru4l/json-patch-plus@0.1.1

## 0.6.0

### Minor Changes

- 7e56721: Use `@n1ru4l/json-patch-plus` for smaller and more efficient patches

### Patch Changes

- Updated dependencies [7e56721]
  - @n1ru4l/json-patch-plus@0.1.0

## 0.5.0

### Minor Changes

- 8e14fd2: improve ESM support by using export fields and .mjs file extensions

### Patch Changes

- Updated dependencies [8e14fd2]
  - @n1ru4l/graphql-live-query-patch@0.5.0

## 0.4.0

### Minor Changes

- a002527: omit empty patches from being sent to clients

### Patch Changes

- Updated dependencies [a002527]
  - @n1ru4l/graphql-live-query-patch@0.4.0

## 0.3.2

### Patch Changes

- 04a7fb6: BREAKING move `@n1ru4l/graphql-live-query-patch` logic to `@n1ru4l/graphql-live-query-patch-json-patch`. `@n1ru4l/graphql-live-query-patch` now contains generic logic for patch generation. `@n1ru4l/graphql-live-query-patch-jsondiffpatch` implements the more efficient jsondiffpatch algorithm
- Updated dependencies [04a7fb6]
  - @n1ru4l/graphql-live-query-patch@0.3.2
