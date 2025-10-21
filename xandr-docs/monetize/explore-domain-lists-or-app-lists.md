---
title: Explore Domain Lists or App Lists
description: Manage domains and apps, add to lists, export for safekeeping and offline use, copy to create new lists, delete existing lists.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Explore domain lists or app lists

> [!NOTE]
> Targeting lists are only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

You can add domains and apps to lists, export domain lists or app lists to a text file for safekeeping or offline use, or delete domain lists and app lists. In addition, you can also create new domain lists or app lists by copying existing lists. For information about creating these lists, see [Create a Domain List or App List](create-a-domain-list-or-app-list.md). For information about updating these lists, see [Update a Domain List or App List](update-a-domain-list-or-app-list.md).

## Overview

To perform any **Actions** on a domain list or app list:

1. In Microsoft Monetize UI, select **Network** >  **Inventory** > **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** or **App Lists** tab.
1. Select the checkbox next to the domain lists or app lists that you would like to perform an action on.
1. Click the **Actions** dropdown and select the appropriate action (see below for details for each action).

> [!NOTE]
> Domain targeting applies only to **Web** and **Mobile Web** impressions and does not apply to **Mobile App** impressions. If you have allowed your campaign to serve on mobile apps while targeting a domain list, the campaign will be unrestricted when buying mobile app inventory unless you have also applied App List targeting. To avoid serving on mobile app inventory, switch the **Apps Placements** toggle in your campaign's targeting profile to OFF.

## Add Domains or Apps to a List

To add domains or apps to a list:

1. In Microsoft Monetize UI, select **Network** >  **Inventory** > **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** or **App Lists** tab.
1. Select the checkbox next to one or more domain lists or app lists.
1. Select **Actions** >  **Add domains** OR **Add apps** and do one of the following options:
    - Select **Enter text** and copy and paste domains or apps into the box. OR
    - Select **Upload a file**, click **Select File**, select the file to upload, and click **Open**.
1. Click **Add**.

> [!NOTE]
> Excel files are not allowed. For more information on formatting requirements for adding domains or apps by copy and paste or file upload, see [Create a Domain List or App List](create-a-domain-list-or-app-list.md).

## Export a domain list or app list

To export a domain list or app list:

1. In Microsoft Monetize UI, select **Network** >  **Inventory**  >  **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** or **App Lists** tab.
1. Select the checkbox next to one or more domain lists or app lists.
1. Select **Actions** >  **Export as .txt file**. A confirmation dialog will appear.
1. Click **Export**.

## Duplicate a domain list or app list

You can create new domain lists or app lists by duplicating existing lists. Once you've duplicated any lists, you can then update them, see [Update a Domain List or App List](update-a-domain-list-or-app-list.md).

To duplicate a domain list or app list:

1. In Microsoft Monetize UI, select **Network** >  **Inventory** > **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** or **App Lists** tab.
1. Select the checkbox next to one or more domain lists or app lists.
1. Select **Actions** >  **Duplicate**. A confirmation dialog will appear. Any duplicated lists will be automatically renamed with the prefix "Copy of", but you can change the list name to whatever you'd like.
1. Click **Copy**.

### Delete a domain list or app list

You can delete domain lists and app lists from the Microsoft Advertising system. Be sure to read the warnings below before you delete a domain list or app list:

> [!WARNING]
> Deleting a domain or app list while it's in use by an active campaign will change the targeting of that campaign. If the list you delete is the only one in use by the campaign, and that campaign does not have individual targeting settings, the result will be a campaign with no targeting, also known as "Targeting the internet." **This is likely to result in massive overspend.**
>
> Deleting a domain or app list is permanent, and deleted lists cannot be restored.

To delete a domain list or app list:

1. In Microsoft Monetize UI, select **Network** >  **Inventory** > **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** or **App Lists** tab.
1. Select the checkbox next to one or more domain lists or app lists.
1. Select **Actions** >  **Delete**. A confirmation dialog will appear. Be sure you really want to delete them before clicking **Delete**. Lists cannot be recovered once deleted.
1. Click **Delete**.

### Related topics

- [Working with Targeting Lists](working-with-targeting-lists.md)
- [Managing Your Targeting Lists](managing-your-targeting-lists.md)
- [Create a Domain List or App List](create-a-domain-list-or-app-list.md)
- [Update a Domain List or App List](update-a-domain-list-or-app-list.md)
