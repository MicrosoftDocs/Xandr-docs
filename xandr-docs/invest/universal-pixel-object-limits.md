---
title: Microsoft Invest - Universal Pixel Object Limits
description: Learn about limits on how many audiences, conversions, custom events, and parameters you can create, as well as how ID will get truncated if your application ID is longer than 200 characters.
ms.date: 10/28/2023
---

# Microsoft Invest - Universal pixel object limits

There are limits for how many audiences, conversions, custom events, and parameters you can create, as well as a data size limit for information transmitted by the parameters.

| Parameters | Data size limit  |
|:--|:--|
| **Audiences** | 1000 |
| **Conversions** | 1000 |
| **Custom Events** | 100 |
| **Custom Parameters** | 100 |

| Parameters | Data size limit  |
|:--|:--|
| **URL length** | 2000 characters |
| **Items passed in an array per single parameter** | 200 items |
| **Single parameter value** | 100 characters |
| **Total number of parameters** | 100 parameters |

> [!NOTE]
> If your application ID is longer than 200 characters, the request will be processed, but the ID will be truncated. Only the last 200 characters will be kept.
