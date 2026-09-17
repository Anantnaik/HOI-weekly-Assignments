The Product Launch Desk

An AI-powered product launch automation system built with n8n,
Google Sheets, Gemini, and Gmail.

The system takes a single product description and automatically turns it
into a complete launch kit.

What It Does

Given basic product information, the workflow generates:

Product positioning

Landing page copy

5-email launch sequence

FAQs

Objection-handling sheet

Social media content

Launch calendar

Launch assets and summary

Workflow

Product Details
      ↓
Google Sheets
      ↓
n8n Workflow
      ↓
Research & Context
      ↓
Multiple Gemini AI Agents
      ├── Positioning Agent
      ├── Landing Page Agent
      ├── Email Sequence Agent
      ├── FAQ Agent
      ├── Objection Writer Agent
      └── Social Pack Agent
      ↓
Launch Assets
      ├── Google Sheets
      ├── Gmail
      ├── Documents / PDFs
      └── Launch Calendar

Tech Stack

Tool                Purpose

n8n             Workflow orchestration and automation
Google Sheets   Product CRM and asset storage
Gemini          AI-powered content generation
Gmail           Email delivery
Web Search      Product and competitor research

Example

Input

A product description such as:

A 500ml bottle of slow-steeped cold brew concentrate made from
single-origin Chikmagalur arabica.

The system also receives information such as:

Product name

Tagline

Category

Price

Target audience

Competitors

Product description

Output

The automation can produce a complete launch kit containing:

A clear positioning strategy

Landing page messaging

A 5-email campaign

Customer FAQs

Responses to common objections

Social content

A launch schedule

Key Features

Multiple AI Agents

Instead of sending everything through one generic prompt, the workflow
uses specialized Gemini agents for different marketing tasks.

Each agent focuses on a specific job, making the generated output more
structured and consistent.

Automated Research

The workflow can research the product, audience, and competitors before
generating the launch assets.

Centralized Asset Management

Generated assets are stored and organized through Google Sheets, making
it easier to track the launch process.

Automated Email Delivery

The workflow can send generated launch content through Gmail.

Reusable System

The workflow is designed as a reusable launch system rather than a
one-off automation.

Change the product information and the same system can generate a new
launch kit.

Example Launch Output

A single product run can generate:

46+ assets

5 emails

8 FAQs

2 creatives

9-day launch plan

The exact output can vary depending on the product and workflow
configuration.

Why This Automation?

Launching a product often requires creating many different assets across
different channels.

Instead of manually starting from a blank document for every asset, this
system connects the entire process:

One product description → research → strategy → content → launch
assets → distribution.

Project Goal

The goal is to create a reusable AI product launch engine that
reduces repetitive marketing work and helps businesses move from product
idea to launch-ready content faster.

Built With

n8n + Google Sheets + Gemini + Gmail

Project Type

AI Automation / Marketing Automation / n8n Workflow

Author

Built as an AI automation project.
