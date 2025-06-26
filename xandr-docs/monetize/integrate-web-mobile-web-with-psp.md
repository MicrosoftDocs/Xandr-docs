---
title: Integrate Web/Mobile Web with PSP
description: In this article, find information about how to integrate web and mobile web inventory with PSP.
ms.date: 06/26/2025
---

# Integrate web/mobile web with PSP

Prebid Server Premium (PSP) supports four options for Direct Supply customers to integrate web and mobile web inventory:

- Prebid.js Send Top Bid
- Prebid.js Send All Bids
- [Non-prebid](non-prebid-integrations-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)

Monetize Ad Server customers do not need to change their current integration into Microsoft Monetize and can instead follow the [PSP Setup Steps](set-up-prebid-server-premium.md).

## Prebid.js send top bid

### Context
In general, Send Top Bid should be used by default when publishers do not have bidder-specific line items already set up in their ad server, or if they do not need all bids for reporting purposes. By using the Send Top Bid option, the winning bid response will indicate Microsoft Monetize as the winner with a buyer member ID as normal even if a separate SSP Demand Partner won through Prebid Server Premium. The publisher's ad server will see Microsoft Monetize as the winner if this top bid wins the ad server auction. Publishers can determine which SSP won, either Microsoft Monetize or another Demand Partner via Prebid Server Premium, by utilizing Microsoft Monetize's [reporting and analytics](prebid-server-premium-analytics.md) and cross-referencing the other SSP Demand Partners' reporting.

### Implementation

To set up Prebid.js with Send Top Bid:

