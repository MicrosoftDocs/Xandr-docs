---
title: Create a Custom Deal
description: Create tailored deals, specify sellers, buyer, inventory, geography, segments, sizes, and attributes. Buyers access deals via line items or campaigns.
ms.date: 10/28/2023
---

# Create a custom deal

As a seller, you can create a custom deal for a specific buyer that applies to specific inventory, geography, segments, impression sizes, or creative attributes. Once a deal is created, the buyer creates a line item or campaign to target the deal. For more information on how buyers target deals, see [Deal Targeting (ALI)](deal-targeting-ali.md) and [Create a Deal Campaign](create-a-deal-campaign.md).

> [!NOTE]
> Before you create a custom deal, you should communicate with the buyer to ensure you're using the correct buyer ID. If you plan to use a buyer seat ID from an external DSP, you should also check the Buyer Seat Migration Status reference table in [External DSPs Using Buyer Seat IDs](external-dsps-using-buyer-seat-ids.md).

<!--If you would like to create a package for buyers to browse and generate their own deals, see [Create a Package](create-a-package.md).-->

This page describes the properties you can define when creating a deal.

> [!NOTE]
> Clients of different types may see different options when creating a deal. This page covers all options in the create a deal workflow. If you do not have access to certain settings or options or have any other questions, please reach out to your Microsoft Advertising representative.
>
> If you are assigning a deal to a curator account, you must [create a deal line item](create-a-deal-line-item.md). Custom deals are not supported with curator members. See [Curated Deals](curated-deals.md) for more information.

## Start a new custom deal

You can start a new deal from two locations:

- From the Deals Screen
- From the Partnership Details Screen

### From the deals screen

On the **Deals** screen (**Partners** \> **Deals**), select the Buyers tab and click **New**.

### From the partnership details screen

On the **Partner Center** screen (**Partners** \> **Partner Center**), select the **Buyers** tab and click on the buyer for whom you'd like to create a deal. Then on the buyer's **Partnership Details** screen, click the number under **Deals** to display any current deals with the buyer and click **New**.

## Define deal details

Enter basic details for the new deal:

- **Name** - Enter the name for the deal.
- **Buyer** - If you are creating a deal from the **Deals** screen, select the buyer for whom you are creating the deal. Buyers can be listed using a Microsoft Advertising member ID or (for external DSPs) using a buyer seat ID. For more information, see [Understanding Buyer Seat IDs](understanding-buyer-seat-ids.md). Note that some seat IDs are visible but aren't yet eligible for bidding: check [External DSPs Using Buyer Seat IDs](external-dsps-using-buyer-seat-ids.md) for the latest information.
- **Code -** If you want to report on the deal using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code here.
- **Start Date -** Enter the start date for the deal.
- **End Date -** Enter the end date for the deal. This information is not required. A deal with no end date will be active until you cancel it.

  > [!NOTE]
  > Start and end date use the UTC date and time standard.

- **Currency** - Select the currency that will be used for the buyer's bid and the transaction of the deal.
- **Deal Type** - Select the auction type for the deal.
  - **Open Auction** - An open auction is similar to a regular RTB auction. The buyer will be competing with the larger pool of RTB buyers. Select **Open Auction** to allow the buyer to more easily target the deal inventory without giving the buyer's bid any preference over other RTB bids.
  - **Private Auction** - In a private auction, the buyer will only compete with other buyers who have a private auction deal for the impression. Select **Private Auction** to give the buyer preference over other RTB bids.
- **Auction Type** - Select the auction type for the deal.
  - **Standard Auction** - This is the standard auction type.
  - **Fixed Price** - If you select a fixed-price auction, you will need to enter an ask price. Any buyer who bids above this value will be eligible to bid on the deal. The winning buyer is responsible for the fixed price plus their fees.
    > [!NOTE]
    > The ask price for Fixed Price deals can now be updated after creation. Please notify the buyer of any price changes, as they will not receive an automated notification. Failing to inform buyers of price increases may halt their line items and impact your revenue flow.
- **Priority** - For a private auction only, you can assign certain higher priority to certain deals. Higher numbers mean higher priority and will always win an auction over a lower priority deal. The default priority setting is 5. Deal priority only applies to private auctions.
  
  For more information on the different auction types, see [Deal Auction Mechanics](deal-auction-mechanics.md).

