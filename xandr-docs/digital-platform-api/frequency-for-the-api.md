---
title: Frequency for the API
description: This article provides information on frequency and recency targeting through the API with an example of how to use it and where to apply it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Frequency for the API

When a user is shown an ad multiple times over a short period, that user can begin to ignore the ad, reaching the point where they don't even see it anymore. Or they can see it often enough that they're simply annoyed by it. This is referred to as overexposure or ad burnout. Frequency and recency targeting helps you prevent overexposure by limiting how often a user is shown a creative. For example, you might decide that after a user has seen the same creative more than three times in a single day, it's not worth showing that creative to that user again. Or you might price a campaign higher if the user has seen it fewer than three times in a day and price it lower if the user has seen it more than three times. This page has information about:

- The frequency and recency targeting supported by our API through the [Profile Service](./profile-service.md)
- Example of how to use this type of targeting
- How and where you can apply frequency and recency targeting

## Supported targeting

Xandr supports several levels of frequency targeting through the API. This targeting is specified on the [Profile Service](./profile-service.md), which can be set at the advertiser, insertion order line item, campaign, and creative level. The API frequency settings follow the format shown here:

:::image type="content" source="media/supported-target.png" alt-text="Screenshot that shows the format of the API frequency settings.":::

| Setting | Profile Field | Description |
|:---|:---|:---|
| x imps per day | `max_day_imps` | The maximum number of times a creative can be served to a user within one day. |
| x imps per hour | `max_hour_imps` | The maximum number of times a creative can be served to a user within a one-hour period. |
| x imps per week | `max_week_imps` | The maximum number of times a creative can be served within one week, beginning on Sunday.<br>Regardless of when a creative is first served to the user, every Sunday the impression count for the user will be reset to zero and the frequency values will begin recounting.  |
| x imps per month | `max_month_imps` | The maximum number of times a creative can be served within one calendar month.<br>Regardless of how far into a month a creative is first served to the user, the impression count for the user will be reset on the first day of the following month and the frequency count will start over.  |
| x imps per lifetime | `max_lifetime_imps` | The maximum number of times a creative can be served to the user. |

The API recency settings follow the format shown here:

:::image type="content" source="media/api-settings.png" alt-text="Screenshot that shows the format of the API recency settings.":::

| Setting | Profile Field | Description |
|:---|:---|:---|
| 1 imp per x minutes/hours/days/weeks | `min_minutes_per_imp` | A single creative will not be shown to an individual user more than once every x minutes. (Value is in minutes, so 1 imp every 2 hours would be a value of `120`.) |

Some additional settings related to frequency capping include the following:

:::image type="content" source="media/frequency-capping.png" alt-text="Screenshot that shows the additional settings related to frequency capping.":::

| Setting | Profile Field | Description |
|:---|:---|:---|
| Serve only 1 imp per page | `max_page_imps` | Creatives from a single advertiser will not be shown on a given page load in more than the specified number of placements. (If this value is set in , the value will be `null` [off] or `1` [on].) |
| Include users without cookies | `require_cookie_for_freq_cap` | A value of `false` indicates you will serve to non-cookie users and ignore the frequency cap settings for those users. There is no way to identify these users, so if you set this field to `false` your frequency and recency caps will not apply for any user without cookies.<br>Setting this option to `true` indicates a creative will serve only to users who use cookies. This setting could limit your delivery. |

In addition to the preceding fields, there are three more fields that can be set only through the API:

| Setting | Profile Field | Description |
|:---|:---|:---|
| Minimum imps per session | `min_session_imps` | Creatives from a single campaign will be shown to a given user at least X times per session. |
| Maximum imps per session  | `max_session_imps` | Creatives from a single campaign will not be shown to a given user more than X times per session. |
| Advanced Frequency Management | `advanced_frequency_management` | Indicates whether you want to use the Advanced Frequency Management feature (AFM). If this field is set to `true`, AFM will be enabled for your line item. If this field is set to `false`, AFM will be disabled.<br>Advanced Frequency Management is an **open beta** feature. This feature is designed to have a UI-enablement option upon full release. |

## Examples

**Show a creative no more than 50 times over the lifetime of the campaign, 3 times per session, and 10 times per day**:

- `max_lifetime_imps` = 50
- `max_session_imps` = 3
- `max_day_imps` = 10

**Show a campaign up to 8 times per day but no more than once per hour**:

- `max_day_imps` = 8
- `min_minutes_per_imp` = 60

**Show a campaign no more than 3 times per hour**:

- `min_minutes_per_imp` = 20 minutes

## Where and how to apply frequency?

Frequency can be applied through profiles to [advertisers](advertiser-service.md), [insertion orders](./insertion-order-service.md), [line items](./line-item-service.md), [campaigns](./campaign-service.md), and [creatives](./creative-service.md), as well as to [payment rules](./payment-rule-service.md) for publishers. The most restrictive setting always takes precedence. For Adserver clients: Frequency can also be used for forecasting. Set the forecasting on the [profile](./profile-service.md), then reference that profile in
the [Inventory Forecasting Services](./inventory-forecasting-services.md).

### Inheritance of frequency or recency caps

When you set a frequency or recency cap for an object at one level, its child objects will inherit that cap, but it will be inherited by all child objects as a group. For example: If you set a frequency cap of ten impressions per day at the advertiser level and have ten line items attached to that advertiser, one line item could potentially use all 10 of the allotted impressions on one user. If you would like to spread the ten impressions out more evenly among your line items, you should also set a frequency cap at the line item level.

### Frequency and recency settings

Another important point to remember is that frequency and recency settings will be applied according to the strictest settings available. For example, imagine that you have two creatives, `A` and `B`, associated with the same line item. The frequency settings for creative `A` specify that it can only serve three times per day (where a day is defined as a calendar day). Creative `B` is set to only serve once per day. The line item settings, however, specify a frequency cap of two impressions per day.

Since the strictest settings are applied, the line item frequency settings override those set at the creative level. Therefore, even though creative `A`'s settings dictate that it can serve three times per day, it will never serve more than the two times per day specified at the line item level. If creative `B` serves its single allowed impression to the user before `A` can serve, `A` will only be allowed to serve once to that user.

## Related topics

- [API Semantics](./api-semantics.md)
- [Advertiser Service](./advertiser-service.md)
- [Insertion Order Service](./insertion-order-service.md)
- [Line Item Service](./line-item-service.md)
- [Creative Service](./creative-service.md)
- [Payment Rule Service](./payment-rule-service.md)
- [Profile Service](./profile-service.md)
