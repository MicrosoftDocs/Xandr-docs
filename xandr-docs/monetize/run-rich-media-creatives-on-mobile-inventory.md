---
title: Microsoft Monetize - Run Rich Media Creatives on Mobile Inventory
description: Learn how to set rich media creatives to serve on mobile devices in this page. This page talks about Interstitials impressions and where MRAID-Certified and Non-MRAID-Certified creatives will serve.  
ms.date: 10/28/2023
---


# Microsoft Monetize - Run rich media creatives on mobile inventory

This document describes how to set up your rich media creatives to serve on mobile devices. It also contains a list of media types supported by each major seller. Note that this is not an exhaustive guide to targeting and running mobile ad campaigns; for a complete description of our mobile targeting, see [Buy Mobile Inventory via RTB](buy-mobile-inventory-via-rtb.md).

> [!NOTE]
> For the purposes of this document, rich media creatives are defined as **interstitials** and **MRAID expandables**, but not video.
> [!TIP]
>
> - For an introduction to how MRAID and Mobile Video work, see [MRAID and Mobile Video Tutorial](../industry-reference/mraid-and-mobile-video-tutorial.md).
> - For more information on how to correctly submit your mobile creatives
> (including MRAID) for audit, see [Mobile Creative Auditing](mobile-creative-auditing.md).

## Interstitials

Buyers can target and purchase interstitial impressions by using creatives with sizes appropriate for mobile interstitials. Typical mobile interstitial sizes include:

| Device Type | Portrait Size | Landscape Size |
|--|--|--|
| Phone | 320x480 | 480x320 |
| Tablet | 768x1024 | 1024x768 |

> [!NOTE]
> For an app interstitial, the size is 1x1.

When setting up an interstitial creative, buyers should select the **Standard Banner** media type and enter one of the interstitial creative sizes listed above. The above sizes are the most common interstitial sizes and apply for all operating systems. Although these creatives will serve as interstitials on mobile devices, they are really just standard, static banner creatives.

> [!WARNING]
> The **Interstitial** media type is not currently supported on external mobile supply partners' inventory; you must select the **Standard Banner** media type.

## MRAID expandables

You can run expandables on mobile app inventory using MRAID creatives. These are trafficked as **Standard Banner** media types in common mobile sizes such as 300x50. Select **Third-party creative** and enter the HTML or JavaScript code of your MRAID creative in the **Tag** text area.

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

## MRAID-Certified

Creatives that are MRAID-certified may serve on external mobile supply sources. During the Microsoft Advertising creative audit process, MRAID creatives with expandable characteristics will only be flagged with the MRAID technical attribute and not with the expandable technical attribute.

## Non-MRAID-Certified

Non-MRAID creatives that have expandable features will **not** serve on external mobile supply. If there are expandable features, our audit team will mark these creatives as having an **Expandable** media type. Expandables will not serve on external mobile supply.

> [!WARNING]
> Creatives that are of the the media type **Expandable** will **not** serve on external mobile supply. For more information about how Microsoft Advertising audits mobile creatives, see [Mobile Creative Auditing](mobile-creative-auditing.md).

## Supported rich media types by seller

All of the mobile sellers in this table support both interstitials and expandables.

| Mobile Seller | Member ID | MRAID Support? | HTML5 Support? | Supported Rich Media Vendors |
|--|--|--|--|--|
| Inneractive | 2047 | Yes | Yes | - Celtra<br> - Phluant<br> - Crisp<br> - Medialets<br> - AdGibbons |
| Microsoft Mobile | 280 | Yes | Yes |  |
| Millennial Media | 2066 | Yes | Yes | - Addroid<br> - AdGibbon<br> - Adxcel<br> - Celtra<br> - Collective<br> - Crisp<br> - Flashtalking<br> - GoldSpot<br> - Google/DART<br> - Innovid<br> - JustAd<br> - Medialets<br> - Mediamind<br> - Mediaplex<br> - MixPo<br> - Mobile-5<br> - MobSmith<br> - Phluant<br> - Pointreach<br> - Pointroll<br> - Pontiflex<br> - Simplytics<br> - Sprout<br> - Unruly Media<br> - Vdopia |
| MoPub | 1813 | Yes | Yes | - Celtra<br> - Medialets<br> - Crisp<br> - Adxcel<br> - Sprout/inmobi<br> - Xtopoly |
| Nexage | 1868 | Yes | Yes | - Celtra<br> - Medialets |
| Smaato | 1752 | Yes | Yes | - Celtra v1-v3, MRAID<br> - JustAd<br> - Medialets<br> - Crisp<br> - Phluant<br> - AdGibbon<br> - [certified rich media vendors](https://www.smaato.com/certified-rich-media-vendors/) |

## Related topics

- [Mobile Creative Auditing](mobile-creative-auditing.md)
- [Buying Mobile Inventory](buying-mobile-inventory.md)