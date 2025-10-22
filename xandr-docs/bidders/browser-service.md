---
title: Bidders - Browser Service
description: In this article, learn about bidders browser service, their JSON fields, and REST API with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Browser service

This is a **read-only** service that shows you the mapping between the browser IDs that you see in the [Bid Request](outgoing-bid-request-to-bidders.md) and their names. For example, you can see that [Google Chrome](https://www.google.com/chrome/)'s ID in our system is 8.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/browser](https://api.adnxs.com/browser) | The basic service call will return a list of browsers available for targeting. |
| `GET` | [https://api.adnxs.com/browser/BROWSER_ID](https://api.adnxs.com/browser/BROWSER_ID) | To return a specific browser. |

## JSON fields

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | ID of the browser entry. |
| `last_modified` | string | The date and time the browser entry was last modified. |
| `name` | string | Name of the browser. |
| `platform_type` | enum - "web", "mobile", or "both" | Describes whether the browser runs on web devices, mobile devices, or both. |

## Example

### To return a specific browser

```
$ curl -b cookies -c cookies  https://api.adnxs.com/browser/2
{
   "response":{
      "status":"OK",
      "browser":{
         "id":2,
         "name":"Firefox (all versions)",
         "last_modified":"2010-06-30 19:38:01"
      },
      "count":1,
      "start_element":null,
      "num_elements":null
   }
   }
```

## Related topics

- [Bid Request](outgoing-bid-request-to-bidders.md)
- [API Services](api-services.md)
- [Bid Request - FAQ](bid-request---faq.md)
