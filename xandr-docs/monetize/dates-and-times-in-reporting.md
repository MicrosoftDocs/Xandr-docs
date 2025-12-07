---
title: Microsoft Monetize - Dates and Times in Reporting
description: This page gives an overview on different timezones and daylight savings and reporting along with examples.
ms.date: 12/7/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Dates and times in reporting

This page explains how our reporting system handles time and date considerations such as time zones and daylight savings time. It also describes how to change your member or advertiser's default time zone.

## Time zones

> [!NOTE]
> All billing data is in Coordinated Universal Time (UTC). Please ensure to adjust your reporting time period to UTC for continued compatibility with billing data when pulling all future reports. 

Currently, most time zones for Monetize objects are set to Eastern U.S. time by default (UTC - 4 hours or UTC - 5 hours, depending on daylight savings). You can change this time zone for your entire network/member, or for individual advertisers.

- You can select a different time zone for any report using the **Timezone** menu (under **Basic**)
- Billing data is always in UTC. However, you can always select the desired time zone when running a report.

### Member time zones

To change your network member time zone, you must contact Microsoft Advertising support or use the [Member Service API](../digital-platform-api/member-service.md). Please note that changing your member's time zone will **not** change the time zone for existing objects (e.g., line items). However, newly created objects will automatically inherit the member time zone (unless the advertiser has a different time zone specified).

To change the time zone for all existing objects in your account, change the time zone of each advertiser. This can be used to propagate a change to the member time zone to all of that advertiser's child objects. For instructions on how to change an advertiser's time zone, see [Create an Advertiser](create-an-advertiser.md).

### Advertiser time zones

Advertisers inherit the time zone of the member when they are first created, unless a different time zone is selected when they are created. For instructions on how to set an advertiser's time zone, see [Create an Advertiser](create-an-advertiser.md).

When you change an advertiser's time zone, you can choose to apply the change to existing child objects. New objects that are created after the change (line items, creatives) will inherit the parent advertiser's time zone.

## A note on eastern daylight time and eastern standard time

In our reporting system, ET (Eastern Time) will automatically take Daylight Saving Time into account. Eastern Daylight Time (EDT) will always mean UTC - 4 hours. Eastern Standard Time (EST) will always mean UTC - 5 hours.

## Daylight savings and reporting

> [!IMPORTANT]
> Certain regions have different naming conventions for annual time changes. For simplicity, we will refer to any such changes as Daylight Saving Time.

Daylight Saving Time (DST) changes can cause confusion around reporting results. This stems from the fact that these changes cause two days each year to have one extra or one less hour in certain regions. While there is no clear best practice for DST reporting, we feel it is worth documenting what you can expect from the time changes each season.

All Microsoft Advertising backend reporting data is stored in UTC. In the simplest case, you may be reporting on a UTC offset that is consistent all year. For example, Argentina Time (ART) does not observe DST. In such cases, no further time zone analysis is required.

However, if you observe DST, note that for each of the two annual changes, reports may show either one extra or one less hour. This happens because our reporting system uses the UTC offset governed by the starting date/hour of the report, instead of grouping metrics for two separate hours into a single row (i.e., combining two time zone offsets in a single report).

> [!NOTE]
> Stats will switch to EST at the time of the change (November 4, 02:00 EDT), but changes may take up to a few hours to propagate. The required processing time is likely to result in a temporary discrepancy between Stats and ET reporting.

<!-- ### Example: Beginning of DST

Let's imagine that I took a trip in March, 2018 to visit an Microsoft Advertising datacenter in Europe for a month. On March 25, 2018 at 01:00 UTC, I observe the flip from 02:00 CET to 03:00 CEST and note that I have one hour less that day (i.e., 23 hours) as a result. If I were to run a report for the day of the change (2018-03-25) that begins at 00:00 CET, I would see a "missing" hour at the end of the report, corresponding with 2018-03-25 23:00 CET (now 2018-03-26 00:00 CEST).

### Example: End of DST

Let's look at an example from New York City. On Sunday, November 4, 2018 at 06:00 UTC, 02:00 EDT reverts to 01:00 EST. Therefore, November 4, 2018 is a 25-hour day. If I were to run a report for the day of the change (2018-11-04) that begins at 00:00 EDT, I would see an extra hour (2018-11-05 00:00 EDT) at the end of the report. -->

## Beginning of DST (Spring Forward)

When Daylight Saving Time (DST) begins, clocks move **forward one hour**, effectively *skipping* an hour of local time. Because our backend data is stored in **UTC**, this affects only how data is presented when reporting in a timezone that observes DST — not how it is stored.

