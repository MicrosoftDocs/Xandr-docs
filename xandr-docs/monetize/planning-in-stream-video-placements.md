---
title: Planning In-Stream Video Placements
description: In this article, find information about the factors to be considered while creating placements and placement groups for in-stream video inventory.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Planning in-stream video placements

Before creating placements and placement groups for in-stream video inventory, you should consider your targeting and reporting needs as well as the operational costs of creating large numbers of placements.

Microsoft Advertising uses the following sell-side hierarchy: Publisher > Placement Group > Placement.

When setting up this hierarchy, you can typically use the following mappings:

| Seller Unit | Microsoft Advertising Object | Example |
|---|---|---|
| Ad slot | Placement | pre-roll |
| Device type | Placement Group | CTV |
| Domain or App | Publisher | DailyCamera.com |

However, you might decide to revise this object hierarchy depending on the nature of your inventory as well as commercial and operational overhead. For example, consider the following factors:

- **Deals implementation:** Will you be using unique targeting, such as targeting specific sections of the site? If so, assigning a placement group to each targeted section will simplify deal targeting.
- **Reporting:** Does the publisher have unique reporting needs, such as breaking out reporting by device or site? If you can't get this information through the standard Microsoft Advertising reports, using placements or placement groups to organize the desired outputs could help.
- **Operational burden of tagging:** If you break out hundreds of placements, the publisher will need to manually traffic these tags on their ad server, and then manually update them with any future changes. Consider organizing placements within placement groups or streamlining the number of placement breakouts in order to reduce operational overhead.
