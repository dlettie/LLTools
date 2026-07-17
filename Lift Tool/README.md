# DemandGen — Dataset Mapper

A single-file, browser-based tool for analyzing geo-lift experiments. You upload
three CSVs, set your experiment dates, and the page merges the data and computes
lift analysis (summary stats, geo-level lift, daily cumulative factors, and
charts), with an option to export everything to Excel.

Everything runs entirely in your browser. No server, no build step, no
installation — it's one `.html` file you open and use.

## Quick start

1. Open `dataset-mapper.html` in any modern browser (double-click it, or host it
   on GitHub Pages / any static host).
2. Upload the three required CSV files (see below).
3. Enter your experiment dates.
4. Click **Process** to generate the analysis.
5. Optionally click **Export** to download results as an Excel workbook.

## Inputs

The tool expects three CSV files:

| File | Purpose | Required columns |
| --- | --- | --- |
| **Sales Summary** | Daily sales by DMA, outcome, and category | `geo_id`, `day` |
| **Cells Mapping** | Maps each DMA to a cell number and type | `DMA ID`, `Cell Number` |
| **Matched Markets** | Control ↔ treatment DMA pairs | `Control DMA ID` |

You also provide three dates:

- **Experiment start** — the AB (test) period begins here. The 30 days prior are
  used as the AA (baseline) period.
- **Experiment end** — the end of the AB period.
- **AC end** (optional) — an additional post-period window that begins the day
  after the experiment end. Leave blank for an open-ended AC period.

## What it produces

After processing, the page displays:

- **Summary statistics** across control and treated cells, by segment
- **Lift by window** — AB vs AC comparison
- **A pair filter** for excluding specific control/treatment pairs
- **Geo-level lift analysis** per segment
- **Daily cumulative factor** trends
- **Lift charts** with hover tooltips
- **The full merged dataset** in a searchable, filterable table

The Excel export produces a workbook with a Summary Stats sheet plus per-segment
Geo Lift and Daily Factor sheets, and a Full Dataset sheet.

The merged dataset uses these columns: `day`, `geo_id`, `DMA`, `period`, `cell`,
`cell_type`, `pair`, `target_variable_nm`, `category_nm`, `category_type`,
`orders`, `actual_sales`, `sales`, `aov`, `targetable_flag`.

## Requirements

- A modern web browser (Chrome, Firefox, Safari, or Edge).
- An internet connection **the first time you load the page** and **if you use
  Excel export** — see the Privacy section for why.

No other dependencies. There is no backend and nothing to install.

## Privacy

**Your uploaded data stays on your machine. It is never sent to any server.**

The tool reads your CSVs with the browser's built-in `FileReader` API and does
all parsing, merging, and analysis locally in the page's memory. There is no
`fetch`, form submission, analytics call, or any other code that transmits your
data off your device. Your data exists only for the current session — it is not
saved to disk, cookies, `localStorage`, or any other browser storage, and it is
gone the moment you close or reload the tab.

That said, the page loads two things from third-party servers. **Neither one
sends your data anywhere** — they are one-way downloads of resources *into* your
browser — but they are worth understanding:

1. **Google Fonts** (`fonts.googleapis.com`, `fonts.gstatic.com`) — loads the
   "Inter" font when the page opens.
2. **Cloudflare CDN** (`cdnjs.cloudflare.com`) — downloads the SheetJS/XLSX
   library, but **only when you click Export**. The Excel file itself is then
   generated locally in your browser.

Because your browser requests these files, those third parties can see standard
request metadata — your IP address, a timestamp, and basic browser information —
simply from the fact that a page was loaded. This metadata reveals **nothing
about the contents of your uploaded CSVs**; it's the same footprint any website
using external fonts or a CDN leaves behind.

### Making the page fully self-contained (optional)

If you want the tool to make **zero external requests** — for example, for use in
an air-gapped environment or with especially sensitive data — you can host these
resources locally instead:

- Download the Inter font files, add them to your repo, and replace the Google
  Fonts `<link>` tags with a local `@font-face` definition.
- Download `xlsx.full.min.js` from the Cloudflare CDN, add it to your repo, and
  point the export code at the local copy instead of the CDN URL.

After those two changes, the page loads and runs without contacting any outside
server at all.

## License

Add your license of choice here.
