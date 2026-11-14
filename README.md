# arity-data

The archive of [arity](https://github.com/collide2954/arity). arity collects
the values and the effects that open-access research articles report, each
with its source and its provenance.

arity makes its database from the records in this repository. The website of
arity shows that database.

## Contents

Each work has one folder, `works/<identifier>/`. The identifier is the PMCID of
the work, or its DOI or PMID.

- `work.json` holds the record of the work: its metadata, its queue entry, the
  address and the SHA-256 digest of each file that arity downloaded, the
  digests of its canonical texts, its notices, and its runs with the checks of
  their reports.
- `run-<sequence>.json` holds one submission, byte for byte. Its digest is in
  `work.json`.

This repository holds no file of a source. To make the database, arity
downloads each file again from its address, and makes sure that its digest
did not change.

## Make the database

```sh
git clone https://github.com/collide2954/arity
git clone https://github.com/collide2954/arity-data
cd arity
cargo run --release -- --data data rebuild ../arity-data
```

The documentation of arity tells the format and the steps of a rebuild:
[Archive and rebuild](https://github.com/collide2954/arity/blob/main/docs/src/archive.md).

## Checks

Each submission names its reader and the person who is responsible for it. A
report is unchecked until a person compares it with its source, and confirms
or rejects it. The checks of each run are in the `work.json` of its work.

A run does not change. To correct a report, record a check that rejects it,
and add a new submission.

## Notices

Each Monday, the workflow `.github/workflows/notices.yml` rebuilds the database
from this repository and reads the notices of each work again from Crossref,
Europe PMC, and PubMed Central. When a source states a new notice, for example
a retraction, the workflow commits it here. Each notice keeps its source, the
type name that its source uses, and the time that arity read it. The website
of arity shows new notices after its next daily build.

## License

The records in this repository are under CC0 1.0. See [LICENSE](LICENSE).

The quotes in the submissions are short parts of their source articles. Each
quote stays under the license of its source. The metadata of each work, in its
`work.json`, names that license.
