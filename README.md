# storage

Standard and secure key/value storage. Part of the [modular_app_template](https://github.com/Yusubov-Engineering/modular_app_template) core modules.

Released as two packages, versioned and tagged together:

- **`storage_api`** — the abstract contract. Feature code and other `_api`
  packages depend on this, never on `storage_impl`.
- **`storage_impl`** — the concrete implementation. Only the app's composition
  root depends on this.

Current release: **`v1.0.0`**.

## Using it

This repo is not published to pub.dev — consume it as a `git:` dependency
pinned to a tag:

```yaml
dependencies:
  storage_api:
    git:
      url: git@github.com:Yusubov-Engineering/storage.git
      path: storage_api
      ref: v1.0.0
  storage_impl:
    git:
      url: git@github.com:Yusubov-Engineering/storage.git
      path: storage_impl
      ref: v1.0.0
```

`storage_impl` also depends on `dependency_injection_api` (its own `git:`
dependency at `v1.0.0`) — see `storage_impl/pubspec.yaml`.

## Local development

Each package resolves independently — there is no shared workspace root:

```bash
cd storage_api && flutter pub get && flutter analyze && cd ..
cd storage_impl && flutter pub get && flutter analyze && cd ..
```

## Releasing

Bump both packages' `version:` in lockstep, then tag:

```bash
git tag -a vX.Y.Z -m "vX.Y.Z"
git push origin vX.Y.Z
```

Every consumer pins an explicit `ref:`, so nothing picks up a new release
until its `pubspec.yaml` is updated to point at the new tag.