- **Payment Type** - Select the payment type to be used for this deal:
  - **CPM** - every impression will result in payment.
  - **vCPM** (viewable impressions) - only impressions that are viewable will result in payment. An impression is determined to be viewable according to the viewability definition supported by the buyer. The viewability definition for this buyer will appear when this option is selected. You must select an **Ask Price** when the vCPM payment type is selected.

   > [!NOTE]
   > **vCPM** will soon be deprecated.

- **Ask Price** - Check the **Specify a price for this deal** checkbox if you would like to enter a price for the deal. You must enter an ask price for private auction deals.
  - **Market Price** - Select this for a Market Price deal. A Market Price deal does not have a deal-specific ask price. It uses a seller's yield management floors or open auction dynamics to determine the deal price.

  - **Specify an ask price** - Select this if you would like to enter a price for the deal. You must enter an ask price for private auction deals. Enter the price you would like the buyer to see in the **Ask Price** field. The system automatically deducts the revenue fee specified in your Microsoft Advertising contract to determine the amount you will receive (**Min. Revenue**).

    - **Ask Price** - This is the **Min. Revenue** plus any fees. This amount, which is visible to the buyer, is the minimum amount the buyer must bid in order to compete for this inventory.
    - **Fees** - The revenue share fees specified in your Microsoft Advertising contract.
    - **Min. Revenue** - The minimum amount you are willing to accept for this inventory. This amount is not visible to the buyer.

    > [!NOTE]
    > If you do not enter a deal-specific price, and the open auction type is selected, your existing floor rules may apply.

## Deal contents

Use the **Inventory**, **Geography**, **Segment**, **Size**, and **Device Type** sections to define the contents of the deal and where it will serve.

> [!TIP]
> Buyers cannot see the inventory or segments included. Use the **Description** field to give buyers insight into the contents.

## Select all of a seller's inventory

By default, **Run of Seller** is selected in the **Inventory** section. All of the seller's inventory will be included.

## Select specific categories of inventory

To include specific categories of inventory, select Category in the **Inventory** drop-down. Then click Edit to select the desired categories.

> [!TIP]
> You can select a combination of Universal Categories and Custom Categories.

When you have selected the categories to include in the package, click **Add** to return to the previous screen.

## Select all of a publisher's inventory

To include or exclude all of a publisher's inventory, select **Publisher** in the **Inventory** drop-down. Then click **Edit** to select the publishers you want to include or exclude.

When you have included/excluded the desired publishers, click **Add** to return to the previous screen.

## Select specific placement groups

To include or exclude specific sites, select **Placement Group** in the **Inventory** drop-down. Then click Edit to select the placement groups you want to include or exclude.

When you have included/excluded the desired placement groups, click **Add** to return to the previous screen.

## Select specific placements

To include or exclude specific placements, select Placement in the **Inventory** drop-down. Then click Edit to select the desired placements.

When you have included/excluded the desired placements, click **Add** to return to the previous screen.

## Select target geography

Click **Edit** button next to **Geography** to target deals based on the geographic location of the users.

> [!WARNING]
> Accuracy of Geographic Targeting
>
> Although geotargeting by country is highly accurate, the more specific the targeting, the more imprecise the results. This is especially true when targeting locations as granular as cities, metro codes, and zip codes. Also, depending upon which geographic targeting options you choose, you may significantly reduce the likelihood of a match.

**Target users by country, region, state, or city**

By default, you will target users in all geographic locations. On the **Country/Region/City** tab, however, you can narrow your targeting to include or exclude specific countries, regions/states, or cities.

- The **Countries** lists shows all of countries that can be targeted. You can either include or exclude countries or drill into a country to see its regions/states. Note that when you exclude a country, its regions and cities are not available for further inclusion or exclusion.

- **Regions** are more granular than countries. Generally speaking, regions are based upon whatever method the country in question uses to divide itself into parts. For example, regions within the United States are states. Canada is divided into its provinces, and India is divided into its states and union territories. The **Regions** lists
  shows all of the regions/states that can be targeted. You can either include or exclude regions/states or drill into a region/state to view its cities. Note that when you exclude a region, its cities are not available for further inclusion or exclusion.

