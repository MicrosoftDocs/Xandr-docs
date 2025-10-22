---
title: OpenRTB Bid Request Requirements
description: This page documents the OpenRTB fields required and the corresponding volume thresholds that need to be met to ensure that buyers have the information they need to bid intelligently. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---


# OpenRTB bid request requirements

Xandr supply partners must provide sufficient auction metadata on [incoming bid requests](incoming-bid-request-from-ssps.md) to ensure that buyers have the information they need to bid intelligently. This page documents the OpenRTB fields required and the corresponding volume thresholds that need to be met. For example, a 95% threshold for the banner height field indicates that 95% of randomly sampled requests must contain information about the banner height. Traffic samples must meet the thresholds for all relevant fields. Inventory that does not meet the requirements outlined below will be eligible for selling through deals, but will not be made available on the open exchange.

Currently, we determine eligibility for the following formats:

- Web Banner
- Web Video
- Web Audio
- Web Native
- App Banner
- App Video
- App Audio
- App Native

The "web" designation includes both desktop web and mobile web;  "app" is defined as in-app inventory. Additional thresholds may be added in the future for other media types such as native or audio.

## Bid request criteria and thresholds

The sections below outline the OpenRTB bid request fields that are required for each format. The "Required OpenRTB Field" column represents the IAB OpenRTB fields that correspond to the "Auction Attribute" in the first column. In cases where multiple OpenRTB fields are listed for a given auction attribute, only one of those fields is required. For example, in order for a request to pass the "Tag ID" criterion for "Web Banner Criteria", either site.id or imp.tagid needs to be passed.

### Web banner criteria

