---
title: Attach Click Trackers
description: In this article, learn what the attachClickTrackers function is and the parameters that can be added to this function.
ms.custom: seller-tag
---

# Attach Click Trackers

This function adds a click event listener to an HTML element that fires click trackers for native ad units.

``` pre
attachClickTrackers(adObj,'htmlId');
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|---|---|---|
| `adObj` | object | The native ad object. (See [Ad Object API](ad-object-api.md).) |
| `adObj` | number | The HTML element to which the click event listener will be attached. |

## Example

``` pre
apntag.onEvent('adLoaded', function(tag) {
    apntag.attachClickTrackers(tag, 'nativeDivId');
});
```