- The **Cities** list shows all of the cities that can be targeted. You can either include or exclude cities.

   > [!TIP]
   > Click the column headers to sort counties, regions, or cities by name or ID, or use the search field to find a particular location.
  > [!WARNING]
  > Do not add conflicting geographic targeting at multiple levels. For example, if you are including the United States, Canada, and Mexico, and then you also
  > include U.S. metro codes, your campaign will only serve the U.S. metro codes targeted. In this scenario, metro code targeting will automatically limit the targeting to the U.S. only

  **Target users by metro code**

  Metro codes are only available for U.S. inventory. Available metro codes range from large cities such as New York, NY and Chicago, IL, to smaller cities such as Rochester, NY, Birmingham, AL, and Pittsburgh, PA.

  Unless you are excluding the **United States** from country targeting, you will target all metro codes by default. On the Metro Code tab, however, you can
  narrow your targeting to include or exclude specific metro codes.

  **Targeting summary**

  Use the Summary tab to review the geography targeting you have applied to this deal.

## Select specific segments

By default, any segment will be included. Click **Edit** to include specific segments. You can select segments in various ways:

- **To target users that are in a single segment** Drag the segments into a single segment group and select **Target any of the following segments**. This creates an OR relationship between the segments, which means that a user in any one of the segments is included.
- **To target users that are in multiple segments** Drag the segments into a single segment group and select **Target all of the following segments**. This creates an AND relationship between the segments, which means that a user must be in all of the segments to be included.
- **To target users in complex combinations of segments** Drag the segments into distinct segment groups. Select **Target and between segment groups** to create an AND relationship between segment groups and an OR relationship between segments within each group. Select Target or between segment groups to create an OR relationship between segment groups and an AND relationship between segments within each group.

> [!TIP]
> Buyers cannot see the segments you have selected. Use the description to give buyers insight into the type of segments that are included.

When you have selected the desired segments, click **Add** to return to the previous screen.

## Select specific creative sizes

By default, any size impression will be included. Click Edit to open the **Size** dialog, and then select the **Specific sizes...** option to select specific impression sizes to include. Click on a size within the **Standard Sizes** area to include it. You can **SHIFT** (or **CONTROL**) + click to select multiple sizes. You can enter any custom sizes within the width and height fields, and then click **Add Size to add it to the Custom Sizes section of the list.**

When you have selected the sizes to be included, click **Set** to return to the previous screen.

Check **Allow deal to include private sizes** to allow impressions from this deal to serve on the additional placement sizes that you have specified in the **Inventory Manager**.

If you allow private sizes, buyers won't see the additional sizes. Include the private sizes in the **Description** field.

## Select device type

Select which types of devices to target for the creatives. You can choose any combination of **Desktops & Laptops**, **Tablets**, and **Phones**.

## Allowed Creatives

Because they are special deals with buyers, deals can have access to a different set of creative attributes than for regular auctions. For example, deals can ignore the usual network ad quality settings of a regular auction. You can also restrict deals to specific brands, languages, categories, and technical attributes and approve or block
specific creatives.

Use the **Brand**, **Creative Category**, **Language**, **Specific Creatives**, **Trust Level**, **Media Types**, and **Technical Attributes** sections to set what types of creatives are allowed for the deal.

See [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md) for more information on how ad quality overrides work.

## Override brand ad quality settings

By default, deals follow network and publisher ad quality settings to determine which creatives associated with a brand will serve in a deal. You can create three different types of overrides:

- Restrict the deal to specific brands only
- Include all brands and ignore ad quality settings for them

Restrict the deal to specific brands and ignore ad quality settings for them

To create an override, click **Edit** in the **Brand** section, then use the **Brands** and **Ad Quality Settings** tabs to configure the type of override:

