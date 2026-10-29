# Cloud Native Buildpacks

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Cloud Native Buildpacks (CNBs) transform application source code into OCI-compliant container images that can run on any cloud, without requiring Dockerfiles. Initiated by Pivotal and Heroku in January 2018, CNB joined the CNCF as a Sandbox project in October 2018 and GRADUATED on 11 August 2026, the foundation's highest maturity tier. It is licensed Apache-2.0. CNB is primarily a specification project: three independently versioned contracts — Buildpack API 0.12, Platform API 0.15 and Distribution API 0.3 — plus reference implementations (the pack CLI and the lifecycle). It centralizes container expertise through composable buildpacks, enables layer rebasing for efficient OS updates, and generates Software Bills of Materials in CycloneDX, SPDX and Syft formats. The pack CLI, the kpack Kubernetes operator and the public Buildpack Registry API are the primary integration points.

**Areas:** Cloud Native Buildpacks · Build Tools · CI/CD · Cloud-Native · CNCF · Container Images · Containers · OCI · Open Source

## Cloud Native Buildpacks on APIs.io

Everything profiled for Cloud Native Buildpacks is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/buildpacks/](https://apis.io/providers/buildpacks/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Buildpack API Specification](https://apis.io/apis/buildpacks/buildpack-api/) — The Buildpack API is the contract between a buildpack and the lifecycle. It defines the detect and build executables, layers, build-plan provisions and…
- [Platform API Specification](https://apis.io/apis/buildpacks/platform-api/) — The Platform API is the contract between the CNB lifecycle and a platform such as pack, kpack, or a CI runner. It defines how builders, stacks, run images,…
- [Distribution API Specification](https://apis.io/apis/buildpacks/distribution-api/) — The Distribution API specifies how buildpacks and builders are packaged as OCI artifacts, signed, and distributed through OCI registries. It also covers how…
- [pack CLI](https://apis.io/apis/buildpacks/pack-cli/) — pack is the reference command-line interface for Cloud Native Buildpacks. It implements the Platform API to build OCI images from source on a developer's…
- [CNB Lifecycle](https://apis.io/apis/buildpacks/lifecycle/) — The CNB Lifecycle is the reference implementation of the Buildpack and Platform APIs. It runs the detect, analyze, restore, build, export, and rebase phases…
- [Buildpack Registry](https://apis.io/apis/buildpacks/registry/) — The Cloud Native Buildpacks registry indexes published buildpacks for discovery and reuse. It mirrors metadata for buildpack packages stored in OCI…
- [Cloud Native Buildpacks Kpack API](https://apis.io/apis/buildpacks/buildpacks-kpack-api/) — The kpack API from Cloud Native Buildpacks — 25 operation(s) for kpack.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [buildpacks-mcp.yml](https://apis.io/servers/buildpacks/buildpacks-mcp-yml/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Buildpacks Kpack Overlay](https://apis.io/overlays/buildpacks/buildpacks-kpack-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Buildpacks Authentication](https://apis.io/security/buildpacks/buildpacks-authentication/)
- [Buildpacks Domain Security](https://apis.io/security/buildpacks/buildpacks-domain-security/)
- [Buildpacks Trust Center](https://apis.io/security/buildpacks/buildpacks-trust-center/)
- [Buildpacks Vulnerability Disclosure](https://apis.io/security/buildpacks/buildpacks-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Buildpacks Plans Pricing](https://apis.io/plans/buildpacks/buildpacks-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Buildpacks Rate Limits](https://apis.io/rate-limits/buildpacks/buildpacks-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Buildpacks Finops](https://apis.io/finops/buildpacks/buildpacks-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://buildpacks.io)
- [Documentation](https://buildpacks.io/docs/)
- [Getting started](https://buildpacks.io/docs/app-journey)
- [API reference](https://buildpacks.io/docs/reference/spec/)
- [Support](https://buildpacks.io/community/)
- [Blog](https://medium.com/buildpacks)
- [Privacy policy](https://www.linuxfoundation.org/privacy/)
- [GitHub](https://github.com/buildpacks)

## API Evangelist rating

**Kin Score 47.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 64.3 |
| Contract quality | 42.0 |
| Contract governance | 18.2 |
| Operational transparency | 36.8 |
| Developer ergonomics | 73.2 |
| Access clarity | 26.3 |

**Agent readiness 24.7** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | derived (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 31.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/buildpacks/](https://apis.io/providers/buildpacks/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Cloud Native Buildpacks: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/buildpacks/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
