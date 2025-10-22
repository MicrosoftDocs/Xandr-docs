---
title: Yield Analytics 8.48
description: This page covers fixes/improvements/additions and integrations affected in Yield Analytics 8.48.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Yield Analytics 8.48

| Fixes, Improvements and Additions | Integrations Affected |
|--|--|
| Order Line Import Clean-up - We are enhancing the nightly import process to clean-up order lines that we've seen in the past, but that are no longer available from the source ad server. If order lines are in a cancelled state and have no historical delivery data, they will be removed and their associated artifacts deleted from the system. This change ensures a clean representation of future demand data to ensure accurate forecasting. | All |
| Line Item Revenue Reporting - Revenue data for Monetize impression based line items will now be calculated at the line item level instead of the previous process that calculated at the campaign level. This process removes potential incorrect revenue at-risk data and allows for more accurate revenue reporting across the Yield Analytics system. | Ad Server: Monetize |
