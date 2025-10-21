---
title: Manage Network Priorities
description: This page gives a step-by-step guide to make changes to your network priorities settings. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Manage network priorities

The **Network Priorities** screen (**Network** \>  **Tools** \> **Network Priorities**) allows you to set priorities that guide line item and campaign setup. Specifically, you can change your network priorities settings to enable minimum margin settings in line item revenue trafficking and campaign buying strategies.

> [!IMPORTANT]
> This network-wide setting should be enabled when you have made a business decision to prioritize margin (the profit margin on booked revenue) on managed campaigns for all line items on the network over delivery (the frequency and number of campaigns served) on managed publishers.
>
> To learn about how to set up minimum margin on the line item, see [Create a Standard Line Item](create-a-standard-line-item.md).

## To make changes to your network priorities settings

1. In the **Network** tab, in the **Tools** menu, select **Network Priorities**. This takes you to the **Network Priorities** screen.
1. On the **Network Priorities** screen, in the **For campaigns targeting direct inventory** dropdown, the default setting is **Always bid**. As the name suggests, this choice prioritizes delivery on managed publishers over margin on your managed campaigns. If you want to prioritize making margin on your managed campaigns, select **Only bid if margin is met**.
1. Once you have made your selection, click **Save** to save your changes.

## Next steps

Now you can set minimum margin during [creation of a standard line item](create-a-standard-line-item.md), under **Tracking Revenue Type**. This effectively sets a bid cap on your campaigns. For your campaigns targeting direct inventory, you can also choose to do a minimum margin check as part of the [campaign creation](create-a-campaign.md) process to ensure they do not serve on publishers that are not profitable for your line items.

## Related topics

- [Create a Standard Line Item](create-a-standard-line-item.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Create a Campaign](create-a-campaign.md)
  (Standard Line Items only)
- [Using Minimum Margin to Balance Margin and Delivery](using-minimum-margin-to-balance-margin-and-delivery.md)