---
title: Domain Targeting
description: Learn what is Domain Targeting, where it is available and how it can be applied. This page lists steps to target domains, domain lists, or a combination of both. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Domain targeting

> [!NOTE]
> This form of targeting is only available for Standard Line Items and the campaigns associated with them. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

Domain list targeting is available at the line item or campaign level, and for campaigns, specific domain targeting is also available. By default, your line item or campaign will target impressions from all domains. However, you can narrow targeting to include or exclude pre-defined domain lists or specific domains.

Domain targeting applies only to web and mobile web impressions, and these settings will not be considered for mobile app impressions. If you don't want to serve on mobile app impressions, turn off the **Apps Placements** toggle under **Device and Supply Targeting**.

Domain list targeting is also limited by any existing domain list settings in your third-party buying filters at the network level. If domain lists are included in your third-party buying filters, only those included domain lists will be available for targeting in your campaign. If domain lists are excluded in your third-party buying filters, those excluded domain lists will be unavailable for targeting in your campaign. To learn more, see [Working with Third-Party Buying Filters](working-with-third-party-buying-filters.md).

To target domains, domain lists, or a combination of both:

1. In the **Targeting** section, click **Edit** next to **Inventory**.

1. If you want to target a list of existing domains, click the **Domains Lists** tab and include or exclude the relevant lists.

    > [!NOTE]
    > It is not possible to include some domain lists and exclude others; all targeted domain lists must be either included or excluded. For instructions on adding domain lists, see [Working with Targeting Lists](working-with-targeting-lists.md).

1. For campaigns only: if you want to target a specific collection of domains rather than (or as well as) existing domain lists, click the **Specific Domains** tab, where you can target up to 25 specific domains.

    > [!NOTE]
    >  There is an OR relationship, not an AND relationship, between included domain lists and included individual domains. 

    1. Enter the domains in a comma-, space-, or line-separated list.
    1. Click **Add Domains**.
    1. Choose whether to include or Exclude the domains.

    > [!NOTE]
    > It is not possible to include some domains and exclude others. All targeted domains must be either included or excluded.

## Related topic

- [Create a Campaign](create-a-campaign.md)
- [Working with Targeting Lists](working-with-targeting-lists.md)