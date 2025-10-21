---
title: Microsoft Monetize - Buy Mobile Inventory via RTB
description: This page is a step-by-step guide to set up a campaign to run on third-party mobile inventory (also known as "RTB" inventory). 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Buy mobile inventory via RTB

> [!NOTE]
> The descriptions in this topic apply only to Standard Line Items (not available in Invest). A new version of this document that is applicable to Invest and Augmented Line Items will be available at a later date.

This document describes how to set up a campaign to run on third-party mobile inventory (also known as "RTB" inventory). RTB inventory is made available for sale by other members of the Microsoft Advertising platform; this includes ad networks and major publishers as well as external partners and exchanges that are integrated with Microsoft Advertising.

For more information on how to buy directly from mobile publishers, see [Buy Mobile Inventory Directly from a Publisher](buy-mobile-inventory-directly-from-a-publisher.md). For answers to frequently asked questions, see the [Mobile Buying FAQ](mobile-buying-faq.md).

Creating a mobile campaign involves defining:

- **Supply Type** - Whether you want to buy mobile app inventory, web inventory optimized for mobile devices, or both.

- **Media Budget** - How much you are willing to spend on buying mobile media (in dollars or impressions).

- **Buying Strategies** - Buying via RTB means you want to run on in-app and/or device-optimized web inventory from other networks on the Microsoft Advertising platform as well as external supply sources. For RTB buys, you define exactly how you want to value impressions and submit bids.

- **Learn Budget** - How much you are willing to spend on optimizing your campaign (in dollars or impressions). Learn budget only applies when buying third-party inventory using a strategy involving optimization.

- **Targeting** - What specific inventory you want to run on and how precisely you want to target users (via system, frequency, segments, geography, etc.).

  For mobile campaigns, **system targeting** is one of the most useful ways to reach users. You can include or exclude users via the types of devices they use (phone, tablet, pc), their device makes and models (i.e., Apple iPhone, HTC Droid Incredible, etc.), their operating systems, the browsers on their devices, and their mobile carriers and connection types (carrier-based or wifi/static). For details, see [System Targeting](system-targeting.md).

  > [!NOTE]
  > Inventory Quality does not apply to in-app inventory. Mobile campaigns will deliver on in-app inventory regardless of your campaigns Inventory Quality setting.
  
## Step 1. Start a new campaign

On the **Advertiser Details** screen, click **Create New** \>  **Campaign**.

You can find **Create New** \> **Campaign** on the insertion order, line item, and campaign screens under the advertiser as well.

This opens the initial **Create New Campaign** screen.

## Step 2. Select the parent line item

In the **Select a Line Item** section, select the line item under which you want to create your campaign and then click **Continue**. If you are creating your campaign directly from a line item or there is only one line item associated with the advertiser, the line item is selected by default.

You can use the search field to find a particular line item by name or ID. Also, all active and inactive line items are listed by default, but you can use the filter to the right of the search field to show just active or inactive line items.

## Step 3. Select the campaign type

In the **Campaign Type** section, select **Buy direct/third-party inventory**. This will reveal the full workflow for setting up a campaign.

You can expand or collapse each section of the screen as you like. To expand or collapse all sections at once, click the **Expand All** or **Collapse All** link in the upper right.

> [!NOTE]
> Changing the campaign type will reset your workflow and available targeting options.

## Step 4. Enter basic details and flight dates

In the **Basic Setup** section, enter the basic details and flight dates for the campaign.

- **Name** - Enter the name for the campaign. You will later be able to search for and report on the campaign using this name.
- **External Code** - If you want to report on the campaign using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code here.
- **State** - The state is set to "Inactive" by default to prevent the campaign from spending before all necessary settings and creatives are complete. You can set the state to "Active" at any time.
- **Flight Dates** - Set the start for the campaign and set an end date or select **Run Indefinitely**. Note that the time format (12-hour or 24-hour) and time zone are inherited from the advertiser. Enter or select the start and end dates and times for the campaign.
  
  > [!NOTE]
  > If flight dates are set for the parent line item, those dates take precedence; regardless of the dates set for the campaign, the campaign will not start before the line item start date and will not continue buying impressions after the line item end date. To further limit serving to specific days and hours of the week, you can use [Daypart Targeting](daypart-targeting.md).

