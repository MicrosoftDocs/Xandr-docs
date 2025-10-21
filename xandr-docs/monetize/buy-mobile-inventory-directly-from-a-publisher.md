---
title: Buy Mobile Inventory Directly from a Publisher
description: This guide is a step-by-step guide to buy mobile inventory directly from a publisher. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Buy mobile inventory directly from a publisher

This document describes the process you have to go through to buy mobile inventory directly from a publisher; it involves the following steps:

- Set up sell-side objects (placements, etc.) that represent the publisher's inventory

- Export and modify placement tags using our mobile ad call parameters, and distribute these tags to the publisher

- Set up campaigns to target this "direct" inventory

  This makes running your campaigns and then reporting on them a fairly straightforward process, provided that things are set up correctly. Each of these steps is described more fully below.

> [!NOTE]
> If you'd like to buy from other networks on the Microsoft Advertising platform, see [Buy Mobile Inventory via RTB](buy-mobile-inventory-via-rtb.md).

Still have questions? See the [Mobile Buying FAQ](mobile-buying-faq.md).

## Step 1. Set up sell-side objects in our system

Set up a publisher, placement groups, and placement tags to represent the publisher's supply; you'll interact with these as "managed sellers" when setting up your campaigns and reporting on them. For instructions on how to set up publishers and placement tags in our system, see [Create a Publisher](create-a-publisher.md) and [Create a Placement](create-a-placement.md).

> [!NOTE]
> When you set up your placement group, you will be prompted to select a **Supply Type** as shown in the screenshot below. The supply type you select here (**Mobile Optimized Website** or **Mobile Application**) must match the supply type you choose in your campaign. See [device and supply type targeting](supply-type-targeting.md) for more details.

We recommend creating your publisher, placement group, and placement hierarchy so it reflects your integration with the publisher. For example, if you buy from multiple publishers, it's best to set up each one as a separate publisher "object" in our system, and use placement groups as "folders" in which to organize the placement tags you'll run on that publisher's inventory. For more information on sell-side basics, see [Working with Publishers](working-with-publishers.md).

## Step 2. Export placement tags and distribute them to the publisher

Create placement tags in our system and export them using the instructions in [Export Placement Tags](export-placement-tags.md). This will provide you with display ad tags (`/ttj`). You'll need to modify them into `/mob` ad tags before distributing them to your publishers. This is a manual process that involves editing the placement tags by hand that you export (see [Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md) for an alternate method). For instructions on how to set up the `/mob` ad tag, see the section **Mobile Tag Format** of the [Mobile Ad Call Reference](mobile-ad-call-reference.md).

### Before you begin campaign setup

- **Prerequisite** - You have already created the line item under which you want to create your campaign. The line item defines your financial agreement with an advertiser, whereas the campaign specifies how to spend the money to make good on your agreement. See [Create a Standard Line Item](create-a-standard-line-item.md) for more details.
- **Recommendations** - If you plan to target user segments and/or domain lists, make sure the relevant segments and domain lists have been created before you start campaign setup. See [Create a Segment Pixel](create-a-segment-pixel.md) and [Working with Targeting Lists](working-with-targeting-lists.md) for more details.

## Step 3. Set up your campaign (standard line items only)

In this section we'll describe how to set up direct campaigns to target the publishers, placement groups, and placements you've created. The process for targeting specific placement tags is described in [Third-Party Inventory Targeting](third-party-inventory-targeting.md).

Creating a mobile campaign involves defining:

- **Supply Type** - Whether you want to buy mobile app inventory, web inventory optimized for mobile devices, or both.
- **Media Budget** - How much you are willing to spend on buying mobile media (in dollars or impressions).
- **Buying Strategies** - In this case, you want to run the campaign on your own device-optimized web or in-app inventory.
- **Learn Budget** - How much you are willing to spend on optimizing your campaign (in dollars or impressions). Learn budget only applies when buying third-party inventory using a strategy involving optimization.
- **Targeting** - What specific inventory you want to run on and how precisely you want to target users (via system, frequency, segments, geography, etc.).

> [!NOTE]
> For mobile campaigns, **system targeting** is one of the most useful ways to reach users. You can include or exclude users via the types of devices they use (phone, tablet, pc), their device makes and models (i.e., Apple iPhone, HTC Droid Incredible, etc.), their operating systems, the browsers on their devices, and their mobile carriers and connection types (carrier-based or wifi/static). See [System Targeting](system-targeting.md) for details.

