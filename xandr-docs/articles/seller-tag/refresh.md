---
title : Refresh
description : Learn how this function initiates a new ad server call and refreshes ads on the page.
ms.custom : seller-tag
ms.date: 10/28/2023
---

# Refresh

This function initiates a new ad server call and refreshes ads on the
page.

``` pre
refresh(['targetId1', 'targetId2'])
```

> [!NOTE]
> The existing iFrames related to the placements passed to the `refresh` method will be replaced and new iFrames created.

The parameter listed below can be sent as an argument in the function.

| Parameter | Type | Description |
|---|---|---|
| `targetId` | string | The unique identifier of a specific ad slot. One or more identifiers can be specified in an array. Omit the parameter to refresh all placements. This is an optional parameter. |

## Example

``` pre
apntag.refresh(['adslot1', 'adslot2']);
```
