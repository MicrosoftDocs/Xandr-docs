---
title: Video Guidance
description: Learn how to run video inventory through Prebid Server Premium (PSP). This page covers concepts on Instream and Outstream along with examples.   
ms.date: 10/28/2023
---

# Video guidance

This page includes guidance on running video inventory through Prebid Server Premium (PSP).

## Web **Prebid.js** send top bid

Guidance on setting up the Prebid.js "send top bid" integration can be found [here](integrate-web-mobile-web-with-psp.md). To ensure video inventory is accurately represented to demand partners through the `/ut/v3/prebid` integration:

1. Ensure the **Prebid.js** version is 8.47.0 or higher is being used.
1. Set `tags.video.context` based on the [values listed in the table](../supply-partners/integration-with-openrtb-2-6.md) under the section **Using "Plcmt and Placement fields together" > Xandr extensions** column.
1. Set `tags.video.startdelay`.
1. Configure other fields, such as `minduration`, `maxduration`, `playback_method`, `skippable`, and so on, as normal.

## Web **Prebid.js** send all bids

Guidance on setting up the *Prebid.js* send all bids integration [can be found here](../monetize/integrate-web-mobile-web-with-psp.md). To ensure video inventory is accurately represented to demand partners through the `/openrtb2/prebid` integration:

1. Ensure the *Prebid.js* version is 8.47.0 or higher is being used.
1. Set `*video.plcmt` based on the [values listed here](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md#list--plcmt-subtypes---video-):

    - instream
    - accompanying content
    - interstitial
    - no content/standalone

1. Set `video.placement` based on the values listed here

    - instream
    - in-banner
    - in-article
    - in-feed
    - interstitial/slider/floating
  
1. Set **video.startdelay** based on the values listed here

    - `>0` mid-roll (value indicates start delay in second)
    - `0` pre-roll
    - `-1` generic mid-roll
    - `-2` generic post-roll

1. If needed or preferred, instead of setting `video.plcmt` and `video.placement` in the bid request, the `imp.video.ext.appnexus.context` field can be used based on [values listed here](../supply-partners/integration-with-openrtb-2-6.md). The final request to demand partners will include `video.placement` and `video.plcmt` based on the logic [in the documentation](../supply-partners/integration-with-openrtb-2-6.md).
1. Set other fields, such as `minduration`, `maxduration`, `playbackmethod`, `skip`, and so on, as normal.
1. For more information on Monetize's support for OpenRTB 2.6, [see this page](../supply-partners/integration-with-openrtb-2-6.md).

### Instream

- Include the Microsoft Advertising PSP `cache.url` object in the config settings as shown in the following example:

  ``` 
  pbjs.setConfig({
     "cache":{
        "url":"https://prebid.adnxs.com/pbc/v1/cache"
     },
     "debug":true,
     "enableSendAllBids":true,
     "s2sConfig":{
        "accountId":9325,
        "bidders":[
           "appnexus"
        ],
        "defaultVendor":"appnexuspsp"
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
                 "bidder":"appnexus",
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
              "bidder":"appnexus",
              "params":{
                 "placementId":1234567,
                 "//first_comment":"Your placement ID."
              }
           }
        ]
     }
  ])                        
                          
  ```

- Microsoft Advertising response includes `prebid.type=video`, but if the user sets additional key-value targeting for Prebid, as shown in the below example, then the `hb_format=video` key-value will be sent to Google Ad Manager (GAM) and can be targeted accordingly.

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

- To leverage passing contextual key-values into the auction, be sure to upgrade to `Prebid.js` version 6.14.0 or higher, and define adUnit-level keywords accordingly. To ensure that the ad request is made properly for `Prebid.js s2s` (with PSP), pass adUnit-level keywords to Microsoft Advertising by including the keywords object within the adUnit definition as shown in the following example:

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
              "bidder":"appnexus",
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

## Related topics

- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Non-prebid Integrations with PSP](non-prebid-integrations-with-psp.md)
- [PSP supported formats and integration paths](prebid-server-premium-supported-formats-and-integration-paths.md)
- [Integration with OpenRTB 2.6 protocol](../supply-partners/integration-with-openrtb-2-6.md)