## Step 4. Select the advertiser

Click the name of the advertiser under which you want to create a new campaign.

This takes you to the **Advertiser Details** screen.

## Step 5. Start a new campaign

On the **Advertiser Details** screen, click **Create New**  \>  **Campaign**.

This opens the initial **Create New Campaign** screen.

> [!NOTE]
> You can find **Create New > Campaign** on the insertion order, line item, and campaign screens under the advertiser as well.

## Step 6. Select the parent line item

In the **Select a Line Item** section, select the line item under which you want to create your campaign and then click **Continue**. If you are creating your campaign directly from a line item or there is only one line item associated with the advertiser, the line item is selected by default.

> [!NOTE]
> You can use the search field to find a particular line item by name or ID. Also, all active and inactive line items are listed by default, but you can use the filter to the right of the search field to show just active or inactive line items.

## Step 7. Select the campaign type

In the **Campaign Type** section, select **Buy direct/third-party inventory**. This will reveal the full workflow for setting up a campaign.

> [!NOTE]
> Since you are creating and distributing the `/mob` tags to the publisher yourself (as described in Step 2. Export placement tags and distribute them to the publisher), you should leave the campaign type set to the default, **Display and Mobile**. This is because our [Mobile Ad Call Reference](mobile-ad-call-reference.md) is just a variation on our standard display ad tag.

You can expand or collapse each section of the screen as you like. To expand or collapse all sections at once, click the **Expand All** or **Collapse All** link in the upper right.

Changing the campaign type will reset your workflow and available targeting options.

## Step 8. Enter basic details and flight dates

In the **Basic Setup** section, enter the basic details and flight dates for the campaign.

- **Name** - Enter the name for the campaign. You will later be able to search for and report on the campaign using this name.
- **External Code** - If you want to report on the campaign using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code here.
- **State** - The state is set to "Inactive" by default to prevent the campaign from spending before all necessary settings and creatives are complete. You can set the state to "Active" at any time.
- **Flight Dates** - Set the start for the campaign and set an end date or select **Run Indefinitely**.

  > [!NOTE]
  > The time format (12-hour or 24-hour) and time zone are inherited from the advertiser. Enter or select the start and end dates and times for the campaign. If flight dates are set for the parent line item, those dates take precedence; regardless of the dates set for the campaign, the campaign will not start before the line item start date and will not continue buying impressions after the line item end date. To further limit serving to specific days and hours of the week, you can use [Daypart Targeting](daypart-targeting.md).

## Step 9. Set the campaign budget

> [!NOTE]
> You can set budgets at the insertion order and line item levels as well. Budgets at these levels take precedence over a child campaign's budget; if they run out, the campaign will stop buying impressions, whether or not it has reached its own budget. For more details about budgeting, see [Budgeting and Pacing](budgeting-and-pacing.md).

By default, your campaign media **Budget** is unlimited. If you prefer, you can define exactly how much you are willing to spend on buying inventory for the campaign. The budget can be in impressions or in media cost (dollars). Note that media cost is in USD rather than the advertiser's currency because USD is the currency in which Microsoft Advertising transacts.

- **Lifetime** - This is the budget that you are willing to spend over the entire lifetime of the campaign. There are two options:
  - **Custom** - Select this option to enter a specific amount of impressions or dollars.
  - **Unlimited** - Select this option to leave your lifetime budget undefined.

  > [!NOTE]
  > If **Lifetime** budget is set to **Unlimited** and the line item and insertion order lifetime budgets are also set to **Unlimited**, severe overspend can occur.

- **Daily** - This is the budget that you are willing to spend on any single day. There are three options:
  - **Custom** - Select this option to enter a specific amount of impressions or dollars. When you enter a custom daily budget, you must select one of the following options:
    - **Pace evenly throughout the day** - Select this option, otherwise known as "daily pacing", if you want to prevent your daily budget from being spent all at once by distributing your spend evenly by hour throughout the day. Note that if you use Daypart Targeting to restrict the hours during which the campaign can serve, daily pacing will adjust to distribute your spend evenly across only the targeted hours. For more details, see [Daypart Targeting](daypart-targeting.md) or [Daily Pacing](daily-pacing.md).
    - **Spend as fast as possible** - Select this option if you do not want to pace your daily budget at all. Note that this option could lead to your entire daily budget being spent in a very short amount of time.

  - **Pace Lifetime Budget** - Select this option to spread your lifetime budget evenly across your flight dates. As each day passes, the system spreads the remaining impression or media cost budget across the remaining days of the flight.

    The system is not able to pace its spending if it does not have a budget amount, and the system must know the number of days in the campaign in order to apply the remaining budget amount equally for the remainder of the flight. Therefore, this option requires that you enter a custom lifetime budget and select an end date. For more details, examples, and best practices, see [Lifetime Pacing](lifetime-pacing.md).

  - **Unlimited** - Select this option to leave your daily budget undefined.

    To enable this feature, speak to your Microsoft Advertising representative.

