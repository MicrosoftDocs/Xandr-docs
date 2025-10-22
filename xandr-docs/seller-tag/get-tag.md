---
title: Get Tag
description: In this article, learn about the Get Tag function and its parameter with a detailed example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Get Tag

This function returns an object containing all tag objects that were created by `defineTag`. The method accepts one optional parameter, the `targetId` of the ad slot on page. Passing in the `targetId` will return the tag object with that ID.

```
getTag('targetId1')
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|:---|:---|:---|
| `targetId` | string | The unique identifier of a specific ad slot. It is an optional parameter. |

## Example

```
apntag.getTag();
apntag.getTag('apn_ad_slot_1');
```

## Example - Returned Tag object

The returned tag object looks like this:

```
{
  "debug": true,
  "displayed": true,
  "initialHeight": 250,
  "initialWidth": 300,
  "invCode": "ABC123",
  "member": "none",
  "modifyTag": "<ƒ (targetId, params)>",
  "off": "<ƒ (event, targetId, handler)>",
  "on": "<ƒ (event, targetId, handler)>",
  "setKeywords": "<ƒ (targetId, params)>",
  "showTagCalled": true,
  "sizes": [300, 250],
  "tagId": 13333444,
  "tagNumber": 0,
  "targetId": "apn_ad_slot_1",
  "utCalled": true,
  "utDivId": "div_utif_ad",
  "utiframeId": "utif_ad_54a77888-dcba-4c4d-abcd-beb888cc9a77",
  "uuid": "63a12376-c123-4212-b123-2dde8b12ab6e"
} 
```