### What Happens under the Hood
- All data is recorded in **UTC timestamps**.  
- UTC does **not change**, even if local timezone observes DST.  
- Consequently, there is no missing or duplicate data at the storage level.

### What Users See in Local Time Reporting
On the day DST begins, when local clocks jump ahead, one local hour disappears. If you run a report in a timezone that observes DST (e.g., CET → CEST), the report will reflect a **23-hour day** (instead of 24).

For example:  
- At **01:00 UTC** on March 25, 2018, local time in Central Europe jumps from **02:00 CET → 03:00 CEST** 
- That missing hour (02:00–02:59 local time) will not appear in the report.

If you run a report for the DST-change date in local time (starting at 00:00 local time), you will notice that the final hour of the day appears to end one hour sooner than a normal 24-hour day. In the example above, you’d see 23 hours of data, with the local-time **23:00 CET** effectively becoming **00:00 CEST (next day)**. 

> [!IMPORTANT]
> This behavior is expected: because local time “skips” the DST-forward hour, data for that hour does *not* exist — and the day is reported as 23 hours long, even though UTC still reflects a full 24-hour span.

### Recommendation for Accurate Analysis
- If you need consistent hourly granularity (e.g., for automated tooling, QA, or charting), prefer reporting in **UTC** — this ensures a full 24-hour view without missing hours.  
- If you report in local timezone, be aware of the DST shift: one hour will be missing on the DST-start day, and reports will reflect 23 hours.

# End of DST (Fall Back)

When Daylight Saving Time (DST) ends, clocks move **back one hour**, creating two occurrences of the same local hour (for example, **01:00–02:00** appears twice). All Monetize reporting data is stored in **UTC**, so this transition affects only how timestamps are **displayed** when you run reports in a local timezone.

## How Data Is Stored
- All data is stored using **UTC timestamps**.  
- UTC hours remain **distinct** even during DST transitions.  
- No data is lost or duplicated at the storage layer.

During the fall-back transition, the following UTC timestamps are separate records:

| UTC Hour | Notes |
|----------|--------|
| 05:00 | Occurs before the fall-back shift in US/Eastern |
| 06:00 | Occurs after the fall-back shift in US/Eastern |

## How Timezone Conversion Works
Timezone conversion happens at the **query/reporting** level.

When you run a report in a timezone that undergoes a fall-back shift (for example, **US/Eastern**):

- Both UTC 05:00 and UTC 06:00 convert to the **same local hour: 01:00**.  
- Because both hours are valid, Monetize **aggregates** all metrics for that repeated local hour.  
- This is **expected behavior**, reflecting real-world repeated local time.

## Example: Fall Back Hour Aggregation

### UTC Reporting
If you run the report in UTC, the hours remain distinct:

- **UTC 05:00:** 3,000,000 impressions  
- **UTC 06:00:** 4,000,000 impressions  
- **Total:** 7,000,000 impressions

### US/Eastern Reporting
When the same data is viewed in **US/Eastern** during fall back:

- **Local 01:00** receives impressions from:
  - UTC 05:00 → Local 01:00  
  - UTC 06:00 → Local 01:00  

- **Displayed value for Local 01:00:**  
  **7,000,000 impressions** (3,000,000 + 4,000,000)

> [!IMPORTANT]
> This combined value is expected because the local hour occurs twice. To avoid repeated-hour aggregation, run reports in **UTC** during DST transitions.

## Reporting Recommendations
- Use **UTC** when you need precise hourly visibility (for example, pacing, anomaly detection, or hourly QA).  
- Use local timezone reporting when business workflows require local time interpretation, understanding that:
  - **Fall back** results in one repeated hour (aggregated).  
  - **Spring forward** results in one missing hour (skipped).


### Further complications of DST

Different regions observe DST changes at different times each year. Additionally, certain sub-regions may not adhere to the policies of their governing region. For example, neither Arizona nor Hawaii observe Daylight Saving Time like the rest of the individual states in the USA. Microsoft Advertising reporting adheres to DST using time zones, not geographies, so we cannot account for these individual region differences within time zones.

Also, some regions have offsets from UTC that are a fraction of an hour. For example, India is UTC + 05:30, and though it does not observe Daylight Saving Time, it is worth noting that Microsoft Advertising reporting operates in hourly granularity. Therefore, a single day 05:30 UTC - 05:29 UTC will actually appear in reports as 05:00 UTC - 04:59 UTC.

> [!NOTE]
> To learn more about Daylight Saving Time and its impact on your region, you can read more on the [Time and Date site](https://www.timeanddate.com/time/dst/).

## Related topics

- [Availability of Reporting Data](availability-of-reporting-data.md)
- [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md)
- [API Timezones](../digital-platform-api/api-timezones.md)
