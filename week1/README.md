# Cold Lead Reactivator for Real Estate Companies

An N8N automation system that reactivates cold leads sitting in your CRM by sending personalized, market-aware follow-up emails — and automatically triages client replies so your sales team only gets pinged when a lead is actually hot.

Built for real estate agencies dealing with large volumes of cold/stale leads that never received proper follow-up.

---

## What This Does

Cold leads are expensive. They sat in your CRM, someone paid to acquire them, and then they went quiet — usually because follow-up was generic, delayed, or never happened at all.

This system fixes that by:

1. Automatically pulling each lead's specific requirements (area, budget, preferences) from the CRM
2. Researching real-time market context for that lead's exact area (price trends, new developments)
3. Generating a fully personalized email — not a template
4. Classifying client replies (Hot / Warm / Cold) and alerting sales instantly on hot leads
5. Keeping the CRM and an activity log updated at every step, with zero manual work

---

## Workflows

### Workflow 1 — Lead Reactivation & Outreach
**File:** `workflow-1-lead-reactivation.json`

**Trigger:** Scheduled / manual (adjust to your needs)

**Steps:**
1. **Fetch Lead Data** — Pulls lead details from the CRM (client requirements, area of interest, budget, etc.)
2. **Market Research** — Runs a Google Search to gather current context on the lead's area (price trends, new developments, market movement)
3. **Generate Personalized Email** — Builds a custom HTML email using the lead's data + market research
4. **Send Email** — Delivers the email to the client
5. **Update CRM Status** — Moves the lead from `Cold` → `Engaged`
6. **Log Activity** — Records the action in the activity log

### Workflow 2 — Reply Classification & Routing
**File:** `workflow-2-reply-classification.json`

**Trigger:** Fires when the client replies to the outreach email

**Steps:**
1. **Capture Reply** — Reads the incoming client email reply
2. **Classify Lead** — Analyzes tone/intent and tags the lead as `Hot`, `Warm`, or `Cold`
3. **Route Hot Leads** — If classified as Hot, sends an instant alert email to the sales team
4. **Update CRM** — Reflects the new classification in the CRM
5. **Log Activity** — Records the classification outcome in the activity log
