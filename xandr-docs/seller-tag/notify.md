---
title: Notify
description: In this article, learn about the Notify function and its parameters with a detailed example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Notify

This function sends a notification to a renderer on a page (such as Outstream).

```
notify(messageType, messagePayload, targetId)
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|:---|:---|:---|
| `messageType` | string | String that indicates the message type sent to the renderer. It is a **Required** parameter.  |
| `messagePayload` | object | Javascript object that contains the message, in a format defined by the specific renderer. The object can be null, or an empty object. |
| `targetId` | string | A string that matches the `targetId` for one of the AST tag objects created by the `defineTag` call. When specified, the notify call will only impact the matching targetId on the page. If the field is left empty, then the notify function will impact all defined tags on the page. It is an **Optional** parameter. |

## Example

```
apntag.notify("startPlayback", {key: "data"}, "topBanner728x90")
```
