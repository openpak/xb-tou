# Deploy: xb-tou

## Repository

- Module `github.com/openpak/xb-tou`, image `ghcr.io/openpak/xb-tou` (static, scratch, uid 10001).
- Shared packages: `github.com/openpak/xb-common` (private; see its README for access). Service map: workspace docs `xbox/native-service-architecture.md`.
- Build and test: `GOWORK=off go build ./... && go vet ./... && go test -race ./...` (with `GOPRIVATE=github.com/openpak/*` and `gh auth setup-git`).
- Image: `podman build --secret id=netrc,src=$HOME/.netrc -t ghcr.io/openpak/xb-tou:dev .`
- Release: push a `vX.Y.Z` tag; `.github/workflows/release.yml` (tags and manual dispatch only) tests and publishes the multi-arch image. CI reads xb-common with the job's `GITHUB_TOKEN` through a netrc build secret; nothing secret is in git or in the image.
- `deploy/` holds the env example and a Podman quadlet example (digests in it are examples; production pins its own).
