---
title: Yahoo Buying Guide
description: Learn how to access and target Xandr inventory in Yahoo DSP, including deal registration, campaign setup, and targeting options.
ms.date: 10/28/2023
---

# Yahoo buying guide

In partnership with Yahoo DSP, Xandr has created this page to help Xandr publishers communicate with their buyers about accessing and targeting Xandr’s publisher inventory using Yahoo DSP. This information has been created in collaboration with and approved by the Yahoo DSP team. Note that platforms can and will change regularly. We will do our best to update this guide as needed. Wherever possible, we've provided links to Yahoo DSP documentation.

We recommend that if buyers are experiencing issues or need assistance using the Yahoo DSP platform, their first point of outreach should be the Yahoo DSP support team.

## Target Xandr in Yahoo DSP

This section explains how to create campaigns and lines in **Yahoo DSP** and target Xandr inventory.  

### Set Up a campaign and line  

To run campaigns in **Yahoo DSP**, you need to create a campaign and set up a line. The following sections outline the steps.

#### Create a campaign

Every line belongs to a specific campaign and inherits default settings (time zone, currency, budget) from the campaign.

To create your first campaign:

1. Click the **Advertisers** icon on the pane in the DSP UI.
1. On the **Advertisers** page, select the advertiser for which you want to create the campaign.

   :::image type="content" source="media/yahoo-advertisers.png" alt-text="Screenshot that explains how Yahoo advertisers help you create a campaign.":::

   - The **Campaigns** page for that advertiser appears.
   - On the **Campaigns** page, you can create a new campaign manually or bulk upload multiple campaigns.
  
1. To create a campaign manually, click the **New Campaign** button.

   :::image type="content" source="media/yahoo-automotive-advertiser.png" alt-text="Screenshot explains how to creat a campaign manually.":::.

1. Enter the campaign name in the **Campaign Name** field.
1. To activate your campaign, move the **Status** slider to the right. If you no longer want the campaign to serve, move the slider back to the left.

   :::image type="content" source="media/yahoo-advertisers-campaign-status-slider.png" alt-text="Screenshot that explains how to use the status slider when you are ready to activate your campaign.":::.

1. Set the **time zone** and **flight dates**.
1. Set the **currency**, **budget**, and **daily budget**.
1. For a single-schedule campaign, leave the slider at **Single** in the **Schedules** area.

   :::image type="content" source="media/yahoo-ad-schedule-single.png" alt-text="Screenshot that explains how to set a single-schedule campaign when activate the campaign.":::.

1. Set the **target KPI** for the campaign.
1. Click **Save Campaign** to complete the setup.

## Create your first line

You create and manage lines on the **Lines** list view.

### To create your first line

1. Select **Advertisers** on the left pane of DSP UI.

   :::image type="content" source="media/create-your-first-line-advertisers.png" alt-text="Screenshot that shows how to select Advertisers tab on the left pane of DSP UI.":::.

1. Select the link for the advertiser you are working with.

   :::image type="content" source="media/link-advertisers.png" alt-text="Screenshot that explains how to select the link for the advertiser.":::.

   The **Campaigns** page appears.

   :::image type="content" source="media/yahoo-partner-manager-advertiser.png" alt-text="Screenshot that shows the Campaign page.":::.

1. On the **Campaigns** page, select the link for the campaign you are working with or create a new one.
    The **Lines** page appears.

   :::image type="content" source="media/campaigns-line-page.png" alt-text="Screenshot that shows the Campaign Lines page.":::.

   > [!NOTE]
   > A line can only have one channel where the channel represents the type of media used to build the line’s creatives. As you are setting up the line, you’ll select the channel type at the top of the page.

1. Select a **Channel Type** for your line:

   - **Display**
   - **Video**
   - **Connected TV**
   - **Native**

   :::image type="content" source="media/campaign-create-new-line.png" alt-text="Screenshot that shows channel type for your line and complete the rest of the line or ad setup.":::.

Complete the rest of the line/ad setup.

## Targeting Xandr inventory

A line in your campaign can target or block one or more exchanges or available private marketplace deals. There are specific rules about line item targeting of exchanges and deals.

### To target exchanges and deals

1. Within your line, navigate to the **Targeting** page and in the **Exchanges and Deals** section, select a radio button to target either exchanges or deals.

   :::image type="content" source="media/exchanges-deals.png" alt-text="Screenshot that displays Exchanges and Deals section.":::.

    > [!NOTE]
    > You can select either **Exchanges** or **Deals**, but not both.

    Do one of the following:

    - Select **Exchanges** to target on one or more Yahoo or third-party exchanges.
    - Select **Deals** to target a private marketplace deal.

1. From the drop-down list, select **Target** or **Block** to determine whether you want to target or block your selected exchanges or deals.
1. Search for your first exchange or deal from the drop-down list:
    a. If you selected **Exchanges**, start typing the name of an exchange to find it.
    b. If you selected **Deals**, start typing the name of an exchange, deal name, deal ID, or exchange deal ID to find the deal you want to target.

    > [!IMPORTANT]
    > Before targeting a deal to a line, register the deal. See the [Create a Deal](Yahoo-buying-guide.md#create-a-deal) section below to learn how to create new deals or search for existing deals in the Registered Deals Dashboard.

1. Add the exchange or deal to the targeting criteria by clicking the **plus sign** next to the exchange or deal name.

   :::image type="content" source="media/exchanges-deals-targeting-criteria.png" alt-text="Screenshot that shows how to add the exchange or deal to the targeting criteria.":::.

1. Continue adding exchanges or deals until you have added all the ones you want.

### Additional Targeting Features

You can also target inventory on a more granular level using:

- **App/Site list**
- **Ad Position** (Display lines only)
- **Player Size** (Video lines only)
- **Ad Initiation** (Video lines only)
- **Video Ad Placement** (Video lines only)
- **Video Content Length** (Video lines only)
- **Ads.txt & App-ads.txt Declaration**
- **Mobile Placement Types**
- **Mobile Measurability**
- **Inventory Quality Targeting**, including:
  - **Bot avoidance** (blocks fraud and malware sites)
  - **Viewability** (targets highly viewable inventory)
  - **Contextuals** (targets or blocks specific categories of interest to advertisers)

## Create a Deal

From the **Registered Deal Dashboard** page, you can drill down to deals available under different supply sources. You can also create a shared deal or exclusive deal on a particular exchange.

### To create a new deal

1. Select **Inventory** in the left pane of the UI.
1. Select **Registered Deals Dashboard**.

    :::image type="content" source="media/create-a-new-deal.png" alt-text="Screenshot that explains how to create a new deal.":::.

    > [!NOTE]
    > Only **non-guaranteed deals** can be created.

1. Click **Create New Deal** or use the search/filter box to find existing deals.

   :::image type="content" source="media/create-a-new-deal-search-filterbox.png" alt-text="Screenshot that explains how to create a new deal or how to use search or filter box to find the existing deals.":::.

1. On the **New Deal Page**, enter the necessary information and click **Create Deal**.

   :::image type="content" source="media/save-deal.png" alt-text="Screenshot that explains how to save a  deal after adding the necessary information.":::.

1. After registering the deal, navigate to the **Targeting** page for a line to which the deal is available and add it to the targeting criteria.
