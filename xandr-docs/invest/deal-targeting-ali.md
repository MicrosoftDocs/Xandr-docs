---
title: Microsoft Invest - Deal Targeting (ALI)
description: In this article, learn how to target specific and all available deals, including the option to target deals and deal lists at a Programmable Split level.
ms.date: 10/28/2023
---

# Microsoft Invest - Deal targeting (ALI)

By selecting **Deals** in the **Inventory & Brand Safety Targeting &gt; Supply Source** subsection of the **Create New Line Item** or **Edit Line Item** screen, you can target all deals from sellers or specific deals/deal lists from one or more sellers.

## Target deals and deal lists

When you select the **Deals** option in the **Inventory & Brand Safety Targeting &gt; Supply Source** subsection of the **Create New Line Item** or **Edit Line Item** screen, you will have the option to target either all the available deals for that line item, or specific deals from sellers using the configurations detailed below.

### Target all deals available to you

1. In the **Inventory & Brand Safety Targeting &gt; Supply Source** subsection, select **Deals** under **Supply Source**.
1. Select **All Deals**.

### Target specific deals available to you

1. In the **Inventory & Brand Safety Targeting &gt; Supply Source** subsection, select **Deals** in the **Supply Source** section.

1. Select **Specific Deals**.

    A pull-down menu displays with **Deals** selected by default.

1. To target specific deals, select one of the following targeting options and complete the corresponding steps:

    | Targeting Option | Steps |
    |:---|:---|
    | **Deals** | a. Search for available deals by name, alias, ID, or code to target.<br> b. Include deals by selecting the **green check**, or exclude deals by selecting the **red dash**.<br><br> **Tip:** You can also select the eye button to view additional details about the deal such as **Currency**, **Type**, **Sizes**, **Brands**, **Media Types**, **Start Date**, and **End Date**. |
    | **Deal Lists** | a. Search for available deal lists by ID or name to target.<br> b. Include deals by selecting the **green check**, or exclude deals by selecting the **red dash**. |

    > [!NOTE]
    > You may either include deals OR exclude deals, and deal lists, but not both. Include and exclude functionality has to be consistent at line item level. For example, you can't include a deal list and exclude a deal from the deal list on the line item.
    >
    > Deal lists and deals follow the line item and split level targeting constraints. If a deal list and associated deals are excluded at the line item level, splits will not be able to target that inventory regardless of any selections made. Whereas if a deal or deal list is included at the line item level, then split targeting will be respected.

1. Select **Save**.

## Target deals and deal lists at the Programmable Split level

You can specify the deals and/or deal lists to include, or exclude in programmable splits for the line item. To target specific deals or/and deal lists for the split:

1. Select **Deals** or/and **Deal Lists** under **Inventory** within the **Select Targeting** menu in the **Programmable Splits** section of the **Create New Line Item** and **Edit Line Item** screens.

1. Select the **pen** icon next to **Any** under **Deals** or/and **Deal Lists** to go to the **Edit Split** pop-up.

1. In the **Deals/Deal Lists** search field, enter a **Deal List ID** or **Deal ID**, or **Name** to search for deals and deal lists.

1. From the search result, select the applicable deal list(s) or/and deal(s).

    The default in the menu is **Include Any** which includes the selected deal lists or deals for that split.

1. If you would like to exclude deal lists or deals, select **Exclude All** in the menu.

1. Select **Apply** to save the configuration.

> [!NOTE]
> If you're targeting both deal(s) and deal list(s) within the same split, the boolean logic between them will be AND.

## Related topics

- [Inventory Targeting (ALI)](inventory-targeting-ali.md)
- [Buy-Side Targeting](buy-side-targeting.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Augmented Line Items (ALI)](augmented-line-items-ali.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Object Hierarchy](object-hierarchy.md)
- [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md)
- [Deal Lists](deal-lists.md)
