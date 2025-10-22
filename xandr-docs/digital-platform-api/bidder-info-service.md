---
title: Bidder Info Service
description: In this article, find information about the Bidder Info Service along with an example response.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Bidder info service

The Bidder Info Service returns the capabilities of each bidder. This includes the platforms, such as app or site, and the mediaTypes, such as banner, that the bidder will bid on. The service also returns a contact email for the bidder maintainer and the current status of the bidder. For more information about available demand partners and their capabilities, see [PSP Demand Partner Integrations](../monetize/prebid-server-premium-demand-partner-integrations.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | `https://api.appnexus.com/prebid/bidder-info` | Return all bidder information for this config. |

## Example response

The response is a JSON object containing bidder info objects.

```
{
  "33across": {
    "capabilities": {
      "app": {
        "mediaTypes": [
          "banner"
        ]
      },
      "site": {
        "mediaTypes": [
          "banner"
        ]
      }
    },
    "maintainer": {
      "email": "dev@33across.com"
    },
    "status": "ACTIVE"
  },
  "adform": {
    "capabilities": {
      "app": {
        "mediaTypes": [
          "banner"
        ]
      },
      "site": {
        "mediaTypes": [
          "banner"
        ]
      }
    },
    "maintainer": {
      "email": "scope.sspp@adform.com"
    },
    "status": "ACTIVE"
  },
  "adkernel": {
    "capabilities": {
      "app": {
        "mediaTypes": [
          "banner"
        ]
      },
      "site": {
        "mediaTypes": [
          "banner",
          "video"
        ]
      }
    },
    "maintainer": {
      "email": "prebid-dev@adkernel.com"
    },
    "status": "ACTIVE"
  },
  "adkernelAdn": {
    "capabilities": {
      "app": {
        "mediaTypes": [
          "banner"
        ]
      },
      "site": {
        "mediaTypes": [
          "banner",
          "video"
        ]
      }
    },
    "maintainer": {
      "email": "prebid-dev@adkernel.com"
    },
    "status": "ACTIVE"
  },
  ...
```
