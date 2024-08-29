---
title: Key Value Auction Feed
description: In this article, find information about the Key value auction feed and details about the columns associated with this data feed.
ms.custom: log-level-data
ms.date: 10/28/2023
---

# Key value auction feed

> [!IMPORTANT]
> This feed is not available to Microsoft Invest clients.

The Log-Level Key Value Auction Feed gives you information on all eligible key/value targets in an auction.

The Xandr internal name for this feed is `auction_kv_labels_feed`.

Impressions with key/value targeting will serve and be reported only for those impressions that were logged by a placement tag containing the **kw_** prefix. For example, a placement tag containing keyname=value1 will not serve and therefore not be logged, whereas a placement tag containing  **kw_keyname=value1** will serve and be logged. This applies to ad calls with the following tag types: */tt*, */ttj*, */fpt*, */jpt*, */pt*, */ptv*, */ssptv*, */mtj*, */map*, and */mob*.

When using Xandr's seller tag, omit the **kw** prefix. AST has the keyword object in the body of the request, so the prefix is not needed.

- Each line returned in the feed represents a single key/value pair. For example, if you target on city = NY or LA, two rows will be returned, one for city/NY and one for city/LA.
- Each feed is delivered hourly and will be retained for 7 days. The feed will be logged when an auction is complete.
- If you enable the key value auction feed, it will be in your feed list along with all your other log-level data feeds. See [Log-Level Data Feeds](log-level-data-feeds.md) for more information.

## Columns

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 1 | date_time | UNIX Epoch time | The time and date of impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 2 | auction_id_64 | bigint | The unique ID of the auction. |
| 3 | user_id_64 | bigint | The Xandr 64-bit user ID stored in the Xandr cookie store. <br> This field is `0` when: <br> - Xandr does not have a match for this user; or <br> - the user's browser doesn't accept cookies; or <br> - you do not have a legal basis to access and process personal data for an impression where GDPR applies <br> It will be `-1` for opt-out/non-consented users. |
| 4 | key_name | string | The key name. |
| 5 | value_name | string | The key value name. |
| 6 | key_label | string | A descriptive name of the key. |
| 7 | value_label | string | A descriptive name of the value. |
| 8 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br> `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767`<br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. |
| 9 | partition_time_millis | UNIX Epoch | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
