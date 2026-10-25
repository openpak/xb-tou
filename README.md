# Xbox Terms of Use Server

OpenPak's Xbox Terms of Use Server.

| | |
| --- | --- |
| Network | Original Xbox |
| Role | Terms of Use and country-info service (gateway service id 11) |
| Depends on | [`xb-common`](https://github.com/openpak/xb-common) (private) |
| Used by | [`xb-gateway`](https://github.com/openpak/xb-gateway) |
| Image | `ghcr.io/openpak/xb-tou` |
| Based on | [Xombie](https://github.com/XombieOnline/xombie) (AGPL-3.0), in part |
| Licence | AGPL-3.0-only |

## What it serves

| Endpoint | What |
| --- | --- |
| `/Country/<Region>/CountryMaster2.INX` | Country master file for a region |
| `/<CC>/CountryInfo2.INX` | Country info file for a country code |
| `/<CC>/TermsOfUse.ini` | Terms of Use file for a country code |

Content comes from operator files (`XB_TOU_CONTENT_DIR`) and an OpenPak-authored built-in set (`XB_TOU_BUILTIN_COUNTRIES`); everything else is 404.

## Run

The service runs as a Podman quadlet from `deploy/`; see [Deploy](docs/deploy.md). To build the image locally:

```sh
podman build --secret id=netrc,src=$HOME/.netrc -t ghcr.io/openpak/xb-tou:dev .
```

## Docs

- [Protocol](docs/protocol.md)
- [Evidence](docs/evidence.md)
- [Deploy](docs/deploy.md)
- [Notes](docs/notes.md)

## Licence

AGPL-3.0-only. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