| Type of override | How to configure it |
|--|--|
| Restrict the deal to specific brands | On the **Brands** tab, click the brands you want to serve in the deal and click **Add**. |
| Include all brands, and ignore the ad quality settings | Do not click any brands on the **Brands** tab. On the **Ad Quality Settings** tab, click **Ignore** for the brands you want to serve, regardless of ad quality settings. |
| Restrict the deal to specify brands and ignore ad quality settings | On the **Brands** tab, click the brands you want to serve in the deal and click **Add**. On the **Ad Quality Settings** tab, click **Ignore** for the brands you want to serve, regardless of ad quality settings. |

> [!TIP]
> Remember, by default, your network and publisher ad quality settings are used to determine the brands that serve for a deal. Overrides are only needed if you want deals to have access to a different set of brands.

## Override creative category ad quality settings

By default, deals follow network and publisher ad quality settings to determine which categories of creatives (such as sports or computers) will serve in a deal. You can create three different types of overrides:

- Restrict the deal to specific categories only
- Include all categories and ignore ad quality settings for them

Restrict the deal to specific categories and ignore ad quality settings for them

To create an override, click **Edit** in the Creative Category section, then use the **Category** and **Ad Quality Settings** tabs to configure the type of override:

| Type of override | How to configure it |
|--|--|
| Restrict the deal to specific categories | On the **Category** tab, click the categories you want to serve in the deal and click **Add**. |
| Include all categories, and ignore the ad quality settings | Do not click any categories on the **Category** tab. On the **Ad Quality Settings** tab, click **Ignore** for the categories you want to serve, regardless of ad quality settings. |
| Restrict the deal to specify categories and ignore ad quality settings | On the **Category** tab, click the categories you want to serve in the deal and click **Add**. On the **Ad Quality Settings** tab, click **Ignor**e for the categories you want to serve, regardless of ad quality settings. |

> [!TIP]
> Remember, by default, your network and publisher ad quality settings are used to determine the categories that serve for a deal. Overrides are only needed if you want deals to have access to a different set of categories.

## Override language ad quality settings

By default, deals follow network and publisher ad quality settings to determine which creatives associated with a language will serve in a deal. You can create three different types of overrides:

- Restrict the deal to specific languages only
- Include all languages and ignore ad quality settings for them

Restrict the deal to specific languages and ignore ad quality settings for them

To create an override, click **Edit** in the Language section, then use the **Languages** and **Ad Quality Settings** tabs to configure the type of override:

| Type of override | How to configure it |
|--|--|
| Restrict the deal to specific languages | On the **Languages** tab, click the languages you want to serve in the deal and click **Add**. |
| Include all languages, and ignore the ad quality settings | Do not click any languages on the **Languages** tab. On the **Ad Quality Settings** tab, click **Ignore** for the languages you want to serve, regardless of ad quality settings. |
| Restrict the deal to specify languages and ignore ad quality settings | On the **Languages** tab, click the languages you want to serve in the deal and click **Add**. On the **Ad Quality Settings** tab, click **Ignore** for the languages you want to serve, regardless of ad quality settings. |

> [!TIP]
> Remember, by default, your network and publisher ad quality settings are used to determine the languages that serve for a deal. Overrides are only needed if you want deals to have access to a different set of languages.

## Override specific creatives

By default, deals follow network and publisher ad quality settings to determine which specific creatives will serve in a deal. You can also specifically block or allow individual creatives. Approved creatives will always be eligible to serve in the deal, regardless of any other ad quality or override. Blocked creatives will never serve, regardless of any other ad quality or override.

A maximum of 100 creative IDs can be approved or blocked.

> [!TIP]
> Use the [Creative Service](../digital-platform-api/creative-service.md) to locate individual creative IDs.
>
> - To always allow a specific creative, list the creative IDs, separated by commas, in the **Approve** box.
> - To always block a specific creative, list the creative IDs, separated by commas, in the **Block** box.

## Override trust level

By default, deals follow network ad quality settings to determine buyer trust level.

To allow deals to serve more creatives, click **Edit** in the Trust Level section and choose one of the following:

- **Default:** Default setting. If selected, this deal uses the existing publisher ad quality buyer trust level.
- **Allow pending creatives:** If checked, the default setting is used but creatives submitted for Microsoft Advertising audit in the "pending" state are allowed to serve. Once the audit is complete, the creative uses the default ad quality setting.
- **Maximum:** If selected, all creatives are allowed to serve for this deal (except for creatives specifically banned; see below).

