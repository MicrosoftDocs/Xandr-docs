---
title: Microsoft Monetize - Buying Microsoft Video Inventory
description: Learn advantages of buying video on Microsoft in this page. This page covers four types of video inventory that are available programmatically.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Buying Microsoft video inventory

Microsoft video inventory combines the targeting effectiveness of programmatic buying with interactive ad formats.

Microsoft video inventory allows brands to deliver a premium narrative that provides a robust understanding of a product to users. By buying video on Microsoft, users gain access to:

- both high-quality, deeply engaged audiences and brand-safe content.
- strong viewability metrics.
- diverse creative formats (availability dependent by market).
- powerful targeting capabilities using Microsoft's first-party data.

If you have any further questions about buying Microsoft Video Inventory, contact your Microsoft Advertising account representative. If you're accessing Microsoft Advertising using an external DSP, work with your associated DSP account manager for additional inquiries.

## Types of Microsoft video inventory

Microsoft offers four types of video inventory that are available programmatically:

- In-stream (MSN)
- Outstream (MSN)
- Bannerstream (MSN)
- Windows Video Interstitials (Windows)

The following table summarizes the benefits and availability of each inventory type:

| Inventory Type | Description | Benefits | Targeting Options | Market Availability |
|--|--|--|--|--|
| Bannerstream | Bannerstream was developed by Microsoft Advertising. It's available on MSN Homepage inventory (with future rollout to other pages). With Bannerstream, buyers have access to an integrated seamless video advertising experience within the MSN Homepage. Bannerstream lets buyers define static "post-show" images that display after the video finishes playing. | - Supports VAST/VPAID video<br> - Provides better publisher control when rendered<br> - Integrates more seamlessly, offering a better user experience<br> - Allows for better tracking of viewability, quartiles, and errors through the Microsoft Advertising VPAID wrapper | Audience such as profile and behavior | 50+ markets |
| In-stream | In-stream video ads are displayed within a video player on a page as pre-rolls (above content). These ads display above premium MSN Video Content on MSN Video and on the video players in article pages across MSN Verticals. They are offered on MSN Desktop Web and Mobile Web. | -  Supports IAB standard pre-roll<br> - Up to 30 seconds in duration<br> - Widely adopted, stable format<br> - High advertiser familiarity and adoption | - Content channels such as auto, news, and finance<br> - Audience such as profile and behavior | 50+ markets |
| Outstream | Outstream video ads are displayed when a user navigates to a designated place on the page where the video player is dynamically inserted within the article content. The video player only displays when the user navigates to that location. When the user navigates away from that location or the video ad has finished playing, the video player disappears automatically. It is not statically positioned on the page. Microsoft offers these types of ads on MSN Desktop Web article pages. | - Appears dynamically when a user navigates to the ad position on a page<br> - Up to 30 seconds in duration<br> - Audio starts on mouse-over | - Content channels such as auto, news, and finance<br> - Audience such as profile and behavior | 50+ markets |
| Windows Video Interstitials | Interstitial video ads are displayed when a user transitions from one content page to another. These ads display mid-transition. Interstitial video ads let you connect with highly engaged consumers on MSN O&O apps and thousands of third-party desktop and mobile apps within the Windows Store. | Offers a full screen audio/video experience | Audience such as profile and behavior | 40+ markets |

## Creative specifications for Microsoft video inventory

To learn more about Microsoft's various video creative specifications, see the following:

- [Microsoft Creative Specifications](https://about.ads.microsoft.com/en-us/policies/home)
- [Microsoft Creative Acceptance Policy](https://about.ads.microsoft.com/en-us/policies/home)

## Targeting Microsoft video inventory

Each video inventory type can be targeted using RTB or Deals. To target Microsoft video inventory, follow the guidelines listed in the table below:

| Targeting Method | Guideline |
|--|--|
| Deals | - Contact your Verizon representatives if you want to target deals in the following markets: US, Canada, UK, Germany, Spain, Italy, France, Brazil, and Japan.<br> - Contact your Microsoft Advertising account representative if you want to target deals in the following markets: Austria, Belgium, Denmark, Finland, Ireland, Netherlands, Norway, Portugal, Sweden, Switzerland, and all emerging markets. |
| External Bidder | - When targeting msn.com, add **msn.com** to the targeted domain list using the [Inventory List Item Service](../digital-platform-api/inventory-list-item-service.md). All MSN domains will be captured by the parent msn.com domain.<br> - When targeting video bid requests, we highly recommend that bidders listen to the [Video AppNexus Object](../bidders/outgoing-bid-request-to-bidders.md) within the Video Extension Object to distinguish In-stream, Outstream, and Bannerstream bid requests. Without listening to this object, it is difficult to differentiate Bannerstream inventory since Bannerstream is a proprietary Microsoft Advertising format.<br>**Note**: If you choose to filter by creative size, the list of creative sizes must be exhaustive. Include 1x1 as a permitted size since all of our video inventory appears as 1x1. For more information, see our [Bidder Profile - FAQ](../bidders/bidder-profile---faq.md). |
| RTB | - **For MSN**: In your inventory list, include the **msn.com** domain. For more information, see [Buying MSN Inventory](buying-msn-inventory.md).<br> - **For Windows**: In your inventory list, target **Windows AppNetwork (348882)**. For more information, see [Buying Microsoft Windows 3rd Party AppNetwork Inventory](buying-microsoft-windows-3rd-party-appnetwork-inventory.md).<br>Depending on market availability, buyers can also target the In-stream and Outstream video position as described in [Video Targeting](video-targeting.md). |

## Availability and volume

To see the latest availability and volume metrics for a particular product and market, download the latest [Excel file](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fdownload.microsoft.com%2Fdownload%2Fe%2Fe%2F5%2Fee544211-092a-45c4-8076-57b5c5aaceb3%2F28%2520Dec%25202023%2Fmsft-video-volume-by-format-final-june-2017.xlsx&wdOrigin=BROWSELINK).

Here are some quick volume metric highlights:

- **Average Daily Global Video Volume**: 176M
- **Average Daily US Video Volume**: 40M
- **Average Completion Rate by Video Format**:
  - Instream - 60%
  - Outstream - 30%
  - BannerStream - 50%
  - Interstitial - 60%

## Related topics

- [Creative Standards](creative-standards.md)
- [Add a Creative](add-a-creative.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
- [Buying Microsoft Inventory](buying-microsoft-inventory.md)