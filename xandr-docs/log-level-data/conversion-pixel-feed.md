---
title: Conversion Pixel Feed
description: In this article, find information about the Conversion pixel feed and details about the columns associated with this data feed.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Conversion pixel feed

The Log-Level Conversion Pixel Feed provides data on the firing of all of your managed advertisers' pixels, both attributed and unattributed. The feed contains one row per pixel.

> [!NOTE]
> The Conversion Pixel Feed does not distinguish between the firing of attributed and unattributed pixels. To view attributed conversion data, see [Advertiser Attributed Conversions](../digital-platform-api/advertiser-attributed-conversions.md). However, pixel loads for users without a Xandr cookie are excluded from this feed because a conversion event is not possible without a cookie. This feed records all pixel fires, whereas the Attributed Conversion report only shows conversions that can be attributed to a line item.

The Xandr internal name for this feed is `pixel_feed`.

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
| 01 | date_time | UNIX Epoch time | The time and date of the impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 02 | auction_id_64 | bigint  | **Deprecated**. This field will always be `0`. |
| 03 | user_id_64 | bigint | The Xandr 64-bit user ID (stored in the Xandr cookie store). Pixel loads for users without a Xandr cookie are excluded from this feed because a conversion event is not possible without a cookie. <br> This field is `0` when: <br> - Xandr does not have a match for this user; or  <br> - the user's browser doesn't accept cookies; or <br> - you do not have a legal basis to access and process personal data for an impression where GDPR applies <br> It will be `-1` for opt-out/non-consented users. <br><br> **Note**: If you receive the `hashed_user_id_64` version of this field, you will not receive the non-hashed version. |
| 04 | pixel_id | int | The ID of the conversion pixel. |
| 05 | order_id | string(36) | The optional value passed in by the buyer on the conversion pixel using the `order_id` parameter. See [Conversion Pixels Advanced](../monetize/conversion-pixels-advanced.md) for more details. |
| 06 | external_data | string(30) | The optional extra data passed in by buyer on conversion pixel using the `other` parameter. See [Conversion Pixels Advanced](../monetize/conversion-pixels-advanced.md) for more details. |
| 07 | http_referer | string(2000) | The HTTP referrer from the conversion pixel fire |
| 08 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br> `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. |
| 09 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
