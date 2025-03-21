---
title: Real-Time Signals Service (Formerly APD)
description: Explore the Real-Time Signals Service (RTSS) that enables segment creation and targeting based on real-time signals.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Real-time Signals Service (formerly APD)

## Overview

RTSS is not generally available to all clients. To request access, contact your account manager.

- RTSS enables audience targeting using the following real-time signals:  
  - IP address  
  - URL path  
  - Geo-targeting  
  - Open location codes (8-character codes)  
  - It is a scalable alternative to cookie-based audience targeting.  

    - **GDPR and the demise of Third-Party Cookies**:  

       With evolving privacy regulations, increased scrutiny on user data collection, and the rise of ad-blocking, reliance on cookies and device IDs is becoming increasingly difficult.  

    - **CTV and the cookie-less environment**

      - There is no universal or persistent standard for device identification in CTV.  
      - The CTV ecosystem is dominated by a few "walled gardens."  
      - Advertisers and agencies must either collaborate directly with each device maker or platform, or buy through Private Marketplace (PMP) deals.  

- **Limitations**

  - Reporting is unavailable for uploaded targets by segment.  
  - Exclusion targeting is not supported for RTSS segments.  
  - The maximum time-to-live (TTL) for a targeting feature is 365 days.  
  - Uploads have regionalized API endpoints and storage.  

- **Processing time**  
  - As per the Xandr SLA, allow up to 24 hours for uploaded files to process.

- For more details on each endpoint and its capabilities, see the [API reference](real-time-signals-service-api-reference.md).
