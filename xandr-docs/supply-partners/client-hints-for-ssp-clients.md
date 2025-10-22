---
title: User Agent Client Hints for SSP Clients
description: In this article, learn about the user-agent client hints API for SSP clients and the supported Open RTB for maximum performance and optimal device targeting.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# User agent client hints for SSP clients

## Overview

The User-Agent Client Hints API is an expansion to the Client Hints API, that enables developers to access information about a user's browser in a more specific and targeted manner, while still preserving the user's privacy and providing users with greater control over the data that is shared about their browsing activity. This API extends the traditional User-Agent header in HTTP requests and allows developers to request only the specific pieces of information they need, rather than exposing the entire header. This helps to eventually reduce the User-Agent string granularity and the amount of potentially sensitive information that can be transmitted.

Client Hints are intended to be an alternative source of information contained in the User-Agent header. User-Agent (UA) reduction is an effort to minimize the identifying information shared in the User-Agent string. As a result, the return values from certain `Navigator` interfaces are reduced, including: `navigator.userAgent`, `navigator.appVersion`, and `navigator.platform`. If we do not make the necessary adjustments and fail to adapt to this change, certain capabilities would be forfeited, including the ability to identify and prevent fraud and bot activity, recognizing browsers for rendering purposes, and targeting buyers based on their devices. Furthermore, buyers would no longer be able to take advantage of device targeting.

**Current UA string (detected as Tablet device):**

``` 
Mozilla/5.0 (Linux; Android 9; SM-T810) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.1234.56 Safari/537.36
```

**Same user with reduced UA string - not using Client Hints (detected as Desktop device):**

``` 
Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.0.0 Safari/537.36
```

## Scenarios

To offer maximum performance and execute optimal device targeting, publishers should pass Xandr the **structured user agent** data in bid requests in programmatic advertising. Currently, Xandr supports Open RTB 2.4 and can receive the structured user agent as an extension object called `user_agent_data`. However, we have also provided an example of Open RTB 2.6 below.

### Open RTB 2.4

```
"device":{
   "ua":"Mozilla/5.0 (Linux; Android 11; CPH1907) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Mobile Safari/537.36",
   "geo":{
      "country":"NZL",
      "region":"HKB",
      "metro":"2145",
      "city":"Waipukurau",
      "zip":"4200",
      "utcoffset":780,
      "ext":{
         "appnexus":{
            "timezone":"Pacific/Auckland"
         }
      }
   },
   "dnt":0,
   "ip":"222.154.65.1",
   "devicetype":4,
   "make":"Oppo",
   "model":"CPH1907",
   "os":"Android",
   "language":"en",
   "connectiontype":0,
   "ext":{
      "user_agent_data":{
         "browsers":[
            {
               "brand":"Google Chrome",
               "version":[
                  "111"
               ]
            },
            {
               "brand":"Not(A:Brand",
               "version":[
                  "8"
               ]
            },
            {
               "brand":"Chromium",
               "version":[
                  "111"
               ]
            }
         ],
         "platform":{
            "brand":"\"Android\""
         },
         "mobile":"1"
      }
   }
},
```

### Open RTB 2.6

```
"device":{
   "ua":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36",
   "ip":"76.89.224.206",
   "geo":{
      "lat":34.17,
      "lon":-118.05,
      "country":"USA",
      "region":"CA",
      "metro":"803",
      "city":"SIERRA MADRE",
      "zip":"91024",
      "type":2,
      "utcoffset":-28800
   },
   "language":"en",
   "os":"Windows 10",
   "osv":"10.0.0",
   "devicetype":2,
   "sua":{
      "browsers":[
         {
            "brand":"Google Chrome",
            "version":[
               "111",
               "0",
               "5563",
               "146"
            ]
         },
         {
            "brand":"Not(A:Brand",
            "version":[
               "8",
               "0",
               "0",
               "0"
            ]
         },
         {
            "brand":"Chromium",
            "version":[
               "111",
               "0",
               "5563",
               "146"
            ]
         }
      ],
      "platform":{
         "brand":"Windows",
         "version":[
            "10",
            "0",
            "0"
         ]
      },
      "mobile":0,
      "architecture":"x86",
      "bitness":"64",
      "model":"",
      "source":2
   }
},
```

### Demand partner OpenRTB format

> [!NOTE]
> We send requests today to demand partners only in Open RTB 2.4 format. Once we switch to Open RTB 2.6, we will send communication on the standard "structured user agent" support.
