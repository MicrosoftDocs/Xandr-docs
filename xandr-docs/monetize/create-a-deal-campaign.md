---
title: Create a Deal Campaign
description: Explore creating campaigns to target Monetize sellers and external partners, mirroring standard setups for effective promotion.
ms.date: 10/28/2023
---

# Create a deal campaign

Creating a campaign that targets deals you have with Monetize sellers and/or external supply partners is similar to setting up a standard [Create a Campaign](create-a-campaign.md). There are a few settings, however, that you must pay particularly close attention to:

- You must select the deal campaign type. See **Step 2. Select the deal campaign type** for details.
- You must select the deals you want to target. See **Step 3. Target deals** for details.
- You must set a buying strategy that is appropriate for deals. See **Step 5. Set the buying strategy** for details.

  For an introduction to the concept of deals and links to other resources, see [Buying Deals](buying-deals.md).

## Before you begin

Before you can target a deal, you must negotiate and set up the deal in cooperation with the seller. For more information, see [Negotiate Deals with Sellers](negotiate-deals-with-sellers.md).

## Step 1. Get started

Select a line item and advertiser, and start a new campaign as you normally would.

On the **Advertisers** screen (**Advertisers** \> **All Advertisers**), click the **Line Items** button near the advertiser under which you want to create a new campaign. Then, on the **Campaign Details** screen, click **Create New** \> **Campaign**. Finally, in the **Select a Line Item** section, confirm that the line item with which you want the campaign associated is selected, then click **Continue**.

> [!TIP]
> You can find **Create New** \> **Campaign** on the insertion orders and line items under the advertiser, as well.
> [!IMPORTANT]
> For more detailed information on initial campaign setup, see the generic campaign setup workflow, [Create a Campaign](create-a-campaign.md).

## Step 2. Select the deal campaign type

In the **Campaign Type** section, select **Buy using Deal ID**. This will reveal the full workflow for setting up a deal campaign.

> [!TIP]
> You can expand or collapse each section of the screen as you like. To expand or collapse all sections at once, click the **Expand All** or **Collapse All** link in the upper right.
> [!WARNING]
> Changing the campaign type will reset your workflow and available targeting options.

## Step 3. Target deals

In the **Deals Selection** section, click the **Edit** button and then include the deals that you want to target.

> [!TIP]
> **Finding Deals** Click the column headers to sort by name, ID, ask price, or seller, or use the search field to find deals by ID, code, or name. Also, all active and inactive deals are listed by default, but you can use the filter to the right of the search field to show just active or inactive deals.
>
> **Viewing Deal Details**
>
> Hover over the **eye icon** to view details about a deal. You can view additional deal details in the [Partnership Details Screen - Buyer View](partnership-details-screen-buyer-view.md).
>
> **Explanation of Deal Details**
>
> - **Ext. Deal ID**
>
>   The custom code for the deal. For deals with external supply partners, this is generally the ID that you use to 
> identify the deal. If a custom code hasn't been defined for the deal, this field will not be shown.
>
> - **Status**
>
>   Whether or not the deal is currently available for buying.
>
> - **Ask Price**
>
>   The minimum CPM that the seller will accept for the deal. Note that when you set your buying strategy, you will need
>   to bid higher than the ask price to account for pre-bid fees and other factors. For more details, see **Step 5. Set the buying strategy**.
>
> - **Currency**
>
>   The currency for the ask price.
>
> - **Type** The type of auction that will be held for the deal. For more details and examples showing how the different types of auctions work, see [Deal Auction Mechanics](deal-auction-mechanics.md).
>
>   - **Open Auction**
>     Buyers targeting the deals and buyers targeting the inventory via other means compete for the impression.
>   - **Private Auction**
>     Buyers targeting the private deals compete for the impression first. Then, if none of the deal buyers win, the auction is opened to  buyers targeting the inventory via other means.
>   - **First Look** Deals considered "First Look" are offered only by external supply partners and have extremely varied auction logic depending on both the supply partner and the seller. You must contact the supply partner for details about how the deal works. Xandr as a buying platform can make no guarantee that first look deals actually give you the first look at an impression.
>
> - **Start Date** The day and time when the deal starts being available to you. Note that this is distinct from your
>   campaign start date.
>
> - **End Date** The day and time when the deal stops being available to you. Note that this is distinct from your
>    campaign end date.
>
> - **Last Updated** The date and time when the deal was last modified by the seller.
>
> - **Sizes** The creative sizes to which the deal applies.
>
> - **Brands** The brands to which the deal applies.
>
> - **Description** The description of the deal. The seller may use the description to provide additional insight or
>    details about the deal.

## Step 4. Enter campaign details

