---
title: Freewheel Priority Values in Yield Analytics
description: In this article, learn about freewheel priority values in Yield Analytics.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Freewheel priority values in Yield Analytics

To appropriately rank competing FreeWheel placements, Yield Analytics maps numerical values to FreeWheel priority values.

## Freewheel summary

Yield Analytics assigns priority values for FreeWheel order lines as follows:

- The highest priority ads are the sponsorship ads that additionally have five levels of prioritization.
- Next in priority are guaranteed ads with set priorities from 20 to 11, with 20 being highest precedence.  
- Next in priority are the typical ads that have no priority setting, but compete based on the CPM value of the placement. The more revenue, the higher the rank.
- The lowest priority are negative values, which indicate lower priority (i.e., non-guaranteed ads, with -10 as the lowest).

## Priority mapping table

The following mappings are based on FreeWheel's values for Contract type and Override, and are displayed in decreasing order of rank. These values are available across the Yield Analytics UI, including availability lookups and reports.

| FreeWheel value | Yield Analytics priority label | Yield Analytics priority value | Notes |
|:---|:---|:---|:---|
| Sponsorship | Sponsorship highest | 27 | Highest value |
| Sponsorship | Sponsorship high | 26 |  |
| Sponsorship | Sponsorship above normal | 25 |  |
| Sponsorship | Sponsorship normal | 24 |  |
| Sponsorship | Sponsorship below normal | 23 |  |
| SOP | Sponsorship SOP | 22 |  |
| SOI | Sponsorship SOI | 21 |  |
| Guaranteed Impression | Above paying ads 20 | 20 |  |
| Guaranteed Impression | Above paying ads 19 | 19 |  |
| Guaranteed Impression | Above paying ads 18 | 18 |  |
| Guaranteed Impression | Above paying ads 17 | 17 |  |
| Guaranteed Impression | Above paying ads 16 | 16 |  |
| Guaranteed Impression | Above paying ads 15 | 15 |  |
| Guaranteed Impression | Above paying ads 14 | 14 |  |
| Guaranteed Impression | Above paying ads 13 | 13 |  |
| Guaranteed Impression | Above paying ads 12 | 12 |  |
| Guaranteed Impression | Above paying ads 11 | 11 |  |
| Guaranteed Impression | Above paying ads 1 | 10 |  |
| Guaranteed Impression | Paying ads 8 | 8 | Default |
| Preemptible Impressions | Below paying ads -1 | -1 |  |
| Preemptible Impressions | Below paying ads -2 | -2 |  |
| Preemptible Impressions | Below paying ads -3 | -3 |  |
| Preemptible Impressions | Below paying ads -4 | -4 |  |
| Preemptible Impressions | Below paying ads -5 | -5 |  |
| Preemptible Impressions | Below paying ads -6 | -6 |  |
| Preemptible Impressions | Below paying ads -7 | -7 |  |
| Preemptible Impressions | Below paying ads -8 | -8 |  |
| Preemptible Impressions | Below paying ads -9 | -9 |  |
| Preemptible Impressions | Below paying ads -10 | -10 | Lowest value |

> [!NOTE]
> The Yield Analytics priority labels for FreeWheel can be customized per client. For more information, contact your services representative.

## Related topic

[Ad Servers Overview](ad-servers-overview.md)
