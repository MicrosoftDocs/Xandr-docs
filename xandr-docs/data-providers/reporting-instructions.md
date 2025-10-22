---
title: Reporting Instructions
description: In this article, explore the facts about the scheduled reports.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Reporting instructions

The following information is helpful when scheduling reports:

- Scheduled reports expire after 6 months. You must create a new scheduled report after 6 months.
- Scheduled reports and saved report templates cannot have a **Lifetime** or **Custom** date range.
- Scheduled reports are run in the order in which they were originally created. For example, if you create two daily reports, the daily report created first runs first each day.
- Daily reports are run and sent each day as soon as the data for the entire day (in the specified timezone) is available.
- Weekly reports are run and sent on the Monday of each week for the previous 7 days.
- Monthly reports are run and sent on the first day of each month.

> [!TIP]
> The report does not include a list of which segments are being targeted. This is why you may want to consider including the segment IDs or codes in the campaign name.
> [!NOTE]
> If you are sending a monthly report, the data provider does not know if you have added or removed segment targeting over the course of that month. Thus, you need to track segment targeting dates manually if any changes are made and send these to the data provider.
>
> For more information on API reporting, see [Report Service](../digital-platform-api/report-service.md).
