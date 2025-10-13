---
title: Load JS Tracker
description: In this article, learn about the Load JS Tracker function and its parameter with a detailed example.
ms.custom: seller-tag
ms.date: 10/13/2025
---

# Load JS Tracker

The `loadJSTrackers` function fires JavaScript (JS) trackers for a native ad object if they exist. It can also render the tracker HTML directly inside a specified DOM element.

## Syntax

```
loadJSTrackers(nativeAdObject, element)
```

## Parameters

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Required | Description |
|:---|:---|:---| :---|
| nativeAdObject | object | Yes |The native ad object returned from the ad response. |
| element | DOM element | No | Optional. Optional. A reference to a DOM element (ideally the ad’s container div). If provided, the JS tracker HTML will be rendered inside this element. If not provided, the HTML will be appended to the `<body>` of the page. |

## Description

Unlike the [fireImpressionTrackers](fire-impression-trackers.md) function, `loadJSTrackers` fires only the JavaScript trackers that exist on the specified native ad object.

This function is typically called in the callback that handles the rendering of a native ad response (for example, in the adAvailable callback).

If a DOM element reference is passed as an argument, the function renders the JS tracker HTML code inside that element. This approach is useful when refreshing the ad container with a new ad, as it removes the old tracker HTML automatically.

If no DOM element is provided, the function writes the JS tracker HTML tags under the `<body>` element of the page.

## Example

```
function adAvailable(ad) {
  const adContainer = document.getElementById("nativeAdDiv");
  
  // Render the native ad
  renderNativeAd(ad, adContainer);

  // Fire JS trackers (if any exist)
  loadJSTrackers(ad, adContainer);
}

```
