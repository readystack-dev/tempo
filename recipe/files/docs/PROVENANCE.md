# Provenance — Tempo (`v3.1.1-CE-ubuntu24.04-r7`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/grafana/tempo
- Revision built: `v3.1.1` (commit `9db7df79d2af105a90d96484e6403e1fda0d011e`)
- Source tree: `b564f0e22361849b102298712e20b1b23f7c5efe890d4c83d6b4c7f97b0ca113` over 15740 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795164606` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/tempo:v3.1.1-CE-ubuntu24.04-r7` — index digest `sha256:26060d5f85520e03fc810bf5e3557f5aeb290f33fd6bc80086ed0095dec08014` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:e7248cbf2b1ec96013e325061e6637c8cb315c6ee2178bf941517ef3534b5cff` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/tempo:v3.1.1-CE-ubuntu24.04-r7`

## Pinned inputs, and why

- 32 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 8, pins in the kit's dockerfiles 10, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.trail.json`, published beside this archive and signed with the release key (`ReadyStack-tempo-v3.1.1-CE-ubuntu24.04-r7.trail.json.sigstore`), and readable at https://readystack.dev/products/tempo/trail/v3.1.1-CE-ubuntu24.04-r7.

