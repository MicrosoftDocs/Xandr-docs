---
title: Microsoft Invest - Buy Seedtag Inventory
description: In this article, you'll learn how to display your creative via Seedtag inventory. Seedtag inventory is available programmatically.
ms.date: 10/28/2023
---

# Microsoft Invest - Buy Seedtag inventory

> [!NOTE]
> [Buying Native Inventory](./buying-native-inventory.md) provides instructions for a global approach in which you reach all sellers simultaneously with a single line item. Scaling is the approach we recommend over the seller-specific settings shown here.

[Seedtag](https://www.seedtag.com) inventory is available programmatically through Microsoft Advertising. Seedtag is the European leader in In-Image advertising and manages more than 1B impressions across the globe. We work with top Publishers and our responsive ad format will allow you to boost your metrics. Seedtag's average Viewability rate is above 90% and our CTR are 5 time higher than traditional display.

Seedtag has office and exclusive agreements with Publishers in the below countries:

- Spain
- France
- Italy
- Mexico

This page will guide you through the process required to display your creative via Seedtag inventory. There are several steps you need to take to get started.

## Set up seedtag as an eligible partner

Before you can sell through Seedtag you need to set them up as an eligible partner. For instructions on setting up a relationship with Seedtag, see [Managing Relationships with Sellers](./managing-relationships-with-sellers.md).

## Send your creative to seedtag

Seedtag's in-image format is a non-IAB Standard ad format which requires them to adapt your creative and provide you with the ad tag to be
implemented. You must send your creative (preferably as a PSD file) to [programmatic@seedtag.com](mailto:programmatic@seedtag.com) to receive a tag that you will apply when adding your creative in Microsoft Invest.

## Request the creation of a deal ID to seedtag

Contact Seedtag at [programmatic@seedtag.com](mailto:programmatic@seedtag.com) to request a deal ID. Specify your buyer ID and the type of audience you're looking for.

## Set up your line item

Your line item must be set up according to the guidelines here.

**Buying strategy:**  
You must select CPM as your **Buying Strategy**. You can select any option under **Pay on a Per-impression (CPM) basis**, but you cannot use any other basis (such as CPC or CPA).

**Inventory quality:**

- Select **Serve only on** Microsoft Advertising-reviewed inventory.
- Select **Also serve on trusted seller-reviewed/unreviewed inventory**.

## Upload a third-party creative

Navigate to the **Creative Manager** screen. Select the **Create New** button and select your creative type from the menu. In the **New Creative** dialog box select the following values:

- Type: **Third-party creative**
- Creative Format: **Third-party tag**
- Tag Type: **This tag is HTML**. Uncheck the **Serve in iFrame** option.
- Media Type: **Banner: Standard Banner**
- Template: **Microsoft Advertising: Standard**
- Size: Select **New** from the dropdown list. Enter a **width** of **600** and a **height** of **105**
- Name: Self-classify the creative with the accurate brand.
  <br>In the Tag field, paste in the tag you received from Seedtag when you sent your creative. You will need to edit the tag. Your tag will contain a section like this:

  ```
  /** PUT THE FINAL URL BETWEEN QUOTES **/ var targetUrl = "https://LandingPageUrl.com"; /** /PUT THE FINAL URL BETWEEN QUOTES **/ 
  ```

  Replace the `targetURL` value with your URL:

  ```
  /** PUT THE FINAL URL BETWEEN QUOTES **/ var targetUrl = "https://YourCampignUrl.com"; /** /PUT THE FINAL URL BETWEEN QUOTES **/ 
  ```

  If you want to use an external click command, put that command in place of your URL.

## Examples

:::image type="content" source="./media/seedtag-a.png" alt-text="Screenshot of creative displayed on laptop screen via seedtag inventory.":::
:::image type="content" source="./media/seedtag-b.png" alt-text="Screenshot of creative displayed on iPad screen via seedtag inventory.":::
:::image type="content" source="./media/seedtag-c.png" alt-text="Screenshot of creative displayed on mobile screen via seedtag inventory.":::
