---
title: Netflix Deal Defined Buying Line Items
description: This article explains about the Netflix PMP deals which are seller-defined. The seller defines the targeting parameters the buyer is allowed to configure.
ms.date: 10/28/2023
---

# Netflix deal defined buying line items

> [!NOTE]
> This feature is currently in Alpha. It is still under development and is subject to change without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

## Overview

Due to the premium nature of Netflix inventory, Netflix PMP deals are considered "Seller Defined Deals," meaning the seller defines the targeting parameters the buyer is allowed to configure. The Deal Defined Line Item workflow in Microsoft Invest only displays the settings the buyer can control, eliminating the potential for conflict between a buyer and seller and thus maximizing win rates. When the Seller Defined Deal allows for buyside targeting, a check is performed to ensure the line item meets the required minimum audience size.

## Before you begin

Before you create a **Deal Defined** line item, you must perform the following tasks:

- [Create an Advertiser](./create-an-advertiser.md)
- [Create an Insertion Order](./create-an-insertion-order.md)

The insertion order you created must have at least one billing period with dates in the future.

You must also have access to one or more Netflix PMP deals to target. Sellers must first create these deals for buyers to access them for targeting. If you have questions about how to gain access to a PMP deal, contact your account manager.

> [!WARNING]
> Advertisers in the following verticals are required to submit their licenses and/or proof of creative approval in select markets to serve their ads on Netflix:
>
> - Alcohol
> - Financial Services
> - Insurance
> - High fat/sugar/salt foods
> - Online sports betting
> - State-run lotteries
> - Healthcare
> - Pharmaceuticals
> - Dating
>
> More information on these requirements, along with web forms for submitting licenses and creative approval, can be found on the Netflix [Restricted Policy Page](https://help.nflxext.com/legal/netflix_ad_restrictions.pdf).

## Access Netflix PMP deals

To access a Netflix PMP deal, do the following:

1. Select **My Deals** in the **Inventory** menu.
1. In the **My Deals** screen, ensure that the **Deal Type** is set to **PMP**.
1. Choose the appropriate deal from the **My Deals** screen.
1. Select the desired **Advertiser** and **Insertion Order**.
1. Select **Go To Line Item Create** to launch the page to create the **Deal Defined Line Item**.

## Start a new deal defined line item

To create a new Deal Defined line item without going through the **My Deals** interface, do the following:

1. Select **Create New** in the **Line Item** menu.
1. On the **Create New Line Item** screen, select **Augmented Line Item** > **Deal Defined** under **Line Item Type**.

   > [!IMPORTANT]
   > You must have an **Advertiser** and **Insertion Order** associated with the Line item in the Advertiser and Insertion Order sections. If necessary, select an Advertiser and Insertion Order.

1. Select **Next** to open the **Create a Deal Defined Line Item** screen.

## Buy Netflix via PMP on Microsoft Invest

The primary difference between a **Deal Defined Line Item** and a standard **Augmented Line Item** is the deal relationship. Only one deal is allowed on a Deal Defined line item, and the settings of that deal determine which targeting settings are displayed for you to configure. Because there is only one deal targeted, the buyer must ensure to take the suggested minimum bid of the deal (ask price + BASC) into account when formulating their bidding strategy. When using maximum revenue bids, the maximum must be higher than this suggestion to win.

When the Netflix PMP deal allows buyside targeting, an audience size check is performed after the line item is saved to ensure it meets the minimum audience size required by Netflix. After creating or editing a Deal Defined Line Item, check the **Line Item Details** page to confirm the size check status. If the audience is too small, the line item will not deliver until settings are updated to broaden the audience or extend flight dates.

### Overview of deal defined line item setup

| Feature | Deal Defined Setup Overview |
|:---|:---|
| Basic Settings | Set the LI name, state, and deal. After selecting a deal, you'll see the details of the deal:<ul><li>**Seller**: ID of the seller of the deal.</li><li>**Start Date**: Date the deal becomes active.</li><li>**End Date**: The date after which the deal is no longer active.</li><li>**Suggested Minimum Bid**: Calculated as the seller's ask price plus your buyer fees, the suggested minimum bid can be used to inform your bidding strategy. <br>**Note**: This suggestion should be used as a starting point, and you might need to increase your bid depending on your revenue type, goals, and deal competition.</li><li>**Price**: The minimum amount the seller will accept for the deal.</li></ul> |
| Budgeting & Scheduling | This section is identical to that of a standard ALI, except that Daypart Targeting might not be available based on deal settings. |
| Optimization | In this section, you can enable/disable optimization, set a performance goal and goal priority, and associate conversion pixels. <br> **Note**: Given that Netflix inventory consists entirely of video content, it is essential to ensure that your goals are tailored to video buys. |
| Inventory & Brand Safety | This section isn't available for **Deal Defined Line Items**. The deal targeting is defined in the **Basic Settings** section. |
| Audience & Location Targeting | Geotargeting is required. Each Netflix PMP deal is set to target a single country, and you must ensure that the Deal Defined Line Item country target matches the deal. More granular geotargeting might be available, depending on the deal settings.<br> **Note**: Frequency, Recency, and Cookieless targeting are hardcoded based on seller requirements. |
| Viewability & Environment Targeting | Device type, video player position, and video content targeting might be available depending on the settings of the deal. |
| Creatives | This section allows you to associate creatives with the line item and specify creative rotation and scheduling. For more information on Netflix-specific creative requirements, see [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md). |
| Measurement | In this section, third-party verification via IAS and DoubleVerify is currently supported for Netflix PMP deals and can be enabled here. These integrations aren't compatible with Microsoft In-Market Audience targeting on Netflix PMP deals. |
| Programmable Splits | Splits and custom models aren't available for **Deal Defined Line Items**. |
| Reporting Labels & Comments | In this section, you can optionally assign custom reporting labels to a line item. This enables you to create reports tracking metrics across multiple line items and add comments to a line item for reference. |
<!-- | Fees | In this section, you can optionally apply a partner fee to track third-party costs. | -->

## Creative rotation and associated creatives

### Creative requirements for Netflix PMP deals

To serve on Netflix inventory, CTV creatives must meet strict guidelines and technical specifications that have been set by Netflix to ensure an optimal user experience. We recommend that Microsoft Invest buyers consider dedicated creatives when buying Netflix and consider the context that the advertisement is in and how it appears on Netflix content. For more information on CTV creative specifications, see [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md).

> [!IMPORTANT]
> The Line item must be associated with a Netflix PMP deal for **Creative Requirements for the Selected Deal** to display. You must have at least one associated creative for each media type and ad size listed for the deal.

### Creative rotation

Select the Creative Rotation Strategy:

- **Auto-optimize creative weight**: The creative with the highest click-through-rate (CTR) delivers the most.
- **Evenly weight creatives**: The even rotation is handled automatically by our system.
- **Manually weight creatives**: The rotation is based on a user-supplied weight.

### Associated creatives

1. Search for the creative name or the ID, to open the **Associated Creatives** dialog.
1. Select the creatives you want to associate with your PG line item from the **Available Creatives** list by selecting the check next to the name. Selected creatives will appear in the **Selected Creatives** list. Ensure that you have at least one associated creative for each media type and ad size listed in the **Creative Requirements for the PG Deal**. For more information on how to add creatives, see [Add a Creative](./add-a-creative.md) and [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md).
1. When you finish making your selections, select **Save**.

## Related topics

- [Programmatic Guaranteed Buying Line Items](./programmatic-guaranteed-buying-line-items.md)
- [Create an Insertion Order](./create-an-insertion-order.md)
- [Add a Creative](./add-a-creative.md)
- [Creative CTV Guidelines and Specifications](creative-ctv-guidelines-and-specifications.md)
