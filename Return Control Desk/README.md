# Returns Control Desk

An AI-powered returns and RTO management automation built with **n8n, Google Sheets, Gemini, and Gmail**.

The system reads return and RTO data, applies business policies, recommends the appropriate action, drafts customer responses, and identifies the SKUs, pincodes, couriers, and return reasons responsible for the biggest losses.

## What It Does

- Reads return and RTO records automatically
- Checks requests against predefined return policies
- Analyzes customer history and return patterns
- Decides between **refund, replacement, rejection, or manual review**
- Generates personalized customer responses
- Sends responses through Gmail
- Logs decisions and actions
- Identifies high-loss SKUs
- Identifies high-risk pincodes
- Analyzes courier RTO performance
- Detects recurring product and sizing issues
- Generates a loss/review report

## Workflow

```text
Return / RTO Data
       ↓
Google Sheets CRM
       ↓
n8n Automation
       ↓
Orders + Products + Customers + Decision Log
       ↓
Policy Check
       ↓
Gemini AI Analysis
       ↓
Refund / Replacement / Reject / Manual Review
       ↓
Generate Customer Reply
       ↓
Gmail
       ↓
Log Decision
       ↓
Loss Analysis
       ↓
Identify Problem SKUs / Pincodes / Reasons
```

## Tech Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow orchestration |
| Google Sheets | CRM, policies, and decision logs |
| Gemini | AI analysis and decision-making |
| Gmail | Customer communication |

## Policy Engine

Business rules are stored in Google Sheets instead of being hard-coded into the workflow.

Example policies:

```text
Return window: 7 days
Exchange window: 14 days
Non-returnable: Innerwear, Fragrance
Damaged item: Photo required
Auto-approve: Under ₹500
Pickup required: Above ₹1,000
COD refund: Bank transfer
Abuse threshold: 3 returns
```

Businesses can update their policies in the sheet without rebuilding the entire workflow.

## AI Decision Engine

The Gemini agent evaluates:

- Return reason
- Order information
- Product information
- Customer return history
- Return policy
- Order value
- Previous decisions

Possible outcomes:

```text
REFUND
REPLACEMENT
REJECT
MANUAL REVIEW
```

## Customer Communication

After a decision is made, Gemini generates a customer-friendly response based on the decision and return details.

```text
Return detected
      ↓
AI decision
      ↓
Customer-specific message
      ↓
Gmail
      ↓
Decision logged
```

## Loss Analysis

The system analyzes return and RTO data to identify:

- High-return products
- Damaged products
- Size-related returns
- High-RTO pincodes
- Poor-performing courier partners
- High-frequency return customers
- Return reasons generating the highest losses

Example:

```text
Handloom Cotton Saree
50% return rate
₹4,419 identified loss

Anarkali Kurta Set
80% return rate
₹4,039 identified loss

High-risk Pincode
110086
50% RTO rate
```

## Example Business Report

```text
Returns & RTO Review

₹9,747 identified losses
30% COD orders refused
3 RTO parcels
₹9,097 stuck coming back

Key issues:
• Courier performance
• Product sizing
• Product damage
• High-risk pincode

Recommended actions:
• Review problematic courier
• Improve product size chart
• Review packaging
• Investigate high-risk locations
```

## n8n Workflow Structure

```text
Trigger
  ↓
Config
  ↓
Read Orders
  ↓
Read Products
  ↓
Read Customers
  ↓
Read Decision Log
  ↓
Loss Engine
  ├──→ Gemini Loss Analyst
  │        ↓
  │    Build Loss Brief
  │        ↓
  │    Send Loss Brief
  │
  └──→ Gemini Parcel Writer
           ↓
       Build Messages
           ↓
       Send Gmail
           ↓
       Log Attempts
```

## Google Sheets Structure

```text
Google Sheets
├── Policy
├── Products
├── Orders
├── Customers
├── Return_Requests
└── Decision_Log
```

## Key Benefits

### Reduce Manual Work
Automates repetitive return evaluation and customer communication.

### Consistent Decisions
Every request is evaluated against the same business policies.

### Faster Customer Responses
AI-generated responses can be prepared automatically after the decision.

### Identify Hidden Losses
Connects return data to products, locations, couriers, and return reasons.

### Data-Driven Actions
The system goes beyond processing returns and identifies why returns are happening and where money is being lost.

## Use Case

Built for **e-commerce businesses** dealing with returns, refunds, replacements, and RTOs.

The system can be adapted to different businesses by changing the policies, product data, customer data, and workflow rules.

## Future Improvements

- WhatsApp customer communication
- Automated pickup scheduling
- Return image analysis
- Fraud and risk scoring
- Real-time returns dashboard
- Shopify / WooCommerce integration
- Courier API integration
- Automated refund processing
- Multi-agent returns management
- Profit and loss forecasting

## Built With

**n8n + Gemini + Google Sheets + Gmail**

> Automate returns. Identify losses. Protect margins.
