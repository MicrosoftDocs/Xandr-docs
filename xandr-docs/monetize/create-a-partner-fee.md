---
title: Microsoft Monetize - Create a Partner Fee
description: In this article, find information on how to create and set up a partner fee.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Create a partner fee

You must have [Network-level access](getting-started-with-roles.md) to perform this task.

1. Go to the **Fees** screen (**Advertisers** > **Fees**).
1. Click **+ New**.
1. Fill out the fee overview and click **Next**.
    1. Enter a fee name that will make sense to other people.
    1. Select a fee vendor. If your vendor isn't listed, select one of the custom vendors to represent them.
    1. Select a fee type. For more information, see [Fee Type](fee-type.md).
    1. Optionally enter a longer fee description.
1. Define the fee calculation and click **Next**. For more information, see [Fee Calculations](fee-calculations.md).
    1. Select **%** (percentage) or **CPM**. If you select **CPM**, select a currency.

        > [!NOTE]
        > Line item currency is inherited from the advertiser. If a fee is created in a currency other than the line item currency, then we will automatically convert the fee to the line item currency at the time of transaction.

    1. Select a calculation method.

1. Make the fee eligible for advertisers.
    1. Select the advertisers for which the fee should be eligible.
    1. Determine whether the fee should be required for all line items.
    1. Determine the supply type(s) to which the fee applies (**Open Exchange Buys**, **Managed Buys**, or **Deals**).

> [!IMPORTANT]
> If a fee is required for all line items, it will be required for all newly created line items and any line items that are opened and edited. Users will not be able to remove the fee from the line item. If you decide you do not want the fee to apply to a line item after all, you must first change the partner fee to be optional, and then remove the fee from the line item.
