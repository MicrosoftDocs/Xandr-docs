---
title: Microsoft Invest - Buy Native Inventory
description: This article provides steps for buying native inventory. Native ads allow publishers to control user's experience by integrating advertising within their inventory.
ms.date: 10/28/2023
---

# Microsoft Invest - Buy native inventory

Native ads seamlessly integrate advertising into a placement's context. In contrast with traditional HTML/JavaScript ads, native ads specify the ad content but not how to display it. This lets publishers control their user's experience by integrating advertising within their inventory, and it affords advertisers higher quality inventory to choose from. This guide contains steps for buying native inventory.

From the Microsoft Advertising platform you have access to a number of native supply sources. While you can set up an individual line item for each source, we recommend that you set up a single line item to reach all of them
simultaneously. This type of setup allows for easier budgeting, reporting, performance-tracking, frequency capping, etc. This page describes the process of setting up a line item to serve across whichever native sellers you choose.

For specific information on individual sellers, see [Native Inventory Seller Specifications](./native-inventory-seller-specifications.md)

> [!IMPORTANT]
> **Third-party pixel support**
>
> For HTML based banner creatives, tracking pixels are always fired. With native, creative assets are typically rendered outside of an iframe, therefore publishers are selective about the javascript they allow to run on their pages. Some publishers may not fire all javascript pixels attached to a creative. However, IAS javascript based pixels are now supported by Outbrain, Sharethrough, Triplelift, and AdYouLike. Note that AdYouLike only supports javascript pixels on deal ID buying.

## Step 1. Ensure you are in native sellers' allowlists

Some native sellers require you to go through a quick buyer audit before they grant access to their inventory. Here is a list of sellers and their allowlist requirements:

| Native Seller | Are you in an allowlist? | How to be put in an allowlist |
|:-|:-|:-|
| Ligatus | You must be in an allowlist to buy Ligatus inventory. You can determine whether you're eligible to serve on Ligatus by checking your settings in Partner Center. See the [Partner Center Guide](./partner-center-guide.md) documentation for more information. | Reach out to [rta@ligatus.com](mailto:rta@ligatus.com) for allowlist approval. |
| Sanoma Finland | If you have not previously bought Sanoma Finland via Microsoft Advertising, you are not yet in an allowlist. | Reach out to [programmatic@sanoma.com](mailto:appnexus@triplelift.com). |
| TripleLift | If you have not previously bought TripleLift via Microsoft Advertising, you are not yet in an allowlist. | Reach out to [appnexus@triplelift.com](mailto:appnexus@triplelift.com). |

The following sellers do not currently have any allowlist requirements:

- L'Agora
- Leboncoin
- Mopub
- MSN
- Outbrain
- Schibsted Norway
- Sharethrough
- Yieldmo

## Step 2. Upload native creatives

Navigate to the **Creative Manager** screen, click **Create New** > **Single creative**. This will bring up the **Create New Creative** dialog.

To maximize reach for your creatives across native inventory sources, here are some general guidelines we recommend:

| Field | Microsoft Advertising Guidelines |
|:---|:---|
| Title | 25 character maximum |
| Body | 300 character maximum |
| Logo | 1:1 aspect ratio |
| Image | 1.91:1 aspect ratio<br>1200x627<br>200 KB max |
| Sponsored By | 25 character maximum (brand of advertisement) |

If a parameter is not mentioned in the table above, enter whatever values make sense for your campaign.

For detailed information on additional fields and uploading a native creative see [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](./add-creatives-in-bulk.md). You can also review our [Native Buy-Side Best Practices](https://download.microsoft.com/download/e/e/5/ee544211-092a-45c4-8076-57b5c5aaceb3/28%20Dec%202023/Buy-Side-Native-Best-Practices.pdf).

> [!WARNING]
> Do not use JavaScript piggyback pixels on native creatives. Only image pixels can be used on native creatives.

## Step 3. Targeting

In terms of targeting, Microsoft Advertising recommends you do not target individual sellers as part of your setup. Instead, we recommend serving on Microsoft Advertising-audited inventory and using [inventory lists](./inventory-targeting-ali.md) to focus delivery on relevant supply.
