[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Ftempo-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/tempo) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/tempo)](https://hub.docker.com/r/readystack/tempo) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/tempo) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# Tempo: ReadyStack build kit

The offline build kit for the Docker image `readystack/tempo:v3.1.1-CE-ubuntu24.04-r7`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v3.1.1-CE-ubuntu24.04-r7](https://github.com/readystack-dev/tempo/releases/tag/v3.1.1-CE-ubuntu24.04-r7)
- Image: [`docker.io/readystack/tempo:v3.1.1-CE-ubuntu24.04-r7`](https://hub.docker.com/r/readystack/tempo/tags), manifest digest `sha256:e7248cbf2b1ec96013e325061e6637c8cb315c6ee2178bf941517ef3534b5cff`
- Product page: https://readystack.dev/products/tempo
- Source and build recipe: https://readystack.dev/products/tempo/recipe
- Build trail: https://readystack.dev/products/tempo/trail/v3.1.1-CE-ubuntu24.04-r7
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=tempo

## The image

ReadyStack Tempo Community Edition build kit.

## Who uses Tempo and why

Teams running many connected services who need distributed tracing to follow requests across them.

Grafana Tempo is a distributed tracing backend that needs only object storage to run. It stores traces from instrumented services, and teams explore them in Grafana to find slow or failing requests.

A typical use: Customers report that checkout is sometimes slow, and each checkout request passes through several services. Every service sends traces to Tempo; an engineer opens the slow traces in Grafana, sees which service call took most of the time, and knows where to look.

From the upstream project's own description: https://github.com/grafana/tempo.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-22 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 11 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`tempo`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-22; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/tempo.

Tempo is distributed under its upstream licence (AGPL-3.0-only); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v3.1.1-CE-ubuntu24.04-r7 release](https://github.com/readystack-dev/tempo/releases/tag/v3.1.1-CE-ubuntu24.04-r7): `ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.tar.gz` (500.7 MB), SHA-256 `94af20375f996d21a27abfc275113797264c50363877b848b979d42ed9d1beae`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.rebuild.json.sigstore ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.tar.gz
cd v3.1.1-CE-ubuntu24.04-r7
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/tempo/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