## Step 5. Set the campaign budget

By default, your campaign media **Budget** is unlimited. If you prefer, you can define exactly how much you are willing to spend on buying inventory for the campaign. The budget can be in impressions or in media cost (dollars). Note that media cost is in USD rather than the advertiser's currency because USD is the currency in which Microsoft Advertising transacts.

You can set budgets at the insertion order and line item levels as well. Budgets at these levels take precedence over a child campaign's budget; if they run out, the campaign will stop buying impressions, whether or not it has reached its own budget. For more details about budgeting, see [Budgeting and Pacing](budgeting-and-pacing.md).

- **Lifetime** - This is the budget that you are willing to spend over the entire lifetime of the campaign. There are two options:
  - **Custom** - Select this option to enter a specific amount of impressions or dollars.
  - **Unlimited** - Select this option to leave your lifetime budget undefined.

    > [!NOTE]
    > If **Lifetime** budget is set to **Unlimited** and the line item and insertion order lifetime budgets are also set to **Unlimited** severe overspend can occur.

- **Daily** - This is the budget that you are willing to spend on any single day. There are three options:
  - **Custom** - Select this option to enter a specific amount of impressions or dollars. When you enter a custom daily budget, you must select one of the following options:
    - **Pace evenly throughout the day** - Select this option, otherwise known as "daily pacing", if you want to prevent your daily budget from being spent all at once by distributing your spend evenly by hour throughout the day. Note that if you use Daypart Targeting to restrict the hours during which the campaign can serve, daily pacing will adjust to distribute your spend evenly across only the targeted hours. For more details, see [Daypart Targeting](daypart-targeting.md) or [Daily Pacing](daily-pacing.md).
    - **Spend as fast as possible** - Select this option if you do not want to pace your daily budget at all. Note that this option could lead to your entire daily budget being spent in a very short amount of time.
  - **Pace Lifetime Budget** - Select this option to spread your lifetime budget evenly across your flight dates. As each day passes, the system spreads the remaining impression or media cost budget across the remaining days of the flight.
    - The system is not able to pace its spending if it does not have a budget amount, and the system must know the number of days in the campaign in order to apply the remaining budget amount equally for the remainder of the flight. Therefore, this option requires that you enter a custom lifetime budget and select an end date. For more details, examples, and best practices, see [Lifetime Pacing](lifetime-pacing.md).
  - **Unlimited** - Select this option to leave your daily budget undefined.

    > [!NOTE]
    > If you have enabled the unlimited budget warning feature, you will not be able to set the budget for your campaign to **unlimited** if the line item and (if applicable) insertion order budgets are also set to unlimited. This feature prevents mistaken overspend that can result when budgets are set to unlimited at all levels. When the feature is enabled, to set your campaign budget to unlimited, you must first limit the budget for either the insertion order or line item associated with the campaign. To enable this feature, speak to your Microsoft Advertising representative.

## Step 6. Define the buying strategies

### Buy third-party inventory

To run the campaign on inventory from other members of the Microsoft Advertising platform and from external partners and exchanges (also known as **RTB** inventory), check the **Buy Third-Party Inventory** box. Then decide how you want to pay for third-party inventory (per impression, per click, and/or per conversion) and define exactly how you want to calculate your bids. Note that the revenue type of the parent line item determines which buying strategy options are available and, of those available, which are recommended. For a detailed explanation of your options, see [Buying Strategies](buying-strategies.md).

Post-view conversions cannot currently be tracked across Safari mobile browsers or in apps. If you use the "Optimize to a predicted CPA goal" strategy, please do so only for post-click scenarios. For more information about why this is so, see [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md).

Post-click conversion tracking works in mobile browsers just like it does in web browsers. In mobile apps, however, post-click conversions can be tracked only when the user performs the action (the conversion) from an app's built-in web view. After clicking an ad in an app, if the user converts in a separate mobile browser (after having closed the app), the correlation to the click in the app cannot be tracked.

When your line item booked revenue is CPM but you want your campaign to optimize to a CPC or CPA goal, for best results, set a **Performance Goal** on your line item and use **Optimize to a % Margin of Booked Revenue** as your campaign buying strategy. For more information, please see [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md). To learn about setting up **Performance Goals** on the line item, see Step 6 of [Create a Line Item](create-a-standard-line-item.md).

