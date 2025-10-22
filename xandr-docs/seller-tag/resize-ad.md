---
title: Resize Ad
description: Learn how this function resizes the iFrame placement for the specified `targetId` after the ad is rendered. This page also lists parameters that can be sent as arguments in the function along with an example.     
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---


# Resize Ad

This function resizes the iFrame placement for the specified `targetId` after the ad is rendered. If called before the ad is rendered, this function will not do anything.

``` 
resizeAd('targetId', [width, height], {config})
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|--|--|--|
| `[width, height]` | array of numbers | The placement size to which the iFrame should be resized, in the format `[300,250]`. |
| `config` | object | Contains optional config like settings to alter typical resizing behavior. See table below for list of supported flags. |
| `targetId` | string | The unique identifier of a specific ad slot. |
| `resizeAdParentDiv` | boolean | Setting this property to true will force the Parent Div container of the Ad creative to resize. This is particularly useful when resizing banner safeframe creatives when the parent div doesn't resize in some environments. By default, this option is turned off.<br><br>**Note**: If the resizeAdParentDiv option is passed to resizeAd, it will take precedence over the global option resizeAdParentDiv defined in defineTag. For example, if the value was set to false in resizeAd call, but the original defineTag had it set to true - the false setting from the resizeAd will be respected. |

## Example

``` 
apntag.resizeAd('apn_ad_40954389053', [100, 100], { resizeAdParentDiv: true });
```
