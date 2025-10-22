---
title: Ad Object API
description: In this article, find information about the various eventType fields and examples for adType objects.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Ad Object API

## eventType

The following section describes the various eventType fields and their respective callback function signatures and data objects:

### adRequested

**Callback Function Signature:** `function(){}`

**Data objects:** N/A

### adAvailable

**Callback Function Signature:** `function(adObj){}`

**Data objects:**

```
adObj = {
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: '$',
adType : 'banner', // could also be 'video' or 'native'
auctionId : '123456',
buyerMemberId : 999, creativeId : 53122972,
source : 'rtb', // could also be 'csm'
tagId : 6051399,
banner : {
// will match adType above; based on source // SEE BELOW
}
}
```

Ad Type can be a banner, video, or native. See the [adType object](#adtype-object) section below for more examples.

When source is real-time bidding (rtb), the Ad Object includes the ad; when source is client-side mediation (csm), it includes just the creative ID.

### adLoaded

**Callback Function Signature:** `adLoaded`

**Data objects:** Ad Object is the same as for `adAvailable`.

### adSlotRenderStart (formerly adCodeRenderStart)

**Callback Function Signature:** `function(adObj) {}`

**Data objects:** Ad Object is the same as for `adAvailable`.

### adNoBid

**Callback Function Signature:** `function(adObj){}`

**Data objects:**

```
adObj = {
auctionId : '123456',
nobid : true,
tagId : 6051399,
}
```

> [!NOTE]
> When using Mediation, normally a mediated bid would return alongside an RTB bid for the same placement/slot. There is a chance the auction request may only return a mediated bid.
> In a normal response, if the mediated bid does not return with a creative it would attempt to fall back to the RTB bid's creative. In the case when there is no RTB bid present, the Mediation script would load the adNoBid event to signify the lack of an available RTB bid. In this case, the adObj will not be populated and the object will be undefined since there is no fallback RTB bid object present.

### adRequestFailure

**Callback Function Signature:** `function(adError){}`

**Data objects:**

```
adError = {
code : 0
errMessage : 'error message';,
exception : e,
targetId : 'apn_ad_slot_1'
}
```

### adError

**Callback Function Signature:** `function(adError, adObj){}`

**Data objects:** `adError` is the same as for `adRequestFailure`.

Ad Object is the same as for `adAvailable`.

### adBadRequest

**Callback Function Signature:** `function(adError){}`

**Data objects:** The tag called a placement that doesn't exist. This could indicate an error from the Impression Bus.

```
adError = {
code : 0
errMessage : 'error message';,
exception : e,
targetId : 'apn_ad_slot_1'
}
```

### adCollapse

**Callback Function Signature:** `function(){}`

**Data objects:** N/A

### adNoBidMediated

**Callback Function Signature:** `function(adObj)`

**Data objects:**

```
adObj = {
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: "$"
creativeId : 12345678,
contentSource : 'csm',
targetId : 7654321,
width: 728
height: 90
banner : {
width: 728,
height: 90,
content: "<!-- Creative 26299226 served by Member 12345 via Xandr --><a href=\"http://lax1.ib.adnxs.com/click?AAAAAAAA6D8AAAAAAADoPwAAAAAAAPA_AAAAAAAA6D8A…"
}
}
```

### adLoadedMediated

**Callback Function Signature:** `function(adObj)`

**Data objects:**

```
adObj = {
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: '$'
creativeId : 12345678,
contentSource : 'csm',
targetId : 7654321,
width: 728
height: 90
banner : {
width: 728,
height: 90,
content: "<!-- Creative 26299226 served by Member 12345 via AppNexus --><a href=\"http://lax1.ib.adnxs.com/click?AAAAAAAA6D8AAAAAAADoPwAAAAAAAPA_AAAAAAAA6D8A…"
}
}
```

## adType object

The adType object specifies the type of ad (banner, native, or video) and the source of the ad, either real-time bidding (rtb) or client-side mediation (csm).

The following section describes examples for the various adType objects:

### Banner with RTB as source

```
adObj = {
adType: "banner",
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: '$',
isExclusive: false,
isRoadblock: false,
feedbackUrl: 'https://www.ilikefeedback.com/info?a=1&b=2...'
source: "rtb",
creativeId: 26299226,
targetId : "target_id_123",
banner: {
width: 728,
height: 90,
content: "<!-- Creative 26299226 served by Member 12345 via AppNexus --><a href=\"http://lax1.ib.adnxs.com/click?AAAAAAAA6D8AAAAAAADoPwAAAAAAAPA_AAAAAAAA6D8A…",
trackers: [{
impression_urls: ["http://lax1.ib.adnxs.com/it?e=wqT_3QK2BMAtAgAAAgDWAAUIo4aftQUQhaGP-8eK89JxG…S4xMy4xMzKoBO6QCbIEBwgAEAAY2AU.&s=7674360f6a0ea8c3ba7018acd3467ba291de4ad0"]
}]
},

// other data in adObj omitted for brevity
}
```

### Banner with CSM as source

```
adObj = {
adType: "banner",
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: '$',
source: "csm",
creativeId: 47259021,
targetId : "target_id_123",
// other data in adObj omitted for brevity
}
```

### Video with RTB as source

```
adObj = {
adType: "video",
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: '$',
source: "rtb",
creativeId: 47259021,
targetId : "target_id_123",
video: {
duration: 20000,
playbackMethods: ["auto_play_sound_on"],
frameworks: [],
content: "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?><VAST version=\"2.0\">...."
},

// other data in adObj omitted for brevity
}
```

### Video with CSM as source

```
adObj = {
adType: "video",
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: '$',
source: "csm",
creativeId: 47211028,
targetId : "target_id_123",
// other data in adObj omitted for brevity
}
```

### Native with RTB as source

```
adObj = {
adType": "native",
cpm: 10,
cpm_publisher_currency: 10,
publisher_currency_code: "$",
source": "rtb",
targetId: "target_id_123",
renderer_id: 123,
renderer_url: "https://renderer.url.com/here",
native: {
title: "Native Creative Title",
body: "Native creative body.",
icon: {
width: 0,
height: 0,
url: "http://cdn.adnxs.com/p/5d/f0/53/fb/5df053fbcb7...png"
},
image: {
width: 2352,
height: 1516,
url: "http://cdn.adnxs.com/p/d9/d9/c7/3f/d9d9c73fb6aed0ba9...jpg"
},
cta: "Click Here",
sponsoredBy: "AppNexus",
impressionTrackers: [
"http://lax1-ib.adnxs.com/it?e=wqT_3QKqBqgqAwAAAwDWAAUBC..."
],
clickTrackers: [
"http://lax1-ib.adnxs.com/click?AAAAAAAA8D8AAAAAAADwPwA..."
],
javascriptTrackers: "",
clickUrl: "https://www.appnexus.com",
clickFallbackUrl: ""
}
}
```
