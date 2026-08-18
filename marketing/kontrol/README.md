[← Home](../../README.md)

# 📊 Marketing > Monitoring

SEO/Ads health checks and alert systems.

---

## Weekly Website SEO Audit System (v3 → v4)

**What it does:** A system that runs a regular, multi-source SEO/technical health/performance audit for the Kepler Club website and produces a PDF report — including a weighted score (0-100, letter grade) and an AI-assisted executive commentary — sent by email. It has evolved through several iterations over time: v3 covers a classic technical SEO audit; v4 adds an **AI Overview / GEO risk scoring** subsystem (visibility risk in Google's AI-powered search summaries) that also automatically generates content recommendations for keywords carrying this risk (see DataForSEO AI Overview Advisor).

**Trigger:** Scheduled — every 3 days or weekly depending on version, in the morning.

**Tools/integrations used:** Google PageSpeed Insights, Google Search Console, SSL check, UptimeRobot, robots.txt/sitemap scan, IP/GEO detection, DataForSEO (in v4), AI Agent (Anthropic Claude-based "SEO & GEO Expert" advisor role), HTML→PDF conversion, Gmail.

**Flow summary:**
- When the scheduler triggers, the target site/domain settings are loaded.
- In parallel, PageSpeed (mobile/desktop), site HTML (meta/title/structured data), robots.txt, sitemap, SSL, uptime, Search Console, and (in v4) GEO data are collected.
- A scoring engine weights all sources to produce an overall score/grade and a list of critical issues.
- An HTML report is generated from the results; an AI Agent interprets the report from an executive perspective, adding an executive summary, opportunities, and strategic recommendations.
- (v4) If the AI Overview risk exceeds a certain threshold, the DataForSEO sub-workflow is called to get content recommendations for the at-risk keywords, which are added to the report.
- The report is converted to PDF and sent by email.

**Status:** Active (different test/production copies of the same system).

---

## DataForSEO AI Overview Advisor — Sub Workflow

**What it does:** A sub-workflow called from the SEO Audit system that identifies Google AI Overview opportunity/risk keywords from DataForSEO SERP data and keyword ideas, and generates AI-assisted content recommendations for those keywords.

**Trigger:** Sub-workflow — runs when called from another workflow (SEO Audit v4); has no scheduled trigger of its own.

**Tools/integrations used:** DataForSEO API, Anthropic Claude (LLM-powered content recommendations).

**Flow summary:**
- The incoming keyword list is processed in batches.
- For each keyword, SERP checks and keyword ideas are retrieved via DataForSEO.
- Opportunities are filtered and scored.
- Content recommendations from the Claude model are retrieved for the scored opportunities, packaged into an HTML block, and returned to the calling workflow.

**Status:** Active (only runs via sub-workflow calls).

---

## Google Ads Metric Alert

**What it does:** A performance monitoring system that compares Google Ads campaigns' critical metrics (CPA/ROAS/CPC) throughout the day (every 6 hours) against a 3-day average and predefined thresholds, sending an email alert with AI-assisted commentary when an anomalous deviation is detected. It also breaks down hourly performance by AB/D region (Europe/US East/US West).

**Trigger:** Scheduled — every 6 hours.

**Tools/integrations used:** Google Ads API, AI Agent (LLM-powered commentary), Gmail.

**Flow summary:**
- Today's and the last 3 days' campaign metrics, plus hourly segment data, are pulled from the Google Ads API.
- CPA/ROAS/CPC are checked against both a fixed threshold and change vs. the 3-day average; region-based hourly performance is also calculated.
- For campaigns exceeding the threshold/change, an AI Agent generates commentary on the likely cause of the deviation and recommended actions.
- Alerts are compiled into a single email and sent.

**Status:** Active.

---

## Upload Keywords to Google Ads

**What it does:** A bridge automation that regularly pulls the existing keywords from the Google Ads account and automatically syncs them to the tracking list used by the competitor/keyword monitoring systems (see the Intelligence category).

**Trigger:** Scheduled — weekly.

**Tools/integrations used:** Google Ads API, Supabase.

**Flow summary:**
- All keywords and their statuses (active/paused/removed) are pulled from the Google Ads account.
- Each keyword is enriched with the standard fields required for the tracking list (location, language, device, priority, etc.).
- Written to the tracking table in Supabase.

**Status:** Active.

---

## marketing-context-control (Skill)

**What it does:** A Claude Code skill that automatically pulls the right context for Kepler Club performance marketing and guest questions — accessing both historical/normalized data in Supabase and live campaign/keyword/search-term data from the Google Ads API to fetch context relevant to the question.

**Trigger:** On demand (kicks in automatically when a question about campaign/performance/guest nationality, etc. is asked).

**Tools/integrations used:** Supabase, Google Ads API, Claude Code skill system.

**Flow summary:**
- Based on the type of question, the relevant data source (historical report vs. live campaign data) is determined.
- The relevant table/GAQL query is run, and the result is presented as context for the question.

**Status:** Actively in use.

---

## pmax-performance-analyzer (Skill)

**What it does:** A Claude Code skill that audits Performance Max campaigns (SAW/KUL/RIX) — analyzing asset group performance and ROAS, asset quality ratings (Best/Good/Low), audience signal strength, and cannibalization risk against standard Search/Shopping campaigns for the same products.

**Trigger:** On demand (e.g. "assess PMax", "is there cannibalization?").

**Tools/integrations used:** Google Ads API (PMax asset group data), Claude Code skill system.

**Flow summary:**
- The relevant PMax campaign's asset groups and performance data are pulled.
- Asset quality, audience signal strength, and overlap with Search/Shopping are analyzed and presented as a summary assessment.

**Status:** Actively in use.
