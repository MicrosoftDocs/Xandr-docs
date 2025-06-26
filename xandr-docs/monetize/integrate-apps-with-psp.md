---
title: Integrate Apps with PSP
description: Learn how to integrate app inventory with PSP. This article provides detailed information and useful resources for integration.
ms.date: 06/26/2025
---

# Integrate apps with PSP

Prebid Server Premium (PSP) supports three options for Direct Supply customers to integrate app inventory:

- Prebid Mobile SDK
- [Non-SDK](non-prebid-integrations-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)

Microsoft Monetize Ad Server customers do not need to change their current integration into Microsoft Monetize and can instead follow the steps mentioned in [Integrate with PSP](integrate-with-psp.md).

## Prebid mobile SDK

### Context

For Direct Supply customers using a mobile app integrated with the Prebid Mobile SDK, Microsoft Monetize sends all bids when the app calls the `/openrtb2/prebid` endpoint, regardless of their ad server line item setup, which may be consolidated (top bid) or bidder-specific (all bids). Microsoft Monetize's Prebid bid response includes Prebid key-values (bidder, price, deal, etc.) for Microsoft Monetize SSP and each SSP demand partner that submitted a valid bid into the PSP auction along with the standard top bid key-values.

### Implementation

To set up Prebid Mobile SDK with PSP:

1. [Implement Prebid Mobile SDK](https://docs.prebid.org/prebid-mobile/prebid-mobile-getting-started.html).

1. In the host section of global settings, update the host URL to the `/openrtb2/prebid` endpoint as shown below:

    ```
    Host custom = Host.CUSTOM;
    custom.setHostUrl("https://ib.adnxs.com/openrtb2/prebid");
    PrebidMobile.setPrebidServerHost(custom); 
    ```

1. While setting up the Prebid Server account, use the publisher's `member id` as the `account id` as shown below:

    ```
    PrebidMobile.setPrebidServerAccountId("Your member id");
    ```

1. While setting up the AdUnits, replace `config id` with the `placement id`. For example, for Banner, Native, and Video Ad Units:

    ```
    BannerAdUnit adUnit = new BannerAdUnit("Your placement id", size.first, size.second);
    NativeAdUnit nativeAdUnit = new NativeAdUnit("Your placement id");
    VideoAdUnit adUnit = new VideoAdUnit("Your placement id", 640, 480, VideoAdUnit.PlacementType.IN_BANNER);
    ```

1. In the Initialize SDK documentation section, note the PSP status endpoint to use is `https://ib.adnxs.com/status`. Implemented, this would be:

   ```
   PrebidMobile.setCustomStatusEndpoint("https://ib.adnxs.com/status")
   ```

1. When offering native inventory through the Prebid Mobile SDK, set `PrebidMobile.assignNativeAssetID(true)` immediately after SDK initialization.
1. Proceed with [PSP Setup](set-up-prebid-server-premium.md) steps.
   > [!NOTE]
   > Prebid Mobile SDK iOS integrations can leverage both tracking and non-tracking domains as detailed [here](https://docs.prebid.org/prebid-mobile/pbm-api/ios/code-integration-ios.html#handling-tracking-domains). The relevant PSP domains are:
  > ```
  > trackingURL = "https://ib.adnxs.com/openrtb2/prebid"
  > nonTrackingURL = "https://adnxs-simple.com"
  > ```

<!--## Non-SDK

### Context

The Prebid Mobile SDK integration method mentioned above returns Prebid key values to the ad server. If the SDK is not implemented and Prebid key values are not needed for PSP demand to compete in the ad server's auction, the SSP customer's existing integration into Microsoft Advertising can be used as listed below:

- `/openrtb2` (For more details see, [Incoming Bid Request from SSPs](../supply-partners/incoming-bid-request-from-ssps.md))
- Video tags (For more details see, [Integrating In-Stream Video with Tags](integrating-in-stream-video-with-tags.md))
  - `/ptv` (client-side video)
  - `/ssptv` (server-side video)
  - `/vmap` (long-form client-side video)
  - `/ssvmap` (long-form server-side video)

### Implementation

In this scenario, maintain the above integration methods and proceed with the steps mentioned in [Integrate with PSP](integrate-with-psp.md).

## Long-form video

### Context

SSP customers with long-form, ad pod app inventory must use the `/prebid/lfv` endpoint. Long-form video durations are at least 30 minutes with potential pre, mid, and post-roll positions.

### Implementation

In this scenario, make POST calls to the `/prebid/lfv` endpoint as detailed under the [Long Form Video Service](../digital-platform-api/long-form-video-service.md).-->

## Related topics

- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Integrate Accelerated Mobile Pages with PSP](integrate-accelerated-mobile-pages-with-psp.md)
- [Non-prebid Integrations with PSP](non-prebid-integrations-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)
- [PSP supported formats and integration paths](./prebid-server-premium-supported-formats-and-integration-paths.md)
