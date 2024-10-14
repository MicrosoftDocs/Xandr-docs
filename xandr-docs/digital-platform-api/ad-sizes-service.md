---
title: Ad Sizes Service
description: Learn about the Ad Sizes service. The service returns accepted ad sizes from the Member service, which cannot be set in PSP.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Ad Sizes service

The Ad Size Service returns the ad sizes that are accepted by the member associated with the Prebid Server Premium (PSP) configuration. These Ad sizes are set at the member level and derived from `standard_sizes` field in the [Member Service](./member-service.md) documentation. Ad sizes cannot be set in PSP and are instead retrieved via the endpoint described below.

The `is_standard` field indicates that the size is a standard size for a creative and not a custom size added to the member.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/prebid/ad-sizes` | Return all ad sizes. |

### Example response

The response is a JSON array of ad size objects.

```
[
  {
    "height": 150,
    "is_standard": false,
    "width": 180
  },
  {
    "height": 250,
    "is_standard": false,
    "width": 300
  },
  {
    "height": 480,
    "is_standard": false,
    "width": 640
  },
  {
    "height": 120,
    "is_standard": false,
    "width": 980
  }
]
```
