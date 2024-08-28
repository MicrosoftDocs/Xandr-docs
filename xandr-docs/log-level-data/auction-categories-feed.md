---
title: Auction Categories Feed
description: In this article, find information about the Auction categories feed and details about the columns associated with this data feed.
ms.custom: log level-data
ms.date: 10/28/2023
---

# Auction categories feed

> [!IMPORTANT]
> This feed is not available to Microsoft Invest clients.

This is a log level data feed that provides you with data on all categories (universal and custom) that were present in an auction where you were the selling member.

The Xandr internal name for this feed is `auction_categories_feed`.

Each feed is delivered hourly and will be retained for 7 days. The feed will be logged when an auction is complete.

If you enable the auction category feed, it will be in your feed list along with all your other log level data feeds. See [Log Level Data Feeds](log level-data-feeds.md) for more information.

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.


| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 1 | date_time | UNIX Epoch time | The time and date of impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*) . |
| 2 | auction_id_64 | bigint | The unique identifier of the auction. |
| 3 | user_id_64 | bigint | The ID of the user. |
| 4 | seller_member_id | int | The member ID of the seller. |
| 5 | universal_categories | int | A list of category IDs for the universal categories that apply to this auction. |
| 6 | custom_categories | int | A list of category IDs for the custom categories that apply to this auction. |
| 7 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br>  `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. |
| 8 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example,  `1568077200000`  can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
