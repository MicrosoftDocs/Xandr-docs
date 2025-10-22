---
title: Show Tag
description: Use the showTag function to indicate that an ad placement has been fully defined and is ready for an ad to be shown in its space.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Show tag

This function indicates that an ad placement has been fully defined and is ready for an ad to be shown in its space. Once this method is called, the impression will be marked as transacted and will be considered an "impression" for accounting purposes.

```
showTag('targetId'[, window])
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|:---|:---|:---|
| `targetId` | string | The unique identifier of a specific ad slot. |
| `window` | NA | (optional) Default value if not passed: `window`. The window where the target div is located. Generally only required when putting the `showTag()` call inside an iframe. |

## Example

```
apntag.showTag('apn_ad_slot_1');
```
