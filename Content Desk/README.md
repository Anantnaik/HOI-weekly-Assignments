# Content Engine Desk

Turn a single line of an idea into a multi-platform content pack using
an n8n workflow, Gemini-powered AI agents, and structured content rules.

The project is designed to help create a consistent first draft for
multiple channels without manually rewriting the same idea for every
platform.

## What it does

Provide one idea and the workflow generates:

-   **LinkedIn post** --- a longer post that develops the central
    argument.
-   **Instagram caption** --- a caption adapted for Instagram.
-   **Three hook options** --- alternative opening lines to choose from.
-   **WhatsApp broadcast** --- a concise message adapted for WhatsApp.

The workflow also uses stored context and writing rules to help keep
outputs aligned with the intended voice and avoid overused phrases.

## Built with

-   **n8n** --- workflow orchestration.
-   **n8n Data Tables** --- structured storage for writing rules and
    workflow data.
-   **Google Gemini** --- the language model behind the specialized
    generation agents.
-   **HTTP Request nodes** --- connect the workflow to the Gemini API.
-   **Telegram** --- shown in the workflow as an output/notification
    path.

> The exact credentials, model names, and node settings depend on the
> local n8n instance and the version of the workflow being deployed.

## How the workflow works

At a high level, the workflow follows this sequence:

1.  **Receive the idea**\
    A single-line idea enters the workflow, together with any available
    context.

2.  **Load writing rules and previous context**\
    The workflow reads the configured voice rules and can retrieve
    information about previously published content.

3.  **Build the content brief**\
    The input is shaped into a brief that downstream agents can use.

4.  **Run specialized AI agents**\
    Separate Gemini-powered stages handle different parts of the content
    pack.

5.  **Check the generated content**\
    The workflow checks the content against the configured rules.

6.  **Prepare and store the outputs**\
    The generated content is organized into platform-specific sections
    and saved or routed through the configured output path.

7.  **Prepare the visual brief**\
    The workflow screenshot also shows an Art Director stage and an
    image-brief reading step. This can be used as an additional
    visual-content branch where enabled.

## AI agent responsibilities

The five core content roles represented in the project are:

  -----------------------------------------------------------------------
  Agent                               Responsibility
  ----------------------------------- -----------------------------------
  Angle Finder                        Finds the central angle or argument
                                      for the idea.

  LinkedIn Writer                     Develops the angle into a LinkedIn
                                      post.

  Hook Doctor                         Produces three alternative hooks.

  Repurposer                          Adapts the idea into an Instagram
                                      caption and WhatsApp broadcast.

  Voice Guard                         Checks the content against the
                                      configured writing rules.
  -----------------------------------------------------------------------

The workflow canvas also shows an **Art Director** stage. Treat this as
an additional visual-brief stage rather than one of the five core
content-writing roles.

## Writing rules table

The `voice_rules` n8n Data Table stores rules used to guide or check
generated content.

The visible table structure includes:

  -----------------------------------------------------------------------
  Field                               Purpose
  ----------------------------------- -----------------------------------
  `rule_id`                           Unique identifier for a rule.

  `rule_type`                         Rule category, such as `banned`.

  `platform`                          The platform the rule applies to,
                                      or `all`.

  `rule`                              The phrase, pattern, or instruction
                                      to check.

  `max_chars`                         Character limit or related numeric
                                      setting used by the workflow.
  -----------------------------------------------------------------------

Example rows in the supplied table include banned phrases such as
`unlock`, `unleash`, `elevate`, and `game changer`.

Add, edit, or remove rules in the n8n Data Table to adapt the content
constraints. Confirm how each rule type is interpreted by the workflow
before adding new categories.

## Example input and output

**Example input idea**

> Building a centralized AI infrastructure is more profitable than
> selling isolated automation workflows.

**Example content pack**

-   A LinkedIn post arguing for integrated AI infrastructure.
-   An Instagram caption using a scene-based opening.
-   Three alternative hooks.
-   A WhatsApp broadcast with a practical business-oriented message.

The generated content is a starting point. Review factual claims, tone,
formatting, and platform suitability before publishing or sending.

## Requirements

Before running the workflow, make sure you have:

-   A working n8n instance.
-   Access to n8n Data Tables.
-   A Google Gemini API key with access to the model configured in your
    workflow.
-   Any required Telegram credentials if you use the Telegram output
    path.
-   The workflow imported into n8n, with credentials and node settings
    configured.

## Setup

1.  Import the workflow JSON into your n8n instance.
2.  Create or import the required n8n Data Tables, including
    `voice_rules`.
3.  Add your Gemini API credential or API key to the relevant HTTP
    Request nodes using n8n credentials or another secure credential
    method.
4.  Configure any Telegram credentials and destination details if that
    branch is enabled.
5.  Review the table names, node references, model identifiers, and API
    request bodies.
6.  Add or customize your writing rules.
7.  Run a test using a non-sensitive sample idea.
8.  Inspect every generated output and confirm the validation and
    storage steps behave as expected.

This README describes the project architecture visible in the supplied
screenshots; it does not contain exported workflow JSON or
environment-specific credential values.

## Configuration notes

Check these items when adapting the workflow:

-   **Model configuration:** Confirm the Gemini model identifier and API
    endpoint used by each agent.
-   **Prompt instructions:** Keep each agent's responsibility distinct
    and define the expected output format.
-   **Voice rules:** Maintain clear rule IDs, rule types, platform
    scope, and values.
-   **Previous-content context:** Ensure the lookup step reads the
    intended source and handles an empty result.
-   **Output parsing:** Validate that each agent returns the fields
    expected by downstream nodes.
-   **Character limits:** Confirm whether limits are enforced, measured,
    or simply provided as guidance.
-   **Retries and errors:** Add appropriate handling for API failures,
    malformed responses, and rate limits.

## Security and privacy

-   Do not commit API keys, Telegram bot tokens, credentials, or private
    client data to version control.
-   Store secrets using n8n's credential system or an appropriate
    secrets manager.
-   Avoid sending confidential or personally identifiable information to
    an AI provider unless you have the necessary permission and have
    reviewed the provider's data handling terms.
-   Redact sensitive information from screenshots, logs, and example
    data before sharing the project publicly.

## Current scope and limitations

-   The system generates drafts; it does not guarantee that content is
    factually correct, legally compliant, or ready to publish without
    review.
-   Writing-rule checks depend on the rules configured in the Data Table
    and how the workflow implements them.
-   Platform formatting and character limits may change; verify current
    requirements before publishing.
-   The exact behavior of the visual-brief and Telegram branches depends
    on the enabled nodes and their configuration.
-   No automatic publishing to LinkedIn, Instagram, or WhatsApp should
    be assumed unless a separate publishing integration has been
    configured.

## Suggested future improvements

-   Add a simple input form or webhook interface for submitting ideas.
-   Add approval steps before content is sent or published.
-   Track generated content and feedback to improve prompts over time.
-   Add duplicate-topic and similarity checks against previous posts.
-   Add platform-specific length and formatting validation.
-   Add execution logging, retry handling, and alerts for failed runs.
-   Add an optional image-generation and asset-review workflow.

## Project summary

**Content Engine Desk** is an n8n-based content generation system that
turns one idea into a LinkedIn post, an Instagram caption, three hook
options, and a WhatsApp broadcast. Its core design combines specialized
Gemini agents with reusable writing rules stored in n8n Data Tables,
making the process more structured than relying on a single
general-purpose prompt.
