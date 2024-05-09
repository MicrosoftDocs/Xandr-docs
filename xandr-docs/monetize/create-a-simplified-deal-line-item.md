---
title: Create a Simplified Deal Line Item
description: Explore the process of creating a simplified Deal Line Item, either from scratch or with a template. Also, learn about the various settings and targeting options associated with it.
ms.date: 04/29/2024
---

# Create a simplified Deal Line Item

> [!NOTE]
> This feature is currently in **Beta** and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

Publishers using Microsoft Monetize can utilize Deal Line Items to set up deals with their advertisers. This helps them offer the latest features available on the Microsoft Monetize platform to their buyers.

## Prerequisites

Before you begin, ensure that you've created the objects that hold all your deals. It's recommended to complete this step only once, as we advise creating all your Deal Line Items under the same Advertiser and Insertion Order for efficiency. If you haven't done this yet, follow the steps outlined in the pages below:

- [Advertiser](create-an-advertiser.md)
- [Seamless Insertion Order](create-an-insertion-order.md): Create an Insertion Order with **Flexible Budget Type**, **No End Date**, **Unlimited Budget**, **Set pacing on the line item** settings.

> [!NOTE]
> Legacy insertion orders aren't supported with the Deal Line Item. The settings you select on the insertion order applies to *all* line items under the insertion order.

## Create a Deal Line Item from scratch

You can create a new Deal Line Item from the **Line Items** screen.

