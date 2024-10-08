---
title: Mediation Bids
description: A bid repesents the amount you think a mediated network will pay for your inventory. In this page, learn steps to create a Bid page. 
ms.date: 10/28/2023
---


# Mediation bids

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

Once a [network is created](mediation-networks.md), mediated bids must be set up to define the following:

- Which publisher bid requests to Monetize are relevant to the network
- Which ad tags to use to call the network

Each bid includes a publisher-defined CPM, which is the amount the network partner is likely to pay for the inventory. For more information about how mediation works, see [Selling Your Inventory through Mediation](mediation-selling-your-inventory-through-mediation.md).

Setup is also required in each network's platform, as covered in [Integrating for Mediation](mediation-integrating-for-mediation.md).

## Step 1: Go to the Create Bid page

From the Monetize navigation menu, select **Mediation** \> **Bids**. This will load the Bids overview screen.

## Step 2: Define basic settings

The following basic settings will apply to all bids created in the current screen.

- **State**: Choose whether the bid is active (can participate in auctions) or inactive (cannot participate in auctions).
- **Waterfall label**: An optional label to track bids that target the same inventory / audience combination. Available as a column and filter on the Bids overview page.
- **Flight Dates**: Control the lifetime of the Bid to run during a specific time frame, or indefinitely by choosing **No End Date**.
- **Daily Budget Cap**: Limit the bid to a certain number of filled impressions or a certain amount of revenue per day. Note that unfilled impressions (passbacks) do not count towards the budget cap.

## Step 3: Define bid specific settings

The **Bid Setup** section allows the creation of one or more bids, each with their own ntwork and settings.

The following information is required for every Bid:

- **Network**: Choose an eligible network from the dropdown. Depending on the type of network, several new fields may appear to provide unique information about the creatives required for that network.
- **Bid Name**: The name that will appear for the Bid in the Monetize UI and reporting. This should be reasonably descriptive to differentiate from other Bids.
- **Bid CPM**: The price the network partner is likely to pay for the inventory. Mediated networks are not connected directly to the Monetize exchange and do not submit bids into the auction in real time.
Publishers must regularly review reporting from each network and adjust Bid CPM values to ensure they represent a realistic price. Otherwise, an inaccurate mediated Bid could win auctions over higher bids from other sources.
- **Response Timeout**: Controls how long the network partner is given to respond to the bid request:
      - If the timeout is too low, revenue could be lost from bids earlier in the waterfall.
      - If the timeout is too high, page load times may suffer or the number of sequential bids that can participate within a single mediation waterfall could be limited.
- **Media Subtype**: The type of creative to be requested from the network (Standard Banner, In-Feed Standard, Standard VAST, etc). If the network supports multiple subtypes, each subtype must be created as a separate Bid with its own Ad Tags.
- **Ad Size**: The dimensions of the banner creative (example: `300x250`).
- **Custom Creative Request Template**: Some network partners offer multiple different creatives formats, which can be selected here.
- **Ad Tag**: The non-secure (HTTP) tag used to call the network for demand.
- **Support SSL**: Controls whether the Bid can serve via HTTPS. Enabling requires a separate, secure version of the ad tag. This only applies to display and mobile web creatives.
- **Secure Ad Tag**: The secure (HTTPS) tag used to call the network for demand.

The following informational fields are provided for each bid:

- **SSL Status**: Reflects audit status of the ad tag in the platform (pending, approved, failed, disabled). Only approved tags can serve.
- **Passback**: If no acceptable Bid is received for a request, a passback can be added to the ad tag to allow the next system in line to bid. Add the network's passback, listed here, to the ad tag to use this option.
Some mediated networks require their equivalent of a Monetize placement ID in the ad request. In some cases, multiple IDs are required. The Monetize Bids UI will prompt for the appropriate IDs from each network to ensure proper setup.

## Custom mobile network bids

When creating a mediated bid for a custom mobile network, additional information is required to connect to the third-party network's mobile SDK.

- **Support SSL**: Controls whether the Bid can serve via HTTPS. Enabling requires a separate, secure version of the ad tag. This only applies to display and mobile web creatives.
- **Device class name**: The Android or iOS class name taken from the code for the SDK. For example, `ediatedBannerAdView`. This field is optional for Monetize, but may be required for the integration with the network to function.
- **Network ID**: A required, unique ID that represents the location in an app where an ad can be shown. In Monetize, this is a "placement", but many networks use other terminology. The ID should not be reused across multiple Bids.
- **Network Parameter**: Optional, arbitrary data available if the network needs to receive more information to function.
  
### Mobile In-App video

For engineering guidance on fetching and displaying instream video ads using the Monetize SDKs, see [Show Instream Video Ads on Android](../mobile-sdk/show-instream-video-ads-on-android.md) and [Show Instream Video Ads on iOS](../mobile-sdk/show-instream-video-ads-on-ios.md).

> [!WARNING]
> Monetize only serves VAST tags through in-app video mediation. Ensure VAST, not VPAID, tags are requested from network partners.

## Step 4: Set bid targeting

The following targeting settings will apply to all the Bids created in the current screen. If separate targeting is required, save the first Bid then create an additional Bid with unique targeting.

When a publisher’s bid request is received, Monetize evaluates the bid request against mediated Bids to determine which, if any, are eligible based on the Bid’s targeting.

- **Inventory Targeting**: Target inventory objects, categories, and lists:
  
  - When a publisher is excluded, its placement groups and placements are not available for further inclusion or exclusion. When a placement group is excluded, its placements are not available for targeting.
  - When a top-level category is excluded, its sub-categories are not available for further inclusion or exclusion. When targeting more than one universal category, the categories have an OR relationship. For example, targeting "Custom Category 1" and "Custom Category 2" would request Bids on inventory that is in either category.

- **Geography Targeting**: Limit which bid requests are sent to networks based on the detected geographic location of the user.
- **System Targeting**: Target technical attributes detected in the bid request such as operating system, browser, language, device model.
- **Segment Targeting**: Target specific groups of users defined by publishers and third parties
- **Daypart Targeting**: Limit which bid requests are sent to networks based on the time of day and day of the week.
- **Frequency Targeting**: Limit how often and how recently users can be shown Bids from the network.
- **Key Value Targeting**: Target bid requests containing specific key values. Key values must be defined in Monetize first.
- **Supply Type Targeting**: Control whether bid requests are sent for web, app, or both types of supply.
- **Device Type Targeting**: Target a specific category of user device.

To improve performance, consider creating separate bids by placement, ad size, geography, and operating system.

## Step 5: Save your settings

Click the **Save** button at the top of the screen to create the bid(s).

[Monetize reports](reporting-guide.md) include Mediated networks as Advertisers and Bids as Line Items (both filters and dimensions).

### Bids and campaign priorities

Mediated bids have priority 5 in the auction, which is required for mediation to function. Any line items of lower priority will not compete unless the networks do not return ads.

Back-end objects associated with bids, such as augmented line items and campaigns, should not be modified directly. Use the **Monetize mediation bids** tab, detailed on this page, or the [Mediated Bid Service](../digital-platform-api/mediated-bid-service.md) to manage bids. Changing the priority of these objects will break mediation.

## Related topics

- [Selling Your Inventory through Mediation](mediation-selling-your-inventory-through-mediation.md)
- [Integrating for Mediation](mediation-integrating-for-mediation.md)
- [Mediation Networks](mediation-networks.md)
- [Mediated Bid Service](../digital-platform-api/mediated-bid-service.md)
