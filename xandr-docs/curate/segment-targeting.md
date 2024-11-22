---
title: Microsoft Curate - Segment targeting
description: In this article, learn how you can target users within segments using boolean expressions.
ms.date: 10/28/2023
---

# Microsoft Curate - Segment targeting

You can target users within segments by using Boolean expressions. Users get added to segments after they've viewed or selected a particular creative.

You can set up segment targeting by going to the **Audience & Location Targeting \> Audience & Location Segments** subsection within the **Create New Line Item** screen or **Edit Line Item** screen. The **Audience & Location Segments** subsection displays all segments belonging to the advertiser for the associated line item as well as segments defined at the Member level.

## Creating boolean expressions between segment groups and segments

You can use the following Boolean operators to narrow or broaden your targeting scope:

| Boolean Operator | Purpose | Targeting Requirement | Example |
|:---|:---|:---|:---|
| AND | Narrows the targeting scope. | - If targeting multiple segments within a segment group, users must belong to all selected segments.<br> - If targeting multiple segment groups that contain multiple segments, an Or relationship will be created between segment groups. Therefore, users only have to belong to one segment group but not all of them to be targeted. | For example, your travel agency wants to sell timeshares at its new resort properties in Miami, Florida and Los Angeles, California. In order to sell as many timeshares as possible, you want to promote a first class getaway to these resorts by targeting travelers who have a desire to travel to Miami or Los Angeles in first class. |
| OR | Broadens the targeting scope. | - If targeting multiple segments within a segment group, users can belong to any of the selected segments.<br> - If targeting multiple segment groups that contain multiple segments, an And relationship will be created between segment groups. Therefore, users must belong to all segment groups to be targeted. | For example, you're hosting a book signing in New York City in the next few weeks, so you want to promote the event throughout the state of New York and possibly nearby states such as Pennsylvania, New Jersey, and Connecticut. The new book is about how to excel in the real estate industry, so you specifically want to target users who are currently working within real estate or users who have an interest in starting a career within real estate. |

For more information about how to set up segment targeting at the augmented line item level, see [Set Up Segment Targeting on a Line Item](../monetize/set-up-segment-targeting-on-a-line-item.md).

## Related topics

- [Create a Segment Pixel](create-a-segment-pixel.md)
- [Associate Segment Pixels with Creatives](../monetize/associate-segment-pixels-with-creatives.md)
