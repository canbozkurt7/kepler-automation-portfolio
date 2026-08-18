[← Home](../../README.md)

# 📊 Marketing > Reporting

Automations that collect performance data and turn it into reports/dashboards.

---

## Google Ads Monthly Comparison Report

**What it does:** A Python script that generates a chart/report page showing month-over-month traffic/conversion/revenue comparison for all active campaigns in the Google Ads account (to be manually added to a slide in a presentation deck).

**Trigger:** Windows Task Scheduler — on the 10th and 20th of the month, at 11:00.

**Tools/integrations used:** Google Ads API, Python (chart/image generation).

**Flow summary:**
- Period-over-period campaign data (this month 1→X vs. last month 1→X) is pulled from the Google Ads API.
- A 1920x1080 image is generated with 3 separate tables for traffic, conversions, and revenue, color-coding improving/worsening/newly-active campaigns.
- The image is manually added to the presentation deck (since automatic slide placement via API isn't supported, this step is manual).

**Status:** Active, runs regularly.

---

## Google Ads Backfill - Report Generator (PDF)

**What it does:** An automation that collects historical weekly campaign/keyword/search-term/impression-share data from the Google Ads account and writes it to a database, then generates a weekly performance report for active campaigns and sends it as a PDF by email.

**Trigger:** Weekly scheduled + manual run option.

**Tools/integrations used:** Google Ads API, Supabase, HTML→PDF conversion, Gmail, AI Agent-assisted commentary block.

**Flow summary:**
- Weekly periods are generated and processed sequentially (with waits in between for rate-limiting).
- Campaign/ad group data and keyword/search-term/impression-share data are pulled separately and written to the database.
- An HTML report is generated from the latest period's data for active campaigns and converted to PDF.
- The report is sent as an email attachment.

**Status:** Active.

---

## Google Ads Backfill (Jan 26 - Today)

**What it does:** A one-time/periodic backfill automation that retroactively fills the database with weekly Google Ads data (campaign, keyword, search term, auction/impression-share stats) from a specific start date to today.

**Trigger:** Manual run.

**Tools/integrations used:** Google Ads API, Supabase.

**Flow summary:**
- The weeks from the start date to today are calculated automatically.
- For each week, campaign, keyword, search-term, and auction impression-share data is pulled from the Google Ads API in sequence.
- Each dataset is formatted and written to the relevant Supabase table, then it moves on to the next week.

**Status:** Active (for one-time/manual use).

---

## Google Analytics: Weekly Report

**What it does:** An automation that groups weekly purchase data from Google Analytics 4 by country and traffic source, turns it into a PDF report, and sends it by email.

**Trigger:** Scheduled — weekly, Monday noon.

**Tools/integrations used:** Google Analytics 4 API, HTML→PDF conversion, Gmail.

**Flow summary:**
- Purchase and conversion rate data by country + source/channel is pulled from GA4.
- Data is grouped and sorted by country, and an HTML report is generated (summary cards + country-based tables).
- The HTML is converted to PDF with a dated filename.
- The report is sent as an email attachment.

**Status:** Active.

---

## PPC Marketing Dashboard

**What it does:** A service running 24/7 on a VPS that pulls Google Ads data hourly, syncs it to a database, and presents it as a live performance dashboard in a React-based web interface (with date-range selection and campaign/channel breakdown).

**Trigger:** Hourly automatic sync (APScheduler) + once on server startup.

**Tools/integrations used:** Google Ads API, Supabase (Postgres), Python (FastAPI + APScheduler), React/TypeScript frontend, Docker, VPS.

**Flow summary:**
- On server startup and every hour, up-to-date data is pulled from the Google Ads API and written to the database.
- The backend serves normalized data for the dashboard via an API.
- The frontend displays this data as charts/tables with a date-range filter.

**Status:** Live, running continuously. (Expansion planned for Meta/Yandex and GA4/Clarity integrations.)
