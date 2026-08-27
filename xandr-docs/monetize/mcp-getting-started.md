---
title: Xandr MCP – Getting started
description: In this article, learn about Xandr MCP
ms.date: 8/19/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
author: v-garittar
ms.author: v-garittar
---

# Xandr MCP – Getting started

## Connect an AI assistant to the Xandr MCP Server for Microsoft Monetize or Microsoft Curate

The Xandr MCP Server lets you query your Microsoft Monetize or Microsoft Curate platform data using plain language from an MCP-compatible AI assistant. Instead of navigating the UI or writing API calls, you can ask for reports, search for objects, inspect configurations, and review change history from your AI client.

The alpha release is read-only. You can search, inspect, and report on existing data, but you can't create or edit deals, line items, advertisers, Curate deal plans, or other objects through the Xandr MCP Server.

## What you can do with the Xandr MCP Server

The Xandr MCP Server supports read-only access to platform data for Microsoft Monetize and Microsoft Curate. The tools, reports, and objects available to you depend on the endpoint you connect to and the permissions associated with your Xandr seat.

| Capability | What you can ask | Microsoft Monetize | Microsoft Curate |
|---|---|---:|---:|
| Reporting | Run reports available to your account, explore metrics and dimensions, download results, and generate time-series charts. | Yes | Yes |
| Report templates | Run pre-built report templates with curated column sets for common analysis workflows. | Yes | Yes |
| Object search | Search and inspect deals, line items, advertisers, insertion orders, targeting profiles, segments, publishers, and placements. | Yes | Yes |
| Reference data | Look up currencies, device types, geo segments, ad categories, and other platform-managed lists. | Yes | Yes |
| Change history | See what changed on an object, when it changed, and who made the change. | Yes | Yes |
| Configuration troubleshooting | Check a deal's configuration chain and surface blocking issues with a structured verdict. | Yes | Yes |
| Inventory forecasting | Estimate available impressions for a given set of targeting criteria. Available to ad server clients only. | Yes | No |
| Deal plan estimates | Retrieve plan details and reach estimates for curated deals. | No | Yes |

## Choose the right endpoint

Connect to the endpoint that matches your Xandr seat.

| Platform | MCP URL |
|---|---|
| Microsoft Monetize | `https://monetize.xandr.com/mcp` |
| Microsoft Curate | `https://curate.xandr.com/mcp](https://curate.xandr.com/mcp` |

Authentication uses your Microsoft identity. You don't need separate Xandr API credentials.

## Prerequisites

Before you connect your AI assistant, make sure you have:

- An active Xandr account on Microsoft Monetize or Microsoft Curate.
- Alpha access granted by your account team.
- A Microsoft Entra ID identity with access to your Xandr member seat.
- An MCP-compatible AI assistant, such as VS Code, Claude Code, or MCP Inspector.
- The ability to add an MCP server configuration, such as `mcp.json` or an equivalent configuration file.

No SDK installation, local server, or API key setup is required. Authentication is handled on first connection through a browser sign-in prompt.

## Connect with VS Code

1. Open your workspace in VS Code.

1. Add a `.vscode/mcp.json` file to your workspace.

1. Add this configuration:

   ```json
   {
     "servers": {
       "xandr": {
         "type": "http",
         "url": "https://monetize.xandr.com/mcp"
       }
     }
   }
   ```

1. If you're a Microsoft Curate user, replace the URL with `https://curate.xandr.com/mcp`.

1. Reload the VS Code window.

1. On first connection, sign in with your Microsoft Entra ID identity when your client opens the browser sign-in prompt.

## Connect with Claude Code

1. Add this configuration to `~/.claude.json` globally, or to `.mcp.json` in your project:

   ```json
   {
     "mcpServers": {
       "xandr": {
         "url": "https://monetize.xandr.com/mcp",
         "transport": "http"
       }
     }
   }
   ```

1. If you're a Microsoft Curate user, replace the URL with `https://curate.xandr.com/mcp`.

1. On first connection, sign in with your Microsoft Entra ID identity when prompted.

## Test with MCP Inspector

Use MCP Inspector for ad hoc testing before you integrate the Xandr MCP Server with an AI client.

1. Run this command in a terminal:

   ```bash
   npx @modelcontextprotocol/inspector
   ```

1. Enter the endpoint URL when prompted.

1. Explore the available tools before integrating with an AI client.

## Verify your connection

After you connect, ask your AI assistant one of these questions:

- "List my active deals"
- "Show me last week's impressions by publisher"

If your client returns data, the connection is working correctly.

## Run reports effectively

The Xandr MCP Server gives you access to more than 100 metrics and dimensions. Before you run a report, ask your AI assistant to list available report types or describe the columns available for a report.

This helps avoid validation errors because report types, metrics, dimensions, columns, filters, and time ranges can vary by platform and account configuration.

Example prompt:

> Show me impressions, revenue, and CPM by publisher for the last 7 days.

For smaller queries, results are returned directly in chat. For larger result sets, reports are processed asynchronously. Your AI client polls for completion and returns the results when they're ready.

## Search and inspect objects

You can search by name, ID, or partial name across major object types. When the object type isn't known in advance, the server resolves it automatically.

Example prompts:

> Find all active line items under advertiser 12345.

> Show me the targeting profile on line item 67890.

