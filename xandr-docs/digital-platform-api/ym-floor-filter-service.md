---
title: YM Floor Filter Service
description: Explore the YM Floor Filter service to view a list of yield management (YM) floor rules that apply to a specific member.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# YM Floor Filter service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This read-only service allows you to view a list of yield management (YM) floor rules that apply to a specific member. The response will include a list of YM floor rule IDs. You can use the ID to get more information on the YM floor rule settings using the [Yield Management Floor Service](yield-management-floor-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/ym-floor-filter?publisher_id=PUBLISHER_ID](https://api.appnexus.com/ym-floor-filter?publisher_id=PUBLISHER_ID) | View all yield management floor rules that apply to a specific publisher. |
| `GET` | [https://api.appnexus.com/ym-floor-filter?buyer_member_id=BUYER_MEMBER_ID](https://api.appnexus.com/ym-floor-filter?buyer_member_id=BUYER_MEMBER_ID) | View all yield management floor rules that apply to a specific buyer. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `ym-floor-filter` | array | The list of yield management floor rule IDs for rules that apply to the member. For more information, see [YM Floor Filter](#ym-floor-filter) below. |

## YM floor filter

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the yield management floor rule.<br><br>**Tip:** You can use the ID to get more information on the YM floor rule settings using the [Yield Management Floor Service](yield-management-floor-service.md). |

## Examples

### View all yield management floor rules that apply to a specific publisher

```
$ curl -b cookies -c cookies "https://api.appnexus.com/ym-floor-filter?publisher_id=1"
  
{
  "response": {
    "status": "OK",
    "ym-floor-filter": [
      "1",
      "7"
    ],
  }
}
```

### View all yield management floor rules that apply to a specific buyer

```
$ curl -b cookies -c cookies "https://api.appnexus.com/ym-floor-filter?buyer_member_id=7"
  
{
  "response": {
    "status": "OK",
    "ym-floor-filter": [
      "1",
      "12"
    ],
  }
}
```

### View all yield management floor rules that apply to any of a series of buyers

```
$ curl -b cookies -c cookies "http://sand.api.appnexus.com/ym-floor-filter?buyer_member_id=35,39,183"
  
{
  "response": {
    "status": "OK",
    "ym-floor-filter": [
      "35075",
      "35074",
      "35306",
      "35069",
      "35112",
      "35067",
      "35217",
      "36605",
      "35207",
      "36558",
      "36634",
      "35216",
      "36604",
      "35206",
      "36557",
      "36619",
      "34369",
      "33928",
      "33925",
      "33922",
      "34329",
      "172",
      "172",
      "172",
      "35089",
      "35089",
      "35089",
      "36610",
      "36609",
      "36610",
      "36609",
      "35232",
      "35232",
      "35422",
      "33920",
      "200",
      "200",
      "200",
      "218",
      "218",
      "218",
      "231",
      "231",
      "231",
      "34353",
      "33996",
      "34349",
      "33992",
      "34345",
      "33988",
      "34349",
      "34345",
      "34341",
      "34337",
      "34361",
      "34357",
      "34321"
    ],
    "count": 57,
    "start_element": 0,
    "num_elements": 57,
  }
  }
```
