---
title: July 08, 2025 - Enhanced Forecast-Shaped Pacing
description: An update to the Forecast-Shaped Pacing (FSP) feature enhances how budgets are allocated for Guaranteed line items (GDLIs) and Programmatic Guaranteed (PG).
ms.date: 07/08/2025
ms.topic: release-notes
ms.author: shsrinivasan
---

# July 08, 2025 - Enhanced Forecast-Shaped Pacing

An update to the Forecast-Shaped Pacing (FSP) feature enhances how budgets are allocated for Guaranteed line items (GDLIs) and Programmatic Guaranteed (PG). FSP currently generates an intraday spend curve using Yield Analytics forecasting data to allocate budgets hourly based on daily capacity. 

With this enhancement, a new line item configuration expands FSP to consider forecasted inventory over a rolling seven-day window to dynamically adjust daily budgets. Instead of distributing the lifetime budget evenly across the flight duration, FSP will allocate daily budgets based on projected capacity. For example, if higher impression volumes are forecasted for weekends, the Line Item will pace more heavily on those days. 

This enhancement helps align delivery more closely with inventory patterns, reducing the risk of under delivery and improving overall pacing accuracy. The feature is enabled by default when creating a GDLI or PG via the Monetize UI but will need to be explicitly set when created via API. 

For more information, see:
- [Forecast-shaped pacing](forecast-shaped-pacing.md)
- [Guaranteed delivery pacing](guaranteed-delivery-pacing.md)
- [Budgeting & scheduling](budgeting-scheduling.md)
- [Budget intervals objects](../digital-platform-api/budget-intervals-objects-api.md)
