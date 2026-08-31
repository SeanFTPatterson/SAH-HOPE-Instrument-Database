# aSAH Measurement Instrument Database — configurable GitHub Pages prototype

This version separates both the **instrument data** and the **website field configuration** from the HTML.

- `data/instruments.csv` contains the instrument records.
- `data/fields.csv` controls which fields appear in the main table, pop-up, filters, and search.
- `images/` contains the replaceable team logo and optional instrument graphics.

## Folder structure

```text
index.html
.nojekyll
README.md

data/
  instruments.csv
  fields.csv

images/
  team-logo.svg
  example-instrument-graphic.svg
```

## Publish on GitHub Pages

1. Create or open your GitHub repository.
2. Upload the **contents of this folder** so `index.html` is at the repository root.
3. Commit the files.
4. Go to **Settings → Pages**.
5. Choose **Deploy from a branch**.
6. Select `main` and `/ (root)`.
7. Save.

## Updating instruments

Edit `data/instruments.csv` in Excel, Google Sheets, or another spreadsheet editor, then replace the CSV in GitHub and commit the change.

You can add/remove rows without editing `index.html`.

## Adding or removing database fields

Each column in `instruments.csv` can be configured in `data/fields.csv`.

`fields.csv` contains:

| Column | Purpose |
|---|---|
| `field` | Exact column header from `instruments.csv` |
| `label` | Human-readable label shown on the website |
| `table` | `Yes` to show as a main table column |
| `popup` | `Yes` to show in the instrument pop-up |
| `filter` | `Yes` to automatically create a dropdown filter |
| `search` | `Yes` to include this field in free-text search |
| `display_order` | Number controlling left-to-right / top-to-bottom order |
| `format` | How the value is displayed |

Supported `format` values:

- `text` — standard text field
- `primary` — primary instrument-name field; automatically shows the acronym beside it
- `badge` — pill-style status display
- `longtext` — full-width text section in the pop-up
- `image` — image displayed near the top of the pop-up
- `hidden` — stored in the CSV but not directly rendered

### Example: add Number of items

1. Add a `number_of_items` column to `instruments.csv`.
2. Add this row to `fields.csv`:

```csv
number_of_items,Number of items,No,Yes,No,Yes,115,text
```

The new field will appear in the pop-up without any HTML edit.

### Example: show Respondent in the main table

Change the `respondent` row in `fields.csv` from:

```csv
respondent,Respondent,No,Yes,Yes,Yes,90,text
```

to:

```csv
respondent,Respondent,Yes,Yes,Yes,Yes,90,text
```

### Example: remove Subdomain as a filter

Change `filter` from `Yes` to `No` for the `subdomain` row.

## Adding/removing a CSV column safely

If you add a new column to `instruments.csv`, add a corresponding row in `fields.csv` if you want the website to use it.

If you remove a column from `instruments.csv`, its `fields.csv` row is automatically ignored, although it is cleaner to remove that configuration row too.

## Replacing the team logo

The placeholder logo beside the website title is:

`images/team-logo.svg`

The easiest approach is to replace that file with your own SVG while keeping the exact same filename (`team-logo.svg`). No HTML change is needed.

If your real logo is PNG/JPG/WebP instead, upload it to `images/` and update this line near the top of `index.html`:

```html
<img class="team-logo" src="images/team-logo.svg" alt="Team logo placeholder" />
```

Change the `src` and `alt` text appropriately.

## Instrument images

Instrument pop-up images are optional.

1. Add the image to `images/`.
2. Put the relative path in the instrument's `image` cell, e.g. `images/moca.png`.
3. Put accessible alternative text in `image_alt`.
4. Leave both blank when no image is available.

Only publish images you have permission to use. Original explanatory graphics created by the team are preferable to reproductions of copyrighted instrument forms or publication figures.

## CSV notes

- Keep each `id` unique.
- Save/export both CSV files as UTF-8.
- Keep categorical wording consistent because filter options are generated from the actual data.
- Quoted commas, quotation marks, and line breaks are supported.

## Local preview

Because browsers restrict `fetch()` from `file://` pages, double-clicking `index.html` may not load the CSVs. GitHub Pages will work normally.

To preview locally from this folder:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## Prototype disclaimer

The included instrument records are sample/demo data for interface testing. They should not be treated as the definitive aSAH instrument inventory or as COS endorsements.
