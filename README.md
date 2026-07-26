# temple-collections-as-data

A Jupyter notebook for treating **Temple University Libraries' digital collections as data**. It queries Temple's ContentDM collections through their IIIF Presentation API, then downloads item metadata and images and lets you explore a collection inline.

**Collection host:** `https://cdm16002.contentdm.oclc.org/iiif` (Temple University Libraries, 51 public collections)

## What the notebook does

`CDM_IIIF_Image_Download.ipynb` walks through:

1. **Browse collections** — list every collection in Temple's ContentDM as a table.
2. **Download metadata** — pull all items in a chosen collection into a flat CSV, one column per metadata field (fields vary by collection).
3. **Download images** — save IIIF images for a collection, with a companion CSV mapping each image file to its metadata.
4. **Preview + explore** — a responsive inline thumbnail gallery, plus quick "collections as data" views (items-per-year, facet frequencies).
5. **Batch metadata** — optionally sweep every collection into per-collection CSVs (resumable — it skips ones already saved).

The harvesting handles IIIF collection pagination, looks metadata up by field label rather than fragile index position, retries politely with a descriptive User-Agent, and rate-limits itself.

## Requirements

```
pip install requests pandas matplotlib
```

Run in Jupyter. Output is written to `downloads/` (gitignored).

## A note on full text / OCR

Temple's ContentDM IIIF manifests do **not** expose OCR or full-text annotations (`otherContent`), so this notebook covers images and structured metadata only. Full text would require a separate download-then-OCR pipeline, which is outside this notebook's scope.

## Prior art / related collections-as-data projects

This notebook grew alongside a set of IIIF "collections as data" examples for other institutions. Earlier versions of this repo bundled modified copies of those third-party example notebooks (adapted to run against different APIs); they have since been removed to keep the repo focused on Temple and to avoid mixing licenses. Those examples are **not bundled here** — they are other people's work and are better read at the source:

- **Gustavo Candela**, [`notebook-iiif-images`](https://github.com/hibernator11/notebook-iiif-images) (University of Alicante, GPL-3.0) — the Europeana, Ghent University, and Smithsonian Open Access IIIF notebooks this project once mirrored.
- **Tim Sherratt**, [GLAM Workbench](https://glam-workbench.net/) — the inline `gallery()` preview function is adapted from here.

## License

MIT — see [LICENSE](LICENSE). (The linked upstream examples are GPL-3.0; keeping them out of this repo avoids mixing licenses.)
