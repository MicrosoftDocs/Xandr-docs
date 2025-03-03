---
title: DV360 Buying Guide
description: Explore efficient connection on DV360, linking publishers and buyers for streamlined communication and optimization through inventory access and targeting.
ms.date: 10/28/2023
---

# DV360 buying guide

In partnership with DV360, Xandr has created this guide to help Xandr publishers communicate with their buyers about accessing and targeting Xandr's publisher inventory using DV360 as their DSP. This information has been created in collaboration with and approved by the DV360 team. Note that platforms can and will change regularly. We will do our best to update this guide as needed. Wherever possible, we've provided links to DV360 documentation.

We recommend that if buyers are having issues, or if they need help using the DV360 platform, their first point of outreach should be the DV360 team.  
  
## Terminology mapping

In a few cases, DV360 and Xandr use different terminology, as shown in the following table.

| DV360 | Xandr |
|--|--|
| [Non-Guaranteed Fixed Deals](https://support.google.com/displayvideo/answer/3289692) (formerly known as Preferred Deals) | Private Deal involving one publisher and one buyer. |
| [Non-Guaranteed Auctions](https://support.google.com/displayvideo/answer/3289702) (formerly known as Private Auctions) | Multi-Buyer Deal involving one publisher and many buyers. |
| Partner ID | Buyer Seat ID |

## Use DV360 to buy Xandr open auction and deals inventory

This section explains how to target Xandr (formerly AppNexus) as an inventory source within the DV360 UI.

> [!NOTE]
> To learn more about managing exchanges with DV360, buyers should see [Managing Exchanges](https://support.google.com/displayvideo/answer/9230278?hl=en)in the DV360 Help.

To set up Xandr Exchange targeting in DV360, the buyer needs to target **AppNexus (Xandr)** as an **Exchange** in **Partner Settings** as shown in the following graphic:

:::image type="content" source="media/dv360-buying-guide-a-edited.png" alt-text="Screenshot that illustrates how to set up Xandr Exchange targeting in DV360, the buyer needs to target AppNexus (Xandr) as an Exchange in Partner Settings.":::

> [!TIP]
> To learn more about targeting an inventory source, buyers should [Inventory Source Targeting](https://support.google.com/displayvideo/answer/2726009) in the DV360 Help.

### Buy using open auction

To buy using **Open Auction**, buyers can use the following steps to target Xandr as an exchange. The process starts from the Inventory Source UI with nothing defined, as shown in the following graphic:

:::image type="content" source="media/dv360-buying-guide-b.png" alt-text="Screenshot that illustrates the process initiates from the Inventory Source UI without any predefined settings.":::

In **Partner Settings**, the buyer should select **AppNexus (Xandr)** as the exchange as shown in the following graphic. If the buyer only wants to buy Xandr inventory, they should make sure the Target new exchanges checkbox is de-selected.

The following graphic shows the Inventory Source screen with Xandr selected as the exchange.

:::image type="content" source="media/dv360-buying-guide-c.png" alt-text="Screenshot that illustrates the Inventory Source screen with Xandr chosen as the exchange.":::
  
#### Deals

Deal Sync with DV360 is currently in beta, and only selected sellers are enabled for this feature. For more information, see the following topics in the DV360 Help:

- [DV360 Buyer UI Deal Acceptance Workflows](dv360-buyer-ui-deal-acceptance-workflows.md)
- [Deal Sync with DV360 - Publisher Guide](deal-sync-with-dv360---publisher-guide.md)
- [Deal Sync with DV360 - FAQ](deal-sync-with-dv360---faq.md)

> [!NOTE]
> The campaign or the line item must be active for the deal to see any activity.

**To set up and target a Xandr deal:**

1. In DV360, the buyer creates a new Xandr deal as shown in the following graphic.

   :::image type="content" source="media/dv360-buying-guide-d.png" alt-text="Screenshot that illustrates how the buyer creates a new Xandr deal.":::

   The second graphic shows an example of a newly created deal in the UI.

   :::image type="content" source="media/dv360-buying-guide-e.png" alt-text="Screenshot that illustrates an example a newly created deal in the user interface (UI).":::

1. The buyer selects the created deal for targeting as shown in the following graphic.

   :::image type="content" source="media/dv360-buying-guide-f.png" alt-text="Screenshot that shows how the buyer selects the created deal for targeting.":::

   The second graphic shows an example of the targeted deal displayed in UI.

   :::image type="content" source="media/dv360-buying-guide-g.png" alt-text="Screenshot that illustrates specific deal presented in the user interface.":::

Refer the buyer to the following topics in the DV360 help for more information about deals.

- [How to Negotiate a Deal](https://support.google.com/displayvideo/answer/7505945?hl=en)
- [Best Practices for Setting Up Deals](https://support.google.com/displayvideo/answer/9198385?hl=en)
- [Deal Troubleshooting](https://support.google.com/displayvideo/answer/6292894?hl=en)

## Programmatic Guaranteed (PG) buying

Programmatic guaranteed buying is currently available with DV360. The DV360 team has detailed information on available programmatic guaranteed publishers and associated contacts. Talk to your Xandr account manager about being included in Xandr's programmatic guaranteed product release.

> [!NOTE]
> Publishers can download the following document and share it with buyers directly: [Leverage Programmatic Guaranteed](../monetize/programmatic-guaranteed-buying-line-items.md).

## Target audiences and content

DV360 allows targeted buying based on audiences and content. To learn more about targeting in DV360, see [Introduction to Targeting](https://support.google.com/displayvideo/topic/3033780?hl=en).

### Audience targeting

Buyers using DV360 have access to a number of different types of audience data. Buyers should note that some of this data has limited reach on third-party exchanges such as Xandr. For more information, see [Details about audience targeting](https://support.google.com/displayvideo/topic/2726036?hl=en), [Audience List Targeting](https://support.google.com/displayvideo/answer/2949947?hl=en), and [Custom List Targeting](https://support.google.com/displayvideo/answer/7583366?hl=en) in the DV360 Help.

| Google Data | Limitations | Tips and Recommendations |
|--|--|--|
| [Custom Affinity](https://support.google.com/displayvideo/answer/7583366?hl=en) | Can be used on Ad Manager and third-party exchanges. Scale is limited on third-party exchanges. First or third-party audiences preferred. | If you are using this type of data, set up your DV360 line item targeting with one or more first- or third-party audience lists in a logical OR relationship to limit scale issues. |
| [Custom Intent](https://support.google.com/displayvideo/answer/7583366?hl=en) | Can only be used on Ad Manager inventory. | N/A |
| [Affinity](https://support.google.com/displayvideo/answer/6021489?hl=en) | Can be used on Ad Manager and third-party exchanges. Scale is limited on third-party exchanges. First or third-party audiences preferred. | N/A |
| [Similar/Lookalike](https://support.google.com/displayvideo/answer/13643641?hl=en&visit_id=638362302043745084-900489057&rd=2) | Can be used on Ad Manager and third-party exchanges. Scale is limited on third-party exchanges. First or third-party audiences preferred. | N/A |
| [In-Market](https://support.google.com/displayvideo/answer/6213232?hl=en) | Can be used on Ad Manager and third-party exchanges. Scale is limited on third-party exchanges. First or third-party audiences preferred. | N/A |
| [Geography](https://support.google.com/displayvideo/answer/2705812?hl=en) | Can be used on Ad Manager and other exchanges (including PMP). | N/A |
| [Day and Time](https://support.google.com/displayvideo/answer/2697407?hl=en) | Can be used on Ad Manager and other exchanges (including PMP). | N/A |
| [Demographics](https://support.google.com/displayvideo/answer/6071542?hl=en) | Can be used on Ad Manager and third-party exchanges. Scale is limited on third-party exchanges. First or third-party audiences preferred. Household income targeting is available on Google Ad Manager and TrueView inventory. | If you are using this type of data, set up your DV360 line item targeting with one or more first- or third-party audience lists in a logical OR relationship to limit scale issues. |
| [Installed App Category](https://support.google.com/displayvideo/answer/13643641?hl=en&visit_id=638362302043745084-900489057&rd=1) | Can be used on Ad Manager and other exchanges (including PMP). | N/A |
| [New Mobile Device](https://support.google.com/displayvideo/answer/13643641?hl=en&visit_id=638362302043745084-900489057&rd=1) | Can be used on Ad Manager and other exchanges (including PMP). | N/A |
| [Third Party Audience](https://support.google.com/displayvideo/answer/6212219?hl=en) | Can be used onAd Manager and other exchanges (including PMP). | N/A |

### Content targeting

To learn more about content targeting, see [Content Targeting](https://support.google.com/displayvideo/topic/2726034?hl=en) in the DV360 Help.

The following table shows content targeting options in DV360 and provides guidance for implementing them.

| Content Type | Limitations | Tips and Recommendations |
|--|--|--|
| [Brand Safety](https://support.google.com/displayvideo/answer/3032915?hl=en) | Using brand safety segments from IAS and DoubleVerify can sometimes cause limited reach if Xandr inventory is not yet categorized or is mis-categorized. | DV360 uses a crawler that checks aspects of all websites/apps and provides a digital content label. For more information on how inventory is labeled, see [Digital content labels in Display & Video 360](https://support.google.com/displayvideo/answer/2735881?hl=en&sjid=1732881213029061792-AP) in the DV360 Help. We recommend adhering to the [Domain transparency recommendations](#domain-transparency-recommendations) domain transparency guidance laid out in the next section. |
| [App, Channel, and Website](https://support.google.com/displayvideo/answer/2650521?hl=en) | N/A | N/A |
| [Keyword](https://support.google.com/displayvideo/answer/2697825?hl=en) | For keywords to work, pages need to be crawlable. | We recommend a minimum of 100 branded keywords and/or 100 generic keywords. Ask the advertiser for their top converting keywords from Adwords. |
| [Category](https://support.google.com/displayvideo/answer/2697826?hl=en) | DV360 does not read Xandr's content categories in the bid request. | We recommend targeting top categories to improve reach. |
| [Environment](https://support.google.com/displayvideo/answer/3232163?hl=en) | N/A | N/A |
| [Viewability](https://support.google.com/displayvideo/answer/6101342?hl=en) | Targeting can only be done using [Active View](https://support.google.com/displayvideo/answer/3214556?hl=en). | For display inventory, viewability measurement can be done using [Active View](https://support.google.com/displayvideo/answer/3214556?hl=en) as well as third-party measurement with DoubleVerify & IAS. Viewability measurement for native inventory can only be done using [Active View](https://support.google.com/displayvideo/answer/3214556?hl=en) at this time. |
| [Language](https://support.google.com/displayvideo/answer/2697406?hl=en) | N/A | N/A |
| [Video](https://support.google.com/displayvideo/answer/6008366?hl=en) | N/A | N/A |
| [Digital Content Label](https://support.google.com/displayvideo/answer/3441297?hl=en) | N/A | Avoid using masked URLs in the bid request. Masked URLs are not analyzed by Google's crawler and will be classified as "Not yet labelled". Semi-transparent inventory may receive any digital content label if the publisher selling the inventory has shared all of the URLs behind the bid request URL with Bid Manager. In these situations, the publisher's inventory will be labeled according to the inventory's minimum brand safety. |
| [Position](https://support.google.com/displayvideo/answer/3441297?hl=en) | N/A | Make sure you are sending `video.placement` in the bid request. |
| [User-rewarded Content](https://support.google.com/displayvideo/answer/9166157?hl=en) | User rewarded inventory is currently limited. Targeting only user-rewarded content can result in narrow reach, and few impressions and clicks. | Make sure you send the rewarded extension. |

## Domain transparency recommendations

The following table shows recommendations for providing domain transparency in bid requests.

| Inventory Type | Limitations | Tips and Recommendations |
|--|--|--|
| All | DV360 can bid on non-transparent inventory but it depends on advertiser's targeting; most campaigns require transparent inventory. | We recommend sending the full URL. In certain circumstances it may make sense to send the domain instead of the full URL in bid requests; this can be applied by the bidder within the Xandr system. For example, if you have inventory with URLs that change based on a user's search terms (because the user's search terms are added in the URL as query strings), the URLs received by DV360 are often unique. It takes time for DV360's crawlers to add a classification or rating to these URLs, which can cause an issue when targeting for brand safety/sensitive category exclusions is in place. In this special circumstance, we recommend standardizing the URL passed in the bid request. |
| Video | The full URL, rather than just the domain, needs to be passed. Otherwise, DV360 identifies the inventory as "non-monetizable content". | We recommend passing the full URL in a video bid request. |

## Creative requirements

DV360 only bids with creatives that have passed Xandr audit.

- To start the Xandr creative audit, the buyer should make sure the line item their creatives are assigned to is active and targets Xandr inventory.
- DV360 users can request a re-sync if a creative's audit status seems to get stuck or if DV360 and Xandr are showing different audit statuses. This can be done at the creative level. The buyer should save the creative to restart the creative review process in **Display & Video 360**. For more detail, see the following:

:::image type="content" source="media/dv360-buying-guide-h.png" alt-text="Screenshot that displays the creative status in Display & Video 360.":::

### Identify the creative ID and audit status

The following graphic shows how to identify the creative ID and audit status for each creative.

:::image type="content" source="media/dv360-buying-guide-i.png" alt-text="Screenshot that demonstrates the process of identifying the creative ID and audit status for each creative.":::

## Buyer identification using buyer seat IDs

DV360 supports Xandr's [Buyer Seat ID](../monetize/understanding-buyer-seat-ids.md) feature. Previously, member breakouts and virtual seats were used for each DV360 buyer. However, they are no longer used for each DV360 buyer. Deals should be set up using DV360 Partner IDs, which Xandr sellers can find in the Partner Center.

Buyers can find their DV360 Partner ID in two ways, as shown in the following graphic. Inspect the URL, which takes the form [https://displayvideo.google.com/#ng_nav/p/xxxx](https://displayvideo.google.com/#ng_nav/p/%2aXXXXX.%2a). `XXXXX` is typically a 5-digit number representing the partner ID.

In the DV360 UI, go to **Partner Settings >  Basic Details**. The Partner ID is at the bottom of the screen.

:::image type="content" source="media/dv360-buying-guide-j.png" alt-text="Screenshot that displays the Partner ID at the bottom of the screen.":::

### Troubleshooting

The **match rate between DV360 and Xandr** is healthy and in line with other platforms. Sometimes there can be confusion when troubleshooting line items not delivering that are using Google data. It is possible that the support team will tell the buyer that the issue in delivery is user match rate or lack of cookies, which is a nuanced issue. The actual issue is the lack of match with the Google audience data. Removing the Google audience data or adding 1st or 3rd party data in an OR relationship can often help in these situations.

If a DV360 buyer has issues serving on Xandr inventory, we recommend that they:

1. Reach out to DV360 support channels as the first step
1. If they cannot resolve the issue using DV360, they should loop in Xandr support.

Sellers can reach out to their Xandr account manager or escalate through [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## DV360 and TCF compliance

Google has officially joined the TCF v2. Full guidance from Google can be found [here](https://support.google.com/displayvideo/answer/9496576?hl=en).

> [!NOTE]
> Google DV 360 is a part of the Global Vendor List v2.0 in the update released on July 23, 2020. If you have adopted TCF v2.0, and you have not re-established legal basis with your users using a version of the Global Vendor List released after this date, you risk losing access to some or all Google DV360 demand . We recommend taking this action promptly to avoid any potential disruption to your business.
