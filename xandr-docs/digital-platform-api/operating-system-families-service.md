---
title: Operating System-Families Service
description: Use the Operating System-Families service to list all available operating systems for caller's member that are not maintained by Prebid Server Premium. 
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Operating System-Families service

The Operating System-Families service returns all the operating systems available for the caller's member.

Operating systems are a Monetize-wide list NOT maintained by Prebid Server Premium. This service can be found at [Operating System Service](./operating-system-service.md). We offer this endpoint in PSP as a convenience to users and also so we can show a list of operating systems for targeting purposes in the UI.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/prebid/operating-system-families` | Return all the operating system-families objects. |

## Example response

The response is a JSON array of operating system-family objects.

```
[
   {
      "id":1,
      "name":"Unknown"
   },
   {
      "id":2,
      "name":"Android"
   },
   {
      "id":3,
      "name":"Apple iOS"
   },
   {
      "id":4,
      "name":"Apple Mac"
   },
   {
      "id":5,
      "name":"Microsoft Windows"
   },
   {
      "id":6,
      "name":"BlackBerry OS"
   },
   {
      "id":8,
      "name":"Linux"
   },
   {
      "id":9,
      "name":"Symbian OS"
   },
   {
      "id":10,
      "name":"Chrome OS"
   },
   {
      "id":11,
      "name":"PlayStation 4 OS"
   },
   {
      "id":12,
      "name":"Firefox OS"
   },
   {
      "id":13,
      "name":"Roku OS"
   },
   {
      "id":14,
      "name":"Tizen"
   },
   {
      "id":15,
      "name":"webOS"
   },
   {
      "id":16,
      "name":"PlayStation 3 OS"
   },
   {
      "id":17,
      "name":"KaiOS"
   },
   {
      "id":18,
      "name":"tvOS"
   },
   {
      "id":19,
      "name":"Vewd OS"
   }
]                
                
```
