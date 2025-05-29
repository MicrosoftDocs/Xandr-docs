---
title: Create a Standard Line Item
description: In this article, find step-by-step instructions on how to create and set up a standard line item.
ms.date: 10/28/2023
---

# Create a standard line item

> [!NOTE]
> This page describes the creation of a Standard Line Item. If you want to begin using [Augmented Line Items (ALI)](augmented-line-items-ali.md), see [Create an Augmented Line Item](create-an-augmented-line-item-ali.md). We recommend using [Augmented Line Items (ALI)](augmented-line-items-ali.md).

A line item defines your financial relationship with an advertiser, including:

- **Budget** - How much the advertiser has allocated for you to spend (in dollars or impressions).
- **Revenue Type** - The basis on which the advertiser has agreed to pay you (CPM, CPC, CPA, Cost Plus, Fixed Fee).
- **Performance Goals** - Performance requirements the advertiser expects you to meet.

This page walks you through the process of creating a line item.

## Before you begin

- **Prerequisite** - You have already created the advertiser under which you want to create your line item.
- **Recommendation** - If you plan to set your line item to track revenue based on conversions, set an advertiser goal based on conversions, or do any conversion tracking, you should create your conversion pixel(s) before creating your line item. See [Create a Conversion Pixel](create-a-conversion-pixel.md) for more details.

## Select the advertiser

On the **Advertisers** screen (**Advertisers** > **Advertisers**), click the name of the advertiser under which you want to create a line item.

You can create line items from the advertiser details screen or from an advertiser's insertion order.

## Start a new line item

### From the advertiser details screen

On the **Advertiser Details** screen of the advertiser under which you want to create an line item, select **Line Item** from the **Create New** menu.

The **Create New Line Item** screen displays, where you define all relevant details for your line item.

### From an insertion order

1. On the **Advertisers** screen (**Advertisers** > **Advertiser**), click the **Orders** of the advertiser under which you want to create a line item.
1. On the **Insertion Orders** screen, click the insertion order under which you want to create the line item.
1. Click **New** button in the **Line Items** section. This opens the **Create New Line Item** screen, where you define all relevant details for your line item.

> [!TIP]
> You can expand or collapse each section of the screen as needed. To expand or collapse all sections at once, click the **Expand All** or **Collapse All** link in the upper right.

## Enter basic details and flight dates

In the **Basic Setup** section, enter the basic details and flight dates for the line item.

- **Insertion Orders** - If your advertiser is set up to use insertion orders, click **Edit** and select the insertion orders you want to associate with this line item. The insertion order is automatically associated if you create the line item from the insertion order details screen.
- **Name** - Enter the name for the line item. You will later be able to search for and report on the line item using this name.
- **External Code** - If you want to report on the line item using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code here.
- **State** - Set the state of the line item. If "**Active**", child campaigns will be eligible to serve. However, it is best practice to set the state to "**Inactive**" until everything related to the buy has been set up and verified. This will avoid spending before you are ready.
- **Currency** - Select the currency in which the advertiser will pay you (revenue currency). This defaults to the currency set at the advertiser level, if any, but can be overridden here. Note that you cannot change the currency after saving the line item.
- **Flight Dates** - Select the start and end dates and times for the line item. Note that the time format (12-hour or 24-hour) and time zone are inherited from the advertiser.

> [!IMPORTANT]
> You can set flight dates for each campaign under the line item as well, but your line item flight dates take precedence. When you reach the line item end date, all campaigns under the line item will stop buying impressions, whether or not they have reached their own end dates.

## Set the line item budget

By default, your line item **Budget** is unlimited. If you prefer, you can define exactly how much the advertiser has allocated for you to spend buying media over the lifetime of the line item and/or on any single day. The budget can be in impressions or in revenue (money).

> [!IMPORTANT]
> You can set budgets at the campaign level as well, but your line item budget takes precedence. When your line item budget runs out, all campaigns under the line item will stop buying impressions, whether or not they have reached their own budgets. Also, if the line item is under an insertion order, note that the insertion order budget takes precedence over the line item budget. For more details about budgeting and best practices, see [Budgeting and Pacing](budgeting-and-pacing.md).
> [!WARNING]
> If you set the **Revenue Type** field to **Do not track Revenue**, your Insertion Order and Line Item budgets will not be respected since they are revenue-based.

