---
title: Mobile for Bidders
description: In this article, learn about mobile inventory for bidders, their creative specifications, and step-by-step instructions on how to buy a mobile inventory.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Mobile for bidders

Buying mobile inventory is very similar to buying other seller-specific external supply on Xandr. This page walks you through the process.

> [!NOTE]
> For full bid request documentation, see [Bid Request](outgoing-bid-request-to-bidders.md).

## Creative specifications

At this time, only creatives conforming to the following specifications can serve on mobile inventory:

- **Type**
  - Standard Banners, including MRAID
  - Additional rich media creative types will be supported in the future
- **Size**
  - 300x50
  - 300x250
  - 320x50
  - 728x90
- **Format**
  - Html
  - JavaScript
  - Image (jpg, gif, png)

## Buying mobile inventory

- [Step 1: Ensure that you accept mobile bid requests](#step-1-ensure-that-you-accept-mobile-bid-requests)
- [Step 2: Target and bid on mobile inventory](#step-2-target-and-bid-on-mobile-inventory)
- [Step 3: Receive auction results](#step-3-receive-auction-results)

### Step 1: Ensure that you accept mobile bid requests

Bidder profiles allow you to filter for the bid requests that you want to receive. To accept mobile bid requests, you must allow the following values within an existing bidder profile or create a new bidder profile specifically for mobile bid requests:

| Field | Value |
|:---|:---|
| `supply_type` | `"mobile_app"`, `"mobile_web"` |

For more details about updating or creating bidder profiles, see [Legacy Bidder Profile Service](legacy-bidder-profile-service.md).

### Step 2: Target and bid on mobile inventory

When Xandr receives an impression from mobile supply sources, Xandr routes these through a publisher, site, and tag ID combination, in increasing order of granularity. The Xandr bid request includes these IDs, allowing you to target specific slices of mobile inventory.
For more information on the content of the inventory, contact your Xandr representative.

The Xandr bid request for a mobile impression includes other fields that may be useful for your bidder to target. These fields include:

- `operating_system`
- `browser`
- `language`
- `ip_address`
- `device_make`
- `device_model`
- `device_type`
- `device_ids`
- `carrier`
- `loc` (only available on small percentage of impressions)
- `app_id`

### Step 3: Receive auction results

The Xandr Notify request is essential to tracking when an impression is served, the win price of the impression, and to provide you with any custom notify data you may have included with the bid.

## Fields supported by mobile bid requests

- [Mobile-specific data](#mobile-specific-data)
- [Device IDs](#device-ids)

### Mobile-specific data

| Field | Scope | Type | Description |
|:---|:---|:---|:---|
| `app_id` | some | string | Global App ID for Android and iOS devices.<br>For example, for Angry Birds app:<br>Android device:<br> `"app_id" : "com.rovio.angrybirds"`<br>iOS device:<br> `"app_id" : "343200656"` or `"com.clickgamer.AngryBirds"` |
| `loc` | some | string | Location of the user, provided in terms of latitude and longitude. <br>Expressed in the format `"snnn.ddd,snnn.ddd"`, for example `+123.456` or `-456.123`. South and west are represented as negative. There can be a maximum of 5 decimal places of precision. |
| `carrier` | some | int | The ID for the carrier. You can use the [Carrier Service](carrier-service.md) to map carrier IDs to names and countries or regions. A special carrier "WIFI" exists for users connecting via WiFi. |
| `device_make` | some | int | The ID of the device make on which the ad will be shown. You can use the [Device Make Service](device-make-service.md) to map device make IDs to names. |
| `device_model` | some | int | The ID of the device model on which the ad will be shown. You can use the [Device Model Service](device-model-service.md) to map device model IDs to names. |
| `device_type` | some | int | The ID of the type of device on which the ad will be shown. This is represented by an integer, and can be looked up using the [Device Model Service](device-model-service.md). Allowed values, and their meanings:<br> - `1` = "pc"<br> - `2` = "phone"<br> - `3` = "tablet" |

### Device IDs

| Field | Scope | Type | Description |
|:---|:---|:---|:---|
| `windowsadid` | some | String | The Microsoft Advertising ID for Windows 8 and Windows Phone devices. |
| `idfa` | some | string | The Apple advertising identifier for iOS devices running iOS 6+. |
| `aaid` | some | string | The Google advertising identifier for Android devices as retrieved from Google Play services. |
| `sha1udid` | some | string | The SHA1 hash of the `ANDROID_ID`. |
| `md5udid` | some | string | The MD5 hash of the `ANDROID_ID`. |
| `sha1mac` | some | string | **sha1mac** was deprecated as of May 7th, 2019. Do not use. |
| `openudid` | some | string | The [OpenUDID](https://github.com/ylechelle/OpenUDID) of the device. This should only be sent for iOS versions 5 and below. |

## Examples of request/response chain

### Bid request

```
{
    "bid_request": {
        "timestamp": "2013-09-19 17:46:12",
        "bidder_timeout_ms": 200,
        "members": [],
        "member_ad_profile_id": 244,
        "tags": [
            {
                "auction_id_64": 7537677183577325000,
                "size": "400x50",
                "sizes": [
                    "400x50"
                ],
                "smaller_sizes_allowed": true,
                "position": "unknown",
                "tag_format": "javascript",
                "supply_type": "mobile_app",
                "site_id": 253281,
                "creative_formats_map": "1111111111",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "vast-url",
                    "text"
                ],
                "visibility_profile_id": 139,
                "venue_id": 114622,
                "allowed_media_types": [
                    1
                ],
                "media_subtypes": [],
                "ecp": 1,
                "eap": 0.5,
                "giveup_price": 0.001,
                "exclusive_default": true,
                "id": 1363482
            }
        ],
        "bid_info": {
            "user_id_64": 4699689268642942000,
            "no_cookies": false,
            "payment_rule_id": 110382,
            "selling_member_id": 2066,
            "no_flash": false,
            "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 5_0 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3",
            "browser": 12,
            "operating_system": 8,
            "operating_system_extended": 68,
            "operating_system_family": 3,
            "carrier": 26,
            "device_make": 26,
            "device_model": 301,
            "device_type": 2,
            "device_ids": {"idfa": "0acf25e9-d278-49f5-9774-b37bfce3f34c" },
            "language": 11,
            "accepted_languages": "en-US,en;q=0.8",
            "ip_address": "192.189.54.0",
            "country": "AU",
            "loc": "45.00000,45.00000",
            "within_iframe": false,
            "publisher_id": 128528,
            "url": "https://apps.mobile.adnxs.com",
            "domain": "adnxs.com",
            "userdata_json": "{}",
            "segments": [],
            "prefer_learn": false
        }
    }
}
```

### Bid response

```
{
    "bid_response": {
        "responses": [
            {
                "auction_id_64": 7537677183577325000,
                "price": 1,
                "member_id": 331,
                "creative_id": 694408,
                "is_cpm": true,
                "exclusive": "true",
                "roadblock": false,
                "learn": false,
                "userdata_js": "uf('a', 87089, 1379612772);uf('r', 694408, 1379612772);",
                "custom_notify_data": "!Zh3JGQiAzRcQiLEqGAAgrt4GMAA4vv8GQARIywJQmpxTWABggQZoAHAAeACAAQCIAQCQAQGYAQGgAQGoAQOwAQC5AQAAAAAAAPA_wQEAAAAAAADwP8kBzczMzMzMBEDZAQAAAAAAAPA_4AEA"
            }
        ]
    }
}
```

The bid response allows custom notify data, which will be returned in the subsequent notifications.