| Auction Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| Height | imp.banner.h | integer | Specifies the exact height of the banner in pixels. | 95% |
| Width | imp.banner.w | integer | Specifies the exact width of the banner in pixels. | 95% |
| User ID | user.buyeruid | integer | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. | 95% |
| Tag ID | site.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
|  Tag ID| imp.tagid | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95%  |
| Publisher ID | site.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Domain | site.domain | string | Specifies the domain of the site (for example, [publishersite.com](https://publishersite.com/)) where the impression will be shown. Set as the referrer domain on the impression if available, or extracted from the `page` field. | 95%<br> |
| Domain | site.page |  | Specifies the full URL of the page where the impression will be shown (for example, [page.publishersite.com/path/to/page](http://page.publishersite.com/path/to/page)). This should be the referrer URL and is preferred over the `domain` field. | 95% |
| IP | device.ip | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, Xandr sets the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to view the models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95% |
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field. | 95% |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. | 95% |

### Web video criteria

| Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| Height | imp.video.h | integer | Specifies the height of the video player, in pixels. | 95% |
| Width | imp.video.w | integer | Specifies the width of the video player, in pixels. | 95% |
| Mime Type | imp.video.mimes | array of strings | Specifies the video content MIME types supported; for example, `video/x-ms-wmv` and `video/x-flv`. If not specified, any MIME type is allowed. | 95% |
| API Type | imp.video.api | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br>- `1`: VPAID 1.0<br>- `2`: VPAID 2.0<br>- `3`: MRAID-1<br>- `4`: ORMMA<br>- `5`: MRAID-2 | 95% |
| User ID | user.buyeruid | integer | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. |  |
| Tag ID | site.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code.  | 95% |
| Publisher ID | site.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Minimum Bitrate | imp.video.minbitrate | integer | Specifies the minimum bit rate, in kilobytes per second. If specified, only return creatives having at least one media file within the appropriate bit range. | 95% |
| Maximum Bitrate | imp.video.maxbitrate | integer | Specifies the maximum bit rate, in kilobytes per second. If specified, only return creatives having at least one media file within the appropriate bit range. | 95% |
| Playback Method | imp.video.playbackmethod | array of integers | Specifies the allowed playback methods. If not specified, all are assumed to be allowed. Currently supported values are:<br>- `1`: Autoplay, sound on<br>- `2`: Autoplay, sound off<br>- `3`: Click to play<br>- `4`: Mouse over to play | 95% |
| Min Duration | imp.video.minduration | integer | Specifies the maximum video ad duration, in seconds. | 95% |
| Max Duration | imp.video.maxduration | integer | Specifies the maximum video ad duration, in seconds. | 95% |
| Start Delay | imp.video.startdelay | integer | Specifies the start delay of the video:<br> - >`0`: For values greater than zero, the delay before video start, in seconds.<br>- `0`: Pre-roll<br>- `-1`: Generic mid-roll<br>- `-2`: Generic post-roll | 95% |
| Protocols | imp.video.protocols | array of integers | Array of supported video bid response protocols. | 95% |
| Domain | site.domain | string | Specifies the domain of the site (for example, [publishersite.com](https://publishersite.com/)) where the impression will be shown. Set as the referrer domain on the impression if available, or extracted from the `page` field. | 95%<br> |
| Domain | site.page |  | Specifies the full URL of the page where the impression will be shown (for example, [page.publishersite.com/path/to/page](http://page.publishersite.com/path/to/page)). This should be the referrer URL and is preferred over the `domain` field. | 95% |
| IP | device.ip | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, we will set the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md)  to view the models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95%|
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field. | 95% |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. | 95% |

The following field values in bid requests must be internally consistent.

| Criteria | Required OpenRTB Field | Description | Threshold |
|--|--|--|--|
| VPAID1 | imp.video.mimes<br>imp.video.api | If the imp.video.mimes array contains value "1" for VPAID1, then the imp.video.mimes array must contain either contain value "application/x-shockwave-flash" or be empty, in which case all mime types are assumed to be supported | 95% |
| VPAID2 | imp.video.mimes<br>imp.video.api | If the imp.video.mimes array contains value "2" for VPAID2, then the imp.video.mimes array must contain either contain value "application/x-shockwave-flash", or "application/javascript" or be empty, in which case all mime types are assumed to be supported | 95% |

### Web audio criteria

| Auction Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| Mime Type | imp.audio.mimes | array of strings | Specifies the audio content MIME types supported; for example, `audio/vnd.wav`, `audio/mpeg`, `audio/mp4`, `audio/ogg`, or `audio/mp2..` | 95% |
| API Type | imp.audio.api | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br>- `1`: VPAID 1.0<br>- `2`: VPAID 2.0<br>- `3`: MRAID-1<br>- `4`: ORMMA<br>- `5`: MRAID-2 | 95% |
| User ID | user.buyeruid | integer | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. | 95% |
| Tag ID | site.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string |Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code.  |  95% |
| Publisher ID | site.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Minimum Bitrate | imp.audio.minbitrate | integer | The minimum bit rate, in kilobytes per second. | 95% |
| Maximum Bitrate | imp.audio.maxbitrate | integer | The maximum bit rate, in kilobytes per second. | 95% |
| Min Duration | imp.audio.maxduration | integer | Specifies the maximum audio ad duration, in seconds. | 95% |
| Max Duration | imp.audio.maxduration | integer | Specifies the maximum audio ad duration, in seconds. | 95% |
| Start Delay | imp.audio.startdelay | integer | Specifies the start delay of the video:<br>- > `0`: For values greater than zero, the delay before video start, in seconds.<br>- `0`: Pre-roll<br>- `-1`: Generic mid-roll<br>- `-2`: Generic post-roll | 95% |
| Protocols | imp.audio.protocols | array of integers | Array of supported video bid response protocols. | 95% |
| Domain | site.domain | string | Specifies the domain of the site (for example, [publishersite.com](https://publishersite.com/)) where the impression will be shown. Set as the referrer domain on the impression if available, or extracted from the `page` field. | 95%<br> |
| Domain | site.page | string | Specifies the full URL of the page where the impression will be shown (for example, [page.publishersite.com/path/to/page](http://page.publishersite.com/path/to/page)). This should be the referrer URL and is preferred over the `domain` field. |95%  |
| IP | device.ip | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, we will set the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md)  to view models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95% |
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field. |95%  |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. |  95%|

### Web native criteria

| Auction Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| User ID | user.buyeruid | integer | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. | 95% |
| Tag ID | site.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Publisher ID | site.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Domain | site.domain | string | Specifies the domain of the site (for example, [publishersite.com](https://publishersite.com/)) where the impression will be shown. Set as the referrer domain on the impression if available, or extracted from the `page` field. | 95%<br> |
| Domain | site.page | string | Specifies the full URL of the page where the impression will be shown (for example, [page.publishersite.com/path/to/page](http://page.publishersite.com/path/to/page)). This should be the referrer URL and is preferred over the `domain` field. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, Xandr sets the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to view the models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95% |
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field. | 95% |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. | 95% |
| IP | device.ip | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. | 95% |
| Version | native.ver | string | Version of the Native Markup version in use.<br>Xandr currently supports the following native versions:<br>- 1.0<br>- 1.1<br>**Note**: Required if using 1.1. If no version is submitted, then we will default to 1.0. | 95% |
| Request | native.request | string | The rendered creative markup to be delivered; native creatives can be returned in this field as a JSON-encoded string.<br>Native 1.0 Example:<br>`` "native": { "request": "{\"native\":{\"ver\":\"1.0\",\"assets\":[{\"id\":3}}]}" }``<br>Native 1.1 Example:<br>**Note**: the main difference of the two versions is the removal of "native" in the request object.<br>``"native": { "request": "{\"ver\":\"1.1\",\"assets\":[{\"id\":3}}]}" }`` | 95% |
| Asset ID | native.request.native.assets.id | integer | Unique asset ID, assigned by exchange. Typically a counter for the array. Every asset object needs to contain a unique Asset ID. Use native.request.native.assets.id for Native Version 1.0 and use native.request.assets.id for Native Version 1.1. | 95% |
| Asset ID | native.request.assets.id | integer | Unique asset ID, assigned by exchange. Typically a counter for the array. Every asset object needs to contain a unique Asset ID. Use native.request.native.assets.id for Native Version 1.0 and use native.request.assets.id for Native Version 1.1. | 95% |
| Title Asset | native.request.assets.title | object | The Title object is to be used for title element of the Native ad. | 95% |

### App banner criteria

| Auction Attribute | OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| Height | imp.banner.h | integer | Specifies the exact height of the banner in pixels. | 95% |
| Width | imp.banner.w | integer | Specifies the exact width of the banner in pixels. | 95% |
| Device ID | device.ifa | string | The "identifier for advertising" is an unhashed device ID sanctioned for advertiser use. This is the [IDFA](https://developer.apple.com/help/app-store-connect/#//apple_ref/doc/uid/TP40011225-CH33-SW8) on iOS and the [AAID](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient) on Android. | 95% |
| Tag ID | app.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code.  |95%  |
| Publisher ID | app.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Domain | app.domain | string | Specifies the domain of the app (for example, [mygame.publishersite.com](https://publishersite.com/)) where the impression will be shown. Set as the referrer domain on the impression if available. | 95%<br> |
| Bundle ID | app.bundle | string | Specifies the application bundle or package name (e.g., `com.foo.mygame`). This is intended to be a unique ID across multiple exchanges. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, Xandr sets the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to view the models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95% |
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the ua field. |  95%|
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. |95%  |

### App video criteria

| Auction Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| Height | imp.video.h | integer | Specifies the height of the video player, in pixels. | 95% |
| Width | imp.video.w | integer | Specifies the width of the video player, in pixels. | 95% |
| Mime Type | imp.video.mimes | array of strings | Specifies the video content MIME types supported; for example, `video/x-ms-wmv` and `video/x-flv`. If not specified, any MIME type is allowed. | 95% |
| API Type | imp.video.api | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br>- `1`: VPAID 1.0<br>- `2`: VPAID 2.0<br>- `3`: MRAID-1<br>- `4`: ORMMA<br>- `5`: MRAID-2 | 95% |
| Device ID | device.ifa | string | The "identifier for advertising" is an unhashed device ID sanctioned for advertiser use. This will be the [IDFA](https://developer.apple.com/help/app-store-connect/#//apple_ref/doc/uid/TP40011225-CH33-SW8) on iOS or [AAID](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient) on Android. | 95% |
| Tag ID | app.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Publisher ID | app.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Minimum Bitrate | imp.video.minbitrate | integer | Specifies the minimum bit rate, in kilobytes per second. If specified, only return creatives having at least one media file within the appropriate bit range. | 95% |
| Maximum Bitrate | imp.video.maxbitrate | integer | Specifies the maximum bit rate, in kilobytes per second. If specified, only return creatives having at least one media file within the appropriate bit range. | 95% |
| Playback Method | imp.video.playbackmethod | array of integers | Specifies the allowed playback methods. If not specified, all are assumed to be allowed. Currently supported values are:<br>- `1`: Autoplay, sound on<br>- `2`: Autoplay, sound off<br>- `3`: Click to play<br>- `4`: Mouse over to play | 95% |
| Max Duration | imp.video.maxduration | integer | Specifies the maximum video ad duration, in seconds. | 95% |
| Start Delay | imp.video.startdelay | integer | Specifies the start delay of the video:<br>- > `0`: For values greater than zero, the delay before video start, in seconds.<br>- `0`: Pre-roll<br>- `-1`: Generic mid-roll<br>- `-2`: Generic post-roll | 95% |
| Protocols | imp.video.protocols | integer | Array of supported video bid response protocols. | 95% |
| Domain | app.domain | string | Specifies the domain of the app (for example, [mygame.publishersite.com](https://publishersite.com/) ) where the impression will be shown. Set as the referrer domain on the impression if available. | 95%<br> |
| Bundle ID | app.bundle | string | Specifies the application bundle or package name (e.g., `com.foo.mygame`). This is intended to be a unique ID across multiple exchanges. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, we will set the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to view the makes registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. |  95%|
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field | 95% |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. | 95% |

The following field values in bid requests must be internally consistent.

| Criteria | Required OpenRTB Field | Description | Threshold |
|--|--|--|--|
| VPAID1 | imp.video.mimes<br>imp.video.api | If the imp.video.mimes array contains value "1" for VPAID1, then the imp.video.mimes array must contain either contain value "application/x-shockwave-flash" or be empty, in which case all mime types are assumed to be supported | 95% |
| VPAID2 | imp.video.mimes<br>imp.video.api | If the imp.video.mimes array contains value "2" for VPAID2, then the imp.video.mimes array must contain either contain value "application/x-shockwave-flash", or "application/javascript" or be empty, in which case all mime types are assumed to be supported | 95% |

### App audio criteria

| Auction Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| Mime Type | imp.audio.mimes | array of strings | Specifies the audio content MIME types supported; for example, `audio/vnd.wav`, `audio/mpeg`, `audio/mp4`, `audio/ogg`, or `audio/mp2..` | 95% |
| API Type | imp.audio.api | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br>- `1`: VPAID 1.0<br>- `2`: VPAID 2.0<br>- `3`: MRAID-1<br>- `4`: ORMMA<br>- `5`: MRAID-2 | 95% |
| User ID | user.buyeruid | integer | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. | 95% |
| Tag ID | app.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string |Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code.  | 95% |
| Publisher ID | app.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Minimum Bitrate | imp.audio.minbitrate | integer | The minimum bit rate, in kilobytes per second. | 95% |
| Maximum Bitrate | imp.audio.maxbitrate | integer | The maximum bit rate, in kilobytes per second. | 95% |
| Max Duration | imp.audio.maxduration | integer | Specifies the maximum audio ad duration, in seconds. | 95% |
| Start Delay | imp.audio.startdelay | integer | Specifies the start delay of the video:<br>- > `0`: For values greater than zero, the delay before video start, in seconds.<br>- `0`: Pre-roll<br>- `-1`: Generic mid-roll<br>- `-2`: Generic post-roll | 95% |
| Protocols | imp.audio.protocols | array of integers | Array of supported video bid response protocols. | 95% |
| Bundle ID | app.bundle | string | Specifies the application bundle or package name (e.g., `com.foo.mygame`). This is intended to be a unique ID across multiple exchanges. | 95% |
| IP | device.ip | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, we will set the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md)  to view the models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95% |
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field. |  95% |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. | 95% |

### App native criteria

| Auction Attribute | Required OpenRTB Field | Type | Description | Threshold |
|--|--|--|--|--|
| User ID | user.buyeruid | integer | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. | 95% |
| Tag ID | app.id | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Tag ID | imp.tagid | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is the Xandr placement code. | 95% |
| Publisher ID | site.publisher.id | string | Specifies the seller's publisher ID, used to look up a Xandr publisher ID. | 95% |
| Bundle ID | app.bundle | string | Specifies the application bundle or package name (e.g., `com.foo.mygame`). This is intended to be a unique ID across multiple exchanges. | 95% |
| Device Data<br> | device.model | string | Specifies the model of the device. If passed, Xandr sets the device `make` and `devicetype` based off the model and not the fields passed in. This value will override the parsed `ua` field if passed in. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to view the models registered in the Xandr system. | 95% |
| Device Data | device.ua | string | Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. | 95% |
| Device Data | device.devicetype | string | Specifies the type of device, using IAB values:<br>- `1`: Mobile/Tablet<br>- `2`: Personal Computer<br>- `3`: Connected TV<br>- `4`: Phone<br>- `5`: Tablet<br>- `6`: Connected Device<br>- `7`: Set Top Box<br>Only used if not supported via the `ua` field. | 95% |
| Device Data | device.make | string | Specifies the make of the device. Only used if the model is not passed in, is not valid, or is not available via parsing the `ua` field. Use the [Device Make Service](../digital-platform-api/device-make-service.md) to view the makes registered in the Xandr system. | 95% |
| IP | device.ip | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. | 95% |
| Version | native.ver | string | Version of the Native Markup version in use.<br>Xandr currently supports the following native versions:<br>- 1.0<br>- 1.1<br>**Note**: Required if using 1.1. If no version is submitted, then we will default to 1.0. | 95% |
| Request | native.request | string | The rendered creative markup to be delivered; native creatives can be returned in this field as a JSON-encoded string.<br>Native 1.0 Example:<br>``"native": "request": "{\"native\":{\"ver\":\"1.0\",\"assets\":[{\"id\":3}}]}" }``<br>Native 1.1 Example:<br>**Note**: the main difference of the two versions is the removal of "native" in the request object.<br>``"native": { "request": "{\"ver\":\"1.1\",\"assets\":[{\"id\":3}}]}" }`` | 95% |
| Asset ID | native.request.native.assets.id | integer | Unique asset ID, assigned by exchange. Typically a counter for the array. Every asset object needs to contain a unique Asset ID. Use native.request.native.assets.id for Native Version 1.0 and use native.request.assets.id for Native Version 1.1. | 95% |
| Asset ID | native.request.assets.id | integer | Unique asset ID, assigned by exchange. Typically a counter for the array. Every asset object needs to contain a unique Asset ID. Use native.request.native.assets.id for Native Version 1.0 and use native.request.assets.id for Native Version 1.1. | 95% |
| Title Asset | native.request.assets.title | object | The Title object is to be used for title element of the Native ad. | 95% |

## Example bid requests

### Web banner request

``` 
{
    "site": {
        "publisher": {
            "id": "534561625"
        },
        "domain": "publishersite.com",
        "id": "537123178",
        "page": "https://page.publishersite.com/path/to/page"
    },
    "imp": [
        {
            "banner": {
                "h": 250,
                "w": 300
            },
            "id": "7bbab3f3-83db-4b00-a82d-faa69fcbb5c5"
        }
    ],
    "device": {
        "os": "Windows",
        "make": "desktop",
        "dnt": 0,
        "ua": "Mozilla/5.0 (Windows NT 6.0; rv:50.0) Gecko/20100101 Firefox/50.0",
        "devicetype": 2,
        "model": "browser",
        "user": {
            "buyeruid": "8320715123477372344"
        },
        "id": "7bbab3f3-83db-4b00-a82d-faa69fcbb5c5"
    }
}
```

### App banner requests

``` 
{
    "app": {
        "publisher": {
            "id": "537133097"
        },
        "bundle": "com.publisher.app",
                "domain": "publisher.com",
                "id": "537252150"
    },
    "imp": [
        {
            "banner": {
                "h": 250,
                "w": 300
            },
            "id": "a4d94cdc-3999-4708-9a6d-6ac01f6c07d4"
        }
    ],
    "device": {
        "os": "Android",
        "language": "en",
        "make": "generic",
        "dnt": 0,
        "ua": "Mozilla/5.0 (Linux; Android 4.4.2; GT-I9301I Build/KOT49H) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/30.0.0.0 Mobile Safari/537.36",
        "devicetype": 4,
        "ifa": "ffab2dd1-c6eb-4be9-b88b-1c24e431766d",
        "ip": "5.90.222.251",
        "model": "android phone"
    },
    "id": "a4d94cdc-3999-4708-9a6d-6ac01f6c07d4"
}
```

### Web video requests

``` 
 {
    "site": {
        "publisher": {
            "id": "74964"
        },
        "domain": "publishersite.com",
        "id": "123456",
        "page": "page.publishersite.com/path"
    },
    "imp": [
        {
            "video": {
                "mimes": [
                    "video/x-flv",
                    "video/mp4",
                    "application/x-shockwave-flash"
                ],
                "api": [
                    1
                ],
                                "minbitrate": 1,
                                "maxbitrate": 2000,
                                "playbackmethod": [2],
                                "maxduration": 30,
                                "startdelay":0,
                                "protocols": [2, 5],
                "h": 360,
                "w": 480
            },
            "id": "1"
        }
    ],
    "device": {
        "language": "en",
        "os": "Windows 10",
        "make": "Google",
        "devicetype": 2,
        "ip": "24.171.153.60",
        "model": "Chrome - Windows",
        "ua": "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36"
    },
    "id": "32683827af9b11e6b43212a6e39f0001",
    "user": {
        "buyeruid": "6415517486677292084"
    }
}
```

### App video requests

``` 
 {
    "app": {
        "publisher": {
            "id": "1100001685"
        },
        "bundle": "com.publisher.app",
        "domain": "publishersite.com",
        "id": "123456",
        "page": "page.publishersite.com/path"
    },
    "imp": [
        {
            "tagid": "130200094",
            "video": {
                                "mimes": [
                    "video/x-flv",
                    "video/mp4",
                    "application/x-shockwave-flash"
                ],
                "api": [
                    1
                ],
                                "minbitrate": 1,
                                "maxbitrate": 2000,
                                "playbackmethod": [2],
                                "maxduration": 30,
                                "startdelay":0,
                                "protocols": [2, 5],
                "h": 480,
                "w": 320
            }
        }
    ],
    "device": {
        "os": "Android",
        "ua": "Mozilla/5.0 (Linux; Android 6.0.1; SM-N920V Build/MMB29K; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/54.0.2840.85 Mobile Safari/537.36",
        "make": "Samsung",
        "devicetype": 1,
        "ifa": "C8A53AB8-D371-4955-BFDA-7805FA931E44",
        "model": "SM-N920V"
    },
    "id": "Nr4EZZiP5z"
}
```