### Pay on a Per-impression (CPM) basis

Select this option to pay publishers for every impression. This payment type is accepted by all sellers (Microsoft Advertising sellers and external sellers).

- **Optimize to a % margin of booked revenue**

  Use this strategy to bid a % margin of the revenue that the advertiser pays you. For example, if your booked revenue is $1 CPM, and you set a bidding strategy margin of 25%, your campaign will bid $0.75. If your booked revenue type is a CPA or CPC goal, it will apply your desired margin and optimize to that predicted goal.

  - **Bid CPM: max_$ CPM min \_ $ CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
  - **Enable Cadence Modifier** - Under **OTHER OPTIONS**, check this box to vary your bid based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently.

- **Optimize to a predicted CPA goal**

  Use this strategy to vary bids based on the likelihood of an attributed conversion for each piece of inventory. This strategy uses the Microsoft Advertising optimization engine.

  - **Bid $_ _ post-click/post-view CPA** - Select the conversion pixel to which you want to optimize and enter the dollar amount per conversion that you want the optimization engine to aim for.
  - **Learn Budget** - The learn budget is the portion of your campaign budget that you want to commit to optimizing your campaign, which helps you quickly find slices of third-party inventory that provide a positive ROI. The first phase of this process is called Learn. You can set a lifetime learn budget of up to 100% of the campaign budget as well as a daily cap for learning.
  - **Bid at most $ _     CPM in Learn Phase** - When your campaign starts to spend on new inventory, the optimization engine submits "learn" bids. If necessary, enter max CPM dollar amount for these bids.
    > [!NOTE]
    > When you set both a cap for learn bids and a max CPM for non-learn bids (next option), the lower of the two will be used for learn.
  - **Bid CPM: max $_CPM min $_CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
  - **Enable Cadence Modifier** - This option appears under **OTHER OPTIONS** and cannot be deselected. When optimizing to a predicted CPA goal, your bids will always vary based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently.

- **Optimize to a predicted CPC goal**

  Use this strategy to vary bids based on the likelihood of a click for each piece of inventory. This strategy uses the Microsoft Advertising optimization engine. {expand:Expand to see more options}

  - **Optimize to $ _ _ per click** - Enter the dollar amount per click that you want the optimization engine to aim for when calculating bids.
  - **Learn Budget** - The learn budget is the portion of your campaign budget that you want to commit to optimizing your campaign, which helps you quickly find slices of third-party inventory that provide a positive ROI. The first phase of this process is called Learn. You can set a lifetime learn budget of up to 100% of the campaign budget as well as a daily cap for learning.
  - **Bid at most $ _ _ CPM in Learn Phase** - When your campaign starts to spend on new inventory, the optimization engine submits "learn" bids. It is recommended to enter a max CPM dollar about for these bids. In doing so, you will avoid learning on inventory that is too expensive while not limiting yourself from optimized inventory sources that are worth higher prices.
  
    > [!NOTE]
    > When you set both a cap for learn bids and a max CPM for non-learn bids (next option), the lower of the two will be used for learn.

  - **Bid CPM: max$ _ CPM min $ _ CPM**- Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
  - **Enable Cadence Modifier** - This option appears under **OTHER OPTIONS** and cannot be deselected. When optimizing to a predicted CPA goal, your bids will always vary based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently.

- **Bid a base $ __  CPM** - Use this strategy to bid a fixed dollar amount.

- **Base CPM $ _ _** - Enter the fixed dollar amount to bid per thousand impressions.

- **Enable Cadence Modifier** - Under **OTHER OPTIONS**, check this box to vary your bid based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently.
  - **Bid CPM: max$ _ CPM min $ _ CPM** - This option is available under **OTHER OPTIONS** only once you enable Cadence Modifier. Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.

**Target reach and delivery (bid via ECP or EAP)**

Use this strategy to bid the going platform rate for each piece of inventory.

