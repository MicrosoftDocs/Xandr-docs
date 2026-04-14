---
title: Xandr MCP – Getting started
description: In this article, learn about Xandr MCP
ms.date: 4/14/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
---

# Xandr MCP – Getting started

The Xandr MCP provides read-only access to Xandr data through the Model Context Protocol (MCP). It is designed for AI clients that need to discover, retrieve, and summarize data from Xandr without making platform changes.

The service currently supports the following Xandr product surfaces:

- **Monetize**: https://monetize.xandr.com/mcp  
- **Curate**: https://curate.xandr.com/mcp  

These endpoint URLs are stable and are not versioned. They will not change.

> [!IMPORTANT]  
> Xandr MCP is currently in closed beta. Tool coverage, schemas, and behavior may change without notice.

---

## Introduction

Xandr MCP is intended for data retrieval, discovery, and analysis workflows. MCP-compatible clients can:

- Query reporting and analytics data  
- Inspect object metadata and platform entities  
- Retrieve reference and lookup data  
- Review change history and saved report information  
- Access selected planning, forecasting, or troubleshooting experiences (where enabled)  

Xandr MCP is currently a **read-only** product. It does not create, update, or delete Xandr objects.

Write operations may be added in the future but would require explicit enablement.

---

## Using Xandr MCP

To connect an MCP client:

1. Configure a remote HTTP MCP server that points to either the Monetize or Curate endpoint  
2. Provide a valid Xandr API authentication token  

### Configuration files

The configuration method depends on the client. For more information about authentication, see **Authentication**.

- **VS Code** uses `mcp.json`  
- **Claude Code** uses `.mcp.json`  
- **Claude.ai and Claude Desktop** use connector configuration in the UI instead of a file  

> `mcp.json` is a client-specific configuration file used to define MCP servers, endpoints, and authentication settings.

Other MCP-compatible tools may support different configuration models, authentication requirements, or setup flows. Refer to the documentation for your client.

---

## VS Code

You can configure MCP servers in:

- A workspace file at `.vscode/mcp.json`  
- Your user profile via the **MCP: Open User Configuration** command  

### Example `.vscode/mcp.json`

```json
{
  "servers": {
    "xandr-monetize": {
      "type": "http",
      "url": "https://monetize.xandr.com/mcp",
      "headers": {
        "authorization": "Bearer ${input:xandrAuthToken}"
      }
    },
    "xandr-curate": {
      "type": "http",
      "url": "https://curate.xandr.com/mcp",
      "headers": {
        "authorization": "Bearer ${input:xandrAuthToken}"
      }
    }
  },
  "inputs": [
    {
      "id": "xandrAuthToken",
      "type": "promptString",
      "description": "Xandr API authentication token",
      "password": true
    }
  ]
}
```
VS Code also supports adding a server through the Command Palette using MCP: Add Server. However, a checked-in .vscode/mcp.json file is typically the clearest option for shared team setups.

After configuration:
1. Open the workspace in VS Code
2. Open .vscode/mcp.json or run MCP: Open User Configuration
3. Save the configuration
4. Allow VS Code to start the server when prompted
5. Use Chat—MCP tools are discovered automatically

If your client supports input prompts, this approach avoids hard-coding the authentication token in the file.

---

## Claude Code

Claude Code supports project-scoped MCP configuration using a `.mcp.json` file at the project root. Its JSON structure differs from VS Code and uses `mcpServers` instead of `servers`.

### Example `.mcp.json`

```json
{
  "mcpServers": {
    "xandr-monetize": {
      "type": "http",
      "url": "https://monetize.xandr.com/mcp",
      "headers": {
        "Authorization": "Bearer ${XANDR_AUTH_TOKEN}"
      }
    },
    "xandr-curate": {
      "type": "http",
      "url": "https://curate.xandr.com/mcp",
      "headers": {
        "Authorization": "Bearer ${XANDR_AUTH_TOKEN}"
      }
    }
  }
}
```
Claude Code also supports adding MCP servers using the CLI instead of manually editing the JSON file.

