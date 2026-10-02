# Field Sales Tracker

An AI-powered field sales automation system built with **n8n, Gemini, Google Sheets, and Gmail**.

It turns messy field notes into structured sales data, scores leads, updates pipeline stages, raises distributor orders, and plans the next day's route.

## What It Does

- Converts Hinglish field notes into structured visit records
- Extracts important sales information from field notes
- Scores leads using predefined business rules
- Automatically updates pipeline stages
- Raises distributor orders based on requirements
- Generates territory and sales reviews
- Plans the next day's field-sales route
- Sends automated summaries and alerts through Gmail

## Tech Stack

- **n8n** — Workflow automation
- **Google Gemini** — AI-powered extraction and analysis
- **Google Sheets** — CRM and business rules
- **Gmail** — Reports, alerts, and order communication

## Workflow

```text
Field Visit Notes
       ↓
AI Extraction
       ↓
Structured Visit Record
       ↓
Lead Scoring
       ↓
Pipeline Update
       ↓
Distributor Orders
       ↓
Territory Review
       ↓
Next-Day Route Plan
       ↓
Email Summary
```

## Files

The `.json` files in this repository contain the n8n workflows.

Import the required JSON file into your n8n instance to use the workflow.

## Setup

Before running the workflows, configure:

1. Google Sheets credentials
2. Gemini API credentials
3. Gmail credentials
4. Your CRM/business-rule sheet
5. Your reps, outlets, pipeline stages, and sales rules

## Note

The workflows are designed as reusable building blocks and can be adapted to different field-sales teams, products, territories, and business rules.
