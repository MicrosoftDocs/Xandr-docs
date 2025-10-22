---
title: Working With Multiple Ad Servers
description: This article provides details about how you can work with multiple ad servers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Work with multiple ad servers

The Yield Analytics interface supports the use of multiple ad servers (e.g., if you use one for mobile, one for video, etc.). This makes it easier to work with each one separately or all together.

## Set the default ad server

If you use multiple ad servers, you can specify which one is the default.

1. In the upper-right corner of any page, select your name, and then select **Preferences**. The **Preferences** page loads.
1. In the **Set Defaults** panel, in the **Ad server for filters** field, select the link for the current setting and then select one of the following ad servers from the dropdown list that appears:
    - **DFPP**
    - **FreeWheel**
    - **AdMarvel**
1. Select **Save Defaults**.

## About priority labels

You can customize priority labels, which are searchable, organized from high to low, and displayed throughout Yield Analytics. In addition, Yield Analytics can hide priority labels that you don't use. Contact your services representative for more information.

## Filter with multiple ad servers

When you specify an ad server (e.g., for an availability lookup), the rest of the filter options and lookup criteria are automatically restricted to show only the products, attributes, and values for the ad server. This helps you more easily locate the product you want. It also eliminates potential duplicate instances (e.g., if two products for different ad servers are named the same thing, only one will appear).

If you are using multiple ad servers (e.g., one for video, another for mobile), you can select the ad server from the filter (e.g., Limit types to those supported by and Limit attributes and values to those supported by).

When specifying the filter:

- Not Specified displays products that are not linked to a specific ad server.
- None Selected returns everything.

> [!TIP]
> Filtering by ad server filters the available product and attribute options, not the actual data returned in the lookup or report. To filter the availability lookup, specify **ad_server** as an attribute.

For historical purposes, all ad servers that your agency has worked with are filter options. If your agency doesn't use multiple ad servers but has migrated ad servers, you can filter by ad server only on the **Contract Type** for historical reporting. Clients that have migrated ad servers will see this filter only on the **Contract Type** for historical reporting.

## Specify priority

If you're working with multiple ad servers (e.g., in Availability Lookup or Scenario Manager) a dialog enables you to specify priority for the secondary ad server.

## Related topics

- [Freewheel Priority Values in Yield Analytics](./freewheel-priority-values-in-yield-analytics.md)
- [Ad Servers Overview](./ad-servers-overview.md)
