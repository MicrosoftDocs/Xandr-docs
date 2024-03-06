---
title: Target Inventory on the Yahoo Ad Exchange
description: Explore optimizing Yahoo Ad Exchange campaigns, understand target inventory, set up effective campaigns for YAX inventory.
ms.date: 10/28/2023
---

# Target inventory on the Yahoo ad exchange

> [!NOTE]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

This page shows you how to set up a campaign to run on Yahoo Ad Exchange (YAX) inventory.

> [!NOTE]
> YAX Marketplace
>
> Clients who have been migrated to the the latest version of the Yahoo Ad Exchange, the YAX Marketplace, can target the entire YAX seller but can no longer target "Seller Lines" or specific YAX inventory.
> [!TIP]
> If you have negotiated deals with YAX, see [Create a Deal Campaign](create-a-deal-campaign.md). For information about negotiating deals with YAX, see [Negotiate Deals with Sellers](negotiate-deals-with-sellers.md).

## Before you begin

### Access to YAX

Buyers that do not have access to the Yahoo Ad Exchange through Microsoft Advertising will not see the YAX seller for targeting. For information about gaining access to YAX, please speak with your Microsoft Advertising representative.

### Creative requirements

Each creative that you want to serve on YAX inventory must meet the following requirements:

- The creative must meet YAX's [size requirements](https://developer.yahooinc.com/native/guide/native-ad-specs/matrix-view/)
- The creative must meet YAX's [language requirements](https://asia.adspecs.yahooinc.com/pages/policies-guidelines/yahoo-ad-policy/creative-content-guidelines/language)
- The creative format must be flash, image, raw-js, raw-html, iframe-html, or url-html.
- The creative template must be a Standard template.
- You must submit the creative for [auditing](creative-standards.md) and it must pass.
- If you want the creative to serve on secure YAX inventory, you must submit the creative for Microsoft Advertising SSL audit, and it must pass.
  
## Step 1. Open your campaign

On the **Campaigns** screen, select the campaign that you want to run on your Yahoo Ad Exchange inventory and click the **Edit** icon.

This will open the **Edit Campaign** screen.

## Step 2. Confirm the buying strategy

Yahoo Ad Exchange is an external supply partner. Therefore, in the **Basic Settings** section under **Buying Strategies**, you should be sure to select **Buy Third-Party Inventory** and set a strategy. For detailed information about the strategies open to you, see [Buying Strategies](buying-strategies.md).

## Step 3. Target Yahoo ad exchange inventory

If you target all third-party inventory, your targeting will include all Yahoo Ad Exchange inventory as well as all other third-party inventory. However, if you want to focus on YAX, you **must** set more specific targets.

First, in the **Targeting** section under **Inventory**, click **Edit**.

This will open the **Inventory Targeting** dialog.

## Option 1. Target all Yahoo ad exchange inventory

In the **Inventory Targeting** dialog, under **3rd Party Inventory** \> **Sellers**, search for "273". Include the seller called **Yahoo Ad Exchange (273)** by clicking on the green checkmark icon.

## Option 2. Target specific Yahoo ad exchange "Seller lines"

> [!NOTE]
> Clients who have been migrated to the the latest version of the Yahoo Ad Exchange, the YAX Marketplace, can target the entire YAX seller but can no longer target "Seller Lines" or specific YAX inventory.

To target specific Yahoo Ad Exchange "Seller Lines", click on "Yahoo Ad Exchange (273)" and either **Include** the specific "Seller Lines" that you want to target or **Exclude** the specific "Seller Lines" that you do not want to target.

> [!TIP]
> **Targeting Yahoo Ad Exchange "Seller Lines" and Other Third-Party Inventory**
>
> - If you want to target specific Yahoo Ad Exchange "Seller Lines" and **all** other third-party inventory, the best method is to **Include** the Yahoo Ad Exchange seller, then **Exclude** the "Seller Lines" that you do not want to target.
> - If you want to target specific Yahoo Ad Exchange "Seller Lines" and **some** other third-party inventory, the best method is to **Include** "Yahoo Ad Exchange (273)" and any other seller that you do want to target and then, under **Publishers & Categories**, **Exclude** the specific "Seller Lines" that you do not want to target.

## Step 4. Adjust your inventory quality filtering

We recommend removing inventory quality filtering when targeting the Yahoo Ad Exchange. Some of the inventory in your "Seller Lines" might not be platform-reviewed. If you are nonetheless confident that your "Seller Lines" are of acceptable quality, the surest way to reach all of the inventory is to disable inventory quality filtering. In particular,
Yahoo O&O inventory is not platform-reviewed.

In the **Targeting** section under **Inventory Quality**, select the **Serve on any inventory** radio button.

## Step 5. Set additional targeting options

In the **Targeting** section, you can further restrict your campaign to target users based on geography, segment, frequency, daypart (day of week and time of day), system (browser and operating system), page properties, and demographics. For more information about targeting, see [Buy-Side Targeting](buy-side-targeting.md).

> [!TIP]
> Since all additional targeting is respected, please be careful not to inadvertently restrict your campaign's reach. For example, if a Yahoo Ad Exchange "Seller Line" covers Yahoo! US and you then use Geography targeting to target just users in Canada, your campaign will likely not serve any impressions.

## Step 6. Review and save your campaign

Once you have finished adjusting your campaign targeting, confirm that the details are correct and then click the **Save** button to save your changes.
