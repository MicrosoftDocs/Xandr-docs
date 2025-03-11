---
title: Microsoft Monetize - March 03, 2025 – Update to Data retention period in Audio, Video, and Analytics report   
description: We are introducing a breaking change to our Audio, Video, and Analytics reports in Microsoft Monetize.
ms.date: 03/03/2025
ms.topic: release-notes
ms.author: shsrinivasan
---


# Microsoft Monetize - March 03, 2025: Update to data retention period in audio, video, and analytics report    

As part of a data migration effort, we are updating the data retention policy to improve performance and efficiency in our Audio, Video, and Analytics reports.

This change will take effect in 15 days, on **March 18, 2025**. 

**Data retention policy updates:**
Most data in Analytics reports remains available, with the following exceptions: 
- After 6 months, hourly data will no longer be available for reporting. However, some reports may have a shorter hourly data retention period. The following reports will retain data for only 100 days: 
    - [Microsoft Monetize - Network Video Analytics](network-video-analytics-report.md) 
    - [Microsoft Invest - Network Video Analytics](../invest/network-video-analytics-report.md)
    - [Microsoft Invest - Network Audio Analytics](../invest/network-audio-analytics-report.md)
    - [Microsoft Monetize - Network Audio Analytics](network-audio-analytics-report.md)
- After 6 months, only daily granularity will be available for reporting. However, data for monthly and cumulative intervals are still available.   
- After 5 years, only the last 5 years of data will be retained, with older data being dropped. The following reports will retain data for only 500 days: 
    - [Microsoft Monetize - Network Video Analytics](network-video-analytics-report.md)
    - [Microsoft Invest - Network Video Analytics](../invest/network-video-analytics-report.md)
    - [Microsoft Invest - Network Audio Analytics](../invest/network-audio-analytics-report.md)
    - [Microsoft Monetize - Network Audio Analytics](network-audio-analytics-report.md) 
 
**The migration impacts the following reports:**  

- [Microsoft Monetize - Network Analytics Report](network-analytics-report.md)
- [Microsoft Invest - Network Analytics Report](../invest/network-analytics-report.md)
- [Digital Platform API - Network Analytics Report](../digital-platform-api/network-analytics-report.md)
- [Microsoft Invest - Advertiser Analytics Report](../invest/advertiser-analytics-report.md)
- [Digital Platform API - Advertiser Analytics Report](../digital-platform-api/advertiser-analytics-report.md)
- [Microsoft Monetize - Advertiser Analytics Report](advertiser-analytics-report.md)
- [Microsoft Monetize - Publisher Analytics Report](publisher-analytics-report.md)
- [Digital Platform API - Publisher Analytics Report](../digital-platform-api/publisher-analytics-report.md)

If you use our reporting API, please update your queries to exclude hourly data configurations for data older than six months. To maintain data consistency and accessibility, proactively save any required hourly data before it reaches the six-month limit. 

To learn more about breaking changes and their implications, see our [Breaking Changes Policy](breaking-changes.md). If you have any questions or require assistance with this update, please reach out to your account representative or contact [Product Support](https://support.ads.microsoft.com/).


