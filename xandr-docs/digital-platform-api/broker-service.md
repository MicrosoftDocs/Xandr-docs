---
title: Broker Service
description: In this article, find information about the Broker Service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Broker service

> [!IMPORTANT]
> The Broker service has been replaced by the [Partner Fee Service](partner-fee-service.md) for augmented line items (ALIs).
>
> The Broker Service can only be used with standard or legacy line items. Broker fees do not apply to augmented line items.

The Broker Service allows users of standard or legacy line items to define brokers. Brokers collect fees from networks when serving an impression. The actual fees are defined through the [Campaign Service](campaign-service.md), the [Line Item Service](line-item-service.md), or the [Insertion Order Service](insertion-order-service.md).

> [!CAUTION]
> If a broker fee is applied to an insertion order, the fee will not apply to any augmented line items associated with the insertion order. It will apply only to the insertion order's standard line items.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| POST | `https://api.appnexus.com/broker` <br> (add-broker JSON) | Add a broker. |
| PUT | `https://api.appnexus.com/modify-broker?id=BROKER_ID` <br> (modify-broker JSON) | Modify a broker. |
| GET | `https://api.appnexus.com/broker` | View all brokers. |
| GET | `https://api.appnexus.com/broker?id=BROKER_ID` | View a specific broker. |

## JSON fields

| Parameter | Type | Description |
|---|---|---|
| `broker_fees` | array of objects | An array of broker fees associated with the broker. Refer to the [Broker Fees](#broker-fees-applied-to-other-objects) section. <br> **Default**: `null` |
| `id` | int | The unique identifier for a broker. <br> **Default**: Auto-incremented Number (i.e., 123) <br> **Required On**: `PUT` |
| `last_modified` | timestamp | **Read-Only**. Time of last modification to this broker in the format **YYYY-MM-DD HH:MM:SS**. |
| `member_id` | int | The unique identification number of the broker's member. When creating a broker, the member of the user is assigned. |
| `name` | string | The unique name used to describe a broker. <br> **Required On**: `POST` |
| `state` | string | The state of the broker. Possible values: `active` or `inactive`. <br> **Default**: active |

## Broker fees applied to other objects

Broker fees are created through the [Campaign Service](campaign-service.md), the [Line Item Service](line-item-service.md), or the [Insertion Order Service](insertion-order-service.md). They can be viewed here but cannot be created or edited through this service. Refer to the Broker Fees section in each of the above-referenced services for details on how to apply fees to brokers.

> [!CAUTION]
> If a broker fee is applied to an insertion order, the fee will not apply to any augmented line items associated with the insertion order. It will apply only to the insertion order's standard line items.

Each object in the `broker_fees` array contains the following fields:

| Field | Type | Description |
|---|---|---|
| `object_type` | string | Indicates whether this fee is associated to one campaign or a group of campaigns. Possible values: `campaign` or `campaign-group`. <br> **Read-Only**. |
| `object_id` | int | The unique identification number of the fee. <br> **Read-Only**. |
| `description` | string | Text that provides information about the fee. <br> **Read-Only**. |
| `fee_type` | string | The Possible values: `commission` or `serving`: <br> - Commission - These are Line Item or Insertion Order broker fees and are deducted from the booked revenue given from the advertiser to the network. Commission is always in the currency of the associated Insertion Order, Line Item or Campaign. <br> - Serving - These are Campaign broker fees and are in addition to the inventory cost that the network paid the publisher. Serving fees are in US Dollars. <br><br> **Read-Only**. |
| `payment_type` | string | Payment type: `cpm` or `revshare`. <br> **Read-Only**. |
| `value` | double | The value of the fee. <br> **Read-Only**. |

## Examples

### Add a broker

```
$ cat add-broker.json

{
    "broker":
    {
    "name": "JMS3"
    }
}

$ curl -b cookies -c cookies -X POST -d @add-broker.json 'https://api.appnexus.com/broker'

    "response":{
        "status":"OK",
        "count":1,
        "id":287,
        "start_element":0,
        "num_elements":100,
        "broker":{
            "id":287,
            "name":"JMS3",
            "state":"active",
            "member_id":1066,
            "last_modified":"2013-09-26 17:17:38",
            "broker_fees":null
```

### Modify a broker

```
$ cat modify-broker.json

{
    "broker":
    {
    "state": "inactive"
    }
}

$ curl -b cookies -c cookies -X PUT -d @modify-broker.json 'https://api.appnexus.com/broker?id=81'

    "response":{
        "status":"OK",
        "count":1,
        "id":"81",
        "start_element":0,
        "num_elements":100,
        "broker":{
            "id":81,
            "name":"Test",
            "state":"inactive",
            "member_id":1066,
            "last_modified":"2013-09-26 17:21:42",
            "broker_fees":null
        },
}
```

### View all brokers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/broker'

{
    "response":{
        "status":"OK",
        "count":6,
        "start_element":0,
        "num_elements":100,
        "brokers":[
            {
                "id":81,
                "name":"Test",
                "state":"inactive",
                "member_id":1066,
                "last_modified":"2013-09-26 17:21:42",
                "broker_fees":null
            },
            {
                "id":145,
                "name":"Test 2",
                "state":"active",
                "member_id":1066,
                "last_modified":"2013-03-15 20:41:47",
                "broker_fees":null
            },
            {
                "id":152,
                "name":"Test 3",
                "state":"active",
                "member_id":1066,
                "last_modified":"2013-03-20 15:30:21",
                "broker_fees":null
            },
            {
                "id":217,
                "name":"Third party",
                "state":"active",
                "member_id":1066,
                "last_modified":"2013-05-21 03:58:36",
                "broker_fees":null
            },
            {
                "id":218,
                "name":"Third party",
                "state":"active",
                "member_id":1066,
                "last_modified":"2013-05-21 04:12:58",
                "broker_fees":null
            },
            {
                "id":287,
                "name":"JMS3",
                "state":"active",
                "member_id":1066,
                "last_modified":"2013-09-26 17:17:38",
                "broker_fees":null
            }
        ],
}
```

### View a specific broker

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/broker?id=81'

{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,        "num_elements":100,
        "broker":{
            "id":81,
            "name":"Test",
            "state":"inactive",
            "member_id":1066,
            "last_modified":"2013-09-26 17:21:42",
            "broker_fees":null
        },
}
```
