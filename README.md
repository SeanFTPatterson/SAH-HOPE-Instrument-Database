# aSAH Measurement Instrument Database — GitHub Pages prototype

This prototype separates the website from the research data. The page reads its instrument records from:

`data/instruments.csv`

## Publish on GitHub Pages

1. Create a new GitHub repository (for example, `asah-instrument-database`).
2. Upload **the contents of this folder** so that `index.html` is at the repository root and `data/instruments.csv` is inside the `data` folder.
3. Commit the files.
4. In the repository, open **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select the `main` branch and `/ (root)`, then save.
7. GitHub will provide the public Pages address after deployment.

## Update the instrument database

Edit `data/instruments.csv` in Excel, LibreOffice, Google Sheets, or a text editor, then replace the existing CSV in the repository and commit the change. The website will read the updated CSV automatically.

Keep the column headers unchanged:

`id,name,acronym,domain,subdomain,construct,type,status,respondent,administration,time,used,description,source`

You can add or remove rows without changing `index.html`.

### Important CSV notes

- Keep every `id` unique.
- Save/export as UTF-8 CSV.
- Spreadsheet software will automatically quote descriptions containing commas. That is supported by the website.
- The prototype also supports quotation marks and line breaks inside properly quoted CSV fields.
- Keep categorical wording consistent (for example, use exactly the same domain and status names) because filters are generated automatically from the CSV.

## Local preview

Because browsers restrict `fetch()` from `file://` pages, double-clicking `index.html` may not load the CSV. GitHub Pages will work normally.

For a local preview, run a simple web server from this folder, for example with Python:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

## Prototype disclaimer

The included records are sample/demo data for interface testing. They should not be treated as the definitive aSAH instrument inventory or as COS endorsements.


## Adding instrument images

This version supports an optional image in each instrument pop-up.

1. Add your image file to the `images/` folder. PNG, JPG/JPEG, WebP, and SVG all work in modern browsers.
2. In `data/instruments.csv`, enter the relative file path in the `image` column, for example: `images/moca.png`.
3. Add accessible alternative text in `image_alt`, for example: `Illustration showing the major cognitive domains assessed by the MoCA.`
4. If an instrument does not have an image, leave both fields blank. The pop-up will automatically omit the image area.

The first sample record points to `images/example-instrument-graphic.svg` so you can see the feature working after deployment. Replace or remove that placeholder before using the resource publicly.

Use only images that you have permission to publish. Original explanatory graphics created by your team are preferable to reproductions of copyrighted instrument forms or publication figures.
