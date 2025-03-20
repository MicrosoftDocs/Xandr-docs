---
title: RTSS Use Cases
description: In this article, explore the supported use cases for the Real-Time Signals Service (RTSS).
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# RTSS use cases

This section outlines the supported use cases for the Real-Time Signals Service (RTSS).

- [RTSS use cases](#rtss-use-cases)
  - [OLC geolocation](#olc-geolocation)

## OLC geolocation

RTSS uses the [Open Location Code (OLC)](https://openlocationcode.com/) open standard for geo-targeting. OLC supports encoding of latitude and longitude coordinates. OLC also allows for targeting the locality around a specific point, removing the need to specify both a point and a radius. Full 10-character OLC codes allow more granular targeting, while shorter codes increase the targeted area around the point. Although RTSS supports 10-character OLC codes, we recommend only using up to 8 characters due to limited granularity of information received on bid impressions. Using 10 characters could severely limit your reach, or prevent your campaign from buying at all.
