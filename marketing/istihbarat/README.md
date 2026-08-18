[← Home](../../README.md)

# 📊 Marketing > Intelligence

Systems that automatically collect competitor and market data.

---

## Google Ads Competitor Keyword Monitor

**What it does:** A competitive intelligence system that scans live Google search result ads weekly for a manually defined list of keywords, compares which competitors are advertising on which keyword and any changes in ad copy/position week-over-week, and sends an AI-assisted summary email when a meaningful change is detected.

**Trigger:** Scheduled — weekly.

**Tools/integrations used:** SerpAPI (live Google search results), Supabase, AI Agent (LLM-powered analysis), Gmail.

**Flow summary:**
- The active keyword list is read from Supabase.
- For each keyword, the current Google ads (position, brand, headline, description) are pulled via SerpAPI and the advertiser name is normalized.
- Results are saved to Supabase; compared against the previous scan of the same keyword to detect newly entered/exited advertisers, headline changes, and position shifts.
- If there's a meaningful change, an AI Agent interprets the findings and drafts a summary analysis email.

**Status:** Active.

---

## Hotel Competitive Price Monitoring

**What it does:** A competitive price monitoring system that weekly scans competitor hotel prices at the SAW/RIX/KUL airport locations, compares them against your own prices, and summarizes the market average and price changes in an email report.

**Trigger:** Scheduled — weekly, Monday 08:00.

**Tools/integrations used:** Apify (Booking.com scraping), Supabase, Google Sheets (own prices), Gmail.

**Flow summary:**
- Check-in/check-out dates are calculated automatically (today +14/+15 days).
- For each location, hotel prices on Booking.com are scraped via Apify and saved to Supabase.
- This week's and last week's data are compared to detect price changes; your own price is compared against the market average to determine position (above/below/equal).
- Results are turned into location-based tables in an HTML email report and sent.

**Status:** Active.

---

## 4 Track Competitor Website Updates

**What it does:** A general-purpose price tracking template that regularly scans a competitor/reference website's pricing page via AI-assisted scraping to detect price/plan changes, updating a record table if a change is found.

**Trigger:** Scheduled — daily.

**Tools/integrations used:** AI Agent (LLM-powered page reading/parsing), a proxy/scraping service, Google Sheets.

**Flow summary:**
- The URL to track and its parameters are defined.
- The last known price data is read from Google Sheets.
- The AI Agent reads the target page and converts plan name/price/feature info into structured data.
- New data is compared against the old; if there's a difference, Google Sheets is updated, otherwise nothing happens.

**Status:** Active. (A general-purpose template; reusable for different competitor/product pages.)

---

## Meta Ads Creative Fatigue Detection

**What it does:** A system that monitors Meta (Facebook/Instagram) ad performance daily, automatically detects which ad creatives are experiencing "creative fatigue" (viewer fatigue from repeated exposure), and alerts the team via Slack.

**Trigger:** Scheduled — weekly, Monday 08:00.

**Tools/integrations used:** Meta Marketing API (Insights), Supabase, Slack, Gmail.

**Flow summary:**
- The last 14 days of daily ad performance data (CTR, frequency, CPM, impressions, etc.) is pulled from the Meta API and written to the database.
- For each ad, the full history is pulled and 3 signals are calculated: CTR drop (20%+), high frequency (3+ impressions to the same person), and a CPM increase + CTR drop combination.
- If 2 or more signals are triggered, the ad is considered "fatigued."
- If no alert has already been sent that day (duplicate-prevention check), an alert is sent to the Slack channel and by email, and logged.

**Status:** Active.

---

## Google Trends

**What it does:** A simple market-interest tracking tool that compares search interest related to the airport "nap room" / capsule hotel concept across different locations and logs it as a time series to a Google Sheet.

**Trigger:** Manual run.

**Tools/integrations used:** SerpAPI (Google Trends data), Google Sheets.

**Flow summary:**
- The weekly/monthly interest index for the last 12 months is pulled for the defined search terms.
- Results are converted into date-based rows and added to Google Sheets.

**Status:** Active, for manual/periodic checking.

---

## kepler-nationality-ad-copy (Skill)

**What it does:** A Claude Code skill that generates high-CTR Google Ads headline/description copy for the SAW (Istanbul), KUL (Kuala Lumpur), and RIX (Riga) airport capsule hotel campaigns, tailored to each location's actual guest nationality and search-language mix (instead of a single generic script).

**Trigger:** On demand (e.g. "write a headline for SAW").

**Tools/integrations used:** Claude Code skill system, Google Ads campaign context.

**Flow summary:**
- The user specifies a location (SAW/KUL/RIX) and campaign type (Search/PMax).
- The skill generates headline, long headline, and description copy matching that location's guest nationality/language profile.

**Status:** Actively in use.
