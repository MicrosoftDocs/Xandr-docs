---
title: Load Viewability Scripts
description: In this article, learn about the Load Viewability Scripts function and its parameter with a detailed example.
ms.custom: seller-tag
ms.date: 10/13/2025
---

# Load Viewability Scripts

The `loadViewabilityScripts` function fires viewability tracking scripts for a native ad object if they exist. It can also render the script HTML directly inside a specified DOM element.

## Syntax

```
loadViewabilityScripts(nativeAdObject, element)

```

## Parameters

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Required | Description |
|:---|:---|:---| :---|
| nativeAdObject | object | Yes |The native ad object returned from the ad response. |
| element | DOM element | No | Optional. A reference to a DOM element (ideally the ad’s container div). If provided, the impression tracker HTML will be rendered inside this element. If not provided, the HTML will be appended to the <body> of the page. |

## Description

Unlike the [fireImpressionTrackers](fire-impression-trackers.md) — which can load viewability scripts automatically if the `trackingManagement` option is configured in `setPageOpts` — the `loadViewabilityScripts` function fires only the viewability script(s) that exist on the specified native ad object.

This function is typically called in the callback that handles the rendering of a native ad response (for example, in the adAvailable callback).

If a DOM element reference is passed as an argument, the function renders the viewability script HTML code inside that element. This approach is useful when refreshing the ad container with a new ad, as it removes the old script HTML automatically.

If no DOM element is provided, the function writes the viewability script HTML tags under the `<body>` element of the page.

## Example

```
function adAvailable(ad) {
  const adContainer = document.getElementById("nativeAdDiv");
  
  // Render the native ad
  renderNativeAd(ad, adContainer);

  // Fire viewability scripts (if any exist)
  loadViewabilityScripts(ad, adContainer);
}

```
