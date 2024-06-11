---
title: Create a Package
description: In this article, find information on what packages are and how to create packages.
ms.date: 10/28/2023
---

# Create a package

Packages are pre-made combinations of your inventory and/or data. Buyers can create deals from your packages "off-the-shelf," or they can use your packages as a starting point for deal negotiations. This page walks you through the package creation process.

For instructions on creating a custom deal for one buyer instead of a package for multiple buyers, see [Create a Custom Deal](create-a-custom-deal.md). For insight into how buyers find and use your packages, see [Get Deals from Seller Packages](get-deals-from-seller-packages.md).

## Step 1. Start a new package

On the **Packages** screen (**Partners** > **Packages**), click the **Create New** button.

## Step 2. Enter basic details

In the **Basic Setup** section, enter a **Name** and **Description** for the package.

> [!TIP]
> Be sure to give your package an intuitive name and description. Buyers cannot see the inventory and segments included in your package, so these fields are very important for showcasing your package's content and value.

## Step 3. Define the package contents

In the **Package Contents** section, define the **Inventory**, **Segments**, and **Size** included in the package.

> [!TIP]
> Buyers cannot see the inventory or segments included. Use the **Description** field to give buyers insight into the contents.

### Select all of a seller's inventory

By default, **Run of Seller** is selected in the **Inventory** section. All of the seller's inventory will be included.

### Select specific categories of inventory

To include specific categories of inventory, select **Category** in the **Inventory** dropdown. Then click **Edit** to select the desired categories.

> [!TIP]
> You can select a combination of **Universal Categories** and **Custom Categories**.

When you have selected the categories to include in the package, click **Add** to return to the previous screen.

### Select all of a publisher's inventory

To include or exclude all of a publisher's inventory, select **Publisher** in the **Inventory** dropdown. Then click **Edit** to select the publishers you want to include or exclude.

When you have included/excluded the desired publishers, click **Add** to return to the previous screen.

### Select specific placement groups

To include or exclude specific sites, select **Placement Group** in the **Inventory** dropdown. Then click **Edit** to select the placement groups you want to include or exclude.

When you have included/excluded the desired placement groups, click **Add** to return to the previous screen.

### Select specific placements

To include or exclude specific placements, select **Placement** in the **Inventory** dropdown. Then click **Edit** to select the desired placements.

When you have included/excluded the desired placements, click **Add** to return to the previous screen.

### Select specific segments

By default, any segment will be included. Click **Edit** to include specific segments. You can select segments in various ways:

- **To target users that are in a single segment:** Drag the segments into a single segment group and select **Target any of the following segments**. This creates an OR relationship between the segments, which means that a user in any one of the segments is included.
- **To target users that are in multiple segments:** Drag the segments into a single segment group and select **Target all of the following segments**. This creates an AND relationship between the segments, which means that a user must be in all of the segments to be included.
- **To target users in complex combinations of segments:** Drag the segments into distinct segment groups. Select **Target and between segment groups** to create an AND relationship between segment groups and an OR relationship between segments within each group. Select **Target or between segment groups** to create an OR relationship between segment groups and an AND relationship between segments within each group.

> [!TIP]
> Buyers cannot see the segments you have selected. Use the description to give buyers insight into the type of segments that are included.

When you have selected the desired segments, click **Add** to return to the previous screen.

### Select specific creative sizes

By default, any size impression will be included. Click **Edit** to open the **Size** dialog, and then select the **Specific sizes...** option to select specific impression sizes to include. Click on a size within the **Standard Sizes** area to include it. You can shift or control+click to select multiple sizes. You can enter any custom sizes within the width and height fields, and then click **Add Size** to add it to the **Custom Sizes** section of the list.

When you have selected the sizes to be included, click **Set** to return to the previous screen.

Check **Allow deal to include private sizes** to allow impressions from this deal to serve on the additional placement sizes that you have specified in the **Placement Manager**.

> [!TIP]
> If you allow private sizes, buyers won't see the additional sizes. Include the private sizes in the **Description** field.

## Step 4. Set allowed creatives

By default, deals follow network and publisher ad quality settings to determine which creatives are available for a package. In the **Allowed Creatives** section, you can modify the package to use different ad quality settings for technical attributes (such as audio or expandable ads) and use a different set of media types.

### Override technical attribute ad quality

To override technical attribute ad quality settings, click **Edit** in the **Technical Attribute** section. By default, all technical attributes are set to **Follow** existing ad quality settings. Click **Ignore** for the technical attributes you want to serve, regardless of ad quality settings.

### Set media types

To limit deals to a specific set of media types, click **Edit** in the **Media Types** section.

1. On the **Media Types** tab, click the media types you want to allow for this deal. Selected media types appear in the right side of the dialog. You can deselect specific media subtypes for each of the main media types.
1. Click the **Media Subtypes** tab to select specific media subjects (sorted by ID).
1. Click **Set** to save your selections.

Check **Allow deal to include private media types** to allow impressions from this package to serve on the additional media types that you have specified in the **Placement Manager**.

## Step 5. Set the ask price

In the **Package Pricing and Visibility** section, specify the minimum price for the package contents. You have two options:

- **Market Price:** Select this option when you are using a package strictly to classify and differentiate inventory, for example, where you group your inventory into channels or verticals to expose them to buyers. Since buyers on external platforms such as Doubleclick or Mediamath cannot see content categories or placement IDs, this is a good way to allow external buyers to target a specific pool of your inventory.
- **Specify an ask price:** Select this option to create a package with an ask price higher or lower than the usual market price. An ask price higher than market price might be for a package that provides additional value to buyers, for example, where you provide extra targeting access privileges or first-party publisher data. An ask price lower than market price might be for a package that rewards buyers for adding value, for example, where buyers agree to a spend goal. For more information about setting a price, see [Deal Best Practices for Sellers](deal-best-practices-for-sellers.md).

## Step 6. Set custom pricing and visibility (optional)

You can enter custom pricing for selected buyers. You can also create a package that is only available to selected buyers.

### Select specific buyers

Click **Select Buyers**, choose the relevant buyers, and then click **Add** to return to the **Create New Package** area.

### Set custom pricing for each buyer

If you would like to define a custom price for the selected buyers, switch the **Custom Ask Price** toggle to **ON** and then enter a price. When viewing this package, the selected buyers will see their custom ask price. All other buyers will see the standard package price you have entered in the **Ask Price** field.

### Limit package visibility to the selected buyers

To make this package visible only to the selected buyers, check the **Only expose this package to the selected buyers** check box. The package will not be available to any other buyers.

## Step 7. Select the package status

In the **Status** section, select the desired package visibility.

- **Published:** The package is visible to buyers. Buyers can create deals from the package and target those deals.
- **Unpublished:** The package is not visible to buyers. Campaigns targeting associated deals continue to run unfettered.
- **Inactive:** The package is not visible to buyers. Campaigns targeting associated deals are prevented from bidding.

## Step 8. Save the package

To finish adding the package, click the **Save** button at the bottom of the page.

By default, your package is set to be part of an open auction, run indefinitely, and include any brand. Once buyers generate deals from the package, you can edit the auction type, flight dates, and included brands for their deals.
