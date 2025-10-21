---
title: Defer to Line Item
description: In this page, learn how Defer to Line Item works, and how you can turn it on.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Defer to line item

If you have a Line Item with a **CPA booked Revenue** it may take some time to collect enough data to optimize to conversions. You may wish to first optimize to a clicks or another event that is on the path to a conversion, because the first action is more common than an actual conversion. This makes sense if you believe that there is a strong correlation between the rate at which users click on a creative and the rate at which they convert.

## How it works

You will select a CPA booked revenue and a CPC campaign bidding strategy, and check **Defer to Line Item**. Once you have 10 conversions for a campaign-creative size-inventory source bucket, that bucket will switch to a CPA bidding strategy based on Booked Revenue. And once that bucket is optimized it will bid based on a Line Item Margin.

## How to turn it on

When you create or edit a campaign and, in the **Buying Strategies** section, optimize the campaign to a predicted CPA or CPC goal, under **Other Options** you will see **Optimization Levers**.

If you click the **Edit** button, you can then check the **Defer to Line Item** box at the top of the dialog that opens. **Defer to Line Item** allows you to first optimize to your campaign bidding strategy, and then - when you have enough data - to your Line Item Booked Revenue.

## Related topic

[Optimization Levers](optimization-levers.md)