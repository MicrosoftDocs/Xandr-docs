---
title: Bidders - Operating System Service
description: In this article, learn about bidders operating system service, their JSON parameters, and REST API with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Operating system service

This is a read-only service that shows you the list of operating systems that you can target in the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md) via the operating system ID.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/operating-system](https://api.adnxs.com/operating-system) | The basic service call will return a list of operating systems. |
| `GET` | [https://api.adnxs.com/operating-system/OPERATING_SYSTEM_ID](https://api.adnxs.com/operating-system/OPERATING_SYSTEM_ID) | To return a specific operating system. |

## JSON parameters

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | ID of the operating system entry. |
| `last_modified` | string | Date and time the operating system entry was last modified. |
| `name` | string | Name of the operating system. |
| `platform_type` | enum - "web", "mobile", or "both" | Describes whether the operating system runs on web devices, mobile devices, or both. |

## Example

To return a specific operating system

```
$ curl -b cookies -c cookies  https://api.adnxs.com/operating-system/1
{
   "response":{
      "status":"OK",
      "operating-system":{
         "id":1,
         "name":"Windows 7",
         "last_modified":"2010-06-30 19:38:01"
      },
      "count":1,
      "start_element":null,
      "num_elements":null
   }
}
```

## Related topics

- [Impression Bus API](impression-bus-api.md)
- [API Services](api-services.md)
