# xb-tou

Original Xbox Terms of Use / country-info service (gateway service id 11, plain HTTP/1.1 over the xbfeature stream, mTLS peer must be `spiffe://openpak/xb-gateway`). Serves `/Country/<Region>/CountryMaster2.INX`, `/<CC>/CountryInfo2.INX` and `/<CC>/TermsOfUse.ini` from operator files (`XB_TOU_CONTENT_DIR`) and an OpenPak-authored built-in set (`XB_TOU_BUILTIN_COUNTRIES`); everything else is 404. Format: workspace docs `xbox/inx-format.md`. Configuration: `deploy/xb-tou.env.example`. It has no HTTP health endpoint (the gRPC listener is the liveness signal; the quadlet has no HealthCmd).

## Repository

- Module `github.com/openpak/xb-tou`, image `ghcr.io/openpak/xb-tou` (static, scratch, uid 10001).
- Shared packages: `github.com/openpak/xb-common` (private; see its README for access). Service map: workspace docs `xbox/native-service-architecture.md`.
- Build and test: `GOWORK=off go build ./... && go vet ./... && go test -race ./...` (with `GOPRIVATE=github.com/openpak/*` and `gh auth setup-git`).
- Image: `podman build --secret id=netrc,src=$HOME/.netrc -t ghcr.io/openpak/xb-tou:dev .`
- Release: push a `vX.Y.Z` tag; `.github/workflows/release.yml` (tags and manual dispatch only) tests and publishes the multi-arch image. CI reads xb-common with the job's `GITHUB_TOKEN` through a netrc build secret; nothing secret is in git or in the image.
- `deploy/` holds the env example and a Podman quadlet example (digests in it are examples; production pins its own).
- Provenance and licence: AGPL-3.0-only, see `LICENSE` and `NOTICE`. Derived from the Xombie project in part; the legacy Rust workspace remains in https://github.com/openpak/xbox-live.
