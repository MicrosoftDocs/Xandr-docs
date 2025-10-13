---
title: Load Click Trackers
description: In this article, learn about the Load Click Trackers function and its parameter with a detailed example.
ms.custom: seller-tag
ms.date: 10/13/2025
---

# Load Click Trackers

The `loadClickTrackerUrls` function fires click trackers for a native ad object if they exist. Unlike [attachClickTrackers](attach-click-trackers.md), which creates a click event listener on a DOM element, this function immediately fires the click trackers independently of the DOM element.

## Syntax

```
loadClickTrackerUrls(nativeAdObject, element)

```

## Parameters

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Required | Description |
|:---|:---|:---| :---|
| nativeAdObject | object | Yes |The native ad object returned from the ad response. |
| element | DOM element | No | Optional. A reference to a DOM element (ideally the ad’s container div). If provided, the impression tracker HTML will be rendered inside this element. If not provided, the HTML will be appended to the `<body>` of the page. |

## Description

Unlike the [attachClickTrackers](attach-click-trackers.md) function — which attaches a click event listener to a DOM element — `loadClickTrackerUrls` immediately fires click trackers that exist on the specified native ad object.

This function is typically called in the callback that handles the rendering of a native ad response (for example, in the `adAvailable` callback) when you want the clicks to be tracked independently of the DOM element itself.

If a DOM element reference is passed, the HTML assets created to fire these click URLs are rendered inside that element. This is useful when refreshing the ad container with a new ad, as it removes the old HTML assets automatically.

If no DOM element is provided, the function writes these HTML assets under the `<body>` element of the page.

## Example

```
function adAvailable(ad) {
  const adContainer = document.getElementById("nativeAdDiv");
  
  // Render the native ad
  renderNativeAd(ad, adContainer);

  // Fire click trackers (if any exist)
  loadClickTrackerUrls(ad, adContainer);
}

```