- **Auto-bid to win most platform impressions (ECP)** - Select this option to bid an estimate of the price that is likely to win most impressions from Microsoft Advertising platform sellers based on historical bids and their success or failure. Since off-platform sellers (e.g., Google Ad Manager, Rubicon, etc.) conduct a secondary auction, bidding ECP does not necessarily ensure winning off-platform impressions.
- **Auto-bid to win ~50% of platform impressions (EAP)** - Select this option to bid an estimate of the price that is likely to win about half of the impressions from Microsoft Advertising platform sellers based on historical bids and their success or failure. Since off-platform sellers (e.g., Google Ad Manager, Rubicon, etc.) conduct a secondary auction, bidding EAP does not necessarily ensure winning half of off-platform impressions.
- **Bid CPM: max$ _ CPM min $ _ CPM** - Enter the highest and lowest CPM dollar amount that you are willing to spend on an impression.
- **Enable Cadence Modifier** - Under **OTHER OPTIONS**, check this box to vary your bid based on how often and recently users have seen your creatives. This feature is based on the idea that an ad is more effective (and therefore worth more) when a user hasn't seen it before or hasn't seen it many times or seen it recently.
- **Pay on a Per-click (CPC) basis** - Select this option to pay publishers only when users click on your ads. This payment type is accepted only by participating Microsoft Advertising sellers, not by external sellers; using it exclusively may therefore decrease your campaign's reach.
- **Pay $ _ per click** - Enter the dollar amount to pay a publisher when a user clicks on one of your ads.
- **Pay on a Per-conversion (CPA) basis** - Select this option to pay publishers only when users convert. This payment type is accepted only by participating Microsoft Advertising sellers, not by external sellers; using it exclusively may therefore decrease your campaign's reach.
- **Pay $ _** **post-click/post-view CPA** - For each selected conversion pixel, enter the dollar amount to pay a publisher when a viewed or clicked ad leads to a conversion.

## Step 7. Show to users without cookies

To target users that you have not seen before and users who have cleared their cookies, check the **Show to users without cookies** box under **Buying Strategies**  \> **OTHER OPTIONS**.

> [!NOTE]
> If using frequency targeting fo this campaign, you must also check the **Show to users without cookies** box in the **Frequency** section of the **Targeting** area. For more details, see [Frequency and Recency Caps](frequency-and-recency-caps.md).

Your campaign will show ads to users without cookies by default when conversion tracking is enabled at the line item level (one or more conversion pixels are attached to the line item). In this case, targeting users without cookies is not the default because we cannot attribute conversions back to an impression view or click when users do not have cookies.

Targeting cookieless users does not affect mobile app targeting. Almost all in-app inventory has a device ID associated with it; this device ID is then associated with one of our platform cookies.

For mobile web campaigns, checking **Show to users without cookies** is currently the only way to serve ads to Safari users, since Safari disables third-party (advertising) cookies by default.

## Step 8. Set optimization levers

If your buying strategy uses the Microsoft Advertising optimization engine, you can adjust **Optimization Levers** to influence how optimization works for your campaign, for example, how much you bid during the Learn phase, how many success events (clicks or conversions) it takes to move from the Learn phase to the Optimized phase, as well as whether you want to optimize to the campaign bidding strategy before optimizing to the line item booked revenue.

To access optimization levers, click the **Edit** button under **Buying Strategies** \>  **OTHER OPTIONS**. For detailed explanations of each lever, see [Optimization Levers](optimization-levers.md).

If you do not have access to optimization levers and are interested in learning more about about them, please contact your Microsoft Advertising account representative.

## Step 9. Add targeting

In the **Targeting** section, you can [Apply a Targeting Template](apply-a-targeting-template.md) or set unique inventory and user targeting for this campaign. Use the links below to learn more about each type of targeting.

