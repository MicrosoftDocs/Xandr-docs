---
title: Create a Simplified Deal Line Item
description: Explore the process of creating a simplified deal line item, either from scratch or with a template. Also, learn about the various settings and targeting options associated with it.
ms.date: 04/29/2024
---

# Create a simplified deal line item

Publishers using Microsoft Monetize can utilize Deal Line Items to set up special deals with their advertisers. This helps them offer the latest features available on the Microsoft Monetize platform to their buyers.

## Prerequisites

Before you begin, ensure that you create the demand-side objects:

- [Advertiser](create-an-advertiser.md)
- [Seamless Insertion Order](create-an-insertion-order.md)

Buyers want to configure their own end dates and budgets within their Demand Side Platform (DSP). You can enter budgets and end dates at either the insertion order or deal line item level. However, these settings are optional at both levels.

> [!NOTE]
> Legacy insertion orders aren't supported with the deal line item. The settings you select on the insertion order applies to *all* line items under the insertion order.

## Create a deal line item from scratch

You can create a new deal line item from the **Advertisers** screen.

1. Go to **Advertisers > Line Items**.
1. On the **Line Items** screen, select **Deal Line Item** from the **+ New** drop-down menu.
1. Select the **Create from Scratch** option under **Creation Mode**. If you wish to create a new deal from template, see [Create a deal line item from template](#create-a-deal-line-item-from-template).
1. Search (by name or ID) and select the desired advertiser and insertion order for the respective **Advertiser** and **Insertion Order** fields.

    > [!TIP]
    > When you select the **Make Default Advertiser** and **Make Default Insertion Order** checkboxes, the advertiser and insertion order information is saved automatically for future deal creation.
1. Select **Next**.

### Basic settings

In the **Basic Setup** section, enter the following details for the deal line item:

- **Deal Name**: Enter a deal name (this deal name is revealed to the buyer).
- **Deal Code**: Enter the deal code (optional, typically used by external sellers for deal mapping).
- **Deal Description**: Enter a description for your deal (optional).

#### Deal details

The **Deal details** section offers a detailed overview of the key components that define your deal.

- **Buyer**: Choose a buyer for the deal. Select the **Edit (pencil icon)** option under **Buyer**. On the **Buyer** screen, select an available buyer (search by name or ID). You cannot change the selected buyer after the deal line item is created and saved. For multi-buyer deals, see [Set Up Multi-Buyer Deals](set-up-multi-buyer-deals.md).
- **Deal Trust Level**: Specifies the level of audit status you want to permit for creatives to serve on a deal. For more information, see the **Trust Level** section in [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md).
- **Ad Type**: Select the type of ad you plan to use. You can select more than one ad type. Possible values are **Banner**, **Video**, **Audio**, and **Native**.
    > [!NOTE]
    >
    > Selecting **Ad Type** determines the availability of other settings (e.g.,**Targeting \>  Completion Rate Threshold**). **Ad Type** selections are automatically synced with the **Media Type** of deal impressions.
- **Ad Size**: Select the standard ad size, or you can also create a custom one. To create a custom ad size:
    1. Select the **Custom** tab.
    1. Select **Add Size**.
    1. Enter the appropriate values for the **Width** and **Height** fields.
    1. Select the **Add Size and Save Size to Member** option. This action automatically saves your custom ad size for future use.
    1. Select **Save**.
- **Deal Priority**: Specifies the deal's ranking in the auction. When a deal priority sits above the network "no reselling priority," the buyer's bid takes precedence over open exchange. When a deal priority sits below, the buyer competes with bids from the open exchange.
- **Pricing Strategy**: Specifies the payment method agreed upon by the advertiser. You can select one of the following revenue types:
  - **Floor Price**: Enter the hard floor price that will apply to the buyer of the deal.
  - **Fixed Price**: Enter the amount that the advertiser will pay you per thousand impressions.
  - **Market Price**: Select this option to use yield management floors if they are available; if they are not available, no floors will be applied to the auction.

#### Deal targeting

Deal line items have the following targeting options:

- **Device Type**: Select the devices you plan to target. You can select more than one device type. Possible values are **Desktops & Laptops**, **Tablets**, **Mobile**, and **CTV**. For more information, see [Device Type Targeting](device-type-targeting-ali.md).
- **Inventory Type**: Set which inventory types you wish to target. You can select one or all of the following inventory types:
  - **Web**: To run on standard websites and those optimized for browsers on mobile devices.
  - **App**: To run in applications installed on mobile tablets, phones, and Windows 8 devices.
- **Inventory Targeting**: Select **Edit (pencil icon)** to select the inventory you wish to target or exclude. For more information, see [Inventory Targeting (ALI)](inventory-targeting-ali.md).
- **Key/Value Targeting**: Define your own keys and their corresponding values to make full use of publisher data and help advertisers reach their intended audience. For more information, see [Key/value Targeting](key-value-targeting.md).
- **Segment Targeting**: Set which shared segments or specific groups you wish to target. For more information, see [Segment Targeting](segment-targeting.md).
- **Geography Targeting**: Target impressions based on the geographic location of the users viewing them. For more information, see [Geography Targeting](geography-targeting.md).

### Advanced settings

In the **Advanced Settings** section, enter any optional advanced settings that are useful.

#### Advanced targeting

The **Advanced Targeting** section offers advanced settings and targeting options to ensure your deal reaches the intended audience.

- **Roadblocking**: Optionally, you can enable programmatic roadblocks for the deal line item. If you select this option, you need to enter the dimensions for the **Master Creative** (that the buyer passes through in their bids) and its **Companion Creative**(s).
  
  > [!NOTE]
  >
  > Programmatic roadblocking is a **Beta** feature that isn't available to all clients. If you'd like to gain access to this feature, contact your account manager for more details.
- **Allowlist**: Search and select an allowlist you would like to apply to this line item. You can select from network/member-level allowlists or [create an allowlist](inventory-targeting-ali.md) directly from the line item. Once applied, you can also view or export the allowlist.
- **Blocklist**: Search and select a blocklist (by default, the Microsoft Advertising blocklist is always applied). Any inventory in the blocklists you apply for is automatically excluded and not bid on by this line item. You can select from network/member-level blocklists or [Inventory Lists](inventory-lists-ali-only.md) directly from the line item. Once applied, you can also view or export the blocklist.
- **Viewability Threshold**: Select the **Viewability Threshold** checkbox and enter a percentage to buy impressions based on their predicted viewability.
- **System targeting**: Target users based on their operating systems, browsers, language, device model, or carrier. For more information, see [System targeting](system-targeting.md).
- **Demographics**: Target specific segments of the audience based on characteristics such as age and gender. For more information, see [Demography targeting](demography-targeting.md).
- **Page properties**: Target impressions based on the position of the creative tag on the page or based on values passed in the query string of the ad call. For more information, see [Page properties targeting](page-properties-targeting.md).
- **Ads.txt**: Select this checkbox to only target web inventory authorized in a publisher's ads.txt file.

> [!NOTE]
> The use of Inventory Lists (e.g., allowlists, blocklists) constrains whatever **Inventory Type** selections you make. For example, if you target an allowlist, the **Inventory Type** option you select is limited to only those domains/apps in that allowlist. If you target a blocklist, the **Inventory Type** option you select serves everything but the domains/apps in that blocklist.

#### Budgeting and scheduling

The **Budgeting and Scheduling** section defines how you will pay for media and the financial relationship between you and the advertiser.

- **Budget Type**: The **Budget Type** is set in the parent insertion order.

  > [!NOTE]
  >
  > When you create a deal line item, the line item inherits its budget type from the parent insertion order, and this impacts the revenue types available on the line item. For example, if the budget type of an insertion order is **Impressions**, the child deal line item can only set up budgets using impressions.
- **Budget**: Set the line item's **Budget**. Select **Unlimited Budget**, **Lifetime Budget**, or **Daily Budget**. The unit of the budget is determined by the **Budget Type**.

  > [!NOTE]
  > All budget types are optional.

  - If you select **Lifetime Budget**, then select one of the following:
    - **Set Lifetime**: Enter a lifetime budget for the line item. This will be the total budget available to the line item for all its flight dates. The deal line item permits buyers to spend quickly, but it stops when the buyer reaches the spending limit.
    - **Set Per Flight**: When selected, a **Budget** field displays each of the line item's flight dates in the **Flights** section. Use the **Flights** field to set the budget for the flight dates.
  - If you select **Daily Budget**, enter the maximum daily budget to use.
- **Flights**: Flights permits you to create limited deals with start and end dates, and “evergreen deals” with no end date. To create one or more flights:

  1. Select either **Set Dates** or **No End Date**. This option is not available if the **Lifetime Budget** is set.

     - **Set Dates**: Enter a **Start Date** and **End Date** for each of the line item's flights. The hour settings for **Start Date** and **End Date** defaults to **12:00 AM** and **11:59 PM**, respectively (you can override the defaults). Flights might not overlap with one another. All flight dates must fall within the billing period dates of the parent insertion order and be a minimum of one day in duration. In addition, if you selected **Lifetime Budget \>  Set Per Flight** in the **Budget** section, you must enter a value for the **Budget** of each flight.
     - **No End Date**: Enter the **Start Date** for the line item. You might not create additional flights for this line item because it has no end date.
  1. Select **Add Another Flight** if you want additional flights. This option is not available if you select **No End Date**.

    > [!NOTE]
    >
    > You cannot change the **Start Date** of a flight once that date has passed. You can add multiple flights to any deal line item.
  
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
  - **Technical Attributes**: Select the technical attributes on which you want to override ad quality settings. When you select **Ignore**, the technical attribute will be allowed on the deal despite ad quality settings. All technical attributes defaults to **Follow**, so they comply with ad quality settings.

#### Reporting labels and comments

In the **Reporting Labels and Comments** section, you can optionally assign custom reporting labels (**Trafficker**, **Sales Rep**, **Line Item Type**, and **OMS ID**) to a line item. You can also add comments to a line item for your reference. Reporting labels let you associate a person or other metadata with advertisers. You can then run reports using these labels. For more information, see [Reporting Guide](reporting-guide.md).

#### Associated objects

The **Associated Objects** section defines objects and entities that are associated with the deal line item.

- **Line Item Name**: Enter the name for the line item.
- **Advertiser Summary**: Review your preselected advertiser details and make changes if needed. However, once the deal is created and saved, you cannot change the advertiser.
- **Insertion Order Summary**: Review your preselected insertion order details and make changes if needed, even after creating and saving the deal.

### Deal summary

The **Deal Summary** pane provides a comprehensive overview of the deal, including its name, buyer, ad type, deal priority, pricing strategy, price, inventory type, device type, and advanced settings such as budget and flights. This view facilitates an efficient review of key deal parameters, reducing the likelihood of errors and ensuring clarity in deal execution.

### Save the deal line item

Select **Save** to save the deal line item, or **Save and Duplicate** if you wish to duplicate this deal line item.

> [!NOTE]
> Using **Save and Duplicate** is the preferred method for duplicating deal line items.

## Create a deal line item from template

You can also create a new deal by selecting the **Create from Template** option under **Creation Mode**.

1. Go to **Advertisers > Line Items**.
1. On the **Line Items** screen, select **Deal Line Item** from the **+ New** drop-down menu.
1. On the **Create New Deal** screen, select the **Create from Template** option under **Creation Mode**.
1. Use the **Deal Template Selection** field to search and select a deal template using either a Line Item ID or name.
1. Review the summary of settings and select **Select This Template**. This action applies all the template settings to your deal settings.
1. Review the settings and summary of your deal, and then select **Save** to save the deal line item. Alternatively, select **Save and Duplicate** if you wish to duplicate this deal line item.
