# Brand MCP System

An MCP-powered commerce system built with **n8n**, **Gemini AI agents**,
and **SAP data**. It exposes brand commerce operations as tools that a
compatible AI application can use, enabling natural-language product
discovery and order processing.

## Overview

The system connects an AI interface to a brand's existing commerce data
and operations through an MCP server implemented in n8n.

Current capabilities include:

-   **Product discovery:** Retrieve product information from SAP.
-   **PIN code validation:** Check whether delivery is available for a
    customer's PIN code.
-   **Order booking:** Create an order using the available product and
    customer details.
-   **Data updates:** Update the relevant SAP tables after order
    processing.

## Architecture

``` text
Customer / AI Application
          |
          v
    MCP-compatible client
          |
          v
      MCP Server
         (n8n)
          |
          v
    Gemini AI agents
          |
          v
   SAP data and tables
   - Product information
   - Delivery serviceability
   - Orders and related records
```

The exact flow depends on how the MCP tools and agents are configured in
the n8n workflows.

## Example Order Flow

1.  A customer asks about a product.
2.  The system retrieves relevant product information from SAP.
3.  The customer provides a delivery PIN code.
4.  The system checks delivery serviceability.
5.  The customer requests and confirms an order.
6.  The system creates the order in SAP.
7.  The relevant tables are updated to reflect the operation.

## Technology Stack

-   **n8n** --- workflow orchestration and MCP server/tools
-   **MCP (Model Context Protocol)** --- exposes commerce operations to
    compatible AI applications
-   **Google Gemini** --- AI agents for task-specific processing
-   **SAP** --- product and order data source

## Potential Integrations

The MCP server can potentially be connected to different compatible AI
clients and customer interfaces. WhatsApp is a possible customer-facing
channel, particularly for the Indian market, but it requires a suitable
WhatsApp integration and is **not represented here as an already
deployed integration**.

Other possible interfaces include a website, a custom chat application,
or other MCP-compatible clients.

## Current Scope

The current implementation focuses on the MCP server, AI-agent
workflows, SAP data, PIN code serviceability checks, order creation, and
table updates.

Customer-facing channel integrations, payment processing,
shipping-provider integrations, and order tracking should only be
considered available if they have been implemented and tested
separately.

## Security and Production Considerations

Before using the system with real customers or orders:

-   Keep SAP credentials and API keys in secure credential storage.
-   Validate product IDs, quantities, customer details, and PIN codes
    before creating orders.
-   Require clear customer confirmation before submitting an order.
-   Prevent duplicate orders when workflows are retried.
-   Handle SAP errors and partial failures without reporting false
    success.
-   Apply appropriate access controls and log important order actions.
-   Test with non-production data before enabling live order creation.

## Project Status

**Built:** n8n-based MCP workflow, Gemini agents, SAP-backed
product/order operations, PIN code serviceability checking, and related
table updates.

**Potential next step:** Connect a customer-facing interface such as
WhatsApp through an appropriate integration, then test the complete
customer journey end to end.

------------------------------------------------------------------------

*Brand MCP System --- connecting AI applications to real commerce
operations.*
