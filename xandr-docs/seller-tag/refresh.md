---
title: Refresh
description: Learn how this function initiates a new ad server call and refreshes ads on the page. This page also lists parameter that can be sent as an argument in the function.  
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Refresh

This function initiates a new ad server call and refreshes ads on the page.

``` 
refresh(['targetId1', 'targetId2'])
```

> [!NOTE]
> The existing iFrames related to the placements passed to the `refresh` method will be replaced and new iFrames created.

The parameter listed below can be sent as an argument in the function.

| Parameter | Type | Description |
|--|--|--|
| `targetId` | string | The unique identifier of a specific ad slot. One or more identifiers can be specified in an array. Omit the parameter to refresh all placements. This is an optional parameter. |

## Example

``` 
apntag.refresh(['adslot1', 'adslot2']);
```