If you have enabled the unlimited budget warning feature, you will not be able to set the budget for your campaign to **unlimited** if the line item and (if applicable) insertion order budgets are also set to unlimited. This feature prevents mistaken overspend that can result when budgets are set to unlimited at all levels. When the feature is enabled, to set your campaign budget to unlimited, you must first limit the budget for either the insertion order or line item associated with the campaign.

## Step 10. Define the buying strategies

In the **Buying Strategies** section, choose to buy direct inventory. You will be buying from the sell-side objects you created to represent the publisher in an earlier step.

### Buy direct inventory

To run the campaign on your own managed publishers or direct buys, check the **Buy Direct Inventory** box. Then weight the campaign against other direct campaigns and, if applicable, enable roadblocking.

- **Campaign Priority** - Since you have already paid for direct inventory, there is no need to input a buying strategy, but you can select a priority to weight the campaign against other direct campaigns within your account. The campaign with the highest priority will always win, even if a lower priority campaign bids more. For more information about managing priority, see [Bidding Priority](bidding-priority.md).

  By default, campaign priority is 5. If you leave this default for all of your direct campaigns, no campaign will be given precendence over any other. As soon as you change the priority in one of your direct campaigns, however, ALL of your eligible campaigns are potentially impacted.

- **Enable Roadblocking** - In cases where your managed publishers are using Microsoft Advertising's Seller Tag (AST) to conduct a single auction for multiple ad slots on a page, you can serve multiple linked creatives in response, also known as roadblocking. If a roadblock campaign is eligible, the campaign priority is effectively 11. There are three possible types of roadblocks:
  - **Normal Roadblock** - The number of creatives is greater than or equal to the number of ad slots.
  - **Partial Roadblock** - One creative for each size must be eligible to serve on the page. All creatives will serve if ad slots are available. If more than one creative per size exists, creatives will rotate through a single slot.
  - **Exact Match** - The number of creatives is exactly equal to the number of ad slots.

  > [!IMPORTANT]
  > Roadblocking is available only for campaigns buying exclusively direct inventory. Also, the partial and exact roadblocking options are available only to some clients. For more details, please see [Target Your Inventory with Roadblocking](target-your-inventory-with-roadblocking.md).
  
## Step 11. Show to users without cookies

To target users that you have not seen before and users who have cleared their cookies, check the **Show to users without cookies** box under **Buying Strategies** \> **OTHER OPTIONS**.

If using frequency targeting for this campaign, you must also check the **Show to users without cookies** box in the **Frequency** section of the **Targeting** area. For more details, see [Frequency and Recency Caps](frequency-and-recency-caps.md). Your campaign will show ads to users without cookies by default except when conversion tracking is enabled at the line item level (one or more conversion pixels are attached to the line item). In this case, targeting users without cookies is not the default because we cannot attribute conversions back to an impression view or click when users do not have cookies.

Targeting cookieless users does not affect mobile app targeting. Almost all in-app inventory has a device ID associated with it; this device ID is then associated with our platform's cookie.

For mobile web campaigns, checking **Show to users without cookies** is currently the only way to serve ads to Safari users, since Safari disables third-party (advertising) cookies by default.

## Step 12. Add targeting

Because you are buying directly from a publisher, the most useful targeting in this section is probably [Direct Inventory Targeting](direct-inventory-targeting.md).

In the **Targeting** section, you can [Apply a Targeting Template](apply-a-targeting-template.md) or set unique inventory and user targeting for this campaign.

When you apply multiple types of targeting (e.g., inventory, segment, geography, etc.), keep in mind that your campaign will buy only impressions that match targeting. In other words, there is an AND relationship between the main types of targeting. For example, if you target seller 123, segment ABC, and the United States, your campaign will bid only on impressions from that seller being viewed by users in that segment and in the United States.

