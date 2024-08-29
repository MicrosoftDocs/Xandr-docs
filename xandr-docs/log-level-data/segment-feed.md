---
title: Segment Feed
description: In this article, find information about the Segment feed and details about the columns associated with this data feed.
ms.custom: log-level-data
ms.date: 10/28/2023
---

# Segment feed

The Log-Level Segment Feed gives you data on the segment pixel loads for all of your network- and advertiser-level segments. Information about your 3rd-party data providers' pixels are not included. The feed contains one row per segment load. Additions (or re-additions) of a user to a segment are included, but removals of a user from a segment are not included in this feed.

The Xandr internal name for this feed is `segment_feed`.

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
| 1 | date_time | UNIX Epoch time | The date and time when the segment pixel fired (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 2 | user_id_64 | bigint | The Xandr 64-bit user ID stored in the Xandr cookie store. <br> This field is `0` when: <br> - Xandr does not have a match for this user; or <br> - the user's browser doesn't accept cookies; or <br> - you do not have a legal basis to access and process personal data for an impression where GDPR applies <br><br> It will be `-1` for opt-out/non-consented users. <br><br> **Note**: If you receive the `hashed_user_id_64` version of this field, you will not receive the unhashed version of this field. |
| 3 | member_id | int | The ID of the member that dropped the pixel. |
| 4 | segment_id | int | The ID of the segment pixel. |
| 5 | is_daily_unique | tinyint | Whether or not the pixel fire is the first for a given user that day. |
| 6 | is_monthly_unique | tinyint | Whether or not the pixel fire is the first for a user in the past 30 days. |
| 7 | value | int | Optional value passed with pixel. |
| 8 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
| 9 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br> `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. |
