---
title: Microsoft Monetize - Create an Augmented Line Item
description: In this article, find step-by-step instructions on how to create and set up augmented line items (ALIs).
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Create an augmented line item

You create augmented line items (ALIs) to define your financial relationship with an advertiser, set up targeting for an advertising campaign, and schedule your advertisements to run.

Before you begin creating a line item, you must first perform the following tasks:

- [Create an Advertiser](create-an-advertiser.md)
- [Create an Insertion Order](create-an-insertion-order.md)

  The insertion order you created must have at least one billing period with dates in the future.

You can create a line item before you have performed the following tasks, but you will need to complete them before you can activate your line item and launch your advertising campaign. If you want to create a line item before you create these other objects, you can create them afterwards and add them to the line item.

- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Working with Creatives](working-with-creatives.md)

If you've created an advertiser and an insertion order, you're ready to create a line item.

1. [Navigate to the Create New Line Item Screen](navigate-to-the-create-a-new-line-item-screen-monetize.md)

    You can create new augmented line items from the **Create New Line Item** screen.

1. [Add Basic Line Item Details](add-basic-line-item-details.md)

    From the **Basic Settings** section, you can set the name, state, and ad type, as well as associate additional insertion orders to the line item. You can also optionally assign an external code.

1. [Set Up Line Item Budgeting and Scheduling](set-up-line-item-budgeting-and-scheduling.md)

    From the **Budgeting & Scheduling** section, you can add revenue type, payment model, budget, flight, underspend catch-up allocation, daypart, daily pacing allocation, and hourly pacing override details for the line item.

1. [Set Up Line Item Optimization](set-up-line-item-optimization.md)

    From the **Optimization** section, you can enable or disable Microsoft Advertising optimization for a line item. If you enable Microsoft Advertising optimization, you must first set a performance goal and goal priority, and then associate the line item with conversion pixels for those goals.

1. [Set Up Line Item Inventory and Brand Safety](set-up-line-item-inventory-and-brand-safety.md)

    From the **Inventory and Brand Safety Targeting** section, you can specify the type of inventory that you want to buy (supply source), target universal or custom content categories, specify whether to advertise on web or app inventory, create and/or apply blocklists or allowlists, define brand safety settings, and set up ads.txt targeting.

1. [Set Up Geography Targeting for a Line Item](set-up-geography-targeting-for-a-line-item.md)

    From the **Audience & Location Targeting** section, you must target users based on at least one geographic element such as country, region, city, metro code, or postal code. You may optionally set up other geographic inclusions or exclusions.

1. [Enable Cross-Device Targeting and Measurement for a Line Item](enable-cross-device-targeting-and-measurement-for-a-line-item.md)

    From the **Audience & Location Targeting** section, you can optionally enable cross-device targeting on a line item to apply frequency caps, conversion attribution, and audience targeting settings for individual users across multiple devices.

1. [Set Up Segment Targeting on a Line Item](set-up-segment-targeting-on-a-line-item.md)

    From the **Audience & Location Targeting** section, you can set up a line item to target segments from third-party data providers or segments you've created.

1. [Set Line Item Frequency and Recency Caps](set-line-item-frequency-and-recency-caps.md)

    From the **Audience & Location Targeting** section, you can set the number of times (*frequency*) and how often (*recency*) creatives can be shown to a given user.

1. [Set Up Viewability and Environment Targeting for a Line Item](set-up-viewability-and-environment-targeting-for-a-line-item.md)

    From the **Viewability & Environment Targeting** section, to narrow your ad campaign's reach to the most valuable inventory, you can set up viewability threshold, device type, system, and page property targeting settings.

1. [Associate Creatives with a Line Item](associate-creatives-with-a-line-item.md)

    From the **Creatives** section, you can associate creatives with a line item, schedule when the creatives will serve, determine how the creatives will rotate through line item inventory, and optionally add creative landing page URLs.

1. [Configure a Programmable Split](configure-a-programmable-split.md)

    From the **Programmable Splits** section, you can use programmable splits to refine line item targeting and dynamically adjust bids, budget allocation, and creative allocation across a line item's targeted inventory. Splits are recommended if you have sophisticated targeting requirements.

1. [Apply a Partner Fee to a Line Item](apply-a-partner-fee-to-a-line-item.md)

    From the **Fees** section, you can optionally apply a partner fee to a line item to track third-party costs.

1. [Add Reporting Labels and Comments to a Line Item](add-reporting-labels-and-comments-to-a-line-item.md)

    From the **Reporting Labels & Comments** section, you can optionally assign custom reporting labels to a line item so that you can create reports tracking metrics across multiple line items, as well as add comments to a line item for your reference.
