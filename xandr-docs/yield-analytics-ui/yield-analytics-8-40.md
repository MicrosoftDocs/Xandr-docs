---
title: Yield Analytics 8.40
description: This page covers fixes/improvements/additions and integrations affected in Yield Analytics 8.40.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Yield Analytics 8.40

| Fixes, Improvements and Additions | Integrations Affected |
|--|--|
| Bug Fix: Show Cancelled Order Lines toggle on Order Line Visibility page was updated to properly hide/show cancelled order lines. | All |
| Changes were made to the API import process for OpenX SSP data to account for updates to their API and data availability. | Supply Side Platform: OpenX |
| Improvements were made to geography targeting on the FatTail integration: Multiple values for the same targeting element are now represented correctly and updates were made to better support geography targeting exclusions. | Order Management System: FatTail |
| Improvements were made to targeting gathered from the OperativeOne Order Import process: Support was added for FreeWheel ad server line items and rate card products that include product-embedded content advanced targeting. | Order Management System: Operative |
| Improvements were made to targeting gathered from the OperativeOne Order Import process: Support was added for FreeWheel ad server line items that include multiple comma separated values within a single targeting option mapped value. | Order Management System: Operative |
| Process improvements were made to data ingestion from Amazon S3: Additional file verification checks were put in place to ensure data integrity. | Ad Server: GAM, FreeWheel Order Management System: Operative Data Management Platform: Krux, Lotame |
