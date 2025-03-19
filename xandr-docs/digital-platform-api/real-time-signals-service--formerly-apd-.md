---
title: Real-Time Signals Service (Formerly APD)
description: Explore the Real-Time Signals Service (RTSS) that enables segment creation and targeting based on real-time signals.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Real-Time Signals Service (RTSS) availability

## Overview

Real-Time Signals Service (RTSS) is not generally available to all clients. To request access, contact your account manager.  

RTSS enables audience targeting based on real-time signals, providing a scalable alternative to cookie-based audience targeting. Supported signals include:  

- **IP address**  
- **URL path**  
- **Geotargeting**  
- **Open location codes** (8-character codes)  

RTSS is particularly useful in the following scenarios:  

- **GDPR and the demise of third-party cookies** – With tightening privacy regulations, increased scrutiny around user data collection, and ad blocking, reliance on cookies and other device IDs is becoming increasingly difficult.  
- **CTV and the cookieless environment** – There is no universal or persistent standard for device identification in CTV. The CTV ecosystem is dominated by a handful of "walled gardens," requiring advertisers and agencies to work directly with each device maker or platform, or buy through PMP.  

### Limitations  

- Reporting on uploaded targets by segment is not supported.  
- Exclusion targeting on RTSS segments is unavailable.  
- The maximum TTL (time-to-live) for a targeting feature is **365 days**.  
- Uploads have **regionalized API endpoints and storage**.  
- Per **Xandr SLA**, allow **up to 24 hours** for uploaded files to process.  
- For details on each endpoint and its capabilities, see the [API reference](real-time-signals-service-api-reference.md).
