---
title: Video Guidance
description: Learn how to run video inventory through Prebid Server Premium (PSP). This page covers concepts on Instream and Outstream along with examples.   
ms.date: 12/19/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Video guidance

This page includes guidance on running video inventory through Prebid Server Premium (PSP).

<!--## Web **Prebid.js** send top bid

Guidance on setting up the Prebid.js "send top bid" integration can be found [here](integrate-web-mobile-web-with-psp.md). To ensure video inventory is accurately represented to demand partners through the `openrtb2/prebidjs` integration:

1. Ensure the **Prebid.js** version is 10.13.0 or higher is being used.
1. Set `tags.video.context` based on the [values listed in the table](../supply-partners/integration-with-openrtb-2-6.md) under the section **Using "Plcmt and Placement fields together" > Xandr extensions** column.
1. Set `tags.video.startdelay`.
1. Configure other fields, such as `minduration`, `maxduration`, `playback_method`, `skippable`, and so on, as normal.
1. For more information about Monetize's support for OpenRTB 2.6, see [Integration with OpenRTB 2.6](../supply-partners/integration-with-openrtb-2-6.md).-->

## Web **Prebid.js** integrations

Guidance on setting up the **Prebid.js** integrations [can be found here](integrate-web-mobile-web-with-psp.md). To ensure video inventory is accurately represented to demand partners through either the `/openrtb2/prebidjs` or /`openrtb2/prebid` integrations:

