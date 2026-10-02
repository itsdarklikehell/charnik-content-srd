# charnik-content-srd


[![CI](https://github.com/itsdarklikehell/charnik-content-srd/actions/workflows/ci.yml/badge.svg)](https://github.com/itsdarklikehell/charnik-content-srd/actions/workflows/ci.yml)
[![License](https://img.shields.io/github/license/itsdarklikehell/charnik-content-srd)](LICENSE)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)


The SRD rules data that [Charnik](https://github.com/FernDragonborn/charnik) ships with, as plain
CSV. It lives in its own repository so **rules data can be corrected and released without shipping
an app build** — a content fix is a commit here, not a new binary.

```
srd-2014/   D&D 5e   — from SRD 5.1    (source tag "SRD 5.1")
srd-2024/   D&D 5.5e — from SRD 5.2.1  (source tag "SRD 5.2.1")
```

Each top-level folder is one **content pack**. A pack is just a folder of CSVs — there is no
manifest or index file; every CSV describes itself in-band through its `#content-*` header
(`#content-source`, `#content-license`, `#content-url`, `#content-id`, `#content-updated_at`,
`#content-hash`, `#content-systems`). Drop another folder in beside these and it is another pack.

## Using it with the app

## Ontwikkeltijdlijn

<video src="https://raw.githubusercontent.com/itsdarklikehell/charnik-content-srd/master/gource.mp4" controls width="100%"></video>


Clone this repo **next to** the app repo — that layout needs no configuration at all:

```
some-folder/
├─ charnik/               ← the app
└─ charnik-content-srd/   ← this repo
```

A different location goes in `charnik.config.json` in the app repo (`{ "contentRepo": "…" }`), or in
the `CHARNIK_CONTENT` environment variable. The app vendors these CSVs into its build, so a release
always carries a working copy of the content as its floor.

## Editing

The CSVs are **generated** from the published SRD markdown by the converters in the app repo
(`tools/srd/`) — data is never authored from memory. After any hand-edit, re-stamp the file's hash
from the app repo, or the app's content-health panel flags it as drifted:

```
pnpm restamp <path-to-file.csv>
```

## License

The rules data is © Wizards of the Coast LLC, licensed under
[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/legalcode). See `LICENSE` and
`ATTRIBUTION.md` — keeping that credit is a condition of use. SRD material only: no Product
Identity, no non-SRD content.