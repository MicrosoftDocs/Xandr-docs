---
title: Set Keywords
description: This function sets the keywords for the specified `targetId`. This page also lists parameters that can be sent as arguments in the function along with an example. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---


# Set keywords

This function sets the keywords for the specified `targetId`.

``` 
setKeywords (('targetId',{keywords},options))
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|--|--|--|
| `keywords` | key/value pair | A set of key/value pairs applicable to this ad slot. Query string segments are defined by key/value pairs in this object. Keywords that contain hyphens must be enclosed in single quote marks. Best practice is to always surround keywords with single quotes. Users can also create a custom macro. The format must be `#{MY_CUSTOM_KEY}`.<br>These key/values/macros are case sensitive (not forced uppercase).<br>**Note**: A maximum of 100 macro replacements are allowed on a pixel/creative, etc. |
| `options` | object | An object specifying additional options available when setting keywords. Values are Boolean.<br>**overrideKeyValue**<br>**true**: Existing values for keywords will be overwritten by values specified in this tag.<br>**false**: (Default) Values of keywords in the current tag will be added to previously-defined keywords. |
| `targetId` | string | The unique identifier of a specific ad slot. |

## Example

```
apntag.setKeywords('apn_ad_slot_1',
        { genre : ['rock','pop'] }
);
apntag.setKeywords('apn_ad_slot_2',
        { 'hello' : 'world' }
);
 
apntag.setKeywords('apn_ad_slot_3',
        { 'genre' : ['hiphop','classical'] },
        { overrideKeyValue: true}
);
```
