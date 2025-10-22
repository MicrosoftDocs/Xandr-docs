---
title: Query String Feed
description: In this article, find information about the Query string feed and details about the columns associated with this data feed.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Query string feed

> [!IMPORTANT]
> This feed has been deprecated as of January 2022.

The Query String Feed provides data about the query strings that come in on your managed publishers' impressions. It contains one row for each sold impression that passes in a query string in the correct format. For more information on the required query string format, see the [Query String Formatting Requirements](#query-string-formatting-requirements) section below.

> [!NOTE]
> You must be specially enabled to log query strings and receive this feed. This is true even if you already get a [Standard Feed](standard-feed.md). For more information contact your Xandr representative.

The Xandr internal name for this feed is `custom_data_feed`.

## Query string formatting requirements

- Only the contents of the `custom_pub_data` querystring parameter will be logged. Other querystring data outside of the `custom_pub_data` parameter will not be logged.
- The contents of `custom_pub_data` should be 70 characters or less (after that it is truncated).
- It is permissible to pass more than 70 characters, but only the first 70 will be logged.
- The characters newline (`"\n"`), tab (`"\t"`), and backslash (`"\"`) are not allowed. Otherwise, all characters that can be displayed by the standard C library function `isprint` are allowed. For more information, see the [ISPRINT(3) Manual Page](https://developer.apple.com/library/archive/documentation/System/Conceptual/ManPages_iPhoneOS/man3/isprint.3.html).

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Columns

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 01 | date_time | UNIX Epoch time | The time the impression was served (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 02 | auction_id_64 | bigint (64 bit) | Xandr's unique auction identifier. |
| 03 | seller_member_id | int (32 bit) | The member ID of the seller. |
| 04 | querystring | string | The `custom_pub_data` parameter from the query string of the impression. |
