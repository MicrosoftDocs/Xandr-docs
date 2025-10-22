---
title: Geo Variable Information
description: This article provides geo variable information. Digital Envoy is used for country and regional data. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Geo variable information

Xandr uses Digital Envoy for its Country and Region data. The Digital Envoy codes are derived from the user's IP address at the time of the ad call.

## Country

- ISO 3166
- United States and Canada are US, CA

  `{"country":"AS","name":"American Samoa"}`

## Region: US and Canada

- ISO 3166-2
- Note that for U.S. traffic, the region is equivalent to the U.S. postal state abbreviation codes (e.g. `"AL"`, `"AK"`, `"AZ"`).
- At present, the designated market areas (such as NYC) are not being passed via the Region codes.

  `{"region":"US:TX","name":"Texas"}`

## Region: International

Non-US/CA traffic will use the FIPS 10-4 codes.

## DMA

U.S. DMA codes are based on the Digital Envoy US metro codes.

`{"dma":"635","name":"Austin TX"}`
