[← Home](../README.md)

# 🚀 Business Development / Growth

Systems that automate customer communication and growth channels.

---

## Instagram DM Replier

**What it does:** A customer service chatbot that automatically responds to direct messages coming into Kepler Club's Instagram account, using an AI Agent to generate answers from a business-specific knowledge base (prices, services, FAQs).

**Trigger:** Webhook — automatically triggered when a new message arrives on Instagram.

**Tools/integrations used:** Instagram Messaging API, AI Agent (Anthropic Claude Haiku), vector-based knowledge base (Supabase), Postgres-based chat memory.

**Flow summary:**
- If the incoming message isn't empty, it's passed to the AI Agent.
- The Agent looks up relevant information from the business-specific knowledge base (identifying which location it belongs to) and generates a response; there are predefined standard responses for special cases like lost items, reservation info screens, and capsule room images.
- Conversation history is kept in memory per user.
- The response is sent back as an Instagram DM.

**Status:** Active.

---

## Kepler Club Mailing

**What it does:** The initial setup step for a new mailing/email marketing integration (via Resend) — an automation designed to trigger when a new contact is created, currently still in the development/setup stage.

**Trigger:** New contact creation event (Resend) + manual test trigger.

**Tools/integrations used:** Resend (email sending platform).

**Flow summary:**
- Currently only the trigger nodes are defined; the actual email content/flow logic hasn't been added yet.

**Status:** Active, in setup.

---

## ElevenLabs AI Assistant

**What it does:** A voice AI assistant — a conversational agent that answers guest/customer questions by voice.

**Trigger:** On demand (when a voice call/conversation is started).

**Tools/integrations used:** ElevenLabs Agents platform.

**Status:** Set up; work in progress on integration/access settings.