1. Go to **Advertisers > Line Items**.
1. On the **Line Items** screen, select **Deal Line Item** from the **+ New** drop-down menu.
1. Select the **Create from Scratch** option under **Creation Mode**. If you wish to create a new deal from template, see [Create a Deal Line Item from template](#create-a-deal-line-item-from-template).
1. Search (by name or ID) and select the desired Advertiser and Insertion Order for the respective **Advertiser** and **Insertion Order** fields.

    > [!TIP]
    > - When you select the **Make Default Advertiser** and **Make Default Insertion Order** checkboxes, the form automatically saves the Advertiser and Insertion Order details. This information is pre-populated for future deal creation. However, you can still modify it if necessary.
    > - The Advertiser and Insertion Order details are saved locally and will be cleared when you clear your browser's cookies.
1. Select **Next**.

### Basic settings

In the **Basic Settings** section, enter the following details for the Deal Line Item:

- **Deal Name**: Enter a deal name (this deal name is transparent to the buyer).
- **Deal Code**: Enter the deal code (optional, typically used by external sellers for deal mapping).
- **Deal Description**: Enter a description for your deal (this description is transparent to buyers).

#### Deal details

The **Deal details** section offers a detailed overview of the key components that define your deal.

- **Buyer**: Select a buyer for the deal by clicking on the **Edit (pencil icon)** option under **Buyer**. From the **Buyer** screen, choose an available buyer by searching their name or ID.

    > [!TIP]
    > If the list of buyers is extensive, select the **DSP** first before searching for the **Buyer** to narrow down the options.
- **Deal Trust Level**: Specifies the level of audit status you want to permit for creatives to serve on a deal. For more information, see the **Trust Level** section in [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md).
- **Ad Type**: Select the type of ad you plan to offer. You can select more than one ad type. Possible values are **Banner**, **Video**, **Native**, and **Audio**.
    > [!NOTE]
    >
    > - When you select ad types **Video**, **Native**, and **Audio**, the default ad size is set to 1x1. However, if you select multiple ad types, such as including the **Banner** ad type, ensure that you include the banner ad size as well.
    > - Selecting **Ad Type** determines the availability of other settings (e.g.,**Targeting \>  Completion Rate Threshold**).
    > - **Ad Type** selections automatically sync with the **Media Type** of deal impressions.
- **Ad Size**: Select one or more standard sizes, choose from existing custom sizes, or create a new custom ad size according to your requirements. To create a custom ad size:
    1. Select the **Custom** tab.
    1. Select **Add Size**.
    1. Enter the appropriate values for the **Width** and **Height** fields.
    1. Select **Add Size for this Deal** to apply the custom ad size for this specific deal. Alternatively, select the **Add Size and Save Size to Member** option from the drop-down menu to save your custom ad size for future use.
    1. Select **Save**.
- **Deal Priority**: Specifies the deal's ranking in the auction. When a deal is created as **Private Auction**, the buyer's bid takes precedence over open exchange. When a deal priority is created as **Open Auction**, the buyer competes with bids from the open exchange.
  - **Priority Level**: This advanced feature offers the flexibility to prioritize deals within the auction. A higher priority number supersedes a lower one. The selectable priority range is preset based on your **Private Auction** or **Open Auction** selection. Every deal is assigned a default priority, reducing the need for frequent changes.
  
    > [!NOTE]
    > If you're using Microsoft Monetize for creating other Line Item types (GDALI, ALI, etc.), this priorioty system is shared across all Line Item types.
- **Pricing Strategy**: Specifies the price agreed upon by the advertiser. You can select one of the following revenue types:
  - **Floor Price**: Enter the hard floor price that will apply to the buyer of the deal.
  - **Fixed Price**: Enter the amount that the advertiser will pay you per thousand impressions.
    > [!NOTE]
    > You can now modify a **Fixed Price** even after saving the Deal Line Item.
  - **Market Price**: Select this option to use yield management floors if they are available; if they are not available, no floors will be applied to the auction.

#### Deal targeting

A Deal Line Item has the following targeting options:

- **Device Type**: Select the devices you plan to target. You can select more than one device type. Possible values are **Desktops & Laptops**, **Tablets**, **Mobile**, and **CTV**. For more information, see [Device Type Targeting](device-type-targeting-ali.md).
- **Inventory Type**: Set which inventory types you wish to target. You can select one or all of the following inventory types:
  - **Web**: To run on standard websites and those optimized for browsers on mobile devices.
  - **App**: To run in applications installed on mobile tablets, phones, and Windows 8 devices.
- **Inventory Targeting**: Select **Edit (pencil icon)** to select the inventory you wish to target or exclude.
- **Key/Value Targeting**: Define your own keys and their corresponding values to make full use of publisher data and help advertisers reach their intended audience. For more information, see [Key/value Targeting](key-value-targeting.md).
- **Segment Targeting**: Set which first-party or third-party segments you wish to target. For more information, see [Segment Targeting](segment-targeting.md).
- **Geography Targeting**: Target impressions based on the geographic location of the users viewing them. For more information, see [Geography Targeting](geography-targeting.md).

### Advanced settings

In the **Advanced Settings** section, enter any optional advanced settings that are useful.

#### Video targeting

When you set **Video** as your **Ad Type**, the **Video Targeting** section automatically appears as the first section in **Advanced Settings**.

- **Video Player Targeting**: Target video inventory based on the position, playback method, player width, video framework, and creative duration. For more information, see [Video Player Targeting](video-player-targeting.md).
- **Completion Rate Threshold**: Select the **Completion Rate Threshold** checkbox and enter a percentage to sell inventory based on their predicted video completion. <!-- Need to confirm "sell inventory". -->

#### Advanced targeting

The **Advanced Targeting** section offers advanced settings and targeting options to ensure your deal reaches the intended audience.

- **Blocklist**: Search and select a blocklist (by default, the Microsoft Advertising blocklist is always applied). Any inventory in the blocklists you apply for is automatically excluded and not bid on by this Deal Line Item. You can select from network/member-level blocklists or [Inventory Lists](inventory-lists-ali-only.md) directly from the Deal Line Item. Once applied, you can also view or export the blocklist.
- **Allowlist**: Search and select an allowlist you would like to apply to this Deal Line Item. You can select from network/member-level allowlists or [create an allowlist](inventory-targeting-ali.md) directly from the Deal Line Item. Once applied, you can also view or export the allowlist.
   > [!NOTE]
   > The use of Inventory Lists (e.g., allowlists, blocklists) constrains whatever **Inventory Type** selections you make. For example, if you target an allowlist, the **Inventory Type** option you select is limited to only those domains/apps in that allowlist. If you target a blocklist, the **Inventory Type** option you select serves everything but the domains/apps in that blocklist.
- **Viewability Threshold**: Select the **Viewability Threshold** checkbox and enter a percentage to sell inventory based on their predicted viewability. <!-- Need to confirm "sell inventory". -->
- **System targeting**: Target users based on their operating systems, browsers, language, device model, or carrier. For more information, see [System targeting](system-targeting.md).
- **Demographics**: Target specific segments of the audience based on characteristics such as age and gender. For more information, see [Demography targeting](demography-targeting.md).
- **Page properties**: Target impressions based on the position of the creative tag on the page or based on values passed in the query string of the ad call. For more information, see [Page properties targeting](page-properties-targeting.md).
- **Frequency and Recency**: A frequency cap is the total number of ads shown to a user. A recency cap is the pace at which ads are shown to a user. **Frequency and Recency** caps can be set on Deal Line Items (as well as on the parent insertion order and advertiser). To apply frequency and recency caps, set the Frequency and Recency toggle to **Caps on** and enter the appropriate **Frequency** and **Recency** settings. For more information, see [Frequency and Recency Caps](frequency-and-recency-caps.md).
- **Ads.txt**: Select this checkbox to only target web inventory authorized in a publisher's ads.txt file.
- **COPPA**: Select this checkbox to only target COPPA-compliant inventory.

#### Budgeting and scheduling

The **Budgeting and Scheduling** section reflects a specific agreement between you and the advertiser.

- **Budget Type**: As most deals are created under a **Flexible Insertion Order**, you can choose either **Revenue** or **Impressions** as the **Budget Type** at the Deal Line Item level.

  > [!NOTE]
  >
  > - When you create a Deal Line Item, it inherits its budget type from the parent insertion order, and this impacts the revenue types available on the Deal Line Item. For example, if the budget type of an insertion order is **Impressions**, the child Deal Line Item can only set up budgets using impressions.
  > - If you can't view the options at the Deal Line Item level, it's due to a specific **Budget Type** set in the parent insertion order.<!-- Need to confirm "specific". -->
- **Budget**: Set the Deal Line Item's **Budget**. Select **Unlimited Budget**, **Lifetime Budget**, or **Daily Budget**. The unit of the budget is determined by the **Budget Type**.

  > [!NOTE]
  > Budget settings are acting only as a cap as Deal Line Items are not pacing.<!-- Need to confirm this note. -->

  - If you select **Lifetime Budget**, then select one of the following:
    - **Set Lifetime**: Enter a lifetime budget for the Deal Line Item. This will be the total budget available to the Deal Line Item for all its flight dates. The Deal Line Item will keep sending requests to the buyer until the budget runs out.
    - **Set Per Flight**: When selected, a **Budget** field displays each of the Deal Line Item's flight dates in the **Flights** section. Use the **Flights** field to set the budget for the flight dates.
  - If you select **Daily Budget**, enter the maximum daily budget to use.
- **Flights**: Flights permits you to create limited deals with start and end dates, and “evergreen deals” with no end date. To create one or more flights:

  1. Select either **Set Dates** or **No End Date**. If the **Lifetime Budget** is set, then the **No End Date** option isn't available for selection.

     - **Set Dates**: Enter a **Start Date** and **End Date** for each of the Deal Line Item's flights. The hour settings for **Start Date** and **End Date** defaults to **12:00 AM** and **11:59 PM**, respectively (you can override the defaults). Flights might not overlap with one another. All flight dates must fall within the billing period dates of the parent insertion order and be a minimum of one day in duration. In addition, if you selected **Lifetime Budget \>  Set Per Flight** in the **Budget** section, you must enter a value for the **Budget** of each flight.
     - **No End Date**: Enter the **Start Date** for the Deal Line Item. You might not create additional flights for this Deal Line Item because it has no end date.
  1. Select **Add Another Flight** if you want additional flights. This option is not available if you select **No End Date**.

    > [!NOTE]
    >
    > You cannot change the **Start Date** or the **End Date** of a flight once that date has passed. You can add multiple flights to any Deal Line Item.
  
- **Daypart Targeting**: Target users based on the day and time when they see impressions. For more information, see [Daypart targeting](daypart-targeting.md).

#### Deal ad quality

The **Deal Ad Quality** section defines ad quality settings you wish to establish for a particular network and publisher.

- **Creative Review**: Select the **Only allow seller-approved creatives** checkbox to ensure that only creatives that you explicitly approve will run.
- **Creative Attributes**: Edit the creative attributes for a deal. To edit the following creative attributes, select **Edit** under each attribute, choose the appropriate values, and then select **Set**. For more information, see [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md).

  - **Brand**
    - **Brand** tab: Only selected brands will be allowed to serve; any brands not selected will not be allowed. If no brands are selected, all brands that follow ad quality rules are allowed.
    - **Ad Quality Settings** tab: Select the brands for which you want to override ad quality settings. When you select **Ignore**, the brand will be allowed on the deal despite ad quality settings. All brands defaults to **Follow**, so they comply with ad quality settings.
  - **Language**
    - **Language** tab: Only selected languages will be allowed to serve; any languages not selected will not be allowed. If no languages are selected, all languages that follow ad quality rules are allowed.
    - **Ad Quality Settings** tab: Select the languages in which you want to override ad quality settings. When you select **Ignore**, the language will be allowed on the deal despite ad quality settings. All languages defaults to **Follow**, so they comply with ad quality settings.
  - **Creative Category**
    - **Creative Category** tab: Only selected creative categories will be allowed to serve; any creative categories not selected will not be allowed. If no creative categories are selected, all creative categories that follow ad quality rules are allowed.
    - **Ad Quality Settings** tab: Select the creative categories in which you want to override ad quality settings. When you select **Ignore**, the creative category will be allowed on the deal despite ad quality settings. All creative categories defaults to **Follow**, so they comply with ad quality settings.
  - **Specific Creatives**: Include specific creatives to either **Approve** (always allow) or **Block** (always block) the deal.
  - **Media Type**: Select the media types you want to include on the deal.
    > [!NOTE]
    > **Ad Type** selections automatically sync with the **Media Type** of deal impressions.
  - **Technical Attributes**: Select the technical attributes on which you want to override ad quality settings. When you select **Ignore**, the technical attribute will be allowed on the deal despite ad quality settings. All technical attributes defaults to **Follow**, so they comply with ad quality settings.

#### Reporting labels and comments

In the **Reporting Labels and Comments** section, you can optionally assign custom reporting labels (**Trafficker**, **Sales Rep**, **Line Item Type**, and **OMS ID**) to a Deal Line Item. You can also add comments to a Deal Line Item for your reference. Reporting labels let you associate a person or other metadata with advertisers. You can then run reports using these labels. For more information, see [Reporting Guide](reporting-guide.md).

#### Associated objects

The **Associated Objects** section defines objects and entities that are associated with the Deal Line Item.

- **Line Item Name**: Enter the name for the line item (this name isn't visible to buyers). If this field is empty, the Line Item will be automatically named the same as the Deal.
- **Advertiser Summary**: Review your preselected advertiser details and make changes if needed. However, once the deal is created and saved, you cannot change the advertiser.
- **Insertion Order Summary**: Review your preselected insertion order details and make changes if needed, even after creating and saving the deal.

### Deal summary

The **Deal Summary** pane offers a detailed overview of the deal, dynamically populated with the selected form settings. This view facilitates an efficient review of key deal parameters, reducing the likelihood of errors and ensuring clarity in deal execution.

> [!NOTE]
> By default, the **Deal Summary** pane displays the required fields that must be configured.

### Save the Deal Line Item

Select **Save** to save the Deal Line Item, or **Save and Duplicate** if you wish to duplicate this Deal Line Item.

> [!NOTE]
> Using **Save and Duplicate** is the preferred method for duplicating Deal Line Items.

## Create a Deal Line Item from template

You can also create a new deal by selecting the **Create from Template** option under **Creation Mode**.

1. Go to **Advertisers > Line Items**.
1. On the **Line Items** screen, select **Deal Line Item** from the **+ New** drop-down menu.
1. On the **Create New Deal** screen, select the **Create from Template** option under **Creation Mode**.
1. Use the **Deal Template Selection** field to search and select a deal template using either a Line Item ID or name.
1. Review the summary of settings and select **Select This Template**. This action applies all the template settings to your deal settings.
1. Review the settings and summary of your deal, and then select **Save** to save the Deal Line Item. Alternatively, select **Save and Duplicate** if you wish to duplicate this Deal Line Item.