### Example CLI commands

```
claude mcp add --transport http --scope project xandr-monetize https://monetize.xandr.com/mcp --header "Authorization: Bearer your-token"
claude mcp add --transport http --scope project xandr-curate https://curate.xandr.com/mcp --header "Authorization: Bearer your-token"
```

After adding the server:

1. Use `/mcp` inside Claude Code to inspect server status
2. Complete any required authentication flow prompted by the client

---

## Claude.ai and Claude Desktop

For remote MCP usage in Claude.ai and Claude Desktop, configuration is done through a custom connector flow rather than a local `mcp.json` file.

### Set up a remote connector

1. Open **Customize > Connectors** in Claude  
2. Select **Add a custom connector**  
3. Enter the MCP endpoint URL (for example, `https://monetize.xandr.com/mcp` or `https://curate.xandr.com/mcp`)  
4. Complete authentication if prompted  
5. Enable the connector for the conversation where you want to use MCP  

For Team and Enterprise plans, connector creation may be restricted to organization owners or admins.

> [!NOTE]  
> Claude Desktop also supports local MCP servers through `claude_desktop_config.json`. However, current Anthropic guidance for remote MCP connectors uses the connector UI rather than `mcp.json`.

For a repository example with additional local and staging configurations, see `mcp.json` example above.

---

## Authentication

Xandr MCP requires a valid Xandr API authentication token. Token format, lifetime, refresh behavior, and all other authentication mechanics are defined by the Xandr Authentication Service.

MCP does not introduce a separate authentication model—it uses the same token flow as the standard Xandr API.

- [Authentication Service](../digital-platform-api/authentication-service.md)

To authenticate requests, include the token in the `Authorization` header:

```http
Authorization: Bearer <your-xandr-token>
```
If the token expires, refresh it using the standard Xandr authentication flow and update it in your MCP client as needed.

## Permissions and access control

Xandr MCP does not introduce a separate permission model.
- Does not grant new platform access
- Respects existing permissions assigned to the authenticated user or token
- Enforces access through the underlying Xandr APIs

In practice, MCP can only expose data and capabilities that the authenticated identity is already authorized to use in Monetize or Curate.

MCP does not enable platform functionality that is not already available to your account, member, or seat. For example, if forecasting is not enabled for your seat, forecasting-related MCP tools will not be available.

---

## Rate limits

Xandr MCP requests are subject to rate limiting. The same throttling principles that apply to the Xandr API also apply to MCP.

For more information, see:

- [Throttling, Pagination, and Filtering](../digital-platform-api/05---throttling-pagination-and-filtering.md)

MCP usage consumes a portion of the API rate limits available to the authenticated client.

- Typical interactive usage is unlikely to reach these limits  
- Automated or high-frequency integrations should handle throttling appropriately  

---

## Available tools

Xandr MCP exposes tools across the following functional areas:

- **Reporting and analytics**: Run supported reports, retrieve dimensions and metrics, and analyze performance data  
- **Report management**: Check report status, download completed reports, and inspect saved report definitions  
- **Object discovery and lookup**: Search supported Xandr entities and inspect available object fields  
- **Reference data**: Retrieve lookup datasets such as geography, device, media, and other classification data  
- **Change history**: Review audit and change-log information for supported entities  
- **Planning and forecasting**: Access selected planning or forecasting data where available for your account  
- **Troubleshooting**: Use diagnostic tools for supported workflows where available

---

### Typical reporting workflow

For reporting scenarios, a common workflow is:

1. Identify the report to use  
2. Inspect available dimensions, metrics, and filters  
3. Run the report with the required grouping, filters, and date range  

#### Examples

- Analyze Monetize inventory performance for the last 7 days by publisher or placement  
- Retrieve Curate deal metrics for a specific buyer or seller deal  
- Check provisional network analytics for same-day delivery trends  
- Inspect a report catalog to understand available columns and filters before running a query  

Depending on the report, MCP may expose:

- **Direct report tools** for commonly used report types  
- **Discovery-style tools** for exploring report metadata and executing queries  
