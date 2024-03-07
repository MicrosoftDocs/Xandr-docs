---
title: Mediation FAQs
description: Learn FAQs on selling inventory through mediation. 
ms.date: 10/28/2023
---


# Mediation FAQs

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

This page has answers frequently asked questions about selling inventory through mediation.

## What is a network?

Under the hood, a mediated network is actually a managed advertiser. For this reason, if your client has any managed advertisers with the same name as one of the mediated networks we support, you will get an error when trying to add the network. You will need to rename any managed advertiser to a different name as mediated networks cannot be renamed.

## How is mediation different from RTB?

In a mediation auction, no bids are placed upfront. Selling inventory through mediation requires running the auction using an estimated bid that represents what we think the buyer will eventually pay. We later pull reporting data that shows the buyer's actual bid.

For more information about mediated auctions, see the examples in [How Auctions Work for Sellers](mediation-how-auctions-work-for-sellers.md).

## Why do I get an error when I try to add a network?

A mediated network is actually a managed advertiser "under the hood". If your client has any managed advertisers with the same name as one of the mediated networks we support, you will get an error when trying to add the network. You will need to rename any managed advertiser to a different name as mediated networks cannot be renamed.

## What happens if the highest bid is a mediated network, and they don't want the impression?

If they return a "no bid" or they timeout, our system automatically redirects to the next highest bid, whether that be another network, your own managed campaigns, or the highest RTB bid.

For more information about how auctions work for sellers using mediation, see the examples in [How Auctions Work for Sellers](mediation-how-auctions-work-for-sellers.md).

## Why doesn't every network give me the option to enter my credentials?

We limit automated reporting to networks where we have significant demand from clients. We will only ask for credentials for networks where reporting can be automated.

## What are the APIDS, SPOT IDS, and other fields I am asked to fill in when creating a bid? Why is it different for each network?

Each mediated network requires us to pass the equivalent of a placement ID in the request for an ad. Every network calls their placement IDs something different and in some cases multiple IDs are required. The UI will prompt you for the appropriate IDs from each network to ensure proper setup.

It's very important to fill in these IDs correctly. We use these IDs to ensure that reporting data is correct.

## How often is reporting from mediated networks updated?

We update reporting once per day for all supported networks. Typically you can expect to see third-party data updated in your account by 8 am EST.

## Which time zone is mediation data reported in?

Under the Networks and Bids tabs, all data is reported relative to the network time zone. For example, Millennial Media reports its data in UTC. Therefore, the impression requests, impressions, fill rate and discrepancy metrics for Millennial Media are all reported in UTC. Likewise, AdMob reports in PST, so all data for AdMob is reported in PST. If you look at the data in the mediation screens and compare it to data in each third-party network's reporting UI, they should match.

In the Network Analytics report, we only adjust revenue from third-party networks and not impressions. Revenue is adjusted in the default time zone of the member.

## Where can I find mediated networks and bids in reporting?

- Mediated networks can be found under the Advertiser filter and dimension in the Network Analytics Report.
- Bids can be found under the Line Item filter and dimension in the Network Analytics Report.

## Do you support passbacks for mobile web and desktop impressions?

Yes.

## Can I add multiple logins for the same network?

This is not supported at this time.

## Which mediation browsers are supported?

Our mediation scripts currently support the following browsers.

When the mediation script encounters a browser that isn't supported, it will bypass all the mediated bids and call back to impbus for a response. The response can be to proceed to RTB, or serve a PSA, default creative, or blank, based on default action settings for the seller and placement.

**Desktop**

- Chrome
- Firefox
- Internet Explorer 8-11
- Opera
- Safari

**Mobile**

- Safari
- Android
- Chrome

## Which mediation networks are supported?

The table below lists the external mediation networks we support. It includes information about the type of integration we have with each network, and whether we pull reporting data from that network.

The Integration Type column describes how the network is integrated for mediation.

- Client indicates that the integration occurs on the client side; works only on the desktop web and mobile web.
- Server indicates that the integration occurs on the server side; works on mobile web and mobile apps, but works best on mobile apps.
- SDK indicates that the network's SDK must be downloaded and implemented. Works only on mobile apps.

  > [!WARNING]
  > We will make our best effort to keep this information up to date. However, more current information may be available directly from the networks.