- **Lifetime** - This is the budget that the advertiser has allocated for you to spend over the entire lifetime of the line item. There are two options:
  - **Custom** - Select this option to enter a specific amount of impressions or money.
  - **Unlimited** - Select this option to leave your lifetime budget undefined.

  > [!NOTE]
  > The lifetime budget allocation and pacing of your line item will be determined based on the flight dates of the underlying campaigns. As a result, we recommend that you have campaigns running for the entire duration of the parent line item's billing periods/flight dates.

- **Daily** - This is the budget that the advertiser has allocated for you to spend on any single day. There are three options:
  - **Custom** - Select this option to enter a specific amount of impressions or money. When you enter a custom daily budget, you must select one of the following options:
    - **Pace evenly throughout the day** - Select this option, otherwise known as "daily pacing", if you want to prevent your daily budget from being spent all at once by distributing your spend evenly by hour throughout the day. For more details, see [Daily Pacing](daily-pacing.md).
    - **Spend as fast as possible** - Select this option if you do not want to pace your daily budget at all. Note that this option could lead to your entire daily budget being spent in a very short amount of time.

  - **Pace Lifetime Budget** - Select this option to spread your lifetime budget evenly across your flight dates. As each day passes, the system spreads the remaining impression or revenue budget across the remaining days of the flight.

    The system is not able to pace its spending if it does not have a budget amount, and the system must know the number of days in the line item in order to apply the remaining budget amount equally for the remainder of the flight. Therefore, this option requires that you enter a custom lifetime budget and select an end date. For more details, examples, and best practices, see [Lifetime Pacing](lifetime-pacing.md).

  - **Unlimited** - Select this option to leave your daily budget undefined.

> [!IMPORTANT]
> When you associate a line item to an insertion order, any budget or impressions that occurred under the line item before it was associated to the insertion order do not count towards the lifetime budget of the insertion order. For example, if you have Line Item XYZ that spent $100,000 of budget before you associate to Insertion Order ABC with a lifetime budget of $250,000, the insertion order will not stop serving until the line item reaches $350,000 ($100,000 before being associated to the insertion order, and $250,000 after).

## Set frequency and recency caps

In the **Frequency & Recency Cap** section, you can cap how many times and how often creatives can be shown to a given user.

See [Frequency and Recency Caps](frequency-and-recency-caps.md) for details on frequency and recency.

> [!NOTE]
> Frequency caps can be set at the advertiser, campaign, and creative levels as well. The most restrictive setting always takes precedence.

## Define how to track revenue

> [!TIP]
> The new **Ensure a minimum margin of __ %** option in the **Tracking Revenue Type** section allows you to set a minimum margin that will be applied to every campaign bidding on third-party inventory under the line item. Minimum margin effectively sets a bid cap on your third-party campaigns.

- To learn how to enable minimum margin for campaigns targeting direct inventory, see [Manage Network Priorities](manage-network-priorities.md).
- To learn about how to balance margin and delivery, see our [Using Minimum Margin to Balance Margin and Delivery](using-minimum-margin-to-balance-margin-and-delivery.md).

In the **Tracking Revenue Type** section, define how the advertiser has agreed to pay you, for example, $3 per thousand impressions (CPM) or $5 per conversion (CPA).

You can choose from the following revenue types:

- **CPM** - Select this revenue type if the advertiser will pay you a flat amount per thousand impressions.
  - **Revenue Value** - Enter the amount that the advertiser will pay you per thousand impressions.
  - **Ensure a minimum margin of ___ %** - If you want to set a minimum margin, check the checkbox and enter the percent minimum margin in the empty field.

- **CPC** - Select this revenue type if the advertiser will pay you every time a user clicks on a creative served by one of the campaigns under the line item.
  - **Revenue Value** - Enter the amount that the advertiser will pay you per click.
  - **Ensure a minimum margin of ___ %** - If you want to set a minimum margin, check the checkbox and enter the percent minimum margin in the empty field.

