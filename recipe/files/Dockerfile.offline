# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS build_tempo
WORKDIR /src
COPY vendored/tempo-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795164606
RUN go build -trimpath -tags "netgo" -ldflags='-s -w -X main.Version=3.1.1 -X main.Branch=HEAD -X main.Revision=9db7df79' -o /tempo ./cmd/tempo && /tempo -version && \
    { readelf -lW /tempo | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /tempo | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /tempo.needs
FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS build_tempo-cli
WORKDIR /src
COPY vendored/tempo-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795164606
RUN go build -trimpath -tags "netgo" -ldflags='-s -w' -o /tempo-cli ./cmd/tempo-cli && /tempo-cli --help && \
    { readelf -lW /tempo-cli | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /tempo-cli | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /tempo-cli.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795164606
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795164606
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'tempo:x:10001:10001::/var/tempo:/bin/sh\n' >> /rootfs/etc/passwd && printf 'tempo:x:10001:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/var/tempo /rootfs/etc/tempo /rootfs/var/tempo/wal /rootfs/var/tempo/blocks /rootfs/var/tempo/live-store && chown -R 10001:10001 /rootfs/var/tempo /rootfs/etc/tempo /rootfs/var/tempo/wal /rootfs/var/tempo/blocks /rootfs/var/tempo/live-store
COPY --from=build_tempo /tempo /rootfs/usr/bin/tempo
COPY --from=build_tempo /tempo.needs /tmp/needs/tempo
COPY --from=build_tempo-cli /tempo-cli /rootfs/usr/bin/tempo-cli
COPY --from=build_tempo-cli /tempo-cli.needs /tmp/needs/tempo-cli
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
COPY tempo-config.yaml /rootfs/etc/tempo/config.yaml
RUN chmod 755 /rootfs/usr/bin/tempo /rootfs/usr/bin/tempo-cli /rootfs/usr/local/bin/rs-probe && \
    chown 10001:10001 /rootfs/etc/tempo/config.yaml && \
    chmod 0644 /rootfs/etc/tempo/config.yaml
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795164606
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.licenses="AGPL-3.0-only"
LABEL com.readystack.license.disclosure="This image includes Grafana Tempo (https://github.com/grafana/tempo), licensed under AGPL-3.0-only. Modifications: the build raises Go-module dependency versions in go.mod and go.sum where upstream's are older than the fixed, upstream-published releases (security updates; no Tempo source file is edited); full diff of every upstream file the build changes at https://readystack.dev/source/tempo/v3.1.1/tempo-v3.1.1-readystack.patch (empty when the build changes none). The upstream source is https://github.com/grafana/tempo/tree/v3.1.1. Operating-system packages come from Ubuntu's archive, unmodified. ReadyStack license holders have access to the image build recipe and patched-package manifest on request via contact@readystack.dev."
LABEL org.opencontainers.image.title="Tempo"
LABEL org.opencontainers.image.source="https://github.com/grafana/tempo"
LABEL org.opencontainers.image.version="v3.1.1-CE-ubuntu24.04-r7"
LABEL org.opencontainers.image.revision="9db7df79d2af105a90d96484e6403e1fda0d011e"
HEALTHCHECK --interval=5s --timeout=30s --start-period=40s \
  CMD /usr/local/bin/rs-probe http://127.0.0.1:3200/ready || exit 1
USER tempo
EXPOSE 3200 4317 4318
ENTRYPOINT ["tempo", "-config.file=/etc/tempo/config.yaml", "-target=all"]
