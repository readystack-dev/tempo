# Tempo: ReadyStack build kit

The offline build kit for the Docker image `readystack/tempo:v3.1.1-CE-ubuntu24.04-r7`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v3.1.1-CE-ubuntu24.04-r7](https://github.com/readystack-dev/tempo/releases/tag/v3.1.1-CE-ubuntu24.04-r7)
- Image: [`docker.io/readystack/tempo:v3.1.1-CE-ubuntu24.04-r7`](https://hub.docker.com/r/readystack/tempo/tags), manifest digest `sha256:e7248cbf2b1ec96013e325061e6637c8cb315c6ee2178bf941517ef3534b5cff`
- Product page: https://readystack.dev/products/tempo
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=tempo

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/tempo/recipe. The complete kit is the release download. Each release is a tag here.
