---
title: Inventory Quality Targeting
description: In this article, learn how to restrict your campaign to target inventory based on inventory quality.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Inventory quality targeting

> [!IMPORTANT]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

In the **Inventory Quality** section of a campaign, you can determine how restrictive your campaign will be about the inventory it serves on.

- **Serve only on Microsoft Advertising-reviewed inventory** - This is the most restrictive option and is selected by default. You will serve only on high-traffic domains that Microsoft Advertising has reviewed for sensitive attributes and intended audience. You will therefore have less volume but better inventory quality assurance.
- **Also serve on trusted seller-reviewed/unreviewed inventory** - This is less restrictive. In addition to serving on Microsoft Advertising-reviewed inventory, you will also serve on seller-reviewed and unreviewed inventory from sellers that you have trusted in your **Seller Eligibility** settings. See [Edit Seller Defaults](edit-seller-defaults.md) for more details.
- **Serve on any inventory** - This is the least restrictive option. You will serve on all inventory (Microsoft Advertising-reviewed, seller-reviewed, and unreviewed) from all eligible sellers.

> [!NOTE]
>
> - By default, inventory quality filtering is enabled to allow platform-reviewed inventory. Since the majority of third-party mobile web inventory comes from external supply sources and is not platform-reviewed, the best way to reach this inventory is to turn off inventory quality filtering.
> - Inventory Quality does not apply to in-app inventory. Mobile campaigns will deliver on in-app inventory, regardless of your campaign's Inventory Quality setting.
> [!IMPORTANT]
> Regardless of your inventory quality settings, you will never serve on sellers that you have blocked in your **Seller Eligibility** settings. For more details, see [Edit Seller Defaults](edit-seller-defaults.md).

If you choose to serve on Microsoft Advertising-reviewed or seller-reviewed inventory, you can click the **Edit** button to further expand your reach to target inventory that has been flagged (by Microsoft Advertising or by the seller) with sensitive attributes and intended audiences.

## Related topics

- [Create a Campaign](create-a-campaign.md)
- [Inventory Lists (ALI)](inventory-lists-ali-only.md)
- [Inventory Targeting (ALI)](inventory-targeting-ali.md)
