# G7 Bond Yields and Debt Dashboard

This page shows 10-year government bond yields and debt-to-GDP for the G7 countries.

The G7 countries are Canada, France, Germany, Italy, Japan, the United Kingdom, and the United States.

## What it shows

- 10-year sovereign bond yields, monthly, in percent per year.
- General government gross debt, annual, as a percent of GDP.
- One chart per country, or all G7 countries in one chart.
- A table with the latest yield, date, and debt value for each country.
- Time ranges of 5, 10, and 20 years, or all data.

## Data sources

The page fetches live data in the browser. No API key is required.

- Yields: OECD Data Explorer, SDMX API (Main Economic Indicators, long-term interest rates).
- Fresher yield data: Bank of Canada Valet (Canada, daily), Bundesbank SDMX (Germany, monthly), US Treasury (United States, daily), Bank of England (United Kingdom, daily).
- Debt: OECD Economic Outlook No. 119, general government gross financial liabilities as a percent of GDP.
- Debt for Germany, France, and Italy: Eurostat quarterly Maastricht debt (`gov_10q_ggdebt`).

If the live APIs are unreachable, the page uses an embedded snapshot from 2026-09-15.

## View the dashboard

Open the live page: https://ezomode.github.io/g7-bond-debt-dashboard/

Or open `index.html` in a browser. The page needs internet access for the chart library and the live data.

## Daily yields snapshot

A GitHub Actions workflow runs daily at 18:00 UTC. It does these steps:

1. Run `scripts/fetch_daily_yields.py`.
2. Fetch US yields from the US Treasury daily yield curve.
3. Fetch UK yields from the Bank of England nominal spot curve.
4. Merge the new values into `data/daily-yields.json`.
5. Commit the file if it changed.

## Run the fetch script

1. Install Python 3.12.
2. Run `pip install openpyxl`.
3. Run `python scripts/fetch_daily_yields.py`.

The script writes `data/daily-yields.json`. It exits with code 1 only if it fetches no data and no snapshot exists.

## Files

- `index.html` — the full dashboard (HTML, CSS, JavaScript, ECharts 5.5.1).
- `data/daily-yields.json` — daily US and UK 10-year yields.
- `scripts/fetch_daily_yields.py` — the daily snapshot script.
- `.github/workflows/daily-yields.yml` — the daily workflow.
