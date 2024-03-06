---
title: Setting Up 24/7 Media Inventory Through the Microsoft Ad Exchange
description: Explore 24/7 media inventory with Microsoft Ad Exchange, using Real Media Group for diverse campaigns. Adjust settings for efficiency.
ms.date: 10/28/2023
---

# Setting up 24/7 media inventory through the Microsoft Ad Exchange

The Microsoft Adverting Exchange (MAX) includes Real Media Group exclusively to 24/7 Open AdStream and Global Web alliances. You canadjust your campaign and targeting settings to purchase inventory according to several different scenarios.

## Universal settings

In addition to the steps of setting up targeting as you do for all campaigns, you must perform the following steps for any scenario involving the purchase of 24/7 Media inventory through the Microsoft Ad Exchange:

## Create new campaign/select line item and scope

When defining the **Campaign Type**, be sure to select **Display and Mobile**.

## Buying strategy

Under **Buying Strategies** in the **Basic Setup** section, select **Buy Third-Party Inventory**.

## Inventory

In the **Targeting** section, the following settings must be in place:

- **Inventory Quality** - Click the **Edit** button and check the **Allow All** checkbox in order to allow sensitive attributes. Approximately 75% of 24/7 Media inventory is currently platform-audited, so excluding sensitive attributes may limit your inventory availability.
- **Inventory** - Select the **3rd Party Inventory** option from the list, then click the Sellers tab in the 3rd Party Inventory pane, and search for **Microsoft Advertising Exchange (280)**.
  - Select **Sellers**
  - Search by **Microsoft** and select **Microsoft Advertising Exchange (280)** - click the check mark to include it.

Allowlists and blocklists cannot be used with any masked URLs because you cannot target masked domains. You must include or exclude groups of URLs through the use of seller bins (defined below).

## Selecting Microsoft "Bins"

Bins are granular buckets of web inventory, usually grouped by country or language. The MSN bins are shown in Microsoft Monetize as "categories." Selecting Microsoft Advertising Exchange at the Sellers includes all publishers and content categories under the Microsoft Ad Exchange by default. Under the Publishers & Categories tab you can exclude either publishers or categories that you would prefer not to target.

The procedure for working with bins is described in detail on the [Target Inventory on the Microsoft Advertising Exchange](target-inventory-on-the-microsoft-advertising-exchange.md).

> [!NOTE]
> bins concern the location of the inventory, not the location of the user. For example, if you target a bin of Canadian inventory, your campaign will serve only to users who are looking at that Canadian inventory.

## Targeting

In addition to the settings listed above, you must determine the exact targeting scenarios that you wish to use. The targeting steps required to set up the specified scenario are listed below:

