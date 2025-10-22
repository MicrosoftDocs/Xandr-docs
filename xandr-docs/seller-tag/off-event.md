---
title: Off Event
description: Learn how this function clears the event listeners on the given `eventType` and `targetId`. This page also lists parameters that can be sent as arguments in the function along with an example.   
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---


# Off Event

This function clears the event listeners on the given `eventType` and `targetId`.

``` 
offEvent('eventType','targetId')
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|--|--|--|
| `eventType` | string | The event to listen for on the tag.<br>- `adRequested`: An ad was requested from the Impression Bus.<br>- `adAvailable`: A creative was returned from the Impression Bus but has not yet been shown.<br>- `adBadRequest`: The tag called a placement that doesn't exist.<br>- `adLoaded`: An ad placement has been fully defined and is ready to be shown; `apn.showTag` has been successfully executed.<br>- `adNoBid`: No bid was received for the ad tag.<br>- `adRequestFailure`: Failure to retrieve the creative. Could indicate a problem with the setup of the ad tag, or a problem contacting the endpoint.<br>- `adError`: Error caused by the creative itself (any first or third party in the chain) that was delivered by AST. Note that the ad may still be shown.<br>- `adCollapse`: Can be triggered by the creative, if the creative contains `window.parent.apntag.collapseAd(document.body.id)`. |
| `targetId` | string | The unique identifier of a specific ad slot. Omit this parameter to disable all the callback functions to be executed for this eventType. This is an optional parameter. |

## Example

``` 
apntag.offEvent('adError','apn_ad_slot_1');
 
apntag.offEvent('adError');
```
