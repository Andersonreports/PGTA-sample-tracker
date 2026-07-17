# PGTA Sample Tracker

A live dashboard for tracking PGT-A samples through the lab pipeline:
**Received → Extraction → Pending → Report Prep → Released.**

It is a single self-contained `index.html` — no build step, no server — that
fetches data from a Google Sheet (via a Google Apps Script Web App) and refreshes
every 30 seconds.

## Live site

Hosted on GitHub Pages: **https://andersonreports.github.io/PGTA-sample-tracker/**

## Features

- Five status stat cards with live counts
- Current-samples table with search, status pills, overdue highlighting, and "View all"
- Fast-track alert panel (overdue / due-soon / stuck samples)
- Summary panel (total, in-progress, completion rate, average turnaround)

## Connecting the live sheet

The dashboard ships with **demo data** so the layout is visible immediately.
To go live, edit `index.html`:

```js
const APPS_SCRIPT_URL = 'REPLACE_WITH_PGTA_APPS_SCRIPT_EXEC_URL';
```

Replace it with the deployed Apps Script Web App `/exec` URL. The script should
return the sheet as a JSON grid (array of rows). Expected column headers
(aliases are matched flexibly): `Sample ID`, `Status`, `Assigned`, `Received`,
`Due`, `Released`.

> **Note:** GitHub Pages is public and static. Once a real endpoint URL is
> embedded here it becomes publicly callable — keep any sensitive access behind
> the Apps Script's own auth, or serve the page from a gated host instead.
