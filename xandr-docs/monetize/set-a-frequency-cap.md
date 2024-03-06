---
title: Microsoft Monetize - Set a Frequency Cap
description: Explore setting frequency caps to strategically limit ad exposure, combining daily, weekly, and monthly caps for controlled creative displays.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set a frequency cap

You can set frequency caps from the **Audience & Location Targeting** section within the **Create New Line Item** and **Edit Line Item** screens.

Day, Week, and Month frequency caps are reset at a region-specific time of the day and during non-peak usage times.

Combining frequency caps could increase the restrictions on how often a creative is shown to a user. For example, if you set a frequency cap of four impressions per week, then set another frequency cap for two impressions per month, the user will never be shown four impressions in a week because they will reach the cap of two impressions in one month
and won't be shown any more for the rest of the month.

An exception to this would be if the month ended mid-week. Because weeks are defined as Sunday through Saturday and a month is a calendar month, in this scenario a user could be shown one impression on Sunday and one on Tuesday. If the month then ends on Wednesday, the user could be shown two more impressions by Saturday. At that point, the monthly cap has been met twice, once for each month in that week, and the weekly cap of four has been met.

1. Under the **Audience & Location Targeting** \> **Frequency & Recency** subsection, click the toggle.
1. Under **Frequency (how many)**, enter the number of impressions (imps) to show and select a timeframe.

   For example, to show a user a maximum of four impressions within one week, enter **4** in the text field and select **week** from the pull-down menu.

1. To add additional timeframes, click **Add another cap**.

   You can apply one frequency cap per timeframe. The following table describes the time period settings available for frequency caps:

   | Timeframe | Description |
   |---|---|
   |  **day** | The maximum number of times a creative can be served to a user within one day. |
   | **hour** | The maximum number of times a creative can be served to a user within a one-hour period. |
   | **lifetime** | The maximum number of times a creative can be served to the user. |
   | **month** | The maximum number of times a creative can be served within one calendar month.<br>Regardless of how far into a month a creative is first served to the user, the impression count for the user will be reset on the first day of the following month and the frequency count will start over. |
   | **week** | The maximum number of times a creative can be served within one week (beginning on Sunday).<br>Regardless of when a creative is first served to the user, every Sunday the impression count for the user will be reset to zero and the frequency values will begin recounting. |

1. Set the following settings:

   | Settings | Description |
   |---|---|
   | **Serve only 1 imp per page** | Use this setting to limit the number of impressions that an individual advertiser can serve on a page in multi-tag auctions. This option is network-specific and may not be available for your network (member). |
   | **Include users without cookies** | Once you set a frequency cap, you can choose to show creatives to users without cookies. There is no way to identify these users, so if you turn on this option your frequency and recency caps will not apply to any user without cookies. However, if you select not to include users without cookies you could limit your delivery. If you toggle this option and have set a daily frequency cap, [Advanced Frequency Management](advanced-frequency-management.md) will be applied to help adhere to your daily frequency cap. |

## Related topics

- [Buy-Side Page Caps](buy-side-page-caps.md)
- [Frequency and Recency Examples](frequency-and-recency-examples.md)