Enter campaign details, flight dates, and set the campaign budget as you normally would. In the **Basic Setup** section, enter the basic details and flight dates for the campaign in the fields provided. Then, in the **Budget** section, set the campaign budget. By default, your campaign media budget is unlimited. If you prefer, you can define exactly how much you are willing to spend by setting a specific budget. The budget can be set in impressions or in media cost (dollars).

For more detailed information on **Basic Setup** and Budget sections, see the generic campaign setup workflow, [Create a Campaign](create-a-campaign.md).

## Step 5. Set the buying strategy

In the **Buying Strategies** section, we recommend using the **Bid a base CPM** option to bid on your deals. Enter the fixed dollar amount to bid per thousand impressions in the **Base CPM $\_** field.

**Highest Targeted Floor**

This amount is the highest ask price of all deals you are targeting. For example, if you target Deal A with an ask price of $1.00 and Deal B with an ask price of $5.00 the highest targeted floor will be $5.00.

**Suggested Minimum Bid**

If you're targeting deals with an ask price, the suggested minimum bid shows you the CPM amount that will likely clear the ask price for your deals. It is based on the highest ask price of all deals you are targeting plus your auction service charge. For deals with external suppliers, this amount will include additional margin to account for
discrepancies and may fluctuate over time as the level of discrepancy between Microsoft Advertising and the third party changes.

> [!NOTE]
> Bidding the suggested minimum will help ensure that you are eligible for the deal but will not guarantee that your bid wins.

Paying on a CPA or CPC basis is not available for deal inventory. The other CPM buying strategy options remain available, although they are not recommended.

- **Optimize to a % margin of booked revenue** - Use this strategy to bid a % margin of the revenue that the advertiser pays you. For example, if your booked revenue is $1 CPM, and you set a bidding strategy margin of 25%, your campaign will bid $0.75. If your booked revenue type is a CPA or CPC goal, it will apply your desired margin
  and optimize to that predicted goal.
  - **Bid CPM: max $\_\_\_ CPM min $\_\_\_ CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
  - **Enable cadence modifier** - Under OTHER OPTIONS, check this box to vary your bid based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently. For more details, see [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md).
- **Optimize to a predicted CPA goal** - Use this strategy to vary bids based on the likelihood of an attributed conversion for each piece of inventory. This strategy uses the Microsoft Advertising optimization engine.
  - **Bid $\_ post-click/post-view CPA** - Select the conversion pixel to which you want to optimize and enter the dollar amount per conversion that you want the optimization engine to aim for.
  - **Learn Budget** - The learn budget is the portion of your campaign budget that you want to commit to optimizing your campaign, which helps you quickly find slices of third-party inventory that provide a positive ROI. The first phase of this process is called Learn. You can set a lifetime learn budget of up to 100% of the campaign budget
    as well as a daily cap for learning. For more information about optimization and learning, see [Targeted Learn](targeted-learn.md).
  - **Bid at most $\_ CPM in Learn Phase** - When your campaign starts to spend on new inventory, the optimization engine submits "learn" bids. If necessary, enter max CPM dollar amount for these bids.
    When you set both a cap for learn bids and a max CPM for non-learn bids (next option), the lower of the two will be used for learn.
  - **Bid CPM: max $\_ CPM min $\_ CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
  - **Enable cadence modifier** - This option appears under OTHER OPTIONS and cannot be deselected. When optimizing to a predicted CPA goal, your bids will always vary based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user
    hasn't seen it before or hasn't seen it many times or seen it recently. For more details, see [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md).
- **Optimize to a predicted CPC goal** - Use this strategy to vary bids based on the likelihood of a click for each piece of inventory. This strategy uses the Microsoft Advertising optimization engine.
- **Optimize to $\_ per click** - Enter the dollar amount per click that you want the optimization engine to aim for when calculating bids.
- **Learn Budget** - The learn budget is the portion of your campaign budget that you want to commit to optimizing your campaign, which helps you quickly find slices of third-party inventory that provide a positive ROI. The first phase of this process is called Learn. You can set a lifetime learn budget of up to 100% of the campaign budget as
  well as a daily cap for learning. For more information about optimization and learning, see [Targeted Learn](targeted-learn.md).
- **Bid at most $\_ CPM in Learn Phase** - When your campaign starts to spend on new inventory, the optimization engine submits "learn" bids.
  It is recommended to enter a max CPM dollar about for these bids. In doing so, you will avoid learning on inventory that is too expensive while not limiting yourself from optimized inventory sorces that are worth higher prices. <b>**Note:**</b> When you set both a cap for learn bids and a max CPM for non-learn bids (next option), the lower of the two will be used for learn.
- **Bid CPM: max $\_ CPM min $\_ CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
- **Enable cadence modifier** - This option appears under OTHER OPTIONS and cannot be deselected. When optimizing to a predicted CPA goal, your bids will always vary based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it
  before or hasn't seen it many times or seen it recently. For more details, see [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md).