If you have an ID, use it directly. Numeric IDs are unambiguous and faster than name-based lookups. If you only have a name or partial information, search first to get the ID, then use the ID in follow-up questions.

Related objects can be retrieved in follow-up questions without repeating the full context.

## Troubleshoot deal delivery

When a deal isn't delivering, ask the server to check its configuration. The server evaluates the deal and its related configuration chain, including the linked line item, insertion order, advertiser, and targeting profile.

Example prompt:

> Deal 987654 is not delivering. What's wrong with the configuration?

The response includes a structured verdict with plain-language descriptions of any issues found, such as a paused line item, expired flight dates, or an archived profile.

For best results, troubleshoot deals by ID. Providing a deal ID or line item ID gives the troubleshooting tool enough context to return a diagnosis in one step.

## Review change history

You can ask what changed on major object types and review field-level change detail.

Example prompts:

> What changed on line item 67890 in the last 48 hours?

> Who last modified deal 987654 and when?

Change history is available for major object types and includes field-level detail.

## Understand the object hierarchy

Understanding how Xandr objects relate to each other can help you ask clearer questions and interpret results.

### Buy-side hierarchy

```text
Member
└── Advertiser
    └── Insertion Order
        └── Line Item
            ├── Profile
            └── Deal
```

A deal connects a buyer to inventory. It is attached to a line item, which sits inside an insertion order under an advertiser. When a deal isn't delivering, any object in that chain can be the cause.

A profile holds the targeting criteria for a line item, such as geo, device, segment, and frequency cap settings. It is a separate object, but it is treated as part of the line item configuration for troubleshooting.

Segments and splits are used for audience targeting and budget allocation within a line item.

### Sell-side hierarchy for Microsoft Monetize

```text
Member
└── Publisher
    └── Placement Group
        └── Placement
```

## Use effective tool patterns

The Xandr MCP Server organizes tools into reusable patterns. You don't need to call these tools directly unless your AI client exposes them, but understanding the patterns can help you ask better questions.

### Discover, then run reports

For reports, ask what is available before running. Discovery helps you confirm which report types, columns, filters, and time ranges are valid.

Common reporting tool patterns include:

- `list_reports`
- `describe_report`
- `run_report`
- `get_report_status`
- `download_report`
- `run_chart_report`

### Search, then describe objects

For objects, search first when you don't have an ID. If you already have an ID, go directly to object details.

Common object tool patterns include:

- `search_<object_type>`
- `describe_object`
- `get_object_meta`
- `identify_object`

### Validate configuration

For troubleshooting, use the validation pattern with a deal ID or line item ID. The validation tool resolves the related parent chain internally.

Common troubleshooting tool pattern:

- `validate_object_config`

### Review change history

For change history, start with a high-level summary, then inspect grouped or field-level change details if needed.

Common change history tool patterns include:

- `get_change_history`
- `get_change_log_group`
- `get_change_log_detail`

## Example questions you can ask

Use these examples as starting points after you're connected.

### Troubleshoot delivery

> Deal 987654 is not delivering. What's wrong with the configuration?

### Run a performance report

> Show me impressions, revenue, and CPM by publisher for the last 7 days.

### Search and inspect objects

> Find all active line items under advertiser 12345.

> Show me the targeting profile on line item 67890.

### Understand recent changes

> What changed on line item 67890 in the last 48 hours?

> Who last modified deal 987654 and when?

### Explore available inventory in Microsoft Monetize

> How much inventory is available for US mobile web, 300x250, targeting finance content?

### Analyze curated deal performance in Microsoft Curate

> Show me the curator analytics report for last month broken down by deal.

> What is the bid rejection rate across my active deals?

### Review network performance trends

> How did my total revenue compare this week vs last week?

> Which 10 publishers drove the most impressions last month?

You can also combine reporting and chart tools by asking for a trend chart, then following up with a breakdown question.

## Alpha scope and limitations

The alpha release surfaces your existing platform data and respects the same permissions, roles, and reporting capabilities your account already has.

The following actions aren't available in this release:

- Creating or modifying objects through the Xandr MCP Server.
- Creating or editing deals, line items, advertisers, or other objects.
- Creating or modifying Microsoft Curate deal plans.

Reading existing Microsoft Curate plan details and retrieving reach estimates is supported.

Alpha access is by invitation only. Contact your account team to request access.

## Common questions

### Can I create or edit deals and line items through my AI assistant?

No. The alpha release is read-only. You can search, inspect, and report on existing data, but you can't create or edit deals, line items, advertisers, or other objects through the Xandr MCP Server.

### Do I need separate Xandr API credentials?

No. Authentication uses your Microsoft identity. You don't need separate Xandr API credentials.

### Which endpoint should I use?

Use the endpoint that matches your Xandr seat:

- Microsoft Monetize: `https://monetize.xandr.com/mcp`
- Microsoft Curate: `https://curate.xandr.com/mcp](https://curate.xandr.com/mcp`

### Why am I getting a validation error when I run a report?

Report types and available columns vary by platform and account configuration. Before you run a report, ask your AI assistant to list available report types or describe the report you want to run.

### Does the Xandr MCP Server respect my existing permissions?

Yes. The server surfaces existing platform data and respects the same permissions, roles, and reporting capabilities your account already has.

### How do I get alpha access?

Alpha access is by invitation only. Contact your account team to request access.