| Network | Optimized for display on... | Optimized for display on... | Optimized for display on... | Reporting? | Integration Type | Contact | Downloads (SDK only) |
|--|--|--|--|--|--|--|--|
|  | **Mobile App** | **Mobile Web** | **Desktop Web** |  |  |  |  |
| AdColony | X |  |  | No | SDK | [AdColony Support](https://www.digitalturbine.com/app-developers/#monetizationsolutions) | - [AdColony SDK](https://www.digitalturbine.com/app-developers/#monetizationsolutions) |
| AdMob | X |  |  | Yes | SDK | [AdMob Support](https://support.google.com/admob/#topic=7383088) | - [AdMob iOS SDK](https://developers.google.com/ad-manager/mobile-ads-sdk#downloadios)<br> - [AdMob Android SDK](https://developers.google.com/ad-manager/mobile-ads-sdk#downloadandroid) |
| AdSense |  | X | X | Yes | Client | [AdSense Support](https://support.google.com/adsense/#topic=3373519) | N/A |
| Amazon (mobile) | X |  |  | No | SDK | [Amazon Support](https://developer.amazon.com/public/support/contact/contact-us) | - [Amazon iOS SDK](https://developer.amazon.com/public/apis/earn/mobile-ads/ios)<br> - [Amazon Android SDK](https://developers.google.com/ad-manager/mobile-ads-sdk#downloadandroid) |
| Amazon (web) |  | X | X | No | Client | [Amazon Support](https://developer.amazon.com/public/support/contact/contact-us) | N/A |
| Claymotion | X |  |  | No | Server | [Claymotion Support](mailto:adops@claymotion.in) | N/A |
| Doubleclick for Publishers | X |  |  | No | SDK | [DFP Support](https://support.google.com/admanager/?hl=en#topic=7505988) | - [DFP SDK](https://developers.google.com/ad-manager/mobile-ads-sdk) |
| Hunt | X | X |  | No | Server | Hunt Support | N/A |
| iAd | X |  |  | No | SDK | [Apple Developer Support](https://developer.apple.com/support/) | - [iAd SDK] |
| InMobi | X | X |  | Yes | Server | [InMobi Support](https://support.inmobi.com/) | N/A |
| Jumptap | X | X |  | Yes | Server | JumpTap Support | N/A |
| Millennial Media (mobile web) |  | X |  | Yes | Client | Millennial Media Support | N/A |
| Millennial Media (mobile app) | X |  |  | Yes | SDK | Millennial Media Support | Millennial Media SDK|
| MobFox | X | X |  | Yes | Server | MobFox Support | - MobFox SDK |
| MobileFuse | X | X |  | Yes | Server | MobileFuse Support | N/A |
| Mojiva | X | X |  | Yes | Server | Mojiva Support | N/A |
| MoPub | X |  |  | No | SDK | [MoPub Support](https://dev.twitter.com/mopub/overview) | -MoPub iOS SDK<br> - MoPub Android SDK |
| OpenX | X | X |  | No | Server | [OpenX Support](http://openx.com/support/) | N/A |
| OpenX Ad Exchange |  | X | X | Yes | Client | [OpenX Support](http://openx.com/support/) | N/A |
| PubMatic |  | X | X | Yes | Client | [PubMatic Support](mailto:info@PubMatic.com) | N/A |
| Rubicon Project |  | X | X | Yes | Client | [Rubicon Support](http://www.rubiconproject.com/contact-us/) | N/A |
| Smaato | X | X |  | Yes | Server | [Smaato Support](http://www.smaato.com/support/) | N/A |
| Smaato (mobile web) |  | X |  | Yes | Client | [Smaato Support](http://www.smaato.com/support/) | N/A |
| Verve | X | X |  | No | Server | Verve Support | N/A |
| Vserv | X | X |  | Yes | Server | Vserv Support | N/A |
| Custom Mobile Network | X |  |  | No | SDK | N/A | N/A |
