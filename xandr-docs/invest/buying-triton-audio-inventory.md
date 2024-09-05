---
title: Microsoft Invest - Buy Triton Audio Inventory
description: In this article, you’ll find information on the Triton Audio Ad Exchange, including testing ads and setting up a line item to target audio inventory. 
ms.date: 10/28/2023
---

# Microsoft Invest - Buy Triton audio inventory

This page provides specific information for the **Triton Audio Ad Exchange**, which includes testing your ads and setting up a line item to target **Triton** audio inventory.

> [!NOTE]
> If you are interested in serving companion banner ads, please contact your Microsoft Advertising or Triton representative.

## Test your ads

After designing your audio creative and adding your creative to Microsoft Advertising, you can test it. See [Buying Audio Inventory](./buying-audio-inventory.md).

Triton Digital has created a test station where you can test your a2x/Microsoft Advertising ads in a replica of a live environment. The test station runs a sequence of one song followed by one or more ads. You can test only one ad at a time.

> [!NOTE]
> To access the test station, a **custom placement ID** and a **player site ID** from Triton Digital is required. To obtain these IDs, contact Triton Digital customer support.

To set up and listen to a test ad:

1. Upload your ad using the **Creative Manager** and assign it to the **Alpha Test** brand in the **Creative Attributes** section, using the **Self-classify** audit option.
1. Create a new line item. In the **Buying Strategies** area of the **Basic Setup** section, set the **Bid a base CPM** to $1.00 CPM.
    > [!NOTE]
    > These impressions will not becharged since this is a testing platform.
1. In the **Targeting** section, select **Inventory** > **3rd Party Inventory** targeting and enter your custom placement ID using the **text** mode.
1. Click **Include** and then **Add**.
1. Go to the following URL: [https://player.listenlive.co/xxxx](https://player.listenlive.co/xxxx), where xxxx is the site ID provided by Triton Digital.

## Target Triton inventory

After setting up your line item, you can target all Triton inventory or specific categories of Triton inventory.

In the **Targeting** section under **Inventory**, click **Edit**. This opens the **Inventory Targeting** dialog.

## Target all Triton inventory

In the **Inventory Targeting** dialog, under **3rd Party Inventory** > **Sellers**, search for "Triton". Include the seller called **Triton Digital** by clicking on the green checkmark icon.

## Target specific categories of Triton audio inventory

Alternatively, you can narrow the inventory to specific formats. Click **Triton Digital** in the **Sellers** view to see a list of all the categories.You are now in the **Publishers and Categories** view. Select the format categories you want to include.

You can narrow the inventory type by excluding categories such as ad type, asset type etc. You can also exclude categories that you don't want instead of including categories that you do.

## Ad type categories: preroll or midroll

If you want to play only preroll ads, exclude the midroll category.

To specify a preroll line item:

1. In the inventory list for Triton Digital, search for **Midroll**.
1. Click the minus icon to exclude the **Midroll** category.

## Device categories

Using inventory targeting, you can narrow the scope of your line item to include or exclude device categories. The available device categories are listed below.

| Category | Description |
|:-|:-|
| Device: Computer App (23876) | Players in PC-based apps such as iTunes, Windows Media Player, Winamp, or VLC. Does not use cookies. |
| Device: Computer Browsers (23875) | Players rendered in PC-based web browsers. Uses cookies. |
| Device: Mobile Apps (23878) | Players in mobile device player apps. Does not use cookies. |
| Device: Mobile Browser (23877) | Players in device-optimized mobile web browsers, such as iOS Safari and Android Chrome. Uses cookies. |
| Device: Uncategorized (23879) | Inventory that is not categorized. The vast majority of this inventory is intended for mobile apps, but it also includes consoles such as Roku. Does not use cookies. <br><br> **Tip**: It is recommended not to exclude the uncategorized category if you want access to the full scale of inventory for mobile devices. |

## Cookie categories

You can also narrow the inventory by specifying if the inventory should target players that use cookies, or those that do not. The available cookie categories are listed below.

| Category | Description |
|:--|:--|
| Cookie: Matched (924163) | Inventory that is assigned to traffic from users who are matched to an ID from Microsoft Advertising using the Microsoft Advertising cookie. |
| Cookie: Not Synced (24164) | Inventory that is assigned to traffic from users who are not synced with an ID from Microsoft Advertising, either because the player does not support cookies or because the player does not have the cookie sync code. |

> [!NOTE]
> There are no controls to keep you from narrowing your scope to a point of excluding all inventory. For example, you can choose to exclude **Category: Mobile Browser** in a line item with a scope of "Mobile: Device-Optimized websites". This will leave you with no available inventory. Make sure to use prudence when targeting categories.
