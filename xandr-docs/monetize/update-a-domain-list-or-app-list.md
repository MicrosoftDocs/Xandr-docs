---
title: Update a Domain List or App List
description: This page provides an overview to update a Domain List or App List. Learn to edit name and description, add or delete domain/apps for Domain List and App List.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Update a domain list or App list

> [!NOTE]
> Targeting lists are only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

You can add, remove, or overwrite a domain list or app list. You can also change the name and/or description of the list.

> [!WARNING]
> Before you proceed, note that changing a domain or app list immediately impacts any campaigns already targeting the list. This could result in incorrect targeting. It's a good idea to make sure you're aware of all the campaigns that could be affected before making changes to your targeting lists. If you change only the name or description of a list, any campaigns using it will be unaffected.

## Domain lists

> [!NOTE]
> Domain targeting applies only to **Web** and **Mobile Web** impressions and does not apply to **Mobile App** impressions. If you have allowed your campaign to serve on mobile apps while targeting a domain list, the campaign will be unrestricted when buying mobile app inventory unless you have also applied App List targeting. To avoid serving on mobile app inventory, switch the **Apps Placements** toggle in your campaign's targeting profile to OFF. Domains which begin with `"www"` will have the `"www"` substring stripped out before being stored in our system. For example,`"www.example.org"` will be shortened to `"example.org"`.

### Edit the name or description

1. Select **Network** \> **Inventory** \> **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** tab.
1. Check the checkbox next to the domain list under **Domain List Name** and click **Edit**.
1. Make edits to the **Name** and/or **Description** and click **Save**.

### Add or remove domains from a domain list

1. Select **Network** \> I**nventory** \> **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** tab.
1. Click the domain list under **Domain List Name**. A panel displays with a list of domains in the domain list.
1. To remove domains, check the checkbox of one or more domain names and select **Actions** \> **Delete**.
1. To add domains, click **+New**
    - Select **Enter text** and copy and paste domains into the box. OR
    - Select **Upload a file**, click **Select File**, select the file to upload, and click **Open**.
1. Click **Add**. For more information on formatting requirements for adding domains by copy and paste or file upload, see [Create a Domain List or App List](create-a-domain-list-or-app-list.md).

### Add a large number of domains to one or more domain lists

1. Select **Network** \> **Inventory** \> **Targeting Lists** from the top navigation menu.
1. Select **Domain Lists** tab.
1. Check the checkbox next to one or more domain lists under **Domain List Name**.
1. Select **Actions** \> **Add domains**.
1. To add domains:
    - Select **Enter text** and copy and paste domains into the box. OR
    - Select **Upload a file**, click **Select File**, select the file to upload, and click **Open**.
1. Click **Add**. For more information on formatting requirements for adding domains by copy and paste or file upload, see [Create a Domain List or App List](create-a-domain-list-or-app-list.md).

## App lists

### Edit the name or description

1. Select **Network** \> **Inventory** \> **Targeting Lists** from the top navigation menu.
1. Select **App Lists** tab.
1. Check the checkbox next to the app list under **App List Name** and click **Edit**.
1. Make edits to the **Name** and/or **Description** and click **Save**.

### Add or remove apps from an app list

1. Select **Network** \> **Inventory** \> **Targeting Lists** from the top navigation menu.
1. Select **App Lists** tab.
1. Click the **app list** under **App List Name**. A panel displays with a list of apps in the app list.
1. To remove apps, check the checkbox of one or more app names and select **Actions** \> **Delete**.
1. To add apps, click **+New**
    - Select **Enter text** and copy and paste apps into the box. OR
    - Select **Upload a file**, click **Select File**, select the file to upload, and click **Open**.
1. Click **Add**. For more information on formatting requirements for adding apps by copy and paste or file upload, see [Create a Domain List or App List](create-a-domain-list-or-app-list.md).

### Add a large number of apps to one or more app lists

1. Select **Network** \> **Inventory** \> **Targeting Lists** from the top navigation menu.
1. Select **App Lists** tab.
1. Check the checkbox next to one or more app lists under **App List Name**.
1. Select **Actions** \> **Add apps**.
1. To add apps:
    - Select **Enter text** and copy and paste apps into the box. OR
    - Select **Upload a file**, click **Select File**, select the file to upload, and click **Open**.
1. Click **Add**. For more information on formatting requirements for adding apps by copy and paste or file upload, see [Create a Domain List or App List](create-a-domain-list-or-app-list.md).

## Related topics

- [Working with Targeting Lists](working-with-targeting-lists.md)
- [Create a Domain List or App List](create-a-domain-list-or-app-list.md)
- [Explore Domain Lists or App Lists](explore-domain-lists-or-app-lists.md)