## Set media types

By default, deals follow network ad quality settings to determine media types. To limit deals to a specific set of media types, click **Edit** in the **Media Types** section.

- On the **Media Types** tab, click the media types you want to allow for this deal. Selected media types appear in the right side of the dialog. You can deselect specific media subtypes for each of the main media types.
- Click the **Media Subtypes** tab to select specific media subjects (sorted by ID).
- Click **Set** to save your selections.

Check **Allow deal to include private media types** to allow impressions from this deal to serve on the additional media types that you have specified in the Inventory Manager.

> [!TIP]
> If you allow private media types, buyers won't see the additional media types. Include the private media types in the **Description** field.

## Override technical attributes ad quality settings

By default, deals follow network and publisher ad quality settings to determine which types of creative technical attributes (such as audio or expandable ads) will serve in a deal. You can ignore ad quality settings for specific technical attributes.

To create an override, click **Edit** in the **Technical Attributes** section. By default, all technical attributes are set to **Follow** existing ad quality settings. Click **Ignore** for the technical attributes you want to serve, regardless of ad quality settings.

> [!TIP]
> Remember, by default, your network and publisher ad quality settings are used to determine the technical attributes that serve for a deal. Overrides are only needed if you want deals to have access to a different set of technical attributes.

## Description

Enter a description for the deal. The buyer cannot see the **Inventory** or **Segment** columns, so it is important for you to be descriptive about the type of inventory the deal includes.

## Data protection

> [!WARNING]
> The **Data Protection** feature is not available to all clients. Contact your account representative for more information.

There may be instances when you want to define the amount of access buyers have to your property. The data protection options allow you to apply custom settings and specify ad servers for a deal.

## Data protection options

To apply custom data protection settings for the **Visibility** and **Add to Segment** options, select **Apply Custom Setting** to display these options.

## Visibility

Use the settings in the Visibility section of **Data Protection** to define what information will be viewable to the buyer. These settings determine what data the buyers
will see in your bid requests, and also what data the buyer will see in reporting.

- **User ID**: Determines whether the user ID is visible to the buyer. Possible settings are **Visible** and **Hidden**.
- **Device ID** - Determines whether the ID of the device the user is on is visible to the buyer. Possible settings are **Visible** and **Hidden**.
- **URL** - Determines whether the URL of the site is visible to the buyer. Possible values are:
  - **Full** - Buyer can view the full URL.
  - **Domain** - Buyer can see only the domain (i.e. [example.com](http://example.com)).
  - **Hidden** - Buyer cannot view the URL.

    > [!NOTE]
    >  Keep in mind that if you hide information from a buyer, that buyer will not be able to target on that information. For example, if you select **Hidden** for Device ID, the buyer won't be able to target your inventory based on the user's device.

> [!WARNING]
> **For members that have VAST Creative Data Protection enabled**: If you hide the User ID, Device ID, or URL, the tracking beacons attached to any video VAST creatives will not be able to view this information when loading these creatives. However, the tracking beacons will be able to still view the User ID, Device ID, or URL when loading from all other creative types (e.g., banner creatives). Reach out to your account manager to learn more about getting VAST Creative Data Protection enabled.

## Add to segment

Use the settings in the **Add to Segment** section of **Data Protection** to determine whether segment data can be gathered by this buyer.

- **On View** - Determines whether to allow any creative to serve that adds users to a segment on view. Possible values are **Allowed** and **Not Allowed**.
- **On Click** - Determines whether to allow any creative to serve that adds users to a segment on click. Possible values are **Allowed** and **Not Allowed**.

## Allow specific ad servers on deal

The **Allow Specific Ad Servers on Deal** option lets you identify specific sets of ad servers you want to allow to serve as part of this deal. (The ad servers in a list can be modified only through the API. See [Deal Service](../digital-platform-api/deal-service.md) for more information.)

To place ad server list protections on this deal, follow these steps:

1. Select the **Allow Specific Ad Servers on Deal** checkbox. This will display the **Select Ad Server List** drop-down.
1. Select an ad server list from the drop-down.

## Save the deal

When you have applied all of the settings for the new deal, click **Create** (or **Save** if you were editing an existing deal).
