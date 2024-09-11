---
title: Data Science Toolkit - Log-Level Custom Model Feed
description: Use the log-level custom model feed to get specific information on models associated with your line items and the values calculated by each model.
ms.custom: data-science
ms.date: 10/28/2023
---

# Data Science Toolkit - Log-level custom model feed

The Log-Level Custom Model Feed gives you specific information on models associated with your line items and the values calculated by each model.

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Integer key

- tinyint = 1 byte (8 bit)
- smallint = 2 byte (16 bit)
- int = 4 byte (32 bit)
- bigint = 8 byte (64 bit)

## Columns

| Column Index | Column Name | Type | Description |
|:---|:---|:---|:---|
| 01 | `date_time` | UNIX Epoch time | The time and date of the impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC))*. |
| 02 | `auction_id_64` | bigint | The AppNexus unique auction identifier. |
| 03 | `buyer_member_id` | int | The member ID of the buyer. |
| 04 | `user_id_64` | bigint | The AppNexus 64-bit User ID stored in the AppNexus cookie store. This field is `0` when AppNexus does not have a match for this user or the user's browser doesn't accept cookies. It will be `-1` for opt-out users.<br><br>**Note**: This field has been deprecated from the API [Log Level Data service](../log-level-data/log-level-data-feeds.md) (in compliance with GDPR). |
| 05 | `model_type` | int | Type of the model. Possible values are:<br> `1` = expected_value<br> `2` = creative_selection<br> `3` = ev_click<br> `4` = click_imp<br> `5` = ev_conv<br> `6` = conv_imp<br> `7` = conv_click<br> `8` = bid_modifier<br> `9` = nonvaluation<br> `10` = cadence<br> `11` = budget_splitter |
| 06 | `model_id` | int | The ID of the custom model used in the auction. When no custom model is used, this defaults to `0`. |
| 07 | `leaf_code` | string | An optional string value that will be passed through to logs and reporting to aid with debugging and performance analysis. `leaf_code` may be up to seven ASCII (7-bit) characters and is not required to be unique, this defaults to `""`. |
| 08 | `origin` | int | Origin indicates whether the model is attached by AppNexus. Possible values are:<br> `0` = Model attached by client<br> `1` = Model attached by AppNexus Optimization<br> `2` = Model attached by Programmable Splits |
| 09 | `experiment` | int | Indicates whether the impression is a test or control impression. This is currently unsupported and will be `0` for all impressions. |
| 10 | `value` | numeric(18,6) | Value calculated by the model |
| 11 | `campaign_group_id` | int | The ID of the Line Item |
| 12 | `hashed_user_id_64` | bytes | The hashed version of the AppNexus 64-bit User ID which will we provided as a proxy in certain cases where AppNexus is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. See [example for hashed_user_id_64](#example-for-hashed_user_id_64) below. |

### Example for `hashed_user_id_64`

```
user_id_64:
XXXXXX304391387YYYY
hashed_user_id_64:
0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767
```

## Related topic

[Custom Models](./custom-models.md)
