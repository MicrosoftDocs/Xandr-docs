---
title: Create a Deal Line Item
description: Create advanced deals in Microsoft Advertising Monetize with Deal Line Items. Monetize provides latest features for buyer interactions.
ms.date: 10/28/2023
---

# Create a deal line item

Deal Line Items let publishers using Microsoft Advertising Monetize as an ad server or SSP set up advanced deals with their buyers and provide all the newest features the Monetize deals platform has to offer.

## About deal line items

Deal line items let you manage auction and pricing dynamics negotiated with a buyer, including:

- **Revenue Type and Floor Pricing** - How the advertiser has agreed to pay you.
  - **Dynamic CPM** ("standard auction") deals that compete in either a first- or second-price auction at the price bid by the buyer, whenever the buyer bids above the ask price.
  - **CPM** ("fixed price") deals that compete in the auction at a fixed price whenever the buyer bids above that price.
- **Priority** - The deal's ranking in the auction. When a deal priority sits above the network "no reselling priority," the buyer's bid will take precedence over open exchange. When a deal priority sits below, the buyer will compete with bids from the open exchange.
- **Budget** - The upper limit of impressions or revenue for the deal, if configured on the deal line item.

## Before you begin

### Prerequisites

**Demand-side objects:** Create the [advertiser](create-an-advertiser.md) and a seamless [insertion order](create-an-insertion-order.md) (legacy insertion orders are not supported with the deal line item).

Buyers will typically want to configure their own end dates and budgets within their DSP. You can choose to enter budgets and end dates at either the insertion order or deal line item level. However, these settings are optional at both levels.

> [!NOTE]
> The settings you select on the insertion order will apply to *all* line items under the insertion order.

## Select the advertiser

On the **Advertisers** screen, click to edit the advertiser under which you want to create a deal line item. Youcan create deal line items from the advertiser details screen or from an advertiser's insertion order.

> [!NOTE]
> All pacing is ignored for deal line items.

## Create a new deal line item

**From the Line Item Order Home screen**

1. On the **Line Items** screen, click the New drop-down and select **Deal Line Item**.
1. Search for (by **Name** or **ID**) and select an appropriate advertiser on the **Select an advertiser** screen.
1. Click **Continue**.

**From the advertiser details screen**

On the **Advertiser Details** screen of the advertiser under which you want to create a deal line item:

1. On the **Create New** drop-down, select **Line Item**.
1. In the **Line Item Type** section of the **Create New Line Item** screen, select **Attach a Deal**. The **Deal Type** will default to **Traffic a Deal**.

**From the insertion orders screen**

1. On the **Advertisers** screen, click the **Insertion Order** for the advertiser under which you want to create a line item.
1. On the **Insertion Orders** screen, click the insertion order under which you want to create the line item.
1. Click **New Deal Line Item** in the **Line Items** section. This opens the **Create New Line Item** screen. The **Deal Type** will default to **Traffic a Deal**.

## Basic setup

In the **Basic Setup** section, enter the basic details for the deal line item.

- **Insertion Orders** - The seamless insertion order associated to the line item. If you create the line item from the **Insertion Order Details** screen, the
  insertion order is automatically associated. Otherwise, click **Edit** to associated the line item  with an insertion order.
