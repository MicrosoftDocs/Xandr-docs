---
title: Microsoft Monetize - Set Split Targeting
description: Explore split targeting, define, set bid multipliers, apply goals, customize categories, toggle inclusion/exclusion.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set split targeting

You can define a split by specifying the targeting goals you want it to meet.

1. Click the pencil icon that displays in the **Name** column for the corresponding split.
1. Click the  **Setup** tab and set the **Bid Multiplier**.
1. Click the **Targeting** tab and select the types of targeting you want to apply using the dropdown menu.

    By default, the targeting goal for a selected category is met if the impression includes any of the values you specify. Click the **Include Any** menu to change this to **Exclude All**.

   This table lists all the features you can use to define a split:

   | Feature Class | Feature Name |
   |---|---|
   | Geo | - Country<br> - Region<br> - City<br> - Metro Code<br> - Postal Code<br><br>**Note**:<br>When specifying postal code, you must also include the country code. For example, to target postcode 2096 in Australia, enter "AU:2096".<br>For more information, see [Additional Geo Restrictions](additional-geo-restrictions-ali.md). |
   | Inventory | - Size<br><br>**Note**: The format for size values is heightXwidth.<br><br> - Domain or app (Not supported by GDALI)<br> - Placement (1st party and 3rd party)<br> - Publisher (1st party and 3rd party)<br> - Seller member (Not supported by GDALI)<br> - Inventory type (web or app)<br> - Inventory URL list targeting (allowlists and blocklists) (Not supported by GDALI)<br>For more information, see [Inventory Targeting (ALI)](inventory-targeting-ali.md). |
   | System | - Operating system family<br> - Operating system version<br> - Browser<br> - Browser language<br> - Device type<br> - Device carrier<br> - Model<br>For more information, see [Buy-Side Targeting](buy-side-targeting.md). |
   | Inventory Performance | - Viewability Threshold (Not supported by GDALI)<br> - Video Viewability Threshold (Not supported by GDALI)<br> - Completion Rate Threshold (Not supported by GDALI)<br>For more information, see [Introduction to Viewability](introduction-to-viewability.md). |
   | Segment | - Segment presence/absence<br> - Segment age: The amount of time since a user was added to a segment.<br> - Segment value: The value associated with the segment (by you or by the buyer). This can be an individual value or a range. |
   | Frequency & Recency | - Daily frequency<br> - Lifetime frequency<br> - Split recency<br><br>**Note**: Split recency caps differ from regular line item recency caps in that you're setting recency caps to "retarget" users who have already been served an impression. This means users are only eligible for an impression through a split's recency caps if that split (or its parent line item) has already served them a creative.<br>For example, if the split recency targeting is set to **<1** day, a creative is served to users who have already seen the creative within the last day.<br> - Advertiser lifetime frequency<br> - Advertiser daily frequency<br> - Advertiser recency<br> - Line item lifetime frequency<br> - Line item daily frequency<br> - Line item recency<br>For more information, see [Frequency and Recency Caps](frequency-and-recency-caps.md).
