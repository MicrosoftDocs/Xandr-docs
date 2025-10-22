---
title: Rich Media Creatives on Mobile
description: In this article, find information on how to set up rich media creatives to serve on mobile devices.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Rich media creatives on mobile

This document describes how to set up your rich media creatives to serve on mobile devices. It also contains a list of media types supported by each major seller.

> [!NOTE]
> For the purposes of this document, rich media creatives are defined as interstitials and MRAID expandables, but not video.

## Interstitials

Buyers can target and purchase interstitial impressions by using creatives with sizes appropriate for mobile interstitials. Typical mobile interstitial sizes include:

| Device Type | Portrait Size | Landscape Size |
|---|---|---|
| Phone | 320x480 | 480x320 |
| Tablet | 768x1024 | 1024x768 |

When setting up an interstitial creative, buyers should choose the Standard Banner media type and enter one of the interstitial creative sizes listed above.

> [!IMPORTANT]
> The Interstitial media type is not currently supported on external mobile supply partners' inventory; you must select the Standard Banner media type.

## MRAID expandables

This section describes how to:

- Check the bid request for MRAID impressions
- Set up MRAID expandable creatives

### Check the bid request for MRAID impressions

You can check the [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) to see if the incoming impression supports MRAID creatives using the `api` array. Check to see if the integers `3` (MRAID v1) or `5` (MRAID v2) are in the array. If they are, the impression supports MRAID creatives using that version of the specification.

For more information, see the IAB [MRAID specifications](https://www.iab.com/guidelines/mraid/).

### Set up MRAID expandable creatives

You can run expandables on mobile app inventory using MRAID creatives. These are trafficked as "Standard Banner" media types in common mobile sizes such as 300x50. Enter the HTML or JavaScript code of your MRAID creative in the `media_url` or `content` fields of the [Creative Service](creative-service.md).

Here is an example MRAID creative; note that the line at the top including `"mraid.js"` is required for it to work:

```
<script src="mraid.js"></script>
<img src="media/png" style="display: none" onerror="
        (function(img) {
            var params = {'placementId': '123456','clickUrl':'${CLICK_URL}','clickEvent':'advertiser','externalAdServer':'AppNexus'};
            var req = document.createElement('script');
            req.id = params.scriptId = 'the-company-script-' + (window.theCompanyScriptIndex = (window.theCompanyScriptIndex||0)+1);
            params.clientTimestamp = new Date/1000;
            req.src = (window.location.protocol == 'https:' ? 'https' : 'http') + '://ads.the-company.com/mraid-ad.js?';
            for (var k in params) {
                req.src += '&amp;' + encodeURIComponent(k) + '=' + encodeURIComponent(params[k]);
            }
            img.parentNode.insertBefore(req, img.nextSibling);
        })(this);
    "/>
```

#### MRAID-certified

Creatives that are MRAID-certified may serve on external mobile supply sources. During the Xandr creative audit process, MRAID creatives with expandable characteristics will only be flagged with the MRAID technical attribute and not with the expandable technical attribute.

#### Non-MRAID-certified

Non-MRAID creatives that have expandable features will not serve on external mobile supply. If there are expandable features, our audit team will mark these creatives as having an Expandable media type.

> [!WARNING]
> Creatives that are of the media type Expandable will not serve on external mobile supply.

## Supported rich media types by seller

> [!NOTE]
> All of the mobile sellers in this table support both interstitials and expandables.

| Mobile Seller | Member ID | MRAID Support? | HTML5 Support? | Supported Rich Media Vendors |
|---|---|---|---|---|
| Inneractive | 2047 | Yes | Yes | - Celtra  <br> - Phluant  <br> - Crisp  <br> - Medialets  <br> - AdGibbons |
| Microsoft Mobile | 280 | Yes | Yes |  |
| Millennial Media | 2066 | Yes | Yes | - Addroid  <br> - AdGibbon  <br> - Adxcel  <br> - Celtra  <br> - Collective  <br> - Crisp  <br> - Flashtalking  <br> - GoldSpot  <br> - Google/DART  <br> - Innovid  <br> - JustAd  <br> - Medialets  <br> - MediaMind  <br> - Mediaplex  <br> - MixPo  <br> - Mobile-5  <br> - MobSmith  <br> - Phluant  <br> - Pointreach  <br> - Pointroll  <br> - Pontiflex  <br> - Simplytics  <br> - Sprout  <br> - Unruly Media  <br> - Vdopia |
| MoPub | 1813 | Yes | Yes | - Celtra  <br> - Medialets  <br> - Crisp  <br> - Adxcel  <br> - Sprout/InMobi  <br> - Xtopoly |
| Nexage | 1868 | Yes | Yes | - Celtra  <br> - Medialets |
| Smaato | 1752 | Yes | Yes | - Celtra v1-v3, MRAID  <br> - JustAd  <br> - Medialets  <br> - Crisp  <br> - Phluant  <br> - AdGibbon |

## Related topics

- [Expandables and Rich Media](expandables-and-rich-media.md)
- [Creative Service](creative-service.md)
- [Creative Template Service](creative-template-service.md)
