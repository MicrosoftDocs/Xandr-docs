---
title: Microsoft Monetize - Viewability Rates for Guaranteed Views
description: In this article, find information about viewability rates and how it affects how much a buyer is charged for guaranteed views.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Viewability rates for Guaranteed Views

> [!IMPORTANT]
> This document describes the viewability rates feature for Guaranteed Views.

While the buyer is only charged for viewable inventory with Guaranteed Views, line item reporting will not show a 100% viewable rate. When buying Guaranteed Views, a buyer's creative is always served to the page to allow the viewability script to measure the actual viewability. If the script determines that the creative was not viewable, then the buyer will not be charged, but the script will still report a measured, non-viewable impression.

We don't recommend comparing viewability rates between vCPM campaigns and CPM campaigns. vCPM campaigns, uniquely, incur no media cost for non-viewable impressions. Instead, you should compare the underlying cost per view. In reporting, this information can be found in the **Clearing Event Buyer Media Cost eCPM** field.

In other words, how much did the advertiser have to spend in order to reach the audience? When the buyer only pays media costs for viewable impressions, inventory with a lower average viewability may nevertheless result in better performance per unit spend for the advertiser.

## Related topics

- [Guaranteed Outcomes](guaranteed-outcomes.md)
- [Reporting on Guaranteed Outcomes](reporting-on-guaranteed-outcomes.md)
