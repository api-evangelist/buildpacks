---
name: publish-a-buildpack-to-the-registry
description: >-
  Package a buildpack, publish it to the Cloud Native Buildpacks Registry, confirm it is indexed
  through the public registry API, and yank or un-yank a version.
api: buildpacks:registry
generated: '2026-09-05'
method: generated
source: >-
  https://buildpacks.io/docs/for-buildpack-authors/how-to/distribute-buildpacks/publish-buildpack/,
  https://github.com/buildpacks/registry-api,
  https://github.com/buildpacks/spec/blob/main/extensions/buildpack-registry.md
operations:
  - GET /api/v1/search
  - GET /api/v1/buildpacks/{namespace}/{name}
  - GET /api/v1/buildpacks/{namespace}/{name}/{version}
---

# Publish a buildpack to the Buildpack Registry

The Buildpack Registry is a discovery index over buildpacks that already live in OCI registries. It
does not store your buildpack — it stores a pointer to an immutable digest.

## Before you start

Your buildpack ID must be `<namespace>/<name>`, exactly one `/`, each side matching
`[a-z0-9\-\.]{1,253}`. That rule is normative:
`https://github.com/buildpacks/spec/blob/main/extensions/buildpack-registry.md`.

```toml
[buildpack]
id = "example/my-cnb"
```

## 1. Package and push the buildpackage

`pack buildpack package` builds the buildpackage; push it to a **public** OCI registry. A
buildpackage is an OCI image (or a `.cnb` tar), and its metadata rides in the
`io.buildpacks.buildpackage.metadata` image label.

## 2. Register it

```sh
pack buildpack register example/my-cnb
```

This opens GitHub in a browser and may ask you to authenticate. You get a **pre-populated GitHub
Issue** whose body is structured data — do not edit it. Submitting the issue is the write operation;
there is no HTTP write endpoint on `registry.buildpacks.io`. The request is processed within seconds
and the issue is closed either way, tagged "Failure" with a diagnostic comment if it did not work.

The first time you publish under a namespace, your GitHub user becomes its owner, and from then on
only you can publish under it. Ownership changes are pull requests against
`https://github.com/buildpacks/registry-namespaces`.

## 3. Confirm it is indexed

The read API is public and needs no credential at all.

```sh
curl "https://registry.buildpacks.io/api/v1/search?matches=my-cnb"
curl "https://registry.buildpacks.io/api/v1/buildpacks/example/my-cnb"
curl "https://registry.buildpacks.io/api/v1/buildpacks/example/my-cnb/0.1.0"
```

Only those three paths are routed. Anything else — including a collection listing like
`/api/v1/buildpacks` — returns 404 with an empty body.

Errors are a bare `{"error": "<string>"}` envelope, not RFC 9457 problem+json:

- `400 {"error":"Missing search string 'matches'"}` — you omitted `?matches=`.
- `404 {"error":"Unknown buildpack"}` — nothing indexed under that `<namespace>/<name>`.

The version path only matches `[0-9]+\.[0-9]+\.[0-9]+[0-9A-Za-z\-\.]*`, so a two-component version
will not route.

## 4. Reading the response

Each entry carries a `latest` object and a `versions` array. The field to trust is `addr` — the OCI
reference including an `@sha256:` digest. That is what a build will actually pull. `yanked` tells you
whether the version has been withdrawn.

## 5. Undo

This is the one reversible action in the whole CNB surface, and it is worth knowing precisely:

```sh
pack buildpack yank example/my-cnb@0.1.0        # mark unusable
pack buildpack yank example/my-cnb@0.1.0 --undo # put it back
```

`--undo` is documented at
`https://buildpacks.io/docs/for-platform-operators/how-to/integrate-ci/pack/cli/pack_buildpack_yank/`.
**No time window is stated** — do not assume one exists, and do not assume one does not.

What you cannot do is delete. The registry index is append-only: entries carry a `yanked` boolean
rather than being removed. Publishing a version is permanent; yanking is the only remedy.