- **Ad Type** - Select the type of ad you plan to use. Possible values are **Banner**, **Video** (includes audio types as well), and **Native**.
  
  > [!NOTE]
  >
  > Selecting **Ad Type** determines the availability of other settings (e.g.,**Targeting \>  Completion Rate Threshold**). This is not the setting that filters out any
  > impressions and does not impact auction logic. To filter out deal impressions by media type, use **Deal Creative Criteria \>  Media Type** (see [Deal Creative Criteria](create-a-deal-line-item.md#deal-creative-criteria)).

- **Roadblocking** - Optionally, you can enable programmatic roadblocks for the deal line item. If you choose to do so, you need to specify the dimensions for the **Master Creative** (that the buyer passes through in their bids) and its **Companion Creative**(s).
  
  > [!NOTE]
  >
  > Programmatic roadblocking is a **Beta** feature that isn't available to all clients. If you'd like to gain access to this feature, contact your account manager for more
  > details.

- **Name** - Enter the name for the deal line item. You will later be able to search for and report on the line item using this name. This name is not exposed to the buyer.
- **External Code** - If you want to report on the line item using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code
  here. The code may only contain alphanumeric characters, periods, underscores, or dashes. The code you enter is not case-sensitive (uppercase and lowercase characters are treated the same). No two line items can use the same code per advertiser.
- **State** - Set the state of the line item. If "**Active**", the line item will be eligible to serve. Best practice for sellers is to set the state to **"Active"** so that buyers can serve on their inventory as quickly as possible.
- **Insertion Order Details** - Insertion order details for **Budget Type**, **Currency**, **Total Lifetime Budget**, **Pacing**, **Start Date**, and **End Date** display in the gray box (you must select an insertion order to display these values).
- **Budget Type** - Budget is set on the parent insertion order.
  
  > [!NOTE]
  >
  > When you create a deal line item, the line item will inherit its budget type from the parent insertion order, and this will impact the revenue types available on the line item. For example, if the budget type of an insertion order is **Impressions**, the child deal line item can only set up budgets using impressions.

## Deal details

1. Select **Create a Deal**.
1. Enter a **Deal Name** (this deal name is exposed to the buyer)
1. Click **Edit** under **Buyer** to choose a buyer for the deal.

    > [!NOTE]
    >
    > For multi-buyer deals, see [Set Up Multi-Buyer Deals](set-up-multi-buyer-deals.md).

1. On the **Select Buyer** screen, select an available buyer (you can search by Name and ID). You cannot change the selected buyer after the deal line item is created and saved.
1. Click **Add**.
1. Enter the deal code in **Code** (optional, typically used by external sellers for deal mapping).
1. Enter a description for your deal in the **Description** box (optional).

    > [!NOTE]
    >
    > This description is visible to buyers.

Details for the newly created or existing deal display in **Deal Details** including:

- **Deal ID** - ID of newly created deal (the **Deal ID** for newly created deals is not created until the deal line item is saved).
- **Auction Type** - Determined by **Line Item Priority** (set in **Supply Strategy**). **Auction Typ**e is “Private” (takes precedence over Open Exchange) if the
  **Line Item Priority** is at or above your member’s reselling priority setting, or “Open” (competes with RTB) if it is below.
- **Price Type** - Determined by **Revenue Type**:
  - **CPM** = Fixed Price
  - **Dynamic CPM** = Standard
- **Ask Price** - Determined by the value set in **Fixed** or **Floor Price** (set in **Revenue Type**)

## Revenue type

Use the **Revenue Type** to define how the advertiser has agreed to pay you. You can choose one of the following revenue types:

- **CPM** ("fixed price" deals) – Deal line item competes in the auction at a fixed price whenever the buyer bids above that price.
  - **Fixed Price** - Enter the amount that the advertiser will pay you per thousand impressions.
- **Dynamic CPM** ("standard auction") - Deal line item competes in either a first- or second-price auction at the price bid by the buyer, whenever the buyer bids above the ask
  price. Select either:
  - **Set Floor Price** - Enter the hard floor that will apply to the buyer of the deal.
  - **Use Market Price** - Select this to use yield management floors if available; if not available, no floors are applied to the auction.

## Budget

Set the line item's **Budget**. Select **Unlimited Budget**, **Lifetime Budget**, or **Daily Budget**. The unit of the budget is determined by the **Budget Type**:

> [!NOTE]
> All budget types are optional.

- If you select **Lifetime Budget**, then select one of the following:
  - **Set Lifetime** - Enter a lifetime budget for the line item. This will be the total budget available to the line item for all its flight dates. The deal line item will
    allow buyers to spend as fast as possible, but will cap out once the buyer reaches the spend cap.
  - **Set Per Flight** - When selected, a Budget field displays for each of the line item's flight dates in the Flights section. Use that
    field to set the budget for the flight dates.
- If you select **Daily Budget**, enter the maximum daily budget to use.

## Flights

Flights let you set up limited deals with start and end dates as well as “evergreen deals” with no end date. To create one or more flights:

1. Select either **Set Dates** or **No End Date** (not available if **Lifetime Budget** is set).

    - **Set Dates**: Enter a **Start Date** and **End Date** for each of the line item's flights. The hour settings for **Start Date** and **End Date** will default to **12:00 AM** and **11:59 PM** respectively (you can override the defaults). Flights may not overlap one another. All flight dates must fall within the billing period dates of the parent insertion order and be a minimum of one day in duration. In addition, if you selected **Lifetime Budget \>  Set Per Flight** in the **Budget** section, you must enter a value for the **Budget** of each flight.
    - **No End Date**: Enter the **Start Date** for the line item. You may not create additional flights for this line item because it has no end date.
1. Click **Add Another Flight** if you want additional flights (this option is not available if you select **No End Date**.)

     > [!NOTE]
     >
     > You cannot change the **Start Date** of a flight once that date has passed. You can add multiple flights to any deal line item.

## Supply strategy

Deal line items are set to **Managed** supply strategy (this setting cannot be changed). Select the priority level for the deal line item in the Line Item
Priority drop-down. Buyer bids on an impression with the same deal priority will compete on price with one another as well as managed line items at the same priority level. Buyer bids on a deal at a higher priority will defeat lower priority bids. The Line Item Priority you set here
determines the **Auction Type** for the deal line item (see [Deal Details](create-a-deal-line-item.md)).

### Payment model

The payment model for deal line items is set to Pay Per Impression (this setting cannot be changed).

## Inventory and brand safety

You can specify the following inventory and brand safety settings for the deal line item:

- **Managed Inventory**: Click **Edit** to select inventory you wish to target or exclude. See [Inventory Targeting (ALI)](inventory-targeting-ali.md) for more details.
- **Inventory Type**: To set which inventory types you wish to target, select one of the following from the menu. By default, your line items will target all inventory types
  (i.e., both App and Web).
  - **App & Web** - To run on both inventory types. This is the default setting.
  - **App Only** - To run in applications installed on mobile tablets, phones, and Windows 8 devices.
  - **Web Only** - To run on standard web sites and those optimized for browsers on mobile devices.
- **Blocklist**: Select one or more blocklists (by default, the Microsoft Advertising blocklist will always be applied). Any inventory in the blocklists you apply
  will automatically be excluded and not bid on by this line item. You can select from network/member-level blocklists or [Inventory Lists](inventory-lists-ali-only.md)  directly from the line item. Once applied, you can also view or export the blocklist.
- **Allowlist**: Select an allowlist you would like to apply to this line item. You can select from network/member-level allowlists or [create an allowlist](inventory-targeting-ali.md) directly from the line item. Once applied, you can also view or export the allowlist.
- **Ads.txt**: Do not use (not supported for deal line items).

> [!NOTE]
> The use of Inventory Lists (e.g., allowlists, blocklists) will constrain whatever **Inventory Type** selections you make. For example, if you target an allowlist,
> the **Inventory Type** option you select will be limited to only those domains/apps in that allowlist. If you target a blocklist, the **Inventory Type** option you select
> will serve on everything but the domains/apps in that blocklist.

## Frequency & Recency

A frequency cap is the total number of ads shown to a user. A recency cap is the pace at which ads are shown to a user. **Frequency and Recency** caps can be set on deal line items (as well as on the parent insertion order and advertiser). To apply frequency and recency caps, set the Frequency & Recency toggle to **Caps on** and enter the appropriate
**Frequency** and **Recency** settings (see [Frequency and Recency Caps](frequency-and-recency-caps.md) for detailed setup information).

## Targeting

You can target deal line items in the same way you can target augmented line items. Deal line items have the following targeting options (see [Buy-Side Targeting](buy-side-targeting.md) for detailed setup information):

- Geography
- Device Type
- Key Value
- Size
- Daypart
- System
- Segment
- Page Properties
- Demographics
- Video position, playback method, player width, framework, and creative duration (when Ad Type = video). For more information, see [Video Player Targeting](video-player-targeting.md).
- Video content specifics such as video program type, delivery method, genre, duration, and rating (when Ad Type = video). For more information, see [Video Content Targeting](video-content-targeting.md).
- Viewability Threshold
- Completion Rate Threshold (when Ad Type = video)

Note the following for deal line item targeting:

- You can now target Key/Values rather than Query String Segments:

  > [!NOTE]
  >
  > Key/Values are reportable; Query String Segments are not reportable.

- Thresholds (**Viewability Threshold** or **Completion Rate Threshold**) create a minimum predicted rate which impressions must surpass in order to be eligible for the deal. The rate set here is compared to our predicted rate based on historical data for the inventory, and is a lower limit - because of this, you should expect a real view/completion rate somewhat higher than the threshold you configure.
- See [Inventory Performance Targeting](inventory-performance-targeting.md) for more information on best practices for inventory performance targeting.

## Deal creative criteria

You can edit the following creative attributes for a deal by clicking **Edit** under each attribute, selecting the appropriate values, and clicking **Set**:

> [!NOTE]
> See [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md) for detailed setup information.

- **Brand**
  - **Brand** tab: Only selected brands will be allowed to serve; any brands not selected will not be allowed. If no brands are selected, all brands that follow ad quality rules are allowed.
  - **Ad Quality Settings tab**: Select the brands on which you want to override ad quality settings. When you select **Ignore**, the brand will be allowed on the deal despite ad quality settings. All brands will default to **Follow** so they comply with ad quality settings.
- **Language**
  - **Language** tab: Only selected languages will be allowed to serve; any languages not selected will not be allowed. If no languages are selected, all languages that follow ad quality rules are allowed.
  - **Ad Quality Settings** tab: Select the languages on which you want to override ad quality settings. When you select **Ignore**, the language will be allowed on the deal despite ad quality settings. All languages will default to **Follow** so they comply with ad quality settings.
- **Trust Level** (see Trust Level section in [Override Ad Quality Settings on a Deal](override-ad-quality-settings-on-a-deal.md) for detailed setup information)
- **Creative Category**
  - **Creative Category** tab: Only selected creative categories will be allowed to serve; any creative categories not selected will not be allowed. If no creative categories are selected, all creative categories that follow ad quality rules are allowed.
  - **Ad Quality Settings** tab: Select the creative categories on which you want to override ad quality settings. When you select **Ignore**,the creative category will be allowed on the deal despite ad quality settings. All creative categories will default to **Follow** so they comply with ad quality settings.
- **Specific Creatives**: Include specific creatives to either **Approve** (always allow) or **Block** (always block) on the deal.
- **Media Type**: Select the media types you want to include on the deal.
  
  > [!NOTE]
  >
  > Limiting the media types of creatives allowed on the deal will also limit the media types of requests sent through the deal. For example, if you select to only allow **Banner** creatives, the deal will only send banner requests to the buyer.

- **Technical Attributes**: Select the technical attributes on which you want to override ad quality settings. When you select **Ignore**, the technical attribute will be allowed on the deal despite ad quality settings. All technical attributes will default to **Follow** so they comply with ad quality settings.

**Reporting labels**

Enter any reporting labels if desired. Reporting labels let you associate a person or other metadata with advertisers. You can then run reports using these labels. See [Reporting Guide](reporting-guide.md) for more information.

## Comments

Enter any comments for this deal line item. Note that the buyers cannot see these comments.

## Save the deal line item

Click **Save** to save the deal line item or **Save and Duplicate** if you want to duplicate this deal line item.

> [!NOTE]
> Using **Save and Duplicate** is the preferred method for duplicating deal line items.
