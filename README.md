# S&P 500 Market Intelligence Dashboard (2014–2017)

An Excel dashboard analyzing trading activity, volatility, weekly patterns, and returns across 506 S&P 500 companies, built entirely with **Power Query** and **Pivot Tables/Charts**.

![Dashboard Preview]([images/dashboard-preview.png](https://github.com/GarimaSingh0109/S-P-Market-Intelligence-Dashboard-2014-2017-/blob/main/Dashboard.png))
*Fig 1: Final dashboard — Trading Activity | Volatility | Weekly Pattern | Investment Return (2014–2017)*

---

## 📌 Project Objective

To design a self-service Excel dashboard that lets a non-technical stakeholder (analyst, investor, or student) understand four years of S&P 500 trading behavior at a glance — without writing a single formula or touching the raw data — by answering:

- How much money moved through the market, and how much volume was traded overall?
- Which stocks and which days drive the most trading activity?
- How volatile are individual stocks over time, and where do the risk spikes occur?
- Which companies delivered the strongest cumulative trading value over the period?

## 💼 Business Problem

Raw tick-level stock market data is large, messy, and not analysis-ready — it typically arrives as one row per stock per trading day, with no derived metrics (returns, price ranges, weekday labels) and no way to compare hundreds of companies side by side.

A trading desk, investment analyst, or content team needing a quick "state of the market" view has two options: build a repeatable Python/BI pipeline, or spend hours manually pivoting spreadsheets every time a new question comes up. Neither is practical for fast, recurring, stakeholder-facing reporting.

**This project solves that by turning ~497K raw price rows into a single-page, refreshable Excel dashboard** that surfaces trading volume, value, volatility, and return metrics on demand — using only Excel's native data modeling tools (Power Query + PivotTables), so it stays lightweight, auditable, and easy for anyone on the team to maintain or extend.

## 🗂️ Dataset Description

| Attribute | Detail |
|---|---|
| **Source** | Maven Analytics — S&P 500 Stock Prices dataset |
| **Time period** | January 2014 – December 2017 |
| **Granularity** | Daily OHLCV (Open, High, Low, Close, Volume) per stock |
| **Companies covered** | 506 S&P 500 constituents |
| **Raw row count** | ~497,000 rows |
| **Raw columns** | `Symbol`, `Date`, `Open`, `High`, `Low`, `Close`, `Volume` |
| **Engineered columns** | `Price Range`, `Daily Return`, `Trading Value`, `Year`, `Month`, `Month Name`, `Weekday`, `Weekday No` |

The engineered columns were derived in Power Query rather than shipped with the source file, so the dataset could support KPI cards and time-based comparisons (see Steps below).

## 🛠️ Tools & Technologies

- **Microsoft Excel** — Power Query (data cleaning & transformation), PivotTables & PivotCharts (aggregation), Excel formulas (KPI cards)
- **Data modeling**: single flat fact table sourced by all pivots (star-schema-lite approach within one sheet)

## 🧭 Steps Followed

1. **Data Import**
   Loaded the raw S&P 500 CSV/dataset into Excel via Power Query (`Get & Transform Data`).

2. **Data Cleaning**
   - Checked and corrected data types (dates, numeric OHLCV fields)
   - Removed duplicate and null rows
   - Standardized stock symbols and date formatting

3. **Feature Engineering (Power Query)**
   - `Price Range` = High − Low
   - `Daily Return` = (Close − Open) / Open
   - `Trading Value` = Close × Volume
   - Extracted `Year`, `Month`, `Month Name`, `Weekday`, and `Weekday No` from `Date` for time-based grouping

4. **Data Loading**
   Loaded the transformed table into the Excel Data Model to support large-scale (497K-row) pivoting without performance lag.

5. **Pivot Table Construction**
   Built individual pivot tables for:
   - Total trading volume and total trading value (all companies, full period)
   - Average trading volume by weekday
   - Top stocks by volume on the single highest-volume trading day
   - Daily volatility (price range) trend for a focus stock
   - Top stocks ranked by cumulative trading value across 2014–2017

6. **KPI Card Design**
   Summarized headline metrics — Total Trading Volume, Total Trading Value, Companies Tracked, Average Daily Return — into four callout cards using formulas referencing the pivot outputs.

7. **Chart Creation**
   Converted each pivot table into a matching PivotChart: horizontal bar (top stocks by volume), column chart (volume by weekday), line chart (daily volatility), and column chart (top 3 stocks by value).

8. **Dashboard Assembly & Formatting**
   Arranged all KPI cards and charts on a single dashboard sheet, applied a consistent navy/gold/green/purple color scheme per section, added titles and a subtitle summarizing the dashboard's scope, and removed all pivot table/filter clutter from the visible sheet.

9. **QA & Refresh Check**
   Validated KPI totals against raw data spot-checks and confirmed the dashboard refreshes cleanly when the underlying query is re-run.

## 📊 Key Metrics on the Dashboard

| KPI | Value |
|---|---|
| Total Trading Volume | 2.11T+ |
| Total Trading Value | 120T+ |
| Companies Tracked | 506 |
| Average Daily Return | 0.03% |

**Dashboard sections:**
- **Top 2 Stocks by Volume on Peek Day** — BAC and AAPL led single-day trading volume
- **Average Trading Volume by Day of Week** — Volume trends upward through the week, peaking on Friday
- **AMZN Daily Volatility (Top 50)** — Highlights AMZN's price-range spikes across 2015–2017
- **Top 3 Stocks in 2014–2017** — BAC, AAPL, and GE led cumulative trading value over the full period

## 🔑 Key Learnings

- Power Query can fully replace manual formula-based cleaning for six-figure-row datasets, keeping the workbook light and the transformation steps auditable/re-runnable.
- Deriving metrics (returns, trading value, weekday) *before* pivoting simplifies every downstream chart and avoids repeated calculated fields.
- A dashboard's usefulness comes as much from restraint (four KPIs, four charts) as from the data behind it — the goal was a one-glance market snapshot, not an exhaustive report.

## 🚀 Future Scope

- Add a slicer/filter panel to let users switch the volatility and top-stock views to any symbol on demand
- Extend the dataset beyond 2017 for a rolling multi-year view
- Rebuild the same model in Power BI to compare performance and interactivity against the Excel version

---
*Part of the "Data Insight with Garima" YouTube series — building real business dashboards in Excel, explained in Hinglish, step by step.*
