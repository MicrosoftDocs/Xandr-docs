---
title: Microsoft Monetize - Set a Recency Cap
description: Explore how to set recency caps where you can specify impressions and frequency for controlled ad displays.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set a recency cap

You can set recency caps from the **Audience & Location Targeting** section within the **Create New Line Item** and **Edit Line Item** screens.

1. Under the **Audience & Location Targeting** \> **Frequency & Recency** subsection, click the toggle if it's not  already selected.
1. Under **Recency (how often)**, click the **Add another cap** button.
1. Enter the number of impressions (imps) to show and select how often to show them.

   For example, to ensure that a user doesn't see a creative more than one time every two days, enter **2** in the text field and select **days** from the pull-down menu.

   > [!NOTE]
   > You can apply only one recency setting.
   >
   > Time frames for recency differ from frequency time frames. Frequency is based on a calendar timestamp. For example, a frequency setting to show four impressions during a one week period will count that  week as beginning on Sunday and ending on Saturday. Recency is based on the time of the impression. If your recency cap is set to show one impression every two weeks, the two-week period encompasses the 14 days from the time the creative is served. For example, if a creative is served to the user on July 1, a recency setting of one impression every two weeks would keep the user from seeing that creative again until at least July 15 regardless of what day of the week that is.

1. Set the following settings:

   | Settings | Description |
   |---|---|
   | **Serve only 1 imp per page** | Use this setting to limit the number of impressions that an individual advertiser can serve on a page in multi-tag auctions. This option is network-specific and may not be available for your network (member). |
   | **Include users without cookies** | Once you set a frequency cap, you can choose to show creatives to users without cookies. There is no way to identify these users, so if you turn on this option your frequency and recency caps will not apply to any user without cookies. However, if you select not to include users without cookies you could limit your delivery. If you toggle this option and have set a daily frequency cap, [Advanced Frequency Management](advanced-frequency-management.md) will be applied to help adhere to your daily frequency cap. |

## Related topics

- [Buy-Side Page Caps](buy-side-page-caps.md)
- [Frequency and Recency Examples](frequency-and-recency-examples.md)
