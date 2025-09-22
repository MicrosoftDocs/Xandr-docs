---
title: Prebid Server Premium Services
description: Explore the API services available for Prebid Server Premium (PSP).
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Prebid Server Premium services

Microsoft Advertising's Prebid Server Premium (PSP) is a self-service, server-side solution that maximizes publisher revenue through unified auctions. Running on open-source Prebid Server Go, it provides transparency into auction mechanics, visibility into winning and losing bids, and access to over 200 demand partners competing with bidders from Monetize marketplace. PSP's integration into the Monetize platform offers publishers flexible, UI-based controls over how inventory is packaged and sent to demand partners. The Monetize Insights dashboard and reporting tools surface optimization opportunities tailored to PSP demand. PSP supports multiple channels (web, mobile web, mobile app, over-the-top, and accelerated mobile pages) and formats (display, native, and video).

## PSP configuration API services

| Service | Description |
|:---|:---|
| [Ad Size Service](ad-sizes-service.md) | Returns the acceptable ad sizes for the member associated with the config. |
| [Bidder Info Service](bidder-info-service.md) | Returns the capabilities of each bidder. |
| [Campaign Object Service](campaign-object-service.md) | Provides instructions for targeting Monetize inventory as input for the [configuration service](config-service.md). |
| [Configuration Service](config-service.md) | Instructions for viewing, creating, and editing configurations which map Xandr inventory to demand partner inventory. |
| [Cross-Partner Settings Service](cross-partner-settings-service.md) | Instructions for viewing and editing the member's global settings which apply across all demand partners. |
| [Demand Partner Service](demand-partner-service.md) | Instructions for adding and editing demand partners. |
| [Demand Partner Schema Service](demand-partner-schema-service.md) | Returns the parameters accepted by the demand partner. |
| [Long Form Video service](long-form-video-service.md) | Instructions to send bid requests for long-form (ad podded) premium video demand. |
| [Operating System Families Service](operating-system-families-service.md) | Returns all the operating systems available for the caller's member. |
| [Prebid Demand Partner Params Service](prebid-demand-partner-params-service.md) | Instructions for viewing, creating, and editing the demand partner parameter mappings within a configuration. |

To leverage the PSP UI instead of APIs, review the documentation below:

- [Add or Edit PSP Global Settings](../monetize/add-or-edit-psp-global-settings.md)
- [Add or Edit a Demand Partner](../monetize/add-or-edit-a-demand-partner.md)
- [Add, Edit, or Delete a PSP Configuration](../monetize/add-edit-or-delete-a-psp-configuration.md)

> [!NOTE]
> Prebid Server Premium is not available to all customers. Please contact Microsoft Advertising to request access.
