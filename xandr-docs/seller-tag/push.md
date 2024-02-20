---
title: Push
description: Learn how this function adds a given function to the `apntag` command queue. This page also lists a parameter that can be sent as an argument in the function along with an example. 
ms.custom: seller-tag
ms.date: 10/28/2023
---


# Push

This function adds a given function to the `apntag` command queue. This is the primary way commands should be called. Before `apntag.js` loads, this function works as `Array.push`, adding commands to the queue. After `apntag.js` loads, this function will execute commands immediately.

``` 
anq.push(function())
```

The parameter listed below can be sent as an argument in the function.

| Parameter | Type | Description |
|--|--|--|
| `function` | function | The function to execute when the event is triggered. |

## Examplel

``` 
apntag.anq.push(function() {
        apntag.showTag('apn_ad_slot_1');
});
```
