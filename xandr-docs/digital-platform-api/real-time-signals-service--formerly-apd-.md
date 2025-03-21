---
title: Real-Time Signals Service (Formerly APD)
description: Explore the Real-Time Signals Service (RTSS) that enables segment creation and targeting based on real-time signals.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Real-time Signals Service (formerly APD)

## Overview

RTSS is not generally available to all clients. Please reach out to your account manager for access.  

- Audience targeting - RTSS enables audience targeting using the following real-time signals:  

  - **IP address**  
  - **URL path**  
  - **Geo-targeting**  
  - **Open location codes (8-character codes)**  

   It provides a scalable alternative to cookie-based audience targeting.  

- GDPR and the Demise of Third-Party Cookies  

  With tightening privacy regulations and increased scrutiny around user data collection—along with ad-blocking—reliance on cookies and other device IDs will become increasingly difficult in the foreseeable future.  

- CTV and the Cookie-less Environment  

There is no universal or persistent standard for device identification for CTV. The CTV ecosystem is dominated by a handful of "walled gardens." As a result, advertisers and their agencies must work directly with each device maker/platform or buy through PMP.  

- Limitations  

The following limitations apply to RTSS:

- Reporting on uploaded targets by segment  
- Exclusion targeting on RTSS segments  
- Max TTL of 365 days for a targeting feature  
- Uploads have regionalized API endpoints/storage  

Per **Xandr SLA**, allow up to **24 hours** for uploaded files to process.  

- For more details on each endpoint and its capabilities, see the [API reference](real-time-signals-service-api-reference.md).
