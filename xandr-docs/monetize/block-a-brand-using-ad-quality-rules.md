---
title: Block a Brand Using Ad Quality Rules
description: This page provides a step-by-step guide to block a brand using Network and Publisher Ad Quality. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Block a brand using Ad Quality rules

You can use Network and Publisher Ad Quality to block a brand from serving creatives on placements for an entire network, a single publisher, or only specific placements.

First, identify the brand(s) you wish to block. If it's unclear what brand a served creative belongs to, run a [Seller Brand Review Report](seller-brand-review-report.md) and filter by publishers and time ranges to find the creative's ID and its corresponding brand name and brand ID. For more information, see [How to Run a Seller Brand Review Report](seller-brand-review-report.md).

You may want to prevent certain brands from serving on your ad placements, whether for an entire network, certain publishers, or even a single placement. For example, it's common to block a competitive brand's ads from serving. You may also wish to block a particular brand because it doesn't match your network or publisher's requirements.

1. Decide whether to block brands for a member, publisher, or certain ad placements:

   | Option | Steps |
   |--|--|
   | **Network-Level Block (blocks brands for all publishers)** | a. Select **Publishers > Ad Quality**.<br> b. Edit your **Network Template**. |
   | **Publisher-Level Block (blocks brands for a single publisher)** | a. Select **Publishers > Ad Quality**.<br> b. Choose the publisher for which you want a brand blocked. Then, create or edit a base rule. |
   | **Placement-Level Block (blocks brands for certain ad placements)** | a. Select **Publishers > Ad Quality**.<br> b. Choose the publisher for which you want a brand blocked. Then create or edit a conditional rule.<br> c. Navigate to the **Inventory Targeting** tab and select the desired placements or placement groups in the **Inventory Targeting** menu under **Profile Targeting Information**. <br> For more information on conditional rule targeting, see [Base and Conditional Rules](base-and-conditional-rules.md). |

1. Navigate to the **Settings** tab and select **Brands**.
1. In the **Brands** section, search for brands to block.

    If a brand you wish to block does not appear in the search results, submit a support ticket at [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) requesting to add the brand to Microsoft Advertising's database.

1. Select the checkbox for each brand you want to block.
1. After you select all the brands you want to block, select **Actions** \> **Banned**.
1. Ensure the **Eligibility** column lists the blocked brands as **Banned**.
1. If you're using Publisher Ad Quality, click **Submit** to save your settings.

   > [!IMPORTANT]
   > When editing the Network Template using Network Ad Quality, your settings are automatically saved and applied.

## Related topics

- [Choosing the Most Useful Ad Quality Rules](choosing-the-most-useful-ad-quality-rules.md)
- [Improving Ad Quality on Your Inventory](improving-ad-quality-on-your-inventory.md)