- [Target Inventory](#target-inventory)
- [Target Users](#target-users)

When you apply multiple types of targeting (e.g., inventory, segment, geography, etc.), keep in mind that your campaign will buy only impressions that match all targeting. In other words, there is an AND relationship between the main types of targeting. For example, if you target seller 123, segment ABC, and the United States, your campaign will bid only on impressions from that seller being viewed by users in that segment and in the United States.

### Target inventory

You can target inventory in numerous ways. Use the links below to learn more about each type of inventory targeting.

- [Inventory Quality Targeting](inventory-quality-targeting.md)
- [Content Category Targeting](content-category-targeting.md)
- [Third-Party Inventory Targeting](third-party-inventory-targeting.md)
- [Domain Targeting](domain-targeting.md)
- [App Targeting](app-targeting.md)
- [Page Properties Targeting](page-properties-targeting.md)

> [!NOTE]
> The majority of mobile supply is external. Although some supply partners categorize their inventory, note that including categories will exclude all uncategorized mobile supply from your campaign.

### Target users

You can target users in numerous ways. Use the links below to learn more about each type of user targeting.

- [Device and Supply Type Targeting](supply-type-targeting.md)
- [Geography Targeting](geography-targeting.md)
- [Segment Targeting](segment-targeting.md)
- [Frequency and Recency Caps](frequency-and-recency-caps.md)
- [Daypart Targeting](daypart-targeting.md)
- [System Targeting](system-targeting.md)
- [Demography Targeting](demography-targeting.md)
- [Test and Control Targeting](test-and-control-targeting.md)

## Step 10. Associate creatives and define a dynamic landing page

In the **Associated Creatives** section, you can select a **Creative Rotation** to determine how you want to rotate and weight multiple creatives. Select one of three options:

- **Evenly weight creatives** (default): Even rotation is handled automatically by our system.

- **Auto-optimize creative weight**: When this option is chosen, 75% of delivery is allocated to the creative with the highest click-through rate; all remaining creatives of the same size receive equal allocations of the remaining 25% of overall delivery.

- **Manually weight creatives**: By selecting this option, you will be able to manually set a weight (between 0 and 1000).

  See [Creative Rotation](creative-rotation-standard-line-item-and-guaranteed-delivery-line-item.md) for more information.

Click **Edit** and select the creatives that you want to run for the campaign. Also, if you want to define a dynamic landing page to be used by multiple creatives associated to the campaign, enter the **Landing Page URL** and then make sure the creatives are set up to use a dynamic landing page. Note that you can set a dynamic landing page at the line item level as well. For more details, see [Dynamic Landing Pages](dynamic-landing-pages.md).

> [!TIP]
> If you prefer, you can associate creatives to the campaign at a later time. For more details, see [Associate Creatives to Campaigns](associate-creatives-to-campaigns.md).

## Step 11. Enter comments

In the **Comments** section, enter any comments that you would like to record with the campaign. Comments are for your reference only and will not affect campaign delivery.

## Step 12. Add serving fees

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

   > [!IMPORTANT]
   > Per broker, you can add no more than one CPM serving fee and one Cost Share serving fee.

## Step 13. Review and save your campaign

Confirm that the campaign details are correct and then click the **Save** button to finish adding the campaign to Microsoft Advertising. The campaign is then added to the list of campaigns on the [Explore Campaigns](explore-campaigns.md) screen.

## Step 14. Complete peer approval

> [!TIP]
> When activated for a user at the network level, the campaign peer approval feature requires a user to get approval from a second user before campaigns can be set to **Active**. This feature minimizes the risk of user-side errors in campaign activation and can help users identify and change settings to improve campaign performance.
> [!NOTE]
> This step applies only to clients who have enabled the peer approval feature for their users. To learn more about enabling peer approval for users, see [Create a User](create-a-user.md).
>
> The campaign peer approval feature sets requirements for who must obtain peer approval, but not who can approve campaigns. Any other user who is able to create campaigns for your network may provide this approval. There is no way to designate a single approver of others' campaigns.

If your campaigns use the peer approval feature, in order to switch a campaign's status from Inactive to Active, you will need peer approval from another user. In the **Create New Campaign** screen in the **Approved By** field, you will see a message alerting you to the need for peer approval and will be unable to save the campaign in an active state.

To approve the campaign, another user from your team must log in, go to the **Campaigns** screen, select the desired campaign and click **Edit**. This will open the **Edit Campaign** screen. On the **Edit Campaign** screen, the alternate user must check the **Approved By** checkbox. Once this step is completed, the campaign can be set to **Active** by any user on your team.

## Next steps

Once you've created a campaign, you can view all its details on the [View Campaign Details](view-campaign-details.md). You can also continue associating creatives to the campaign. For more details, see [Associate Creatives to Campaigns](associate-creatives-to-campaigns.md).

## Related topics

- [Buy Mobile Inventory Directly from a Publisher](buy-mobile-inventory-directly-from-a-publisher.md)
- [Mobile Buying FAQ](mobile-buying-faq.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)