- **Target reach and delivery (bid via ECP or EAP)** - Use this strategy to bid the going platform rate for each piece of inventory.
  - **Auto-bid to win most platform impressions (ECP)** - Select this option to bid an estimate of the price that is likely to win most impressions from Microsoft Advertising platform sellers
    based on historical bids and their success or failure. Since off-platform sellers (e.g., Google Ad Manager, Rubicon, etc.)
    conduct a secondary auction, bidding ECP does not necessarily ensure winning off-platform impressions.
  - **Auto-bid to win ~50% of platform impressions (EAP)** - Select this option to bid an estimate of the price that is likely to win about half of the impressions from Microsoft Advertising platform sellers based on historical bids and their success or failure. Since off-platform sellers (e.g., Google Ad Manager, Rubicon, etc.) conduct a secondary auction, bidding EAP does not necessarily ensure winning half of off-platform impressions.
  - **Bid CPM: max $\_ CPM min $\_ CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
  - **Enable cadence modifier** - Under OTHER OPTIONS, check this box to vary your bid based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently. For more details, see [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md).

Although **Enable cadence modifier** is available under OTHER OPTIONS, this setting is not recommended as it will limit your campaign delivery. You can set performance goals at the line item level to achieve similar results.

- **Enable cadence modifier** - Under **OTHER OPTIONS**, check this box to vary your bid based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently. For more details,
  see [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md).
- **Bid CPM: max $\_\_\_ CPM min $\_\_\_ CPM** - This option is available under OTHER OPTIONS only once you enable cadence modifier. Enter the highest and lowest CPM
  dollar amount that you are willing to spend on an impression.

## Step 6. Add advanced targeting

In the Advanced Targeting section, you can [apply a predefined targeting template](apply-a-targeting-template.md) or set unique inventory and user targeting for this campaign. Use the links in the **Target inventory** and Target users sections below to learn more about each type of targeting.

> [!WARNING]
> Layering advanced targeting over your deals will limit your campaign's reach. Be sure to use targeting that is not in direct conflict with the terms of your deal. For example, if your deals cover inventory in the US and you then use Geography targeting to target just users in Canada, your campaign will serve only to Canadian users who happen to be looking at the US inventory in your deals. If you [Apply a Targeting Template](apply-a-targeting-template.md), be sure to apply one designed for deal campaigns. If you apply a template designed for a non-deal campaign, your campaign type will be changed and your workflow and available targeting options will be reset.

### Target inventory

> [!NOTE]
> You cannot use frequency capping or your own first-party or third-party data, nor may you add users to segments on view when targeting audience deals on LinkedIn.

You can target inventory in numerous ways. Use the links below to learn more about each type of inventory targeting.

- [Inventory Quality Targeting](inventory-quality-targeting.md)
- [Content Category Targeting](content-category-targeting.md)
- [Direct Inventory Targeting](direct-inventory-targeting.md)
- [Third-Party Inventory Targeting](third-party-inventory-targeting.md)
- [Domain Targeting](domain-targeting.md)
- [App Targeting](app-targeting.md)
- [Page Properties Targeting](page-properties-targeting.md)

### Target users

You can target users in numerous ways. Use the links below to learn more about each type of user targeting.

- [Supply Type Targeting](supply-type-targeting.md)
- [Geography Targeting](geography-targeting.md)
- [Segment Targeting](segment-targeting.md)
- [Frequency and Recency Caps](frequency-and-recency-caps.md)
- [Daypart Targeting](daypart-targeting.md)
- [System Targeting](system-targeting.md)
- [Test and Control Targeting](test-and-control-targeting.md)

## Step 7. Finish creating your campaign

You can now add creatives, add serving fees, enter comments, review your campaign settings, and set campaign peer approval as you would for any campaign.

Complete the **Associated Creatives** section to set your creative rotation preferences and add landing page URLs. If you owe serving fees to third parties for services such as creative hosting or user data, you can add these fees in the **Serving Fees** section. Enter any **comments** you have in the Comments section, then review and save your campaign. Complete peer approval for the campaign if necessary.

> [!IMPORTANT]
> For more detailed information on these sections, see the generic campaign setup workflow, [Create a Campaign](create-a-campaign.md).

### Related topics

- [Buying Deals](buying-deals.md)
- [Negotiate Deals with Sellers](negotiate-deals-with-sellers.md)
<!-- [Get Deals from Seller Packages](get-deals-from-seller-packages.md)-->
- [Deal Auction Mechanics](deal-auction-mechanics.md)
- [Buy-Side Reporting on Deals](buy-side-reporting-on-deals.md)
- [Partnership Details Screen - Buyer View](partnership-details-screen-buyer-view.md)
