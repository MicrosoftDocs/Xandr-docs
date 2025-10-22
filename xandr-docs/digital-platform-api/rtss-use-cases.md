---
title: RTSS Use Cases
description: In this article, explore the supported use cases for the Real-Time Signals Service (RTSS).
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# RTSS use cases

The RTSS beta is still under development and may have additional features deployed in response to changing use cases. This page lists the current supported use cases.

## Supported use cases

- **OLC geolocation**  
  RTSS uses the Open Location Code (OLC) open standard for geo-targeting. We recommend using OLC-8 codes due to limited granularity of information received on bid impressions. Using OLC-10 is not recommended as it could severely limit your reach or prevent your campaign from buying at all.  
  OLC targeting requires latitude/longitude location information on the impression.

- **IP address targeting**  
  RTSS supports targeting IPv4 addresses.

- **URL targeting**

  RTSS URL targeting currently supports:
  - URL reference matching (i.e., whole address)
  - URL component matching up to three paths deep

## Use cases

RTSS serves different types of users by enabling targeting capabilities in various contexts:

- **Publishers**: RTSS provides publishers and their data management platforms (DMPs) with a viable alternative to onboard and monetize their first-party (1P) audience based on contextual signals in a secure, privacy-compliant way.

- **Curators**: RTSS enables curators to create context-based audiences using alternative signals. They can then pair these unique audience datasets with supply from the Xandr exchange to create media products, which can be sold through deals to any demand-side platform (DSP).

- **Buyers**: RTSS enables buyers to create their own audiences or access premium publishers' audiences and target them in a cookie-less environment, such as connected TV (CTV).