1. [Integrate with a Prebid.js instance](https://docs.prebid.org/prebid/prebidjs.html) that uses the [Microsoft Monetize (AppNexus) Prebid.js adapter](https://docs.prebid.org/dev-docs/bidders/appnexus.html).

    This should not require any changes to the "appnexus" adapter setup on page if already integrated through Microsoft Monetize this way.

1. Call the Microsoft Monetize SSP client-side using the `/ut/v3/prebid` endpoint.

1. If Demand Partners are already being called client-side, remove partners other than 'appnexus' (Microsoft Monetize) from the Prebid.js client-side instance.

1. Configure those, and any additional SSP Demand Partners, in Microsoft Monetize via **Publishers** > **Prebid Server Premium** > **Demand Partner Configurations**.

    For more information, see [Add, Edit, or Delete a PSP Configuration](add-edit-or-delete-a-psp-configuration.md).

1. For video-specific nuances, see the guidance [here](video-guidance.md).
1. Proceed with [PSP Setup steps](set-up-prebid-server-premium.md).


## Prebid.js send all bids

### Context

Send All Bids should be used if Demand Partner-specific line items in the ad server are absolutely required. PSP will set key value targeting for the top CPM bid, along with the standard top bid key values (bidder, price, deal) for each included Demand Partner per ad unit.

### Implementation

To set up Prebid.js with Send All Bids:

1. [Integrate with a Prebid.js instance](https://docs.prebid.org/prebid-server/use-cases/pbs-pbjs.html) that uses the [Microsoft Monetize (AppNexus) Prebid.js adapter](https://docs.prebid.org/dev-docs/bidders/appnexus.html).

    This should not require any changes to the "appnexus" adapter setup on page if already integrated through Microsoft Monetize this way.

   > [!NOTE]
   > When using Prebid.js 10 and higher, the anPspParamsConverter module is not necessary.
   > When using Prebid.js 9.x, include the anPspParamsConverter module in every Prebid.js build for pages that use Microsoft Monetize for PSP demand. This module converts client-side calls to the format required for server-side endpoints.

1. Call the Microsoft Monetize SSP client-side using the `/openrtb2/prebid` endpoint

1. Follow the Prebid GitHub example [here](https://github.com/prebid/Prebid.js/blob/master/integrationExamples/gpt/prebidServer_example.html).

Make the below changes to the s2sConfig:

1. Set the **accountId** to your Microsoft Monetize Seller Member ID.

1. Set **enabled** to **true**.

1. Set **defaultVendor** to **'appnexuspsp'**.

1. Set **allowUnknownBidderCodes** to **true**.

1. Include both **includebidderkeys**, **includewinners**, and **includeformat** in the **extPrebid targeting** object as shown in the following example:

    ```
    extPrebid = ([
       {
          "targeting":{
             "includebidderkeys":true,
             "includewinners":true,
             "includeformat":true
          }
       }
    ])            
                
    ```

1. Include **'appnexus'** in **bidders**.

1. Set the timeout value to the number of ms the browser should wait for a response from Microsoft Monetize.

    > [!NOTE]
    > This value should be greater than your Microsoft Monetize (PSP) auction timeout. If the value is lower, there is a risk that the client-side timeout will hit before Microsoft Monetize responds with a bid, potentially preventing receipt of demand from Microsoft Monetize. For more information, see the Demand Partner Timeout section in [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md).

   See below for a **s2sConfig** example:

   ```
   pbjs.setConfig({
   "s2sConfig":{
      "accountId":9325,
      "bidders":[
         "appnexus"
      ],
      "defaultVendor":"appnexuspsp",
      "enabled":true,
      "allowUnknownBidderCodes":true,
      "timeout":1000,
      "extPrebid":{
         "targeting":{
            "pricegranularity":"dense",
            "includebidderkeys":true,
            "includewinners":true,
            "includeformat":true
               }
            }
         }
   })        

   ```

   When using Send All Bids, report on the key values in an external ad server, such as Google Ad Manager (GAM), by defining key values appropriately and setting them as reportable. GAM documentation can be found [here](https://support.google.com/admanager/answer/7352444?hl=en).

1. For video-specific nuances, see the guidance [here](video-guidance.md).
1. Proceed with [PSP Setup steps](set-up-prebid-server-premium.md).

### Targeting key values

As noted above, it is recommended to set all three parameters (`includebidderkeys`, `includewinners`, `includeformat`) to true to receive the most information from PSP in the form of targeting key values.

In the `s2sConfig`, at least one of `includewinners` or `includebidderkeys` must be set to true to receive any targeting keys.

If `includewinners` is true, the following targeting keys will be received:

- `"hb_bidder": "appnexus"`,
- `"hb_pb": "0.00"`,
- `"hb_size": "600x500"`

If `includebidderkeys` is true, the following targeting keys will be received:

- `"hb_bidder_appnexus": "appnexus"`,
- `"hb_pb_appnexus": "0.00"`,
- `"hb_size_appnexus": "600x500"`

If `includeformat` is also set to true **in addition to either of the above parameters**, this key will be received as well:

- `"hb_format_appnexus": "banner"`

<!--## Non-prebid

### Context

The above Prebid.js integration methods return Prebid key values to the ad server. If Prebid.js is not implemented on the pages and Prebid key values are not needed for PSP demand to compete in the ad server's auction, the SSP customer's existing integration into Microsoft Monetize can be used instead:

- `/openrtb2` (For more details see, [Incoming Bid Request from SSPs](../supply-partners/incoming-bid-request-from-ssps.md))
- Video tags (For more details see, [Integrating In-Stream Video with Tags](integrating-in-stream-video-with-tags.md))
  - `/ptv` (client-side video)
  - `/ssptv` (server-side video)
  - `/vmap` (long-form client-side video)
  - `/ssvmap` (long-form server-side video)
- `/ttj` (For more details see, [TinyTags](../bidders/tinytags.md))

### Implementation

In this scenario, maintain the above integration methods and proceed with the [PSP Setup Steps](integrate-with-psp.md).

## Long-form video

### Context

Direct Supply customers with long-form, ad pod web inventory must use the `/prebid/lfv` endpoint. Long-form video durations are at least 30 minutes with potential pre, mid, and post-roll positions.

### Implementation

In this scenario, make POST calls to the `/prebid/lfv` endpoint as detailed under the [Long Form Video Service](../digital-platform-api/long-form-video-service.md).-->

## Related topics

- [Integrate Apps with PSP](integrate-apps-with-psp.md)
- [Integrate Accelerated Mobile Pages with PSP](integrate-accelerated-mobile-pages-with-psp.md)
- [Prebid Server Premium Identity & User Syncing](prebid-server-premium-identity-and-user-syncing.md)
- [Non-prebid Integrations with PSP](non-prebid-integrations-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)
- [PSP supported formats and integration paths](./prebid-server-premium-supported-formats-and-integration-paths.md)
- [Integration with OpenRTB 2.6 protocol](../supply-partners/integration-with-openrtb-2-6.md)
