---
title: Auction Segment Feed
description: In this article, find information about the Auction segment feed and details about the columns associated with this data feed.
ms.custom: log level-data
ms.date: 10/28/2023
---

# Auction segment feed

> [!IMPORTANT]
> This feed is not available to Microsoft Invest clients.

This is a log level data feed that provides you with information on all eligible segments in an auction that your seller member has access to. The segments in this feed include pixel, query string, and 3rd-party shared segments.

The Xandr internal name for this feed is `auction_segment_feed`.

Each feed is delivered hourly and will be retained for 7 days. The feed will be logged when an auction is complete.

If you enable the auction segment feed, it will be in your feed list along with all your other log level data feeds. See [Log Level Data Feeds](log level-data-feeds.md) for more information.

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 1 | date_time | UNIX Epoch time | The time and date of impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*) . |
| 2 | auction_id_64 | bigint | The unique ID of the auction. |
| 3 | user_id_64 | bigint | The ID of the user. |
| 4 | seller_member_id | int | The member ID of the seller. |
| 5 | segments | segment_key_value | A list of segments. Each segment consists of: <br> - segment_id (int): The segment ID of the pixel, query string, or shared segment. <br> - segment_value (int): A value that can be passed with the segment. <br> - last_seen_min (int): The number of minutes since this user was last tagged with this segment. Given in Posix time (represented in minutes). Multiply this value by 60 to get the number of seconds since the epoch when this segment was updated.|
| 6 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br>  `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. |
| 7 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example,  `1568077200000`  can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
