---
title: Sync Report Service
description: This article lists the reports that use the Sync Report service. This service is currently under-development.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Sync Report service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This page is a placeholder, as this service is currently under development.

## Reports using this service

The following reports use this service. See the pages below for example usage.

- [Segment Overlap Report](./segment-overlap-report.md)
- [Seller Report](./seller-report.md)

## Sorting and pagination

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `offset` | int | `24` | The starting position of the pointer into the array of results.<br><br>**Default**: `0`<br>**Filter by**: No<br>**Sort by**: No |
| `count` | int | `5` | How many results to return, starting at the value of `offset`.<br><br>**Default**: `20`<br>**Filter by**: No<br>**Sort by**: No |
| `orders` | array of objects | `[{"direction": "DESC", "order_by": "avg_imps"}]` | You may sort the results, e.g. to see the highest-volume sellers, sort in descending order by `avg_imps`.<br><br>**Default**: `20`<br>**Filter by**: No<br>**Sort by**: No |