- [Target all Microsoft Advertising Exchange inventory including 24/7 Media](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md#target-all-microsoft-advertising-exchange-inventory-including-247-media)
- [Target all Microsoft Advertising Exchange inventory but exclude 24/7 Media inventory](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md#target-all-microsoft-advertising-exchange-inventory-but-exclude-247-media-inventory)
- [Target specific Microsoft Ad Exchange inventory only](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md#target-specific-microsoft-ad-exchange-inventory-only)
- [Target only 24/7 Media inventory](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md#target-only-247-media-inventory)
- [Target specific Microsoft Ad Exchange (including 24/7 Media)](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md#target-specific-microsoft-ad-exchange-including-247-media)
- [Targeting specific Microsoft Ad Exchange domains where visible (select sites and countries)](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md#targeting-specific-microsoft-ad-exchange-domains-where-visible-select-sites-and-countries)

## Target all Microsoft Advertising Exchange inventory including 24/7 media

1. In the **Targeting** section under **Inventory**, click edit to open the **Inventory Targeting** dialog.
1. In the **Inventory Targeting** dialog, select **3rd Party Inventory**.
1. 3rd Party Inventory pane in the Sellers view, enter the term **Microsoft** in the search field. Include **Microsoft Advertising Exchange (280)** by clicking the green checkmark icon.
1. The selection should now appear in the **Selected 3rd Party Inventory** pane.

  > [!NOTE]
  > **Microsoft Advertsing Exchange (Seller 280)** is included by default in any non-targeted campaign, so it is not necessary to specify this targeting unless you wish to dedicate budgets specifically to this source.

## Target all Microsoft Advertising Exchange inventory but exclude 24/7 media inventory

You can choose all Microsoft Ad Exchange inventory while excluding all
24/7 Media inventory. The steps are as follows:

1. In the **Targeting** section under **Inventory**, click edit to open the **Inventory Targeting** dialog.
1. In the **Inventory Targeting** dialog, select **3rd Party Inventory**.
1. In the **3rd Party Inventory** pane in the **Sellers** view, enter the term **Microsoft** in the search field. Include **Microsoft Advertising Exchange (280)** by clicking the green checkmark icon.
1. The selection should now appear in the **Selected 3rd Party Inventory** list as a green "include" item.
1. Select **Custom Categories** (also in the **Inventory Targeting** dialog).
1. In the **Custom Categories** pane, enter the term 247 in the search field. Exclude **247_Media (23204)** by clicking the red exclude icon.
1. The selection should now appear in the **Selected Custom Categories** list as a red "exclude" item.

## Target specific Microsoft Ad Exchange inventory only

You can choose to serve on only certain portions of Microsoft Ad Exchange inventory. The steps are as follows:

1. In the **Targeting** section under **Inventory**, click edit to open the **Inventory Targeting** dialog.
1. In the **Inventory Targeting** dialog, select **3rd Party Inventory**.
1. In the **3rd Party Inventory** pane in the **Sellers** view, enter the term **Microsoft** in the search field. Click on the row to expose the **Content Category** list for Microsoft Ad Exchange.

    > [!NOTE]
    > Do not not click the green include icon or the red exclude icon, as this will simply include or exclude all Microsoft Ad Exchange inventory.

1. **Content Categories** on the Microsoft Advertising platform correspond to bins in Microsoft terminology. Choose the content categories to include by clicking the corresponding icons for those categories.
1. The bins you chose to include or exclude should now appear in the **Selected 3rd Party Inventory** list.

## Target only 24/7 media inventory

You can choose to target only 24/7 Media inventory. The steps are as follows:

1. In the **Targeting** section under **Inventory**, click edit to open the **Inventory Targeting** dialog.
1. In the **Inventory Targeting** dialog, select **3rd Party Inventory**.
1. In the **3rd Party Inventory** pane in the **Sellers** view, enter the term **Microsoft** in the search field. Include **Microsoft Advertising Exchange (280)** by clicking the green checkmark icon.
1. The selection should now appear in the **Selected 3rd Party Inventory** list as a green "include" item.
1. Select **Custom Categories** (also in the **Inventory Targeting** dialog).
1. In the **Custom Categories** pane,  enter the term 247 in the search field. Include **247_Media (23204)** by clicking the green checkmark icon.
1. The selection should now appear in the Selected Custom Categories list as a green "included" item.

## Target specific Microsoft Ad Exchange (including 24/7 Media)

You can choose to target specific inventory including 24/7 Media inventory. The steps are as follows:

1. In the **Targeting** section under **Inventory**, click edit to open the **Inventory Targeting** dialog.
1. In the **Inventory Targeting** dialog, select **3rd Party Inventory**.
1. In the **3rd Party Inventory** pane in the **Sellers** view, enter the term **Microsoft** in the search field. Include **Microsoft Advertising Exchange (280)** by clicking the green checkmark icon.
1. The selection should now appear in the **Selected 3rd Party Inventory** list as a green "include" item.
1. Select **Custom Categories** (also in the **Inventory Targeting** dialog).
1. In the **Custom Categories** pane, enter the term 247 in the search field. Include **247_Media (23204)** by clicking the green checkmark icon.
1. The selection should now appear in the **Selected Custom Categories** list as a green "included" item.
1. In the **3rd Party Inventory** pane in the **Sellers** view, enter the term **Microsoft** in the search field. Click on the row to expose the **Content Category** list for Microsoft Ad Exchange.

   > [!NOTE]
   > Do not click the green include icon or the red exclude icon, as this will simply include or exclude all Microsoft Ad Exchange inventory.

1. **Content Categories** on the Microsoft Advertising Platform correspond to **bins** in Microsoft terminology. Choose the content categories to include by clicking the corresponding icons for those categories.
1. The bins you chose to include or exclude should now appear in the **Selected 3rd Party Inventory** list.

## Targeting specific Microsoft Ad Exchange domains where visible (select sites and countries)

Currently, visible domain availability consists of **Microsoft MSN** and **Live** properties in **NL**, **ES**, **NO**, **DK**, **SE**, **ES**, **FR**, **US**, and **UK**.

1. Under **Targeting** in the **Inventory Targeting** section, click the **Edit** button. This opens the **Inventory Targeting** dialog.
1. Select **Specific Domains**.
1. Using the list on the [Microsoft Advertising Exchange Inventory](microsoft-advertising-exchange-inventory.md) page, copy-and-paste all desired Microsoft domains into this field, each separated by a comma. You can enter up to 25 domains per campaign.
1. Click the **Add Domains** button.
1. Excluded is the default settings, so you will need to click the **Include** buttons to switch the inventory from excluded to included.

## Related topics

- [Buy-Side Targeting](buy-side-targeting.md)
- [Target Inventory on the Microsoft Advertising Exchange](target-inventory-on-the-microsoft-advertising-exchange.md)
- [Microsoft Advertising Exchange Inventory](microsoft-advertising-exchange-inventory.md)
