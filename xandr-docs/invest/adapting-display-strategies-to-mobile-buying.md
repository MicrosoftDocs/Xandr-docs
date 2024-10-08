---
title: Microsoft Invest - Adapt Display Strategies to Mobile Buying
description: Understand how the technical limitations of mobile buying affects your overall strategy and what you can do to adapt.
ms.date: 10/28/2023
---

# Microsoft Invest - Adapt display strategies to mobile buying

This article aims to help buyers who are already familiar with display buying and would like to start to [Buy Mobile Inventory via RTB](buy-mobile-inventory-via-rtb.md).The goal of this article is to help buyers understand how the [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md) can affect their overall strategy, and what they can do to adapt.

For general questions about mobile buying, please visit the [Mobile Buying FAQ](mobile-buying-faq.md). For general questions about optimization, please visit the [Optimization Guide - ALI](optimization-guide-ali.md). For line item setup information and how-tos, see [Working with Line Items](working-with-line-items.md).

## Create separate mobile apps and mobile web campaigns

As described on the [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md), mobile apps cannot be platform-reviewed. However, you might still want to serve on platform-reviewed mobile web inventory. In this case, you should separate campaigns targeting apps from those targeting mobile web inventory.

> [!NOTE]
> It is up to the sellers to declare the supply type for their placements. In other words, this is not a part of the Microsoft Advertising platform review process. Some sellers may not describe their placements' supply type accurately. For this reason, it is best practice to set mobile web campaigns to include both mobile web and web supply.

To target a range of mobile inventory, select multiple inventory types - for example, phones and tablets - for your supply type.

For more information on line item setup and targeting, see [Create an Augmented Line Item](create-an-augmented-line-item-ali.md). For additional information, see [Buying Mobile Inventory](buying-mobile-inventory.md) and [Buy-Side Targeting](buy-side-targeting.md).

## Mobile specific reporting and targeting

In general, it is best to start by optimizing your targeting for the broadest reach, then use the data you have gathered via reporting and by reviewing delivery and performance to optimize towards better performance without sacrificing delivery.

[Mobile-Specific Reporting](mobile-specific-reporting.md) can be a big help when assessing performance and delivery. Available fields and dimensions include **Device Type**, **Device Make**, **Device Model**, **Carrier**, and **Apps Lists**.

- When creating an app list, try to use clear, explicit names, for example "Premium Apps - Allowlist" or "Poorly-performing Apps for Advertiser XYZ - Blocklist". When you set up your targeting, you will have to choose between multiple app lists, and you will find clear names useful.
- Unfortunately some impressions don't pass us the App ID, and appear in reporting as "---". In order to avoid serving on unidentified    apps, you may want to use allowlists.

## Mobile, Cookies, and Device ID: Carefully monitor your frequency capping strategy

[Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md) covers some key challenges of mobile user tracking. For example, unlike display buying, it may be hard to apply frequency capping as some apps don't pass along the Device ID.

To avoid limiting your reach and missing out on cheap but valuable inventory, you can follow the steps below:

1. Gather data by launching campaigns where frequency capping is turned off.
1. Once you have gathered enough data, create a [Creative Frequency and Recency Report](creative-frequency-and-recency-report.md).
1. Based on the data, decide which campaigns should have frequency capping to optimize performance, and which campaigns should run without frequency capping to extend reach.

## Related topics

- [Welcome to Mobile](welcome-to-mobile.md)
- [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md)
- [Mobile-Specific Reporting](mobile-specific-reporting.md)
- [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md)
- [Mobile Targeting and Attribution Challenges](mobile-targeting-and-attribution-challenges.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
