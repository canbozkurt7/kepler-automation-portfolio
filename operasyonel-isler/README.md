[← Home](../README.md)

# 🔧 Operations

Systems that automate daily operations (guest reviews, feedback, internal knowledge base, internal reporting).

---

## Multi-Business Google Reviews

**What it does:** A multi-business review management system that automatically monitors Google Business Profile reviews across Kepler Club's different locations (SAW, KUL Airside/Landside, RIX Airside/Landside), detects new reviews and generates AI-drafted replies, sends instant WhatsApp alerts to the relevant team for low-rated reviews, and logs all review data to Google Sheets and Supabase.

**Trigger:** Designed to run automatically via a separate Google Business Profile trigger per location (when a new review comes in); currently running in manual-run mode in production.

**Tools/integrations used:** Google Business Profile API, Google Sheets, Supabase, WhatsApp Business API, OpenAI-powered AI Agent (LangChain).

**Flow summary:**
- Reviews coming from each location are compared against existing records in Google Sheets to filter out the new ones.
- New reviews are converted to a standard format and routed by location.
- The AI Agent generates a draft reply automatically, which is sent back as a reply to the review via the relevant Google Business Profile.
- Reviews rated below 5 stars trigger a WhatsApp alert to the internal team.
- All reviews are logged to Google Sheets and Supabase.

**Status:** Active (production trigger not yet connected, run manually).

---

## Monthly Receptionist Mention Count

**What it does:** A performance tracking system that calculates how many times receptionist names are mentioned in guest reviews during the month and emails the report to the relevant managers.

**Trigger:** Scheduled — on the 15th and last day of the month at 09:00.

**Tools/integrations used:** Supabase (mention counting via RPC query), Gmail.

**Flow summary:**
- Triggered on the set days; per-staff mention counts are retrieved via a Supabase function call.
- Results are converted into an HTML table.
- Sent by email to the relevant managers.

**Status:** Active.

---

## WhatsApp Chatbot - Supabase v2

**What it does:** A customer service chatbot that receives guest messages coming in via WhatsApp (text, voice note, image) for Kepler Club and automatically replies through an AI Agent, supporting reservation and general information questions.

**Trigger:** Webhook — automatically triggered on an incoming WhatsApp message.

**Tools/integrations used:** WhatsApp Business API, AI Agent (LangChain, LLM-powered), voice transcription and image analysis models, Postgres-based chat memory, availability check/reservation/price calculation tools via an external MCP server.

**Flow summary:**
- Incoming messages are processed differently depending on type (text/voice/image); voice is converted to text, images to analysis text.
- The AI Agent generates its response by relying only on defined tools (document search, availability check, price calculation) — it's restricted from making assumptions from general knowledge.
- Conversation history is kept in memory per user.
- The reply is sent back to the same WhatsApp conversation.

**Status:** Active.

---

## Upload data to Supabase

**What it does:** An infrastructure automation that automatically chunks documents uploaded to Google Drive (FAQs, room/service info, etc.), converts them into embeddings, and uploads them to Supabase's vector database, keeping the knowledge source for the chatbots (WhatsApp/Instagram) up to date.

**Trigger:** Automatic when a new file is added to a specific Google Drive folder (polling, checked every minute) + manual run option.

**Tools/integrations used:** Google Drive, OpenAI Embeddings, Supabase Vector Store (LangChain).

**Flow summary:**
- When a new file is detected, it's downloaded and split into text chunks.
- Each chunk is passed through the OpenAI embedding model.
- Results are written (as vectors) into Supabase's `documents` table, so the chatbots can search this information.

**Status:** Active (triggered manually/per file).

---

## Slack → Google Sheets Guest Feedback (OCR)

**What it does:** A Node.js application that automatically parses guest feedback forms dropped into Slack channels as text or images (via OCR, with Turkish support) and logs them to Google Sheets.

**Trigger:** When a new message/image is posted to Slack (bot event-driven), plus a catch-up mode for messages missed while offline.

**Tools/integrations used:** Slack API, Tesseract.js (OCR), Google Sheets API (Service Account), Node.js. Starts automatically via Task Scheduler on Windows startup.

**Flow summary:**
- Form submissions in the Slack channel (Name, Date, Receptionist, Rating, etc. fields) are detected.
- If it's an image, it's converted to text via OCR.
- The parsed data is validated, duplicate entries are prevented (state tracking), and it's added as a row to Google Sheets.

**Status:** Active, running continuously (as a Windows service).