1. Ensure the *Prebid.js* version is 10.13.0 or higher is being used.
1. Include the header `x-openrtb-version: 2.6`.
2. Set `video.plcmt` based on the [values listed here](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md#list--plcmt-subtypes---video-):

    - `1` instream
    - `2` accompanying content
    - `3` interstitial
    - `4` no content/standalone

3. Set `video.placement` based on the [values listed here](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md#list--placement-subtypes---video-)

    - `1` instream
    - `2` in-banner
    - `3` in-article
    - `4` in-feed
    - `5` interstitial/slider/floating
  
4. Set `video.startdelay` based on the [values listed here](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md#list--start-delay-modes-)

    - `>0` mid-roll (value indicates start delay in second)
    - `0`  pre-roll
    - `-1` generic mid-roll
    - `-2` generic post-roll

<!--5. If needed or preferred, instead of setting `video.plcmt` and `video.placement` in the bid request, the `imp.video.ext.appnexus.context` field can be used based on [values listed here](../supply-partners/integration-with-openrtb-2-6.md). The final request to demand partners will include `video.placement` and `video.plcmt` based on the logic [in the documentation](../supply-partners/integration-with-openrtb-2-6.md).-->
5. Set other fields, such as `minduration`, `maxduration`, `playbackmethod`, `skip`, and so on, as normal.
6. For more information on Monetize's support for OpenRTB 2.6, [see this page](../supply-partners/integration-with-openrtb-2-6.md).

### Instream

- Include the Monetize PSP `cache.url` object in the config settings as shown in the following example:

  ``` 
  pbjs.setConfig({
     "cache":{
        "useLocal":true
     },
     "debug":true,
     "enableSendAllBids":true,
     "s2sConfig":{
        "accountId":9325,
        "bidders":[
           "msft"
        ]
     }
  });                        
                          
  ```

- To ensure that the relevant cache key-values are returned, include the `extPrebid.cache.bids[{}]` object within the `s2sConfig` as shown in the following example:

  ``` 
  extPrebid = ([
     {
        "cache":{
           "bids":[
              {
                 "bidder":"msft",
                 "params":{
                    "placementId":1234567
                 }
              }
           ]
        },
        "targeting":{
           "includebidderkeys":true,
           "includewinners":true
        }
     }
  ])                       
                          
  ```

### Outstream

- To ensure that the ad request is made for `Prebid.js s2s` (with PSP), include the renderer object within the adUnit definition as shown in the following example:

  ``` 
  var adUnits = ([
     {
        "code":"video1",
        "//first_comment":"This renderer would apply to all prebid creatives.",
        "renderer":{
           "url":"https://acdn.adnxs.com/video/outstream/ANOutstreamVideo.js",
           "render":"function (bid)",
           "ANOutstreamVideo.renderAd":{
              "targetId":"bid.adUnitCode",
              "adResponse":"bid.adResponse"
           }
        },
        "mediaTypes":{
           "video":{
              "context":"outstream",
              "playerSize":[
                 640,
                 480
              ],
              "mimes":[
                 "video/mp4"
              ],
              "protocols":[
                 1,
                 2,
                 3,
                 4,
                 5,
                 6,
                 7,
                 8
              ],
              "playbackmethod":[
                 2
              ],
              "skip":0,
              "playback_method":[
                 "auto_play_sound_on"
              ]
           }
        },
        "bids":[
           {
              "bidder":"msft",
              "params":{
                 "placementId":1234567,
                 "//first_comment":"Your placement ID."
              }
           }
        ]
     }
  ])                        
                          
  ```

- Monetize response includes `prebid.type=video`, but if the user sets additional key-value targeting for Prebid, as shown in the below example, then the `hb_format=video` key-value will be sent to Google Ad Manager (GAM) and can be targeted accordingly.

  ``` 
  {
     "targetingControls":{
        "addTargetingKeys":[
           "SOURCE",
           "ADOMAIN",
           "FORMAT"
        ]
     }
  }                        
                          
  ```

- To leverage passing contextual key-values into the auction, be sure to upgrade to `Prebid.js` version 6.14.0 or higher, and define adUnit-level keywords accordingly. To ensure that the ad request is made properly for `Prebid.js s2s` (with PSP), pass adUnit-level keywords to Monetize by including the keywords object within the adUnit definition as shown in the following example:

  ``` 
  var adUnits = ([
     {
        "code":"div-1",
        "mediaTypes":{
           "banner":{
              "sizes":[
                 {
                    "height":600,
                    "width":160
                 }
              ]
           }
        },
        "bids":[
           {
              "bidder":"msft",
              "params":{
                 "placementId":21230286,
                 "keywords":{
                    "test-key":[
                       "test-value"
                    ]
                 }
              }
           }
        ]
     }
  ])
  ```

- For more information, see [Ad Unit specific data](https://docs.prebid.org/features/firstPartyData.html#supplying-adunit-specific-data) and [auction-level keywords](https://docs.prebid.org/dev-docs/bidders/appnexus.html#appnexus-auction-keywords).

## Demand partner response

Demand partners should send duration with all bids to ensure ads fill the expected time for both instream and ad pod opportunities.
- Instream: Duration is not strictly required. If duration sent is 0 the bid could still win and serve but Monetize cannot ensure the video is the appropriate length.
- Ad Pod: Bids must include the video creative duration in either `bid.dur` (for OpenRTB 2.6) or `ext.prebid.video.duration` (if OpenRTB 2.6 is not yet supported). Note that the duration is not parsed from XML.

## External ad server setup

When an ad server other than Monetize is used, Prebid line items and the associated creative might require a VAST tag URL or a cache URL. More information about these scenarios are available in Prebid.org [documentation](https://docs.prebid.org/adops/setting-up-prebid-video-in-dfp.html).

When using an external ad server with PSP,
- configure Prebid.js web: See Prebid.js client-side caching and local client-side caching options documented [here](https://docs.prebid.org/dev-docs/publisher-api-reference/setConfig.html#client-side-caching-of-vast-xml) and configure according to your requirement. Also, see `setConfig` bid cache functions [here](https://docs.prebid.org/dev-docs/publisher-api-reference/setConfig.html) and take appropriate steps.
- configure Prebid Mobile SDK app: Ideally the ad server combines the `hb_cache_host` and `hb_cache_path` targeting keys from the PSP response to get the full and dynamic cache URL. If that is not supported, the ad server requires a static and hard-coded path. You can use `https://ib.adnxs.com/prebid/cache?uuid=%%PATTERN:hb_uuid_BIDDERCODE%%` as static url.


## Related topics

- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Non-prebid Integrations with PSP](non-prebid-integrations-with-psp.md)
- [PSP supported formats and integration paths](prebid-server-premium-supported-formats-and-integration-paths.md)
- [Integration with OpenRTB 2.6 protocol](../supply-partners/integration-with-openrtb-2-6.md)