### Target inventory

You can target inventory in numerous ways. Use the links below to learn more about each type of inventory targeting.

- [Inventory Quality Targeting](inventory-quality-targeting.md)
- [Content Category Targeting](content-category-targeting.md)
- [Direct Inventory Targeting](direct-inventory-targeting.md)
- [Domain Targeting](domain-targeting.md)
- [App Targeting](app-targeting.md)
- [Page Properties Targeting](page-properties-targeting.md)

### Target users

You can target users in numerous ways. Use the links below to learn more about each type of user targeting.

- [Device and Supply Type Ttargeting](supply-type-targeting.md)
- [Geography Targeting](geography-targeting.md)
- [Segment Targeting](segment-targeting.md)
- [Frequency and Recency Caps](frequency-and-recency-caps.md)
- [Daypart Targeting](daypart-targeting.md)
- [System Targeting](system-targeting.md)
- [Demography Targeting](demography-targeting.md)
- [Test and Control Targeting](test-and-control-targeting.md)

## Step 13. Associate creatives and define a dynamic landing page

In the **Associated Creatives** section, you can select a **Creative Rotation** to determine how you want to rotate and weight multiple creatives. Select one of these options:

- **Evenly weight creatives** (default): Even rotation is handled automatically by our system.
- **Auto-optimize creative weight**: When this option is chosen, 75% of delivery is allocated to the creative with the highest click-through rate; all remaining creatives of the same size receive equal allocations of the remaining 25% of overall delivery.
- **Manually weight creatives**: By selecting this option, you will be able to manually set a weight (between 0 and 1000).

See [Creative Rotation (Standard Line Item and Guaranteed Delivery Line Item)](creative-rotation-standard-line-item-and-guaranteed-delivery-line-item.md) for more information.

Click **Edit** and select the creatives that you want to run for the campaign. Also, if you want to define a dynamic landing page to be used by multiple creatives associated to the campaign, enter the **Landing Page URL** and then make sure the creatives are set up to use a dynamic landing page. Note that you can set a dynamic landing page at the line item level as well. For more details, see [Dynamic Landing Pages](dynamic-landing-pages.md).

If you prefer, you can associate creatives to the campaign at a later time. For more details, see [Associate Creatives to Campaigns](associate-creatives-to-campaigns.md).

## Step 14. Enter comments

In the **Comments** section, enter any comments that you would like to record with the campaign. Comments are for your reference only and will not affect campaign delivery.

## Step 15. Add serving fees

If you owe serving fees to third parties for services such as creative hosting or user data, you can add these fees in the **Serving Fees** section. Serving fees can be either a percentage of costs or a flat CPM. Please note the following:

- Serving fees are added to your media cost.
- When you use a third-party buying strategy that involves optimization ("Optimize to a predicted CPA/CPC goal" or "Optimize to a % margin of booked revenue"), bids are automatically reduced to account for serving fees.
- When you buy direct inventory or use a third-party buying strategy that does not involve optimization, bids are not reduced to account for serving fees.

To add a new serving fee:

1. Click the **Add Fee** button.
1. In the **Broker** field, select the relevant broker or create a new broker.
1. In the **Description** field, enter details about the serving fee.
1. Select the **Fee Type** (CPM or Cost Share) and enter the relevant **Fee Value** (dollar amount for CPM, percentage for Revenue Share).
1. Click **Add**.

Per broker, you can add no more than one CPM serving fee and one Cost Share serving fee.

## Step 16. Review and save your campaign

Confirm that the campaign details are correct and then click the **Save** button to finish adding the campaign to Microsoft Advertising. The campaign is then added to the list of campaigns on the [Explore Campaigns](explore-campaigns.md).

## Step 17. Complete peer approval

See [Peer Approval](peer-approval.md) for more information.

### Next steps

Once you've created a campaign, you can view all its details on the [View Campaign Details](view-campaign-details.md). You can also continue associating creatives to the campaign. For more details, see [Associate Creatives to Campaigns](associate-creatives-to-campaigns.md).

## Related topics

- [Welcome to Mobile](welcome-to-mobile.md)
- [Buy Mobile Inventory via RTB](buy-mobile-inventory-via-rtb.md)
- [Mobile Buying FAQ](mobile-buying-faq.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)
