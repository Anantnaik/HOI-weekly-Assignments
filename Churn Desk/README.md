# The Quiet Churn Desk

**An AI-powered customer retention monitoring system built with n8n,
Google Sheets, Gemini AI agents, and Telegram.**

The Quiet Churn Desk learns each customer's usual ordering rhythm,
detects when that pattern starts to change, and ranks at-risk customers
by potential revenue exposure. Instead of relying only on a fixed
inactivity rule such as "no order in 90 days," it looks for
customer-specific changes in ordering behaviour.

> **Core idea:** Identify customers who are quietly drifting away early
> enough for the business to investigate and take action.

------------------------------------------------------------------------

## What it does

-   Tracks customer ordering patterns using historical order data.
-   Compares each customer's current inactivity against their usual
    ordering gap.
-   Classifies customers into statuses such as **Healthy**, **Watch**,
    **Slipping**, **Gone Quiet**, **Seasonal**, and **Too New**.
-   Estimates yearly customer value and revenue at risk.
-   Uses Gemini AI agents to interpret customer data and write clear
    explanations and suggested next actions.
-   Sends business-owner briefs and individual customer cards through
    Telegram.
-   Records owner decisions and supports actions such as taking action
    or snoozing a customer.
-   Provides a dashboard view of customer health and revenue-at-risk
    trends.

## Why it is different from a basic 90-day churn alert

A fixed inactivity rule treats every customer the same. But customers do
not all order at the same frequency.

For example: - A customer who normally orders every 7 days may need
attention after a relatively short delay. - A customer who normally
orders every 30 days should not be treated the same way. - A seasonal
customer may naturally have a longer quiet period.

The Quiet Churn Desk uses each customer's usual ordering gap as context,
with configurable thresholds and a seasonal lookback, to make the
monitoring more relevant to their behaviour.

------------------------------------------------------------------------

## System architecture

  -----------------------------------------------------------------------
  Component                           Responsibility
  ----------------------------------- -----------------------------------
  **Google Sheets**                   Customer/order CRM data,
                                      configuration, results, and
                                      recorded decisions

  **n8n**                             Workflow orchestration, data
                                      processing, integrations, and
                                      delivery

  **Gemini AI agents**                Read and interpret customer data,
                                      explain risk signals, and draft
                                      recommendations

  **Telegram**                        Owner-facing briefs, customer
                                      cards, and decision interactions

  **Dashboard / report**              Customer status overview and
                                      revenue-at-risk monitoring
  -----------------------------------------------------------------------

### High-level flow

1.  Customer and order data is maintained in Google Sheets.
2.  The n8n workflow retrieves the relevant data and prepares it for
    analysis.
3.  The system checks customer ordering history and compares current
    inactivity with each customer's usual ordering gap.
4.  Gemini agents help interpret the results and write customer-specific
    reasons and suggested next actions.
5.  The workflow packages the results, saves the output, and sends a
    brief and selected customer cards through Telegram.
6.  The owner can record a decision, such as taking action or snoozing a
    customer. The decision is written back to the system.

------------------------------------------------------------------------

## Customer monitoring

The CRM view includes fields such as:

  Field               Meaning
  ------------------- --------------------------------------------------
  `customer`          Customer or account name
  `status`            Current customer health classification
  `usual_gap_day`     Typical number of days between orders
  `days_silent`       Days since the most recent order
  `last_order`        Date of the most recent order
  `orders`            Number of recorded orders
  `avg_bill_rs`       Average bill value in rupees
  `yearly_value_rs`   Estimated yearly customer value
  `at_risk_rs`        Estimated value currently considered at risk
  `likely_reason`     Explanation for the customer's changed behaviour

Actual column names in your Google Sheet may vary depending on your
implementation.

## Configuration

The system uses a settings sheet so important thresholds and delivery
behaviour can be changed without editing the workflow.

  ------------------------------------------------------------------------
  Setting                              Example value Purpose
  --------------------- ---------------------------- ---------------------
  `min_orders`                                   `4` Minimum order history
                                                     required before
                                                     judging a customer

  `min_days_late`                                `3` Minimum lateness
                                                     threshold before a
                                                     customer can be
                                                     flagged

  `cards`                                        `5` Number of customer
                                                     cards sent through
                                                     Telegram

  `ai_top`                                      `10` Number of top
                                                     customers for which
                                                     AI writes a reason
                                                     and message

  `snooze_days`                                 `30` Number of days to
                                                     leave a snoozed
                                                     customer alone

  `seasonal_lookback`                          `120` Lookback window used
                                                     when checking for
                                                     seasonal ordering
                                                     patterns

  `allow_discount`                              `no` Whether a win-back
                                                     message may mention a
                                                     discount

  `language`                              `hinglish` Language for
                                                     generated messaging
                                                     (`hinglish` or
                                                     `english`)
  ------------------------------------------------------------------------

These are example settings from the project configuration. Adjust them
to match the values in your own sheet.

------------------------------------------------------------------------

## Example Telegram experience

The owner-facing Telegram brief can include:

-   Total estimated yearly revenue at risk.
-   Counts of customers by status.
-   A short summary of what changed during the latest run.
-   Priority customers to contact first.
-   Customer-specific risk explanations and suggested messages.
-   Decision actions, including taking action or snoozing a customer.

The goal is to make the output actionable: the owner should be able to
see **who needs attention, why they need attention, and what to do
next**.

------------------------------------------------------------------------

## Technology stack

-   **Workflow automation:** n8n
-   **Customer data and configuration:** Google Sheets
-   **AI analysis and message generation:** Google Gemini
-   **Owner notifications and interaction:** Telegram
-   **Reporting:** Dashboard / HTML report

------------------------------------------------------------------------

## Setup overview

This repository documents the project. The exact setup depends on the
n8n workflow exports, Google Sheet structure, and credentials used in
your deployment.

1.  Create or configure the Google Sheets CRM and settings tabs.
2.  Set up an n8n instance.
3.  Import or recreate the n8n workflows used by the project.
4.  Configure Google Sheets access in n8n.
5.  Configure the Gemini API credential and the Telegram bot credential.
6.  Update workflow references to point to your own spreadsheet, bot,
    and required endpoints.
7.  Test with sample customer/order data before connecting live business
    data.
8.  Verify the generated classifications, revenue estimates, Telegram
    messages, and owner-decision writeback.


------------------------------------------------------------------------

## Project summary

The Quiet Churn Desk turns customer order history into an early-warning
and action workflow. By combining customer-specific ordering patterns,
configurable business rules, AI-generated explanations, and
Telegram-based owner actions, it helps businesses focus retention
efforts on the customers who may need attention before a long period of
inactivity passes.

**Built with n8n, Google Sheets, Gemini AI, and Telegram.**
