---
title:Load Impression Tracker
description: In this article, learn about the Load Impression Tracker function and its parameter with a detailed example.
ms.custom: seller-tag
ms.date: 10/13/2025
---

# Load Impression Tracker

The `loadImpressionTrackerUrls` function fires impression trackers for a native ad object if they exist. It can also render the impression tracker HTML directly inside a specified DOM element.

## Syntax

```
loadImpressionTrackerUrls(nativeAdObject, element)
```

## Parameters

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Required | Description |
|:---|:---|:---| :---|
| nativeAdObject | object | Yes |The native ad object returned from the ad response. |
| element | DOM element | No | Optional. A reference to a DOM element (ideally the ad’s container div). If provided, the impression tracker HTML will be rendered inside this element. If not provided, the HTML will be appended to the <body> of the page. |

## Description

Unlike the fireImpressionTrackers function, `loadImpressionTrackerUrls` fires impression trackers only if they exist on the specified native ad object.

This function is typically called in the callback that handles the rendering of a native ad response (for example, in the `adAvailable` callback).

If a DOM element reference is passed as an argument, the function will render the impression tracker HTML code inside that element. This is useful when refreshing the ad container with a new ad, as the old impression tracker HTML will be removed automatically.

If no DOM element is provided, the function writes the impression tracker HTML tags under the `<body>` element of the page.

## Example

```
function adAvailable(ad) {
  var adContainer = document.getElementById("nativeAdDiv");
  
  // Render the native ad
  renderNativeAd(ad, adContainer);

  // Fire impression trackers (if any exist)
  loadImpressionTrackerUrls(ad, adContainer);
}

```
