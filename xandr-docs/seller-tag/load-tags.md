---
title: Load Tags
description: In this article, learn about the Load Tags function and its parameter with a detailed example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Load Tags

This function makes an ad server call to load ads that have been defined by `defineTag` calls.

```
loadTags(['targetId1', 'targetId2'])
```

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|:---|:---|:---|
| `targetId` | string | The unique identifier of a specific ad slot. One or more identifiers can be specified in an array. The tags identified need to have been defined first using `apntag.defineTag`. Omit the parameter to load all tags. It is an optional parameter. |

## Example

```
apntag.loadTags(['adslot1', 'adslot2']);
```
