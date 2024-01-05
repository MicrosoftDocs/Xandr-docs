---
title: Set Up Mobile In-App Video Mediation
description: Learn how to setup a video mediation network for mobile in-app inventory.
ms.date: 10/28/2023
---


# Set up mobile In-App video mediation

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

This page describes how to set up a video mediation network for mobile
in-app inventory.

For engineering instructions on how to fetch and display instream video
ads using the SDK, see [Show Instream Video Ads on Android](../mobile-sdk/show-instream-video-ads-on-android.md) and [Show Instream Video Ads on iOS](../mobile-sdk/show-instream-video-ads-on-ios.md).

> [!WARNING]
> **VAST tags only**
>
> At this time, we can only serve VAST tags through in-app video mediation. Please make sure you request VAST (not VPAID) tags from your network partners.

## Step 1: Configure mediation networks

The setup of a video mediation network is simple - just navigate to the
**Mediation**
\> **Networks** page and follow
these steps.

1. Press the **New** button.

1. Select **Custom Video Network** in the
    **Network** drop down.

1. Under **Currency**, set the
    network's currency if different from your seat's default currency.

1. Change the **Network Name** to reflect
    the particular network or partner you are working with.

1. Set the **Brand** of the network. If
    working with a network or partner that doesn't fit to one brand,
    select **Unknown** brand.
    
    > [!TIP]
    > If we don't have an existing brand for a video demand source, it can be created. Please talk to your Xandr representative

1. Press **Save**.

   > [!WARNING]
   > **Report Sync Not Supported** 
   > 
   > The **Report Sync** feature is not supported for Mobile In-App Video Mediation.

## Step 2: Configure mediation bids

A mediation bid allows you to set how much you expect the mediated
network will pay for a video impression on a particular placement,
thereby allowing the mediated network to compete for the impression
against RTB demand in the Xandr auction.

To setup a mediation bid you need to have the average bid price you want
to use and a third party URL, which can call the mediated network
appropriately. If the URL can accept a cachebuster, please insert the
Xandr *${CACHEBUSTER}* macro so we can insert a randomly generated
number and make each URL call unique.

> [!TIP]
> The Mediated URL Field accepts Creative Macros
>
> The mediated URL field will accept any Xandr creative macro.

To create a bid navigate to
**Mediation**
\> **Bids** and follow these steps:

1. Click **Create Bid**.
2. Click the **Edit** button next to
    **Inventory** to target your bid
    to specific publisher(s), placement group(s) or placement(s). The
    targeting you choose depends highly on your object hierarchy. For
    example, if you want to setup one bid per placement you'll want to
    target individual placements; however if you want one bid to target
    multiple placements it may be easier to target placement groups.
1. Click the **Edit** buttons next to
    **Geography** or
    **System** to further refine when
    this mediated bid will compete for an impression.
1. Under the **Bids** section select
    the network you created previously.
. Once selected you will be able to add the network's VAST
    **URL**. Replace any dynamic values in
    the VAST tag with the appropriate creative macro.
1. **Bid Name** is displayed in the
    **mediation** dashboard (accessed from the
    Mediation tab) so use a
    descriptive name. As an example, a good format would be
    "\<network\> - \<inventory\> - \<geography\> - video" like
    "MyVideoNetwork - Story Page - US - video".
1. Set the **Bid CPM** to the average
    eCPM that this mediated video network generates for this particular
    combination of inventory, geography, and system. You should check
    this via the mediated network's reporting system and update your
    **Bid CPM** regularly to make sure it
    closely represents how much the network will receive for filling the
    impression.
1. Add any desired targeting under the
    **Advanced Settings** section.

> [!WARNING]
> The **Response Timeout** field on the bid setup is not currently used by client-side mediation. The placement/member-level settings are used instead.

## Related topics

- [Xandr Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md)
- [Show Instream Video Ads on Android](../mobile-sdk/show-instream-video-ads-on-android.md)
- [Show Instream Video Ads on iOS](../mobile-sdk/show-instream-video-ads-on-ios.md)
- [Mediate with Android](../mobile-sdk/mediate-with-android-sdk-instructions.md)
- [Mediate with iOS](../mobile-sdk/mediate-with-ios.md)