- **CPA** - Select this revenue type if the advertiser will pay you every time a user "converts". A conversion happens when a user lands on a page containing a conversion pixel, generally as a result of taking some action (completing a purchase, submitting a form, etc.), and Microsoft Advertising determines that the event can be attributed to the user having clicked or viewed one of the advertiser's creatives previously. For more details, see [Conversion Attribution](conversion-attribution.md).
  - **Select Conversion Pixels** - When you select CPA as the revenue type, you must then click Edit to view the conversion pixels under the advertiser, select the correct conversion pixel(s) to pay attention to, and then enter the Post-Click Revenue amount and/or Post-View Revenue amount for each selected pixel.
  - **Ensure a minimum margin of ___ %** - If you want to set a minimum margin, check the checkbox and enter the percent minimum margin in the empty field.

- **Cost Plus (CPM or % Margin)** - Select this revenue type if the advertiser will pay you your media cost (whatever you spend on buying inventory) plus either an extra CPM or a percentage of what you spend.
  - **Revenue Value** - Select whether the advertiser will pay you a CPM or a % Margin on top of your media cost and then enter the revenue value. Note that the revenue value will apply only to publisher inventory with non-revshare pricing.

- **Fixed Fee** - Select this revenue type if the advertiser will pay you a flat amount. There are two options for allocating fixed fees:

  - **Cost Per Day**: The advertiser will pay a flat fee each day throughout the flight. The flight can be of any length, but must have an end date. Under **Revenue Value per Day**, enter the amount that will be paid out daily. The specified daily revenue value will not be allocated on any day that the line item has not served at least 1 impression.
  - **One Time Allocation**: The advertiser will pay out the full amount of the fee on the end date of the flight. The end date must be within one month of the start date. Under **Revenue Value**, enter the full amount to be paid. If you pay managed publishers a percentage of your revenue, their share will be paid out on the allocation date, after which the line item will no longer be editable.

  Fixed fee revenue numbers will not be logged in reporting on the Campaign level. They will be logged only on the Line Item level.

  Fixed fee will not be booked on the allocation date unless the line item has served at least 1 impression.

  > [!NOTE]
  > You must enter start and end dates for flights with fixed fees. End dates must have an end time of 11:59 PM, day parting is not supported for fixed fees.

