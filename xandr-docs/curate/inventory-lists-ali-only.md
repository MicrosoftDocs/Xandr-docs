---
title: Microsoft Curate - Inventory Lists
description: This page gives an overview on Inventory lists which are used to group the domains, apps, and app bundle IDs that you want to target or exclude on your insertion orders and line items.  
ms.date: 11/14/2023

---


# Microsoft Curate - Inventory lists

## Introduction

Inventory lists are a way to group the domains, apps, and app bundle IDs that you want to target or exclude on your insertion orders and line items. Each inventory list must be either an allowlist (for restricting targeting) or blocklist (for excluding) and can contain any combination of domains, apps, or app bundle IDs. Examples of items that may be included in your inventory lists are:

- app bundle IDs:
  - 617263396
  - com.magmamobile.game.Elements
- raw URL (domain):
  [yahoo.com](https://sg.yahoo.com/?p=us&guccounter=1&guce_referrer=aHR0cHM6Ly9kb2NzLnhhbmRyLmNvbS9idW5kbGUvY3VyYXRlX2N1cmF0ZS1zdGFuZGFyZC9wYWdlL3RvcGljcy9pbnZlbnRvcnktbGlzdHMtYWxpLW9ubHkuaHRtbA&guce_referrer_sig=AQAAAMSoXxyw3IEmTV0V-VHeMJVlfGxL_SiW9qW1TXmUnxbXG-dIQlBveckoB3VFQsJYErKnqj0y0ZyGh86t-ZlmJyLBvHAOLi2-irA1ujjG0yk1Ozc_psHpUpLrV1FU4TZqTeWGamHONbF1Z-EuWrgQt9rALpQPk9kGkC61tvEhJk0K)
- raw URL (app): [Funny Laughs LOL!](https://apps.apple.com/us/app/funny-laughs-lol-pics-jokes/id617263396)

Inventory Lists can be applied via the **Allowlist** or **Blocklist** fields within the **Inventory & Brand Safety** section for line items and **Supply Strategy** section for insertion orders.

## Domains

- You can target domains (`test4.com`) and subdomains (`review.test4.com`), but you can't target specific directories within domains (`test4.com/review`) by default. For example, targeting `test4.com/review` is not supported as a standard practice in the system. However, such directories can be targetted on a case by case basis as exceptions.
- The process of targeting of domains (`test4.com`) and subdomains (`review.test4.com`) depends on whether the subdomains are mapped or not. A subdomain is mapped if it has an ID associated with it. In that case, the subdomain can be allowed or blocked within a list independent of the top-level domain.
- Alternatively, if a subdomain is unmapped or defined as unsupported, the top-level domain must be included in a list and a checkbox **Include subdomains** needs to be selected to target the subdomains under it. This option of **Include subdomains** checkbox is given under each top-level domain for this purpose.
  
  > [!IMPORTANT]
  > The **Include subdomains** checkbox will only appear if a domain is broken out for subdomain audit in the system. If a domain is not broken out, the checkbox will not appear and all subdomains under the targetted top-level domain will be included for targeting automatically.

- Domains that begin with `www` will have the `www` substring stripped out before being stored in our system. For example, `www.example.org` will be shortened to `example.org`.

## Apps

### App Bundle ID (App ID)

An app bundle ID (or app ID) is just a unique identifier for a specific app. App IDs are defined differently depending on whether the app runs on iOS or Android:

- Every iOS app has a unique iTunes ID
- Every Android app has a unique Android Package Name

### Find App IDs

To find the IDs for an Android or IOS app, find the app's detail page - the easiest way is to do a web search. The URL of the app store's detail page will show the app's ID.

For example, here are the detail pages for the "Candy Crush" app:

- Google Play: [Candy Crush Saga](https://play.google.com/store/apps/details?id=com.king.candycrushsaga)
  - ID: com.king.candycrushsaga
- iTunes: [App Store: Candy Crush Saga](https://apps.apple.com/us/app/candy-crush-saga/id553834731)
  - ID: 553834731

### Select target apps

To identify specific mobile apps to target, we recommend targeting the region you're interested in, activating your campaign, and after a few days running the [Site Domain Performance](../invest/site-domain-performance.md) report, which will show you the apps that you've been reaching. You can then update your targeting to include or exclude specific apps to meet your needs.

## Key to Domain or App audit flags

Each domain or app in a list can have one of the following audit statuses:

- :::image type="content" source="media/audit-check.png" alt-text="Screenshot of audit check."::: - the domain/app has been audited and approved.
- **Rejected** : The reason the domain/app has been rejected after being audited (e.g., Hate Speech).
- "**--**" - the domain/app is either unauditable (has been reviewed but can't be audited) or is pending audit (has not been reviewed yet, but is in the audit queue).
- **Masked** - the seller is not exposing the domain/app's actual URL for targeting or reporting. However, the real domain/app URL is still audited by Microsoft Advertising inventory quality controls within the bid request.
- **Unsupported** - the domain/app is not yet in the Microsoft Advertising audit queue. You should submit a Salesforce ticket to have it reviewed.

> [!NOTE]
> For audit status "`--`" or "*Unsupported*", creatives will be delivered through managed inventory or deals. They will not be delivered in open exchange unless you have allowed unauditable creatives for the line item.
>
> The domains with audit status of either  :::image type="content"  source="media/audit-check.png" alt-text="Screenshot of audit check."::: or "**--**" are available for use in the augmented line item inventory lists.

## Create a new inventory list

1. Go to the **Inventory Lists** screen. Select **Inventory \> Inventory Lists**.
1. Select **New**. The **Create List** window displays.
1. Enter a name for the inventory list.
1. Select **Add list description** to add a description if necessary.
1. Select the **List Type**:
    - **Allowlist** (for restriction)
    - **Blocklist** (for exclusion)
1. Specify whether this inventory list will be **Available to**:
    - **Any Advertiser** - the inventory list will be available for selection on the insertion orders and line items of any advertiser. If you select the **Require for all Line Items** checkbox, the inventory list will be applied to **all** existing and new line items under all of your advertisers and can't be removed from each individual line item. However, you can clear the checkbox if you want to undo this for all existing and new line items.

      > [!NOTE]
      > The inventory lists that are set to **Required for all** will only be applied to third-party inventory.

    - **Specific Advertiser** - the inventory list will only be available for selection on the insertion orders and line items of a specific advertiser (select a specific advertiser in the **Select one** drop-down).
1. Select **Next**.
1. Select either:
    - **Copy and paste domains & apps** to enter or paste a list of domains and/or apps to be included in this inventory list.
    - **Import from file** to import a list of domains and/or apps to be included in this inventory list.

      > [!NOTE]
      > The maximum number of domains and/or apps per inventory list is limited to 100,000.

1. Select **Validate Domains & Apps**. The list will be checked to ensure that:
    - None of the domains or apps you entered violate Microsoft Advertising policies.
    - Unsupported URLs are flagged. Unsupported means the Microsoft Advertising targeting system hasn't audited these URLs yet so that you won't be able to serve on them.
    - Invalid URL formats (i.e., non-http or non-https) are removed from the list.
1. Select **Next**. The domains and apps you entered will be listed along with **Flags** for each ( see [Key to Domain or App audit flags](#key-to-domain-or-app-audit-flags) for more information). If the list is large, use the arrows to advance through the pages. Note the following:
    a. Unsupported domains or apps will be flagged.
    b. You can also remove any domains or apps that violate Microsoft Advertising policies by selecting **Remove**. However, you will never serve on them even if you leave them in the list.
    c. Select **Include subdomains** to include subdomains. For example, if you selected this option for "mydomain.com", you would also serve on its subdomains such as "mydomain.com/foo" and "foo.mydomain.com".
1. Select **Create List**. The inventory list is created and displays in **Inventory Lists**.

1. ## Export an inventory List

1. Go to the **Inventory Lists** screen. Select **Inventory \> Inventory Lists**.
1. Locate the list(s) you want to export.
1. Select the checkbox next to the list that you want to export. (You can select up to five lists.)
1. Select **Export List** from the **Actions** menu.

The list(s) you selected will be downloaded to your local drive. If you exported:

- A single list, the file will have a `.csv` extension.
- More than one list, a file with today's date and `.zip` extension will be downloaded. That `.zip` file will contain a `.csv` file for each list that you exported.

## Duplicate an inventory list

1. Go to the **Inventory Lists** screen. Select **Inventory \> Inventory Lists**.
1. Locate the list(s) you want to duplicate.
1. Select the checkbox next to the list that you want to duplicate.
1. Select **Duplicate List(s)** from the **Actions** menu.
1. On the **Duplicate List(s)** screen, enter a **Duplicate Name** and a **Description** (optional) for the list(s).
1. Select **Duplicate**. The duplicate of any list(s) you selected displays in **Inventory Lists**.

## Search for inventory lists

1. Enter the name of the list that you wish to find in the search field. If you only know part of the name, enter some characters that you know are in its name. You can filter the results with the **Allowlists & Blocklists** and **Domains & Apps**  drop-downs. The inventory lists that match the criteria you entered display. Lists that are set to **Require for all Line Items** will have a small lock icon next to their name.

1. Locate the desired inventory list.

1. Select its row to see more details.

## Delete an inventory list

> [!WARNING]
> Deletions are permanent. Deleted inventory lists cannot be retrieved.

1. Go to the **Inventory Lists** screen. Select **Inventory \> Inventory Lists**.
1. Locate the inventory list that you want to delete and select the corresponding checkbox. (You can select more than one.)
1. You can now do any of the following:
    - **Add**: Add domains/apps to the list.
      1. Select **Add**.
      1. Enter the domains/apps that you wish to add (or import them from an existing file). See steps 8-10 in the [Create a New Inventory List](#create-a-new-inventory-list) section for more information.
      1. Select **Save**.
    - **Replace**: Replace the current domains/apps in the inventory list with a new list of domains/apps.
      1. Select **Replace**.
      1. Enter the domains/apps that you wish to add (or import them from an existing file). See steps 8-10 in the [Create a New Inventory List](#create-a-new-inventory-list) section for more information.
      1. Select **Save**.
    - **Remove**: Remove domains/apps from the list.
       > [!WARNING]
       > This action cannot be undone.
      1. Select the checkbox of each domain or app that you want to remove.
      1. Select **Remove**.
      1. Select **Delete**.
    - **Search**: Search for domains/apps in the list.
      1. Use the search field to locate specific domains or apps in the list.

## Edit an existing inventory list

1. Go to the **Inventory Lists** screen. Select **Inventory** \> **Inventory Lists**.
1. Select the row of the inventory list that you want to edit. The domains and/or apps in the list are displayed in the lower portion of the screen. The actions that you can perform on an inventory list with respect to domains/apps include:
    - **Add**: Add domains and/or apps to the list.
      1. Select **Add**.
      1. Enter the domains/apps that you wish to add (or import them from an existing file). See steps 7-9 in the [Create a New Inventory List](#create-a-new-inventory-list) section.
    - **Remove**: Remove domains or apps from the list.
       > [!WARNING]
       > This action cannot be undone.

      1. Select the checkbox of each domain or app that you want to remove.
      1. Select **Remove**.
      1. Select **Delete Domains & Apps**.
    - **Search**: Search for domains or apps in the list.
      - Use the search field to locate specific domains or apps in the list.
1. To edit the details of the inventory list, select the pencil icon next to the inventory list name and ID.
1. Do any of the following:
    - Update the name and description.
    - Change whether this inventory list will be available for selection on the line items of **Any Advertiser** or only on those of a **Specific Advertiser**.

      If you select **Specific Advertiser**, you must select an advertiser in the drop-down.

    - Select or clear the **Require for all Line Items** checkbox.

      If you select the **Require for all Line Items** checkbox, the inventory list will be applied to all existing and new line items under all of your advertisers and can't be removed from the individual line items (you can clear the checkbox if you want to undo this for all existing and new line items).

## Related topics

- [Buy-Side Targeting](buy-side-targeting.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Object Hierarchy](object-hierarchy.md)
