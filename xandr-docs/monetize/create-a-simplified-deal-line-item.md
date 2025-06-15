---
title: Create a Simplified Deal Line Item
description: Explore the process of creating a simplified deal line item, either from scratch or with a template. Also, learn about the various settings and targeting options associated with it.
ms.date: 06/16/2025
---

# Create a simplified deal line item

Publishers using Microsoft Monetize can utilize deal line items to set up deals with their advertisers. This helps them offer the latest features available on the Microsoft Monetize platform to their buyers.

## Prerequisites

Before you begin, ensure that you've created the objects that hold all your deals. It's recommended to complete this step only once, as we advise creating all your deal line items under the same advertiser and insertion order for efficiency. If you haven't done this yet, follow the steps outlined in the pages below:

- [Advertiser](create-an-advertiser.md)
- [Seamless insertion order](create-an-insertion-order.md): Create an insertion order with **Flexible Budget Type**, **No End Date**, **Unlimited Budget**, **Set pacing on the line item** settings.

> [!NOTE]
> Legacy insertion orders aren't supported with the deal line item. The settings you select on the insertion order applies to *all* line items under the insertion order.

## Create a deal line item from scratch

You can create a new deal line item from the **Line Items** screen.

1. Go to **Advertisers > Line Items**.
1. On the **Line Items** screen, select **Deal Line Item** from the **+ New** drop-down menu.
1. Select the **Create from Scratch** option under **Creation Mode**. If you wish to create a new deal from a template, see [Create a deal line item from a template](#create-a-deal-line-item-from-a-template).
1. Search (by name or ID) and select the desired advertiser and insertion order for the respective **Advertiser** and **Insertion Order** fields.

    > [!TIP]
    > - When you select the **Make Default Advertiser** and **Make Default Insertion Order** checkboxes, the form automatically saves the advertiser and insertion order details. This information is pre-populated for future deal creation. However, you can still modify it if necessary.
    > - The advertiser and insertion order details are saved locally and will be cleared when you clear your browser's cookies.
1. Select **Next**.

### Basic settings

In the **Basic Settings** section, enter the following details for the deal line item:

- **Deal Name**: Enter a deal name. This deal name is transparent to the buyer.
- **Deal Code**: Optional, enter the deal code to report on a deal using your own code. The code might contain alphanumeric characters, periods, underscores, or dashes. The code you enter must be unique, and it is not case-sensitive (uppercase and lowercase characters are treated the same). No two line items can use the same code per advertiser. This feature is typically used by external sellers for deal mapping.
- **Deal Description**: Enter a description for your deal. This description is transparent to buyers.

#### Deal details

The **Deal Details** section offers a detailed overview of the key components that define your deal.

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
  - **Priority Level**: This advanced feature offers the flexibility to prioritize deals within the auction. A higher priority number supersedes a lower one of the same deal priority auction type (private deals will always have priority over open deals regardless of the priority level). The selectable priority range is preset based on your **Private Auction** or **Open Auction** selection. Every deal is assigned a default priority, reducing the need for frequent changes.
  
    > [!NOTE]
    > If your member is also running guaranteed campaigns in the Monetize Ad Server, private deals will, by default, be assigned a priority level lower than the member’s reselling priority. This is due to the fact that all line item types operate within a unified priority framework, and this configuration helps mitigate the risk of underdelivery for guaranteed campaigns.
    > Although the **Prioritize above all** else setting remains available—allowing a private deal to be placed above the member’s reselling priority—its use is strongly discouraged when there are GDALIs configured at a lower priority. Enabling this setting may jeopardize the delivery of those guaranteed line items. To better understand how priority settings impact the auction logic, please refer to this page for a detailed explanation.

- **Pricing Strategy**: Specifies the price agreed upon by the advertiser. You can select one of the following revenue types:
  - **Floor Price**: Enter the hard floor price that will apply to the buyer of the deal.
  - **Fixed Price**: Enter the amount that the advertiser will pay you per thousand impressions.
    > [!NOTE]
    > You can now modify a **Fixed Price** even after saving the deal line item.
  - **Market Price**: Select this option to use yield management floors if they are available; if they are not available, no floors will be applied to the auction.

#### Deal targeting

A deal line item has the following targeting options:

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
- **Completion Rate Threshold**: Select the **Completion Rate Threshold** checkbox and enter a percentage to sell inventory based on their predicted video completion.

#### Advanced targeting

The **Advanced Targeting** section offers advanced settings and targeting options to ensure your deal reaches the intended audience.

- **Blocklist**: Search and select a blocklist (by default, the Microsoft Advertising blocklist is always applied). Any inventory in the blocklists you apply for is automatically excluded and not bid on by this deal line item. You can select from network/member-level blocklists or [Inventory Lists](inventory-lists-ali-only.md) directly from the deal line item. Once applied, you can also view or export the blocklist.
- **Allowlist**: Search and select an allowlist you would like to apply to this deal line item. You can select from network/member-level allowlists or [create an allowlist](inventory-targeting-ali.md) directly from the deal line item. Once applied, you can also view or export the allowlist.
   > [!NOTE]
   > The use of Inventory Lists (e.g., allowlists, blocklists) constrains whatever **Inventory Type** selections you make. For example, if you target an allowlist, the **Inventory Type** option you select is limited to only those domains/apps in that allowlist. If you target a blocklist, the **Inventory Type** option you select serves everything but the domains/apps in that blocklist.
- **Viewability Threshold**: Select the **Viewability Threshold** checkbox and enter a percentage to sell inventory based on their predicted viewability.
- **System targeting**: Target users based on their operating systems, browsers, language, device model, or carrier. For more information, see [System targeting](system-targeting.md).
- **Demographics**: Target specific segments of the audience based on characteristics such as age and gender. For more information, see [Demography targeting](demography-targeting.md).
- **Page properties**: Target impressions based on the position of the creative tag on the page or based on values passed in the query string of the ad call. For more information, see [Page properties targeting](page-properties-targeting.md).
- **Frequency and Recency**: A frequency cap is the total number of ads shown to a user. A recency cap is the pace at which ads are shown to a user. **Frequency and Recency** caps can be set on deal line items (as well as on the parent insertion order and advertiser). To apply frequency and recency caps, set the **Frequency and Recency** toggle to **Caps on** and enter the appropriate **Frequency** and **Recency** settings. For more information, see [Frequency and Recency Caps](frequency-and-recency-caps.md).
- **Ads.txt**: Select this checkbox to only target web inventory authorized in a publisher's ads.txt file.
- **COPPA**: Select this checkbox to only target COPPA-compliant inventory. For more information, see [Set up line item inventory and brand safety](set-up-line-item-inventory-and-brand-safety.md).

#### Budgeting and scheduling

The **Budgeting and Scheduling** section reflects a specific agreement between you and the advertiser.

- **Budget Type**: As most deals are created under a **Flexible Insertion Order**, you can choose either **Revenue** or **Impressions** as the **Budget Type** at the deal line item level.

  > [!NOTE]
  >
  > - When you create a deal line item, it inherits its budget type from the parent insertion order, and this impacts the revenue types available on the deal line item. For example, if the budget type of an insertion order is **Impressions**, the child deal line item can only set up budgets using impressions.
  > - If you can't view the options at the deal line item level, it's due to a specific **Budget Type** set in the parent insertion order.
- **Budget**: Set the deal line item's **Budget**. Select **Unlimited Budget**, **Lifetime Budget**, or **Daily Budget**. The unit of the budget is determined by the **Budget Type**.

  > [!NOTE]
  > Budget settings act only as a cap, as deal line items aren't pacing.

  - If you select **Lifetime Budget**, then select one of the following:
    - **Set Lifetime**: Enter a lifetime budget for the deal line item. This will be the total budget available to the deal line item for all its flight dates. The deal line item will keep sending requests to the buyer until the budget runs out.
    - **Set Per Flight**: When selected, a **Budget** field displays each of the deal line item's flight dates in the **Flights** section. Use the **Flights** field to set the budget for the flight dates.
  - If you select **Daily Budget**, enter the maximum daily budget to use.
- **Flights**: Flights permits you to create limited deals with start and end dates, and “evergreen deals” with no end date. To create one or more flights:

  1. Select either **Set Dates** or **No End Date**. If the **Lifetime Budget** is set, then the **No End Date** option isn't available for selection.

     - **Set Dates**: Enter a **Start Date** and **End Date** for each of the deal line item's flights. The hour settings for **Start Date** and **End Date** defaults to **12:00 AM** and **11:59 PM**, respectively (you can override the defaults). Flights might not overlap with one another. All flight dates must fall within the billing period dates of the parent insertion order and be a minimum of one day in duration. In addition, if you selected **Lifetime Budget \>  Set Per Flight** in the **Budget** section, you must enter a value for the **Budget** of each flight.
     - **No End Date**: Enter the **Start Date** for the deal line item. You might not create additional flights for this deal line item because it has no end date.
  1. Select **Add Another Flight** if you want additional flights. This option is not available if you select **No End Date**.

    > [!NOTE]
    >
    > You cannot change the **Start Date** or the **End Date** of a flight once that date has passed. You can add multiple flights to any deal line item.
  
- **Daypart Targeting**: Target users based on the day and time when they see impressions. For more information, see [Daypart targeting](daypart-targeting.md).

#### Deal ad quality

The **Deal Ad Quality** section defines ad quality settings you wish to establish for a particular network and publisher.

- **Creative Review**: Select the **Only allow seller-approved creatives** checkbox to ensure that only creatives that you explicitly approve will run.
- **Creative Attributes**: Edit the creative attributes for a deal. To edit the following creative attributes, select **Edit** under each attribute, choose the appropriate values, and then select **Set**. For more information, see [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md).

  - **Brand**
    - **Brand** tab: Only selected brands will be allowed to serve; any brands not selected will not be allowed. If no brands are selected, all brands that follow ad quality rules are allowed.
    - **Ad Quality Settings** tab: Select the brands for which you want to override ad quality settings. When you select **Ignore**, the brand will be allowed on the deal despite ad quality settings. All brands default to **Follow**, so they comply with ad quality settings.
  - **Language**
    - **Language** tab: Only selected languages will be allowed to serve; any languages not selected will not be allowed. If no languages are selected, all languages that follow ad quality rules are allowed.
    - **Ad Quality Settings** tab: Select the languages in which you want to override ad quality settings. When you select **Ignore**, the language will be allowed on the deal despite ad quality settings. All languages default to **Follow**, so they comply with ad quality settings.
  - **Media Type**: Select the media types you want to include on the deal.
    > [!NOTE]
    > **Ad Type** selections automatically sync and pre-populate the **Media Type** selection of deal impressions.
  - **Creative Category**
    - **Creative Category** tab: Only selected creative categories will be allowed to serve; any creative categories not selected will not be allowed. If no creative categories are selected, all creative categories that follow ad quality rules are allowed.
    - **Ad Quality Settings** tab: Select the creative categories in which you want to override ad quality settings. When you select **Ignore**, the creative category will be allowed on the deal despite ad quality settings. All creative categories default to **Follow**, so they comply with ad quality settings.
  - **Specific Creatives**: Include specific creatives to either **Approve** (always allow) or **Block** (always block) the deal.
  - **Technical Attributes**: Select the technical attributes on which you want to override ad quality settings. When you select **Ignore**, the technical attribute will be allowed on the deal despite ad quality settings. All technical attributes default to **Follow**, so they comply with ad quality settings.

#### Reporting labels and comments

In the **Reporting Labels and Comments** section, you can optionally assign custom reporting labels (**Trafficker**, **Sales Rep**, **Line Item Type**, and **OMS ID**) to a deal line item. You can also add comments to a deal line item for your reference. Reporting labels let you associate a person or other metadata with advertisers. You can then run reports using these labels. For more information, see [Reporting Guide](reporting-guide.md).

#### Associated objects

The **Associated Objects** section defines objects and entities that are associated with the deal line item.

- **Line Item Name**: Enter the name for the line item (this name isn't visible to buyers). If this field is empty, the line item will be automatically named the same as the deal.
- **Advertiser Summary**: Review your pre-selected advertiser details and make changes if needed. However, once the deal is created and saved, you cannot change the advertiser.
- **Insertion Order Summary**: Review your pre-selected insertion order details and make changes if needed, even after creating and saving the deal.

### Deal summary

The **Deal Summary** pane offers a detailed overview of the deal, dynamically populated with the selected form settings. This view facilitates an efficient review of key deal parameters, reducing the likelihood of errors and ensuring clarity in deal execution.

> [!NOTE]
> By default, the **Deal Summary** pane displays the required fields that must be configured.

### Save the deal line item

Select **Save** to save the deal line item, or **Save and Duplicate** if you wish to duplicate this deal line item.

> [!NOTE]
> Using **Save and Duplicate** is the preferred method for duplicating deal line items.

## Create a deal line item from a template

This feature enables publishers to create a new deal line item using an existing deal as a template. The following sections outlines the three ways to accomplish this task.

### Use the pre-selection screen

You can create a new deal line item from the pre-selection screen by selecting the **Create from Template** option under **Creation Mode**.

1. Go to **Advertisers > Line Items**.
1. On the **Line Items** screen, select **Deal Line Item** from the **+ New** drop-down menu.
1. On the **Create New Deal** screen, select the **Create from Template** option under **Creation Mode**.
1. Use the **Deal Template Selection** field to search and select a deal template using either a Line Item ID or name.
1. Review the summary of settings and select **Select This Template**. This action applies all the template settings to your deal settings.
1. Review your deal settings and summary, make any necessary updates, and then select **Save** to save the deal line item. Alternatively, select **Save and Duplicate** if you wish to duplicate this deal line item.

### Use the monitoring grid view

1. Search for the deal line item you wish to use as a template.
1. In the **Line Name** column, hover over the deal line item, and two icons will appear. Select the **Use as Template** icon.
1. Review your deal settings and summary, make any necessary updates, and then select **Save** to save the deal line item. Alternatively, select **Save and Duplicate** if you wish to duplicate this deal line item.

### Use the monitoring settings pane

1. Search for the deal line item you wish to use as a template.
1. In the **Line Name** column, click on the deal line item to expand the **Settings** pane.
1. Select the **Use as Template** option located at the upper-right corner of the page.
1. Review your deal settings and summary, make any necessary updates, and then select **Save** to save the deal line item. Alternatively, select **Save and Duplicate** if you wish to duplicate this deal line item.

> [!NOTE]
>
> - When you create a new deal line item from a template using any of the three ways, it will automatically be placed under the same advertiser and insertion order of the original deal line item. If you're using multiple advertiser and insertion orders and need to update them, you can make the changes directly in the creation form from the **Associated Objects** section in the **Advanced Settings**.
>
> - If you want to create multiple deals from a template, use the **Save and Duplicate** option after you've created the first deal line item. This feature creates a deal line item and opens a new form pre-populated with the same settings.

## Related topics

- [Set up multi-buyer deals](set-up-multi-buyer-deals.md)
- [Understanding multi-buyer deals](understanding-multi-buyer-deals.md)
