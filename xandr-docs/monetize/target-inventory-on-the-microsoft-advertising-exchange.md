---
title: Target Inventory on the Microsoft Advertising Exchange
description: Explore effective Microsoft Advertising Exchange targeting. Direct campaigns for better inventory utilization.
ms.date: 10/28/2023
---

# Target inventory on the Microsoft Advertising Exchange

> [!NOTE]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

This page shows you how to target a campaign to run on Microsoft Advertising Exchange inventory using Microsoft Monetize Monetize. You can target:

- All Microsoft Advertising web inventory
- Specific Microsoft Advertising "bins" for MSN inventory
- Specific domains for Microsoft Advertising web inventory in Denmark, Sweden, Norway, the Netherlands, Spain, Austria, Switzerland, India and South-East Asia

> [!TIP]
> For details on how to target Outlook.com, see [Buying Microsoft Outlook.com Inventory](buying-microsoft-outlook-com-inventory.md).

## Step 1. Open your campaign

On the Campaigns screen, select the campaign that you want to run on Microsoft Advertising inventory and click the **Edit** icon.

This will open the **Edit Campaign** screen.

## Step 2. Confirm the buying strategy

Microsoft Advertising is an external supply partner. Therefore, in the **Basic Settings** section under **Buying Strategies**, you should be sure to select **Buy Third-Party Inventory** and set a strategy. For detailed information about the strategies open to you, see [Buying Strategies](buying-strategies.md).

## Step 3. Turn off inventory quality filtering

Under **Inventory Quality**, the default settings allow only platform-reviewed inventory. Since some Microsoft Advertising inventory might not be platform-reviewed, the surest way to reach all the Microsoft Advertising inventory that you want to target is to allow your campaign to service on any inventory.

To do this, under **Inventory Quality**, select the **Serve on any inventory** radio button.

## Step 4. Confirm that universal categories and custom categories are not targeted

(Note that this only applies to non Microsoft Ads in Apps Inventory.)

Microsoft Advertising inventory cannot be targeted based on content category by most buyers. If you target any particular category, you will be excluding Microsoft Advertising inventory. Therefore, you should make sure that your campaign allows all categories.

Under Inventory, click the **Edit** button to open the **Inventory Targeting** dialog, then click **Universal Categories** and make sure it is set to **Any Universal Category** and **Custom Categories** is set to **Any Custom Category**.

## Step 5. Target Microsoft Advertising inventory

If you target all third-party inventory, your targeting will include all Microsoft Advertising inventory. However, if you want to focus on Microsoft Advertising, you **must** set more specific targets. This step walks you through the following options:

- [Option 1. Target all Microsoft Advertising web inventory](target-inventory-on-the-microsoft-advertising-exchange.md#option-1-target-all-microsoft-advertising-web-inventory)
- [Option 2. Target specific Microsoft Advertising MSN](target-inventory-on-the-microsoft-advertising-exchange.md#option-2-target-specific-microsoft-advertising-msn-bins)
- [Option 3. Target specific domains for Microsoft Advertising web inventory in Denmark, Sweden, Norway, the Netherlands, Spain, Austria, Switzerland, India and South-East Asia](target-inventory-on-the-microsoft-advertising-exchange.md#option-3-target-specific-domains-for-microsoft-advertising-web-inventory-in-denmark-sweden-norway-the-netherlands-spain-austria-switzerland-india-and-south-east-asia)
  
### Option 1. Target all Microsoft Advertising web inventory

In the **Inventory Targeting** dialog, under **3rd Party Inventory** \> **Sellers**, search for "Microsoft Advertising Exchange" seller. Include the seller **"Microsoft Advertising Exchange (280)"** by clicking on the green checkmark icon.

### Option 2. Target specific Microsoft Advertising MSN "bins"

To target specific Microsoft Advertising bins, follow the steps in **Option 1**, and then click on **Seller: Microsoft Advertising Exchange (280)** to expose a list of bins - named "Content Categories" on the Microsoft Advertising platform. You can then either **Include** the specific bins that you want to target or **Exclude** the specific bins that you do not want to target.

> [!IMPORTANT]
> For a complete list of MS Ad Exchange bins with descriptions, see [Microsoft Advertising Exchange Inventory](microsoft-advertising-exchange-inventory.md).
> [!TIP]
> **Targeting Microsoft Advertising and Other Third-Party Inventory**
>
> - If you want to target specific Microsoft Advertising bins and **all** other third-party inventory, the best method is to **Exclude** the specific Microsoft Advertising Exchange bins that you do not want to target (shown below).
> - If you want to target specific Microsoft Advertising bins and **some** other third-party inventory, the best method is to **Include** the specific Microsoft Advertising Exchange bins you want to target and **Include** other inventory at the **Seller** or **Custom Categories** level.

### Option 3. Target specific domains for Microsoft Advertising web inventory in Denmark, Sweden, Norway, the Netherlands, Spain, Austria, Switzerland, India and South-East Asia

To target these domains, under **Targeting** in the **Inventory Targeting** section, click the **Edit** button. This opens the **Inventory Targeting** dialog. Select **Specific Domains**, enter the domains you want to target, click the Add Domains button, then use the **Include** or **Exclude** buttons as appropriate.

## Step 6. Set additional targeting options

In the **Targeting** section, you can target users based on geography, segment, frequency, daypart, system, page properties, and demographics. In general, demographic and tag targeting are not recommended when targeting Microsoft Advertising, as they could inadvertently restrict your reach. For more information, see [Buy-Side Targeting](buy-side-targeting.md).

> [!IMPORTANT]
> **Combining Inventory Bin Targeting and Geography Targeting**
>
> Bins concern the location of the inventory, whereas geography targeting concerns the location of the user, based on information from the user's browser. For example, if you target a bin for Canadian inventory, and you target users in the Unites States, your campaign will serve only to US users who happen to be looking at that Canadian inventory.

## Step 7. Review and save your campaign

Once you have finished adjusting your campaign targeting, confirm that the details are correct and then click the **Save** button to save your changes.

> [!IMPORTANT]
> For additional details regarding targeting 24/7 inventory for MAX, see [Setting Up 24/7 Media Inventory Through the Microsoft Ad Exchange](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md).

## Related topics

- [Microsoft Advertising Exchange Inventory](microsoft-advertising-exchange-inventory.md)
- [Setting Up 24/7 Media Inventory Through the Microsoft Ad Exchange](setting-up-24-7-media-inventory-through-the-microsoft-ad-exchange.md)
