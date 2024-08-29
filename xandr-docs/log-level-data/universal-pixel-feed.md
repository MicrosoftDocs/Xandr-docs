---
title: Universal pixel Feed
description: In this article, find information about the Universal Pixel feed and details about the columns associated with this data feed.
ms.custom: log-level-data
ms.date: 10/28/2023
---

# Universal pixel feed

The Log-Level Universal Pixel Feed provides you with data on the firing of all of your Universal Pixels. The feed contains one row per pixel fire. Each row includes both the data received on the fire as well as any segment and conversion IDs that were associated with the event based on the Audience and Conversion rules that matched the traffic. It is possible for a pixel fire to satisfy no Audience or Conversion rules.

The Universal Pixel Feed does not distinguish between attributed and unattributed conversions. To view attributed conversion data, see [Advertiser Attributed Conversions](../digital-platform-api/advertiser-attributed-conversions.md) or the [Standard Feed](standard-feed.md).

The Xandr internal name for this feed is `universal_pixel_feed`.

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Integer key

- tinyint = 1 byte (8 bit)
- smallint = 2 byte (16 bit)
- int = 4 byte (32 bit)
- bigint = 8 byte (64 bit)

## Columns

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 01 | date_time | UNIX Epoch time | The time and date of the universal pixel fire. <br> (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*.) <br><br> **Note**: The EPOCH time is in **milliseconds format**, and not the standard EPOCH time. |
| 02 | pixel_uuid | string | The UUID of the universal pixel. |
| 03 | user_id_64 | bigint | The Xandr 64-bit user ID (stored in the Xandr cookie store). <br> This field is `0` when: <br> - Xandr does not have a match for this user; or <br> - the user's browser doesn't accept cookies; or <br> - you do not have a legal basis to access and process personal data for an impression where GDPR applies <br> It will be `-1` for opt-out/non-consented users. |
| 04 | url | string | The entire URL of the page the pixel is on. |
| 05 | http_referer | string | The entire URL of the referrer to the page the pixel is on. |
| 06 | event | string | The event associated with the pixel fire. The standard universal pixel events are: <br> - PageView (default) <br> - LandingPage <br> - ItemView <br> - AddToCart <br> - InitiativeCheckout <br> - AddPaymentInfo <br> - Purchase <br> - Lead |
| 07 | item_ids | array of strings | Strings passed in on the `item_id` parameter within your pixel. This value is an array (e.g, `['product_5', 'product_6']`). |
| 08 | item_types | array of strings | Strings passed in on the `item_type` parameter within your pixel. This value is an array (e.g, `['apparel']`). |
| 09 | item_names | array of strings | Strings passed in on the `item_name` parameter within your pixel. This value is an array (e.g., `['ford fiesta']`). |
| 10 | segment_ids | array of int | The list of IDs for the segments the user was added to as a result of the universal pixel firing. |
| 11 | conversion_pixel_ids | array of int | The list of IDs for the conversion events triggered by the user as a result of the universal pixel firing. |
| 12 | partition_time_millis | long | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
| 13 | event_value | numeric | The nominal value of the event (passed in as a float from the `value` parameter within your pixel). |
| 14 | traffic_type | string | The source of the traffic being tracked by the pixel. Possible values are `WEB` or `APP`. |
| 15 | application_id | string | The ID of the application (in the app store) that the pixel has been placed on. This value can be numeric or alphanumeric (e.g., `com.xandr.application_name`). |
| 16 | device_unique_id | string | The unique identifier representing the mobile device. The numeric prefix indicates the type of unique device identifier: <br> - `0` = IDFA (Apple ID for Advertising) <br> - `1` = SHA1 <br> - `2` = MD5 <br> - `3` = ODIN <br> - `4` = OPENUDID <br> - `5` = AAID (Android Advertising ID) <br> - `6` = WINDOWSADID (Microsoft Advertising ID) <br> - `7` = RIDA (Roky id for Advertising) <br> - `8.9` = AFAI (Amazon Fire OS) <br> - `8.10` = TIFA (Tizen Identifier for Advertising (Samsung Ad ID)) <br> - `8.11` = VIDA (Vizio Advertising ID) <br> - `8.12` = LGUDID (LG Unique Device ID) <br> **Note**: The value of this field will be `null` except for specific integrations. |
| 17 | custom_parameters | array of messages | Contains all custom parameters that were sent with the pixel fire. This is represented as a repeated protobuf field with a key (string) and values (repeated string). |
| 18 | order_id | string | An optional value passed in by the buyer on the Universal Pixel using it (e.g., `'119'`). |