- **Do Not Track Revenue** - Select this option if you do not want to track booked revenue in the Microsoft Advertising system. Please note that, although defining your revenue values at the line item level is optional for third-party campaigns, not entering your revenue values limits to a great degree the amount of information we can present in the billing reporting tools. If you have any direct campaigns under a line item, you must enter a revenue value (even if it's $0) as this determines how much you will pay your publishers.

> [!WARNING]
> **CPC/CPA Revenue Tracking** - Budgeting based on CPC and CPA revenue is less exact than budgeting based on media cost (Cost Plus) or impressions (CPM) because the "budget events" for CPC- and CPA-based budgets are, by their nature, not within the control of the network or ad server. In these cases, a "budget event" is a click or conversion, as opposed to an impression. For example, your campaign may buy several thousand impressions, but many corresponding clicks or conversions may not happen for hours or even days.

## Set roadblocking

In cases where your managed publishers are using Microsoft Advertising's Seller Tag (AST) to conduct a single auction for multiple ad slots on a page, you can serve multiple linked creatives in response to create a roadblock. The ability to enable roadblocking depends on the following requirements:

- You can set roadblocks on the line item or campaign level, but not both. If a campaign already has roadblocking enabled, you cannot enable it on the associated line item. Alternatively, once you enable roadblocking on the line item, you cannot set it on a campaign.
- Roadblocking can be enabled only for direct inventory. If a campaign is set up to buy third-party inventory, roadblocking cannot be enabled on the line item (or campaign).

To enable roadblocking on the line item, perform the following actions:

1. Select **Enable roadblocking**.
1. Select the type of roadblock:
    - **Normal** - The number of creatives is greater than or equal to the number of ad slots.
    - **Partial** - One creative for each size must be eligible to serve on the page. All creatives will serve if ad slots are available. If more than one creative per size exists, creative will rotate through a single slot.
    - **Exact** - The number of creatives is exactly equal to the number of ad slots.
1. Select the budgeting, pacing, and frequency capping option for the line item. Under **Count an impression (for budgeting, pacing and frequency capping) on delivery of**, select either:
    - **Each creative** - Count each creative delivered as part of the roadblock as a unique impression. For example, if your insertion order is budgeted for 100 impressions and 4 impressions are delivered to a user as a roadblock, your budget will have 96 impressions remaining.
    - **The line item** - Count only the master creative as a delivered impression, regardless of how many creatives were delivered for the roadblock. If your insertion order is budgeted for 100 impressions and 4 impressions are delivered to the user as part of this roadblock, your budget will have 99 impressions remaining. Note that if the master creative is not one of those 4 impressions delivered, you budget remains at 100 impressions.
1. If you opt to budget based on **The line item**, you must select a size from the **Master size** list. Select the size of the creative you want to act as the master (the creative that will be used to count impressions). If you have more than one creative of this size, one will be chosen at the time of auction to be the master.

See [Target Your Inventory with Roadblocking](target-your-inventory-with-roadblocking.md) for more in-depth details and examples for roadblocking.

## Set optimization (to a performance goal)

Optimization (to a performance goal) selections are made via the **Primary KPI** menu. You may set your line item to a primary KPI of CPC, CPA, or CTR.

> [!NOTE]
> Optimization to a Primary KPI works in conjunction with CPM, CPC, or CPA revenue types when advertisers want to meet goals that are different from the payment types they have chosen (e.g., an advertiser wants to pay CPM but would like you to meet a $50 CPA primary KPI). For all campaigns under the line item, the Microsoft Advertising optimization engine will consider your entries in the Optimization section fields when deciding whether or not to bid on inventory.

For more information on the relationship between revenue and tracking, see [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md).

## Set a primary KPI of CPC

Select this option if your advertiser wants to achieve a goal based on clicks. Note that this option is not available when your revenue type is CPC. Complete the **Track performance against client goal of $_ field**, entering the performance goal your advertiser has given you. If you would like to set a bid/no bid decisioning limit, check the **Do not bid if post-click eCPC is above _** checkbox and enter the limit in the empty field.

> [!NOTE]
> The **Track performance against client goal $ __** field uses this value for reporting purposes only. The **Do not bid if post-click eCPC is above** checkbox controls the bid/no bid decision.

## Set a primary KPI of CPA

Select this option if your advertiser wants to achieve a goal based on conversions. When you select CPA as the goal type, you must then select the correct conversion pixel(s) to pay attention to. Then, complete the **Track performance against client goal of $_** field, entering the performance goal your advertiser has given you. If you would like to set a bid/no bid decisioning limit, check the **Do not bid if post-click eCPA is above $_** checkbox and enter the limit in the empty field.

> [!NOTE]
> The **Track performance against client goal of $ __** field uses this value for reporting purposes only. The **Do not bid if post-click eCPA is above** checkbox controls the bid/no bid decision.

## Set a primary KPI of CTR

Select this option if your advertiser wants to achieve a goal based on click-through-rate. Complete the **Track performance against client goal of $_** field, entering the performance goal your advertiser has given you. If you would like to set a bid/no bid decisioning limit, check the **Do not bid if CTR is below _ %** checkbox and enter the limit in the empty field.

> [!NOTE]
> The **Track performance against client goal of $__** field uses this value for reporting purposes only. The **Do not bid if CTR is below** checkbox controls the bid/no bid decision.

**No Performance Goal** - Select this option if you do not want to use performance goals when deciding whether or not to bid on inventory.

## Attach pixels for conversion tracking

In the **Conversion Tracking** section, click **Edit** to select conversion pixels that you want to be available for reporting, attribution, or CPA optimization for any campaign under the line item. Conversion pixels selected for tracking revenue or advertiser goals will already be selected here. If no conversion pixels exist for the advertiser, see [Create a Conversion Pixel](create-a-conversion-pixel.md) for step-by-step instructions.

> [!NOTE]
> You can attach a maximum of 20 conversion pixels to a line item. This includes conversion pixels associated with booked revenue and performance goals. If you need to attach more, please speak with your Microsoft Advertising representative.

## Choose targeting settings

In the **Targeting** section, you can target inventory and users in various ways. Use the links below to learn more about each type of targeting.

- [Direct Inventory Targeting](direct-inventory-targeting.md)
- [Domain Targeting](domain-targeting.md)
- [Device and Supply Type Targeting](supply-type-targeting.md)
- [Geography Targeting](geography-targeting.md)
- [System Targeting](system-targeting.md)
- [Segment Targeting](segment-targeting.md)
- [Query String Targeting via Placement Tags and Segments](query-string-targeting-via-placement-tags-and-segments.md)

> [!NOTE]
> **Boolean Logic** - When you apply multiple types of targeting (e.g., inventory, segment, geography, etc.), keep in mind that your campaign will buy only impressions that match all targeting. In other words, there is an AND relationship between the main types of targeting. For example, if you target seller 123, segment ABC, and the United States, your campaign will bid only on impressions from that seller being viewed by users in that segment and in the United States.

## Set associated creatives

### Choose campaign-level or line item-level creatives

In the **Associated Creatives** section, you can choose whether you want to associate creatives at the line item level or the campaign level.

> [!NOTE]
> When you choose to associate creatives at the line item level, all campaigns will inherit the creatives of their parent line item, and you cannot override this setting on individual campaigns. For this reason, you may choose to manage creatives on either the campaign or the line item, but not both.
> [!TIP]
> If you plan to serve the same creatives across a range of campaigns under the same parent line item, the best choice is to associate creatives on the line item level. However, if you plan to serve a variety of different creatives through different campaigns with the same parent line item, it's best to associate creatives on the campaign level.

If you want to associate creatives on individual campaigns, click the **on the Campaign level** button.

If you want to associate creatives to the line item you are creating, click the **on the Line Item level** button.

#### For line item creatives, select and associate your creatives

In the **Associated Creatives** section, with line item creatives selected, click the **Edit** button. This opens the **Associated Creatives** dialog. Select the creatives you want to associate to your line item from the **>Available Items** list by clicking on them. They will appear in the **Selected Items** list. When you finish making your selections, click **Add**.

When you return to the main **Create a New Line Item** screen, you will see the number of creatives associated in the **Associated Creatives** section.

## Enter reporting labels (optional)

In the **Reporting Labels** section, you can associate a **Trafficker**, **Sales Rep**, or **Line Item Type** to the line item. This enables you to report on performance by these labels in [Network Reporting](network-reporting.md). For example, you might associate a Trafficker with each line item and then run a report grouped by Trafficker to find out which ones are responsible for which line items or compare line item performance across traffickers.

For more details, see [Reporting Labels](reporting-labels.md).

## Add commissions (optional)

If you need to attribute revenue to third parties, you can add fees in the **Commissions** section. Commissions are deducted from the booked revenue (the amount the advertiser pays you) of each line item under the insertion order, and can be defined either as a percentage of booked revenue or a flat CPM.

> [!NOTE]
> Commissions at the line item level override commissions at the insertion order level.

To add a new commission:

1. Click the **Add Fee** button to display the other fields.

1. In the **Broker** field, select the relevant broker or create a new broker.

1. In the **Description** field, enter details about the commission.

1. Select the **Fee Type (CPM or Revenue Share)** and enter the relevant **Fee Value** (dollar amount for **CPM**, percentage for **Revenue Share**).

1. Click **Add**.

    Per broker, you can add no more than one CPM commission and one Revenue Share commission.

    > [!NOTE]
    > The decimal position support for the broker fees is for 1 place after the decimal. For example, if you set 16.67% as a broker fee in the **Commissions** section, after saving, the value would round off to 16.7%. However, there is no restriction on number of places after the decimal if the [Insertion Order service API](../digital-platform-api/insertion-order-service.md) is used to create the broker fee.

## Define a dynamic landing page

If you plan to associate multiple creatives to a single landing page, you can set the landing page URL in the Dynamic Landing Page section. Note that you can set a dynamic landing page at the campaign level as well. For more details, see [Dynamic Landing Pages](dynamic-landing-pages.md).

## Save the line item

To finish adding the line item, click **Save** button.

You can also save and create another object. Click the dropdown arrow next to the **Save** button and select one of the following:

- **Save and Duplicate**. Save the current line item and immediately start a new line item with the same settings.
- **Save and Create Campaign**. Save the line item and immediately create a new campaign.
- **Save and Create New Line Item**. Save the line item and start a new line item under the same insertion order. This option preserves the IO context for each new line item created.

## Next steps

Once you've created a line item, you can set up campaigns to buy media for the advertiser and make good on your financial agreement. For a diagram of how line items interact with campaigns and the overall network configuration, see [Object Hierarchy](object-hierarchy.md).

## Related topics

- [Working with Line Items](working-with-line-items.md)
- [View Line Item Details](view-line-item-details.md)
- [Working with Advertisers](working-with-advertisers.md)
- [Working with Conversion Pixels](working-with-conversion-pixels.md)
