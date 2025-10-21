---
title: Microsoft Curate - Universal Pixel Object Limits
description: This article provides details on the universal pixel object limits.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Universal pixel object limits

There are limits for how many audiences, conversions, custom events, and parameters you can create, as well as a data size limit for information transmitted by the parameters.

## Object limits

|  |  |
|:---|:---|
| **Audiences** | 1000 |
| **Conversions** | 1000 |
| **Custom Events** | 100 |
| **Custom Parameters** | 100 |

## Request limits

|  |  |
|:---|:---|
| **URL length** | 2000 characters |
| **Items passed in an array per single parameter** | 200 items |
| **Single parameter value** | 100 characters |
| **Total number of parameters** | 100 parameters |

> [!NOTE]
> If your application ID is longer than 200 characters, the request will be processed, but the ID will be truncated. Only the last 200 characters will be kept.
