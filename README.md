

# Germany's Energy Transition Dashboard

**A 3-page interactive Power BI analysis of Germany's path to 80% renewable energy by 2030.**

Built on hourly electricity market data from Bundesnetzagentur (SMARD), covering April 2021 through early 2026.

---

## 🎬 Demo

Page 1

https://github.com/user-attachments/assets/2023b9d6-098b-49ed-9b26-c7e881e471f0



Page 2

https://github.com/user-attachments/assets/59263fa3-630f-4f0c-baf5-9be9dc342969



Page 3

https://github.com/user-attachments/assets/68b29914-dcfe-4b64-9238-ad8a2b0a5c9a



**↑ interactive walkthrough** — date slicer driving all visuals, page navigation, hover tooltips, heatmap interactivity.

---

## The Question

Is Germany on track to meet its 2030 renewable energy target — and where are the bottlenecks?

This dashboard answers it through three analytical lenses:

1. **The Headline** — how close are we to the target?
2. **The Mix** — what's actually being generated, by what, and when in the day?
3. **The Reality Check** — when does Germany *use* electricity, and does generation align with demand?

---

## Page 1 — Overview: Are We On Track?

![Page 1 Overview] <img width="2560" height="1440" alt="Screenshot 2026-05-14 184940" src="https://github.com/user-attachments/assets/326676f6-31c8-462b-ad94-589ea90f5b5a" />


**Headline finding**: Germany's renewable share climbed from 47% in early 2021 to summer 2025 peaks near 80%. The trajectory is real, but seasonal swings like solar-rich summers vs fossil-heavy winters reveal the deeper systemic challenge.

Key elements: KPI strip with time-intelligence YoY comparison, headline trend line with 2030 reference target, stacked area of the generation mix evolving over time, and an interactive date range slicer driving every visual on the page.

---

## Page 2 — Generation Mix Deep-Dive

![Page 2 Generation Mix]<img width="2560" height="1440" alt="Screenshot 2026-05-14 184956" src="https://github.com/user-attachments/assets/b5d33fea-7e65-470b-9967-366d0a57a683" />


**Key insights**:
- **Wind onshore is now Germany's #1 single source** (535 TWh over the 5-year window, ahead of even lignite)
- **Nuclear vanished** from the mix in April 2023 (visible in the source × year heatmap matrix)
- **Solar's daily profile** shows the classic noon peak — the visual story of why grid flexibility matters

The matrix uses conditional color formatting to turn the year-by-year table into an at-a-glance heatmap. Sources are color-encoded consistently across the dashboard (green = renewable, dark = fossil, purple = nuclear, gray = storage).

---

## Page 3 — Consumption Reality Check

![Page 3 Consumption] <img width="2560" height="1440" alt="Screenshot 2026-05-14 185214" src="https://github.com/user-attachments/assets/e00c1bad-98ea-410f-8372-e2c4ed3fe699" />


**The mismatch**: Generation peaks at noon. Consumption peaks at 11:00 with industrial demand and stays elevated through 18:00 ,but solar drops sharply after 14:00. That afternoon-evening gap is the German energy transition's *real* unsolved problem: **not generation, but storage and grid flexibility**.

The day-of-week × hour heatmap matrix reveals the underlying industrial signal cleanly, sharp weekday demand walls 09:00–13:00, distinct weekend dips.

---

## Technical Highlights

**Data Source**: [SMARD by Bundesnetzagentur](https://www.smard.de) - Germany's official electricity market data platform. Hourly granularity, April 2021 - April 2026, Germany-wide, ~480K rows across Generation and Consumption.

**Data Modeling**:
- **Star schema** with two dimension tables (`Date_Dim` for daily granularity, `Hour_Dim` for hour-of-day) and two fact tables (Generation in long format via unpivot, Consumption)
- `Source_Category` calculated column classifying each source as Renewable / Fossil / Nuclear / Storage
- `Hour` calculated columns on both fact tables, related via `Hour_Dim` to enable cross-table hourly analysis (the marquee visual on Page 3 wouldn't work without this)

**13 DAX Measures**, including:
- Time intelligence with `SAMEPERIODLASTYEAR` for YoY comparisons in percentage points
- Conditional aggregations using `CALCULATE` + filter modifications via `IN` clauses and `Source_Category` filters
- Hour-of-day averages that handle filter context correctly across both long-format and wide-format fact tables
- `Generation Deficit` measure surfacing Germany's net import/export status by period

**Power Query M ETL**: handled German number formats, missing values for retired generators (nuclear post-April-2023 stored as `"-"`), unpivot from wide to long format, date-only column derivation, and hour extraction.

---

## Visual Types Used

Cards · Line charts with reference lines · Stacked area chart · Donut chart · Clustered bar chart with category coloring · Dual-line hour-of-day overlay · Matrix heatmap with conditional formatting · Date range slicer · Page navigation buttons

---

## Stack

Power BI Desktop · DAX · Power Query M ·  SMARD CSV

---

## How to View

| What | Where |
|---|---|
| 🎬 Interactive walkthrough video | Top of this README |
| 🖼️ Static screenshots | `/screenshots` folder |
| 📄 PDF export | `screenshots/energiewende-dashboard.pdf` |
| 🗂️ Full interactive file | `energiewende.pbix` — open with Power BI Desktop |
| 🎨 Theme file | `energiewende-theme.json` |

> A public Power BI Service URL was blocked at the university tenant level (a common security restriction in German academic Microsoft 365 environments). The `.pbix` file fully reproduces all interactivity locally, and the walkthrough video at the top demonstrates it live.

---


**Built by [Avishkar Potale](https://github.com/Avishkar1117)**
