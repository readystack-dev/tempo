# Tempo v3.1.1 — ReadyStack release `v3.1.1-CE-ubuntu24.04-r7`

Generated 2026-11-22 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/tempo:v3.1.1-CE-ubuntu24.04-r7` (linux/amd64). Index digest `sha256:26060d5f85520e03fc810bf5e3557f5aeb290f33fd6bc80086ed0095dec08014` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:e7248cbf2b1ec96013e325061e6637c8cb315c6ee2178bf941517ef3534b5cff` [`TARGET_DIGEST.txt`].
- **Upstream:** Tempo v3.1.1 built from source at `v3.1.1` of https://github.com/grafana/tempo — upstream notes: https://github.com/grafana/tempo/releases/tag/v3.1.1 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `tempo`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v3.1.1-CE-ubuntu24.04-r6`.

## What changed in this release

- Upstream version unchanged (v3.1.1); ReadyStack rebuild.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `github.com/go-jose/go-jose/v4` raised from upstream's `v4.1.4` to at least `v4.1.6` (shipped: `v4.1.6`)
  - `github.com/andybalholm/brotli` raised from upstream's `v1.2.2` to at least `v1.2.7` (shipped: `v1.2.7`)
  - `golang.org/x/net` raised from upstream's `v0.60.0` to at least `v0.62.0` (shipped: `v0.62.0`)
  - `github.com/klauspost/compress` raised from upstream's `v1.19.1` to at least `v1.20.2` (shipped: `v1.20.2`)
  - `github.com/apache/thrift` raised from upstream's `v0.24.0` to at least `v0.25.0` (shipped: `v0.25.0`)
- Tempo v3.1.1 is unchanged from the release this supersedes (v3.1.1-CE-ubuntu24.04-r6); this release rebuilds it. Changes: the image is rebuilt on the current ubuntu:24.04 image (sha256:9c7f200c07e3…), which its maintainers updated after v3.1.1-CE-ubuntu24.04-r6 was built on sha256:2198e4c65076…. Settings, ports and data volumes are those of v3.1.1-CE-ubuntu24.04-r6: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-20)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `tempo` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/tempo:v3.1.1-CE-ubuntu24.04-r7` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:e7248cbf2b1ec96013e325061e6637c8cb315c6ee2178bf941517ef3534b5cff`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 6 of 6 use cases passed (6 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None recorded.

## Defects fixed

- 23 problems found before release and fixed before it shipped (23 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/tempo:v3.1.1-CE-ubuntu24.04-r7
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

