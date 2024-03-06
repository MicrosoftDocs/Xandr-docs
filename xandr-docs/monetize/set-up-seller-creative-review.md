---
title: Set Up Seller Creative Review
description: Explore and approve creatives in the Political category before serving on seller inventory. Seller review will extend to additional categories.
ms.date: 10/28/2023
---

# Set up seller creative review

Currently, sellers can review and approve creatives within the Political category before they serve on seller inventory. In the future, Microsoft Advertising will support seller review of additional categories.

Seller Creative Review requires the following initial setup before it can show you a list of creatives to review:

- Block supported creative categories by default in **Ad Quality Network**/**Publisher Template**. If you aren’t blocking the creative category, you don’t need to manually prove creatives.
- Configure deal line item to:
  - Only allow seller-approved creatives.
  - Ignore the **Ad Quality** block of the supported creative categories.

## Block supported creative categories

You’ll need to block any supported creative categories by default, so creatives in this category won’t run on your inventory unless you review and explicitly approve them individually in the **Seller Creative Review** window.

> [!NOTE]
> Seller Creative Review currently supports the following political creative categories:
>
> - **Politics**
> - **Political: “Hot button” issue for commercial use**
> - **Political: Negative Attack Ads**

To block supported creative categories by default:

1. Open the **Ad Quality Network/Publisher Template** (for Network Template: **Network** \> **Ad Quality**; for Publisher Template: **Publisher Ad Quality**). For more information, see [Working with Network Ad Quality](working-with-network-ad-quality.md) and [Working with Ad Quality](working-with-publisher-ad-quality.md)
1. Select the **Settings** tab.
1. In the **Categories** section, search for the supported creative categories you want to review.
1. Under **Eligibility** for each category you want to review, select **Banned** from the drop-down.

## Configure deal line item

To be able to review and explicitly approve creatives to run on your inventory for a deal, you must create a deal line item and configure it to ignore the **Ad Quality** block, but only for seller-approved creatives. The **Seller Creative Review** window only lists creatives that are actively bidding and creating errors against a deal in your network over the last 7 days. To ensure results are actionable, creatives that are bidding on open exchange inventory are not included. Because you initially blocked the supported creative categories in the **Ad Quality Network/Publisher Template**, creatives in these categories won’t run on your inventory without explicit approval.

> [!NOTE]
> The **Seller Creative Review** feature is only supported for deal line items. Before you can create a deal line item, you’ll need to create or already have access to an advertiser and insertion order.

To create a deal line item configured for the **Seller Creative Review** feature:

1. Create a deal line item that includes the following settings in the **Deal Creative Criteria** section (for more information, see [Create a Deal Line Item](create-a-deal-line-item.md)):
   1. Next to **Creative Review**, select the **Only allow seller-approved creatives** checkbox so that only creatives that you explicitly approve will run.
   1. Click **Edit** under **Creative Category** and select the **Ad Quality Settings** tab.
   1. Search for the supported creative categories you blocked in the **Ad Quality Network**/**Publisher Template**. For example, to list the three political categories, enter “`politic`“ in the search window and click **Ignore** in the **Ad Quality Settings** column for each creative category.
1. Finish configuring the remaining settings in the new deal line item and click **Save**.

The **Seller Creative Review** window will now display creatives for this deal that require seller review. The **Seller Creative Review** window is updated daily and includes creatives that generate errors against a deal in the prior 7 days. For more information, see [Seller Creative Review List](seller-creative-review-list.md).

## Related topics

- [Seller Creative Review](seller-creative-review.md)
- [Seller Creative Review List](seller-creative-review-list.md)
- [Approve and Reject Creatives](approve-and-reject-creatives.md)
