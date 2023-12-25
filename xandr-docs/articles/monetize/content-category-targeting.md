---
title: Microsoft Monetize - Content Category Targeting
description: The article defines content category targeting where the argeting is only available to Standard Line Items.
ms.date: 10/28/2023
---

# Microsoft Monetize - Content Category Targeting

> [!NOTE]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see
> [Buy-Side Targeting](buy-side-targeting.md).

There are two types of content categories:

- **Universal:** Universal categories are defined by Xandr. When Xandr reviews inventory, we apply these categories based on the inventory's content. For example, a car dealership placement group would be assigned to the "Autos & Vehicles" category. Sellers can apply universal categories when self-reviewing inventory as well.
- **Custom:** Custom categories are defined by sellers. Sellers create these and apply them to slices of their inventory to package their inventory for specific buyers to target.

This page explains how to target each type of content category.

## Target universal categories

By default, your campaign will target all universal categories. However, you can narrow your targeting to include or exclude specific universal categories.

1.  In the **Targeting** section, click **Edit** next to **Inventory**.
1.  On the **Universal Categories** tab, include or exclude custom categories.
    a. The **Categories** lists shows all top-level universal categories defined by Xandr. You can either include or exclude top-level categories or drill into a category to view
    b. its child categories.
    c. The **Sub-Categories** list shows all child universal categories in the context of their parent categories. You can either include or exclude sub-categories. Note that when you exclude a top-level category, its sub-categories are not available for further inclusion or exclusion.

      > [!IMPORTANT]
  >  When targeting more than one universal category, the categories have an OR relationship. For example, if you target the "News" and "Finance" categories, you will bid on inventory that is in either category. The inventory does not need to be in both categories.

3.  Click **Add**.

## Target custom categories

By default, your campaign will target all custom categories. However, you can narrow targeting to include or exclude specific custom categories that you have applied to your own placement groups and/or placements for direct buying as well as custom categories that other sellers have exposed to you for third-party buying.

1.  In the Targeting section, click **Edit** next to **Inventory**.

1.  On the **Custom Categories** tab, include or exclude custom categories.

    a. When targeting more than one custom category, the categories have an OR relationship. For example, if you include "Custom Category 1" and "Custom Category 2", you will bid on inventory that is in either category. The inventory does not need to be in both categories.

1.  Click **Add**.

## Related topics

- [content-categories.md](Content Categories)
- [Manage Custom Content Categories](manage-custom-content-categories.md)
- [Create a Campaign](create-a-campaign.md)
