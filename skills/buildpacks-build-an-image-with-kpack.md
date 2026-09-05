---
name: build-an-image-with-kpack
description: >-
  Declare a continuously rebuilt OCI image in a Kubernetes cluster running kpack, then watch the
  Build it produces through to a pushed image digest.
api: buildpacks:kpack
generated: '2026-09-05'
method: generated
source: openapi/buildpacks-kpack-swagger.json
operations:
  - createImage
  - getImage
  - getImageStatus
  - listNamespacedBuilds
  - getBuildStatus
  - getClusterBuilder
  - listAllClusterbuilders
---

# Build an image with kpack

kpack turns a source location plus a builder into an OCI image, and keeps rebuilding it whenever the
source or the base image changes. You declare intent with an `Image` resource; kpack creates `Build`
resources for you.

## Before you start

- You are calling **the operator's own Kubernetes API server**, not any buildpacks.io host. Every
  path below is relative to `/apis/kpack.io/v1alpha1/`.
- Authentication and authorization are the cluster's: a ServiceAccount token or client certificate,
  plus RBAC on the `kpack.io` API group. The published contract declares no `securityDefinitions`,
  but every operation declares `401 Unauthorized` — see `authentication/buildpacks-authentication.yml`.
- kpack must already be installed in the cluster. This skill does not install it.

## 1. Find a builder to build with

Call `listAllClusterbuilders` (`GET /apis/kpack.io/v1alpha1/clusterbuilders`) to see the
cluster-scoped builders available, or `getClusterBuilder`
(`GET /apis/kpack.io/v1alpha1/clusterbuilders/{name}`) if you already know the name.

Check `status.conditions` for a `Ready` condition of `"True"` before using a builder. A builder that
is not Ready will produce Builds that never start.

## 2. Declare the Image

Call `createImage` (`POST /apis/kpack.io/v1alpha1/namespaces/{namespace}/images`).

The body is a `kpack.build.v1alpha1.Image`. The fields that matter:

- `spec.tag` — where the built image is pushed.
- `spec.builder` — an object reference to the Builder or ClusterBuilder from step 1.
- `spec.serviceAccount` — the ServiceAccount holding registry and git credentials.
- `spec.source` — exactly one of `git`, `blob` or `registry`.

**This create is not replay-safe.** `createImage` is a POST to a collection. If you retry after a
timeout, the second call is rejected because the object name is already taken — which protects you
from duplicates but is name-uniqueness, not an idempotency contract. If you need a repeatable
apply, use `replaceImage` (`PUT .../images/{name}`) instead, which IS idempotent. See
`conventions/buildpacks-conventions.yml`.

## 3. Watch it build

Two ways, both real:

- Poll `getImageStatus` (`GET .../images/{name}/status`) and read `status.latestBuild` /
  `status.latestImage`.
- Stream: add `watch=true` to `listNamespacedBuilds`
  (`GET .../namespaces/{namespace}/builds?watch=true`). The response is
  `application/json;stream=watch`. Resume from the last `metadata.resourceVersion` you saw.

Call `getBuildStatus` (`GET .../builds/{name}/status`) for per-step detail on a single Build.

## 4. Paging, if you list a lot

List operations take `limit` and `continue`. A `continue` token expires in roughly five to fifteen
minutes; after that the server returns **410 ResourceExpired** with a fresh token. Resuming from
that token gives you a page from a *newer* snapshot, which is inconsistent with the pages you already
have — restart the list without `continue` if you need consistency.

`fieldSelector` and `labelSelector` narrow a list server-side.

## 5. Undo

There isn't one. `deleteImage` is not reversible: no restore, no soft delete, no undo operation
exists anywhere in the kpack contract. Recovery means re-applying your manifest, so keep it in
version control before you delete anything. See `conventions/buildpacks-conventions.yml` →
`reversibility`.

## Errors you will actually hit

The contract models only `200`, `201` and `401`. In practice you will also see `403` (RBAC denial),
`404`, `409` (name already taken, or a stale `metadata.resourceVersion`) and `422` (admission
rejection) — all returned as the standard Kubernetes `Status` envelope, none of them documented.
`errors/buildpacks-problem-types.yml` records this gap.
