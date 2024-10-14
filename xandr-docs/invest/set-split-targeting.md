---
title: Microsoft Invest - Set Split Targeting
description: In this article, you'll learn how to set split targeting. You can define a split by specifying the targeting goals you want it to meet.
ms.date: 10/28/2023
---

# Microsoft Invest - Set split targeting

You can define a split by specifying the targeting goals you want it to meet.

1. Select the pencil icon that displays in the **Name** column for the corresponding split.
1. Select the **Setup** tab and set the **Bid Multiplier**.
1. Select the **Targeting** tab and select the types of targeting you want to apply using the dropdown menu.
    By default, the targeting goal for a selected category is met if the impression includes any of the values you specify. Select the **Include Any** menu to change this to **Exclude All**.

    This table lists all the features you can use to define a split:

    | Feature Class | Feature Name |
    |:---|:---|
    | Geo | - Country <br> - Region <br> - City <br> - Metro Code <br> - Postal Code <br> **Note**: When specifying postal code, you must also include the country code. For example, to target postcode 2096 in Australia, enter `"AU:2096"`. For more information, see [Additional Geo Restrictions](./additional-geo-restrictions-ali.md).<br> - Postal Code Lists. <br><br>For more information, see [Postal Code Lists](./postal-code-lists.md). |
    | Inventory | - Size <br> **Note**: The format for size values is height x width.<br> - Domain or app<br> - Placement (1st party and 3rd party)<br> - Publisher (1st party and 3rd party)<br> - Seller member<br> - Inventory type (web or app)<br> - Inventory URL list targeting (allowlists and blocklists)<br><br> For more information, see [Inventory Targeting (ALI)](./inventory-targeting-ali.md). |
    | System | - Operating system family<br> - Operating system version<br> - Browser<br> - Browser language<br> - Device type<br> - Device carrier<br> - Model<br><br>For more information, see [Buy-Side Targeting](./buy-side-targeting.md). |
    | Inventory Performance | - Viewability Threshold<br> - Video Viewability Threshold<br> - Completion Rate Threshold<br><br>For more information, see [Introduction to Viewability](./introduction-to-viewability.md). |
    | Segment | - Segment presence/absence<br> - Segment age: The amount of time since a user was added to a segment.<br> - Segment value: The value associated with the segment (by you or by the buyer). This can be an individual value or a range. |
    | Frequency & Recency |  - Daily frequency<br> - Lifetime frequency<br> - Split recency<br> <br>**Note**: Split recency caps differ from regular line item recency caps in that you're setting recency caps to "retarget" users who have already been served an impression. This means users are only eligible for an impression through a split's recency caps if that split (or its parent line item) has already served them a creative. <br><br>For example, if the split recency targeting is set to **<1 day**, a creative is served to users who have already seen the creative within the last day.<br><br> - Advertiser lifetime frequency<br> - Advertiser daily frequency<br> - Advertiser recency<br> - Line item lifetime frequency<br> - Line item daily frequency<br> - Line item recency<br><br>For more information, see [Frequency and Recency Caps](./frequency-and-recency-caps.md). |
