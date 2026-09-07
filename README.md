# First Mass — dataset

© 2026 First Mass / Catholic West — https://firstmass.net · Licensed [CC BY 4.0](LICENSE)


The open dataset behind **[firstmass.net](https://firstmass.net)**: a crowdsourced, source-linked
record of the earliest documented Catholic Mass said in each place that became part of the
United States and its territories.

Brought to you by [Catholic West](https://x.com/_CatholicWest).

## Files

| File | What |
|------|------|
| [`masses.json`](masses.json) | The canonical dataset — an array of entry objects. This is the source of truth. |
| [`masses.csv`](masses.csv) | Same data, flattened. `sources` and `images` are collapsed into single `` ; ``-separated cells of the form `Label \| URL`. |
| [`masses.xml`](masses.xml) | Same data as XML, with `sources` and `images` kept as nested elements. |
| [`schema-dataset.json`](schema-dataset.json) | schema.org `Dataset` descriptor. |

`masses.csv` and `masses.xml` are generated from `masses.json`. If they ever disagree, the JSON wins.

## Entry schema

Each object in `masses.json`:

| Field | Notes |
|-------|-------|
| `id` | Unique slug. Also the entry's page on the site: `firstmass.net/entries/<id>.html`. |
| `location` | Where the Mass was said, as specific as the sources allow. |
| `state_territory` | Modern US state or territory. |
| `county` | Modern county (or municipality / borough / parish equivalent). |
| `modern_diocese` | Present-day Catholic diocese covering the location. |
| `historical_diocese` | Diocese with jurisdiction at the time, or `Unorganized` if none existed yet. |
| `date_display` | Human-readable date at whatever precision is known — `November 12, 1602`, `July 1827`, `1629`. |
| `date_sort` | ISO-ish sort key (`1602-11-12`, or a bare year). Drives the site's timeline. |
| `date_precision` | `exact`, `year-only`, or `disputed`. |
| `priest` | Celebrant(s), or a description where unnamed. |
| `religious_order` | e.g. `Society of Jesus (Jesuits)`, `Order of Friars Minor (Franciscans)`, `Diocesan / Secular clergy`. May be blank. |
| `rite` | Usually `Roman (Latin) Rite`; a handful of Eastern-rite entries. |
| `expedition` | Free-text name of the journey or expedition the Mass was part of, if any. |
| `expedition_id` | Slug grouping entries into a shared expedition (optional). |
| `lat`, `lng` | Coordinates. Best available; some are approximate. |
| `confidence` | **`confirmed`** — a source explicitly documents a Mass. **`disputed`** — a popular claim without solid support. **`inferred`** — a strong circumstantial case (a resident priest, recorded baptisms) but no source that says "Mass" outright. Please preserve this distinction in anything you build. |
| `submitter_twitter` | X/Twitter handle of the contributor, where credited (optional). |
| `sources` | Array of `{label, url}`; `url` may be empty for offline sources. **The real evidence lives here — cite these, not just this dataset.** |
| `images` | Array of `{url, caption}` (optional). URLs are relative to firstmass.net. |
| `notes` | Prose: the sourcing story, caveats, competing theories, why an entry is `disputed` or `inferred`. |

## Using it

Reuse, remix, and commercial use are all fine under [CC BY 4.0](LICENSE) — just credit **firstmass.net**.
If you build something on top of this, a few asks:

- Treat `masses.json` as the source of truth.
- Keep the `confidence` levels — don't flatten `disputed` / `inferred` into settled fact.
- Cite the underlying `sources`, not just this dataset.

## Staying current

`masses.json` here is a snapshot. The live dataset — which grows as new submissions are researched
and reviewed — is always at **`https://firstmass.net/data/masses.json`**. Corrections and new entries
go through the submission form at [firstmass.net/submit.html](https://firstmass.net/submit.html).
