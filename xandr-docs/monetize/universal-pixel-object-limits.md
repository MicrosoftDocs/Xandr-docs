---
title: Microsoft Monetize - Universal Pixel Object Limits
description: In this article, find a list of limits for the different objects and requests for universal pixel.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Universal Pixel object limits

There are limits for how many audiences, conversions, custom events, and parameters you can create, as well as a data size limit for information transmitted by the parameters for universal pixels.

## Object limits

The table below shows the limits to the number of objects you can create.

| Object | Limit |
|---|---|
| **Audiences** | 1000 |
| **Conversions** | 1000 |
| **Custom Events** | 100 |
| **Custom Parameters** | 100 |

## Request limits

The table below shows the size limits for the information transmitted by parameters.

| Request | Limit |
|---|---|
| **URL length** | 2000 characters |
| **Items passed in an array per single parameter** | 200 items |
| **Single parameter value** | 100 characters |
| **Total number of parameters** | 100 parameters |

> [!NOTE]
> If your application ID is longer than 200 characters, the request will be processed, but the ID will be truncated. Only the last 200 characters will be kept.
