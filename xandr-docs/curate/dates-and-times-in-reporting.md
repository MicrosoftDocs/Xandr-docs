---
title: Microsoft Curate - Dates and Times in Reporting
description: This article explains how the reporting system handles time and date considerations such as time zones and daylight savings time.
ms.date: 11/10/2023
---

# Microsoft Curate - Dates and times in reporting

This page explains how our reporting system handles time and date considerations such as time zones and daylight savings time. It also describes how to change your member or advertiser's default time zone.

## Time zones

> [!NOTE]
> If you have signed a new contract with Microsoft Advertising and completed the cutover, your billing data is in UTC. Customers who migrate in the future also have their billing data set to UTC. Please ensure to adjust your reporting time period to UTC for continued compatibility with billing data when pulling all future reports.

Currently, most time zones for Curate objects are set to Eastern U.S. time by default (UTC - 4 hours or UTC - 5 hours, depending on daylight savings). You can change this time zone for your entire network/member, or for individual advertisers.

- You can select a different time zone for any report using the **Timezone** menu (under **Basic**).
- Billing data is always in UTC. However, you can always select the desired time zone when running a report.

## Member time zones

To change your network member time zone, you must contact Microsoft Advertising support or use the [Member Service API](../digital-platform-api/member-service.md). Note that changing your member's time zone will **not** change the time zone for existing objects (e.g., line items). However, newly created objects will automatically inherit the member time zone (unless the advertiser has a different time zone specified).

To change the time zone for all existing objects in your account, change the time zone of each advertiser. This can be used to propagate a change to the member time zone to all of that advertiser's child objects. For instructions on how to change an advertiser's time zone, see [Create an Advertiser](./create-an-advertiser.md).

## Advertiser time zones

Advertisers inherit the time zone of the member when they are first created, unless a different time zone is selected when they are created. For instructions on how to set an advertiser's time zone, see [Create an Advertiser](./create-an-advertiser.md).

When you change an advertiser's time zone, you can choose to apply the change to existing child objects. New objects that are created after the change (line items, creatives) will inherit the parent advertiser's time zone.

## Note on Eastern Daylight Time (EDT) and Eastern Standard Time (EST)

In our reporting system, ET (Eastern Time) will automatically take Daylight Saving Time into account. Eastern Daylight Time (EDT) will always mean UTC - 4 hours. Eastern Standard Time (EST) will always mean UTC - 5 hours.

## Daylight saving and reporting

> [!IMPORTANT]
> Certain regions have different naming conventions for annual time changes. For simplicity, we will refer to any such changes as Daylight Saving Time.

Daylight Saving Time (DST) changes can cause confusion around reporting results. This stems from the fact that these changes cause two days each year to have one extra or one less hour in certain regions. While there is no clear best practice for DST reporting, we feel it is worth documenting what you can expect from the time changes each season.

All Microsoft Advertising backend reporting data is stored in UTC. In the simplest case, you may be reporting on a UTC offset that is consistent all year. For example, Argentina Time (ART) does not observe DST. In such cases, no further time zone analysis is required.

However, if you observe DST, note that for each of the two annual changes, reports may show either one extra or one less hour. This happens because our reporting system uses the UTC offset governed by the starting date/hour of the report, instead of grouping metrics for two separate hours into a single row (i.e., combining two time zone offsets in a single report).

> [!NOTE]
> Stats will switch to EST at the time of the change (November 4, 02:00 EDT), but changes may take up to a few hours to propagate. The required processing time is likely to result in a temporary discrepancy between Stats and ET reporting.

### Example: Beginning of DST

Let's imagine that I took a trip in March, 2018 to visit an Microsoft Advertising datacenter in Europe for a month. On March 25, 2018 at 01:00 UTC, I observe the flip from 02:00 CET to 03:00 CEST and note that I have one hour less that day (i.e., 23 hours) as a result. If I were to run a report for the day of the change (2018-03-25) that begins at 00:00 CET, I would see a "missing" hour at the end of the report, corresponding with 2018-03-25 23:00 CET (now 2018-03-26 00:00 CEST).

### Example: End of DST

Let's look at an example from New York City. On Sunday, November 4, 2018 at 06:00 UTC, 02:00 EDT reverts to 01:00 EST. Therefore, November 4, 2018 is a 25-hour day. If I were to run a report for the day of the change (2018-11-04) that begins at 00:00 EDT, I would see an extra hour (2018-11-05 00:00 EDT) at the end of the report.

### Further complications of DST

Different regions observe DST changes at different times each year. Additionally, certain sub-regions may not adhere to the policies of their governing region. For example, neither Arizona nor Hawaii observe Daylight Saving Time like the rest of the individual states in the USA. Microsoft Advertising reporting adheres to DST using time zones, not geographies, so we cannot account for these individual region differences within time zones.

Also, some regions have offsets from UTC that are a fraction of an hour. For example, India is UTC + 05:30, and though it does not observe Daylight Saving Time, it is worth noting that Microsoft Advertising reporting operates in hourly granularity. Therefore, a single day 05:30 UTC - 05:29 UTC will actually appear in reports as 05:00 UTC - 04:59 UTC.

> [!NOTE]
> To learn more about Daylight Saving Time and its impact on your region, you can read more on the [Time and Date site](http://www.timeanddate.com/time/dst/).

## Related topics

- [Availability of Reporting Data](./availability-of-reporting-data.md)
- [Dimensions, Metrics, Filtering, and Grouping](./dimensions-metrics-filtering-and-grouping.md)
- [API Timezones](../digital-platform-api/api-timezones.md)
