---
title: Digital Platform API - May 15, 2025 – Updated Data Retention Policy for Identifiers and Buyer Reach & Frequency Reports   
description: As part of a backend data migration initiative aimed at improving performance and system efficiency, we are updating the data retention policy for the Digital Platform API Identifiers – Distinct IDs and Digital Platform API Buyer Reach and Frequency reports.
ms.topic: release-notes
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---


# Digital Platform API - May 15, 2025: Updated Data Retention Policy for Identifiers and Buyer Reach & Frequency Reports 

As part of a backend data migration initiative aimed at improving performance and system efficiency, we are updating the data retention policy for the following reports: 
- [Identifiers – Distinct IDs](identifiers--distinct-id-report.md)  
- [Buyer Reach and Frequency](buyer-reach-and-frequency-report.md).

This change will take effect on **May 15, 2025**. 

Currently, both reports retain 90 days of data. Starting **May 15, 2025**, the retention period will be reduced: 

- Identifiers – Distinct IDs report will retain **50 days of data**. 
    - [Microsoft Invest - Identifiers – Distinct IDs](../invest/identifiers-distinct-id-report.md) 
    - [Microsoft Monetize - Identifiers – Distinct IDs](../monetize/identifiers--distinct-id-report.md) 
    - [Digital Platform API - Identifiers – Distinct IDs](identifiers--distinct-id-report.md) 

- Buyer Reach and Frequency report will retain **42 days of data**. 
    - [Microsoft Invest - Buyer Reach and Frequency](../invest/buyer-reach-and-frequency-report.md) 
    - [Microsoft Monetize - Buyer Reach and Frequency](../monetize/buyer-reach-and-frequency-report.md) 
    - [Digital Platform API - Buyer Reach and Frequency](buyer-reach-and-frequency-report.md)

Beginning **May 16, 2025**, the data retention for both reports will incrementally increase by one day per calendar day, until it reaches the standard 90-day window again. 
For example: 
- On **May 16**, retention will be **51 days and 43 days**, respectively. 
- On **May 17**, it will be **52 days and 44 days**, and so on. 

To ensure continuity during the interim, a data snapshot will be made available to support access to key information while the reports are repopulated under the new retention model. 
 
To learn more about breaking changes and their implications, see our [Breaking Changes Policy](breaking-changes.md). For assistance or access requests, please reach out to your account representative or contact [Product Support](https://support.ads.microsoft.com/).


