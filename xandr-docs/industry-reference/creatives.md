---
title: Creatives
description: In this article, learn about creatives, their types, CDNs, impressions, and ways to track clicks and conversions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Creatives

> [!NOTE]
> You may want to read [Introduction to Ad Serving](introduction-to-ad-serving.md) and [Ad Tags](ad-tags.md) first.

A creative is the actual advertisement viewed by a user. Creatives can function purely to promote a brand, but because the Internet is based round interactive media and experiences, many online creatives are intended to convince a user to take some action, like sign up for membership or make a purchase. Creative formats include GIF, JPEG, JavaScript, Flash, HTML5, video, and mobile. Creatives can be static images or they can contain video; they can expand or respond to user input. These files are managed via an [ad server](introduction-to-ad-serving.md), which is responsible for sending the file to the browser at the time of an ad call.

## Types of creatives

There are many kinds of creatives used on the Internet. Some of the key types include:

- **Banner ads** - Text or image ads that appear above or alongside content.
- **Expandable ads** - Ads that can be enlarged beyond their initial dimensions, often by user interactions such as scrolling down the page or mousing over the ad.
- **Pop ads** - Ads that display in a secondary browser window. Pop-up ads display in front of the initial browser window, while pop-under ads display behind it.
- **Video ads** - Video ads may play before, during, or after the main video content. You can see examples of this type of ad on [YouTube](https://www.youtube.com) and [Hulu](https://www.hulu.com).
- **Mobile ads** - Mobile ads may be in-app ads or web ads that are optimized for display on mobile devices.

## Creatives and impressions

An impression is the display of a single creative to a single user at a certain point in time. Sometimes serving a creative and serving an impression are essentially the same thing, but often the server deciding which advertiser should display a creative, the server deciding which creative should be shown, and the [CDNs](#what-are-cdns-content-delivery-networks) (content delivery network) that actually hosts and returns the creative image file are all different. In this case, the act of serving an impression and the act of serving the creative are two different events. In reporting, no matter how many servers are involved, the number of impressions and creatives served should match, if all went smoothly.

:::image type="content" source="media/creatives-and-impressions.png" alt-text="Diagram that shows how impression tracking pixels work.":::

This is a simple example of an advertiser that uses a CDN (Content Delivery Network) rather than an ad server to host its creatives.

Here's how it works:

1. When the user visits a publisher web site, the browser sends an ad tag to the ad server. This ad tag contains information about the user and the ad placement.
1. The ad server optionally passes an ad tag to a third-party data provider to retrieve information about user segmenting or contextual targeting.
1. The ad server then passes an ad tag to the advertisers. Depending on the publisher-advertiser relationship, this may mean simply directly requesting ads for guaranteed buys, or it may involve requesting bids from multiple advertisers and carrying out an auction to determine the most profitable result for the publisher.
1. The ad server returns an ad tag with a creative URL to the browser.
1. The browser retrieves the creative and an associated **impression tracking pixel** from the CDN (Content Delivery Network). ("Pixel" is something of a misnomer: this is a piece of JavaScript more often than it's an image.) Even though the ad server doesn't serve the creative, the pixel will allow the ad server to record impressions.

## What are CDNs (Content Delivery Networks)?

A Content Delivery Network is a huge network of servers located across the globe that exist to deliver static content quickly. Most advertisers prefer to have all their creatives served from a CDN in order to simplify reporting and creative updates. Advertisers may work with many different networks, exchanges, publishers, or platforms, and if creatives were hosted by each of these, their reporting data would be scattered. In addition, the advertiser may want to maintain control over its creatives and probably wants to independently verify that its creatives are being properly served. With a single ad server, the advertiser can compare impression numbers with its partners to make sure everything is working correctly.

Occasionally, an advertiser will use the ad server to host creatives instead of a separate CDN. Possible reasons include:

- A desire to minimize redirects and latency.
- The publisher may ban third-party tags because such tags can rotate creatives and be generally hard to audit.

## Tracking clicks and conversions

Advertisers and publishers may also want to track a creative's performance. For display advertising, this typically means tracking clicks and conversions.

- **Clicks** - When users click on a creative, they are directed to a landing page. For example, they see an ad for Prostarr Sportswear, they click on the ad, and they are directed to prostarr.com/summersale. These clicks can be tracked by either a pixel on the landing page or a URL associated with the creative. If you track clicks through a pixel, the pixel fires when the landing page loads. If you track clicks through the creative URL, the creative URL directs the browser to a click-tracking server before redirecting it to the landing page.
- **Conversions** - The user performs some desired action such as making a purchase or signing up for membership. This can happen immediately or during a specified "lookback" period, if advertiser and publisher agree to count the user as a conversion as long as they perform the action within that time period. Conversions may also be called acquisitions. They're generally tracked through a pixel on the confirmation page for the action (for example, the confirmation that users see when they've purchased items or signed up for mailing lists).

## Child pages

- [Integrating the Xandr HTML5 Library with Ads Created in Adobe Edge](integrating-the-xandr-html5-library-with-ads-created-in-adobe-edge.md)
- [Integrating the Xandr HTML5 Library with Ads Created in Google Web Designer](integrating-the-xandr-html5-library-with-ads-created-in-google-web-designer.md)
- [Use IAB's HTML5 clickTag Standard on Xandr](use-iab-s-html5-clicktag-standard-on-xandr.md)
- [Build an HTML5 Xandr Creative in Google Web Designer](build-an-html5-xandr-creative-in-google-web-designer.md)
- [Build an HTML5 Xandr Creative in Adobe Edge](build-an-html5-xandr-creative-in-adobe-edge.md)
- [Build an HTML5 Xandr Creative in Adobe Animate CC](build-an-html5-xandr-creative-in-adobe-animate-cc.md)

## Related topic

[Ad Tags](ad-tags.md)
