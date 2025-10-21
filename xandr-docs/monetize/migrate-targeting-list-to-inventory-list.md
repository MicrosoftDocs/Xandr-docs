---
title: Migrate Targeting List to Inventory List
description: This page is a step-by-step guide to migrate your existing targeting lists to an inventory lists. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Migrate targeting list to inventory list

Legacy line items used targeting lists to include or exclude domains and apps from campaign targeting. With augmented line items, targeting lists have been replaced by inventory lists. If you've been using legacy line items and are switching to using augmented line items, you can migrate your existing targeting lists to inventory lists.

## Copy an existing targeting list to an inventory list

1. Go to **Network** \> **Inventory** \> **Inventory Lists**.
1. Select **Copy existing Targeting Lists** from the **+ New** menu.
1. The **Create List from Targeting Lists** window is displayed.
1. Enter a name for the inventory list you are creating. You may also optionally add a description.
1. Specify whether the inventory list is to be an **Allowlist** (for restriction) or a **Blocklist** (to exclude). If you are creating a list from within the **Inventory and Brand Safety** section of a line item, this option will automatically be set. Remember, targeting lists can be used as allowlists or blocklists (and can only contain apps OR domains). However, each inventory list must be either an allowlist or a blocklist and can contain both apps and domains.
1. Click **Next**. A list of existing targeting lists will be displayed.
1. Select the targeting lists you would like to copy into the inventory list you are creating.
1. Click **Next**. The list of all domains and/or apps in the targeting lists you selected will be displayed.
1. Click **Validate Domains & Apps**. Depending on the size of the list, this may take a moment. The list will be checked to ensure that:
    - none of the domains or apps that you entered violate Microsoft Advertising policies.

    - unsupported URLS are flagged. Unsupported means that the Microsoft Advertising targeting system has not yet audited these URLs and, as a result, you will not be able to serve on them.

    - invalid URL formats (i.e., non-http or non-https) are removed from the list.

      For a description of what each status means, see the **Key to domain/app audit flags** section above.
1. You can also optionally add additional domains and/or apps individually or import from an external file by clicking **Import from file**.
1. Click **Next**. The domains and apps you entered or imported will be listed (if the list is large, use the arrows to advance through the pages).
    - Unsupported domains or apps will be flagged.
    - You can also remove any domains or apps that violate Microsoft Advertising policies by clicking **Remove from list**. However, you will never serve on them even if you leave them in the list.
    - You can choose whether to additionally include subdomains in the list. For example, if you selected this option for "mydomain.com", you would also serve on its subdomains such as "mydomain.com/foo" and "foo.mydomain.com". By default, subdomains are included.
1. Click **Create List**. The inventory list will be created.

## Switch to targeting lists

If you want to access your existing targeting lists, they will continue to exist during the transition period and be available for use with line items when targeting or excluding domains and apps.

> [!NOTE]
> Remember, each targeting list can be used to restrict \*or\* exclude the domains and apps in it (and can only contain apps \*or\* domains). They can be used as allowlists or blocklists. In contrast, each inventory list must be either an allowlist or a blocklist and can contain both apps and domains.
>
> 1. Click **Switch to Targeting Lists (Legacy)**.
> 1. The **Targeting List** screen will be displayed.

## Related topics

- [Inventory Lists (ALI)](inventory-lists-ali-only.md)
- [Inventory Targeting (ALI)](inventory-targeting-ali.md)