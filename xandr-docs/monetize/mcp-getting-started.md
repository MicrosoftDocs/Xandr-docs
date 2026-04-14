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
