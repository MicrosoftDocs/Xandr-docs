---
title: Mediated Network Service
description: Use the Mediated Network service to create and maintain mediated networks.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Mediated Network service

> [!NOTE]
> Mediation is only available to Microsoft Monetize Ad Server customers.

Microsoft Monetize Ad Server mediation allows demand from sources not integrated into the Monetize exchange or [Prebid Server Premium](../monetize/prebid-server-premium.md) to compete for publisher inventory. This includes both well-known partners like Google and custom networks. To call each partner for demand, they must first be created as networks [via the Monetize UI](../monetize/mediation-networks.md) or the Mediated Network service outlined below. It is recommended to limit the number of networks in the waterfall to no more than 3 or 4 for each impression. Having more networks can lead to increased ad serving latency and negatively affect user experience. For additional information on mediation, see [Selling Your Inventory through Mediation](../monetize/mediation-selling-your-inventory-through-mediation.md).

Setup is also required in each Network’s platform, as outlined in [Integrating for Mediation](../monetize/mediation-integrating-for-mediation.md). In addition, [Monetize reports](../monetize/reporting-guide.md) include Mediated Networks as Advertisers and Bids as Line Items (both filters and dimensions).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/mediated-network` | View all mediated networks |
| `GET` | `https://api.appnexus.com/mediated-network?id=NETWORK_ID` | View a specific mediated network |
| `GET` | `https://api.appnexus.com/mediated-network/meta` | Retrieve available fields to filter and sort |
| `POST` | `https://api.appnexus.com/mediated-network` | Add a new mediated network |
| `PUT` | `https://api.appnexus.com/mediated-network?id=NETWORK_ID` | Modify a mediated network |
| `DELETE` | `https://api.appnexus.com/mediated-network?id=NETWORK_ID` | Delete a mediated network |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The system-generated unique ID for this network.<br><br>**Required On**: `PUT` |
| `name` | string | The name of the network, as supplied by the user.<br><br>**Required On**: `POST` |
| `advertiser_id` | int | **Read-only**. The unique, system-generated ID of the advertiser associated with this mediated network. |
| `member_id` | int | **Read-only**. Every Monetize advertiser object is associated with a parent [member](./member-service.md). The unique, system-generated ID of the member to which the advertiser and network described by `advertiser_id` belongs. |
| `active` | boolean | Controls whether bids in this network request demand from the partner.<br><br>**Default**: `false` |
| `creative_custom_request_partner_id` | int | The partner platform the network is associated with. See creative [custom request partner service](./creative-custom-request-partner-service.md) for more information.<br><br>**Required On**: `POST`|
| `default_bid_currency` | string | The currency to be used for bids from this network.<br><br>**Default**: `USD` |
| `last_modified` | date | **Read-only**. The date and time at which the mediated network object was last modified. |
| `network_type` | string | The type of mediated network. Allowed values:<br>- `mobile`: The network is focused on purchasing mobile inventory.<br> - `banner`: The network is focused on purchasing web inventory.<br><br>**Default**: `mobile` |

## Examples

### Add a mediated network

```
$ cat add-network
{
    "mediated-network": {
        "name": "JMS Test 2",
        "creative_custom_request_partner_id": 1
    }
} 

$ curl -b cookies -c cookies -X POST -d @add-network.json 'https://api.appnexus.com/mediated-network

{
    "response":{
        "status":"OK",
        "count":1,
        "id":371,
        "start_element":0,
        "num_elements":100,
        "mediated-network":{
            "id":371,
            "name":"JMS Test 2",
            "advertiser_id":110692,
            "member_id":4209,
            "active":true,
            "creative_custom_request_partner_id":1,
            "default_bid_currency": "USD",
            "last_modified":"2014-04-28 14:59:11",
            "bid_count":0,
            "network_type":"mobile"
        }
    }
}
```

### Update a mediated network

```
$ cat add-network

{
    "mediated-network": {
        "id": 368,
      "active": false   
    }
}

$ curl -b cookies -c cookies -X PUT -d @update-network.json 'https://sand.api.appnexus.com/mediated-network?member_id=4209' | json-pp

{
    "response":{
        "status":"OK",
        "count":1,
        "id":368,
        "start_element":0,
        "num_elements":100,
        "mediated-network":{
            "id":368,
            "name":"Integration Test TEST1398457680380",
            "advertiser_id":110648,
            "member_id":4209,
            "active":false,
            "creative_custom_request_partner_id":1,
            "default_bid_currency": "USD",
            "last_modified":"2014-04-28 14:56:48",
            "bid_count":0,
            "network_type":"mobile"
        }
    }
}
```

### View all mediated networks

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/mediated-network

{
    "response":{
        "status":"OK",
        "count":20,
        "start_element":0,
        "num_elements":100,
        "mediated-networks":[
            {
                "id":89,
                "name":"Doubleclick for Publishers",
                "advertiser_id":110021,
                "member_id":4209,
                "active":false,
                "creative_custom_request_partner_id":28,
                "default_bid_currency": "USD",
                "last_modified":"2014-04-18 23:37:01",
                "bid_count":0,
                "network_type":"mobile"
            },
            {
                "id":90,
                "name":"Tim's Custom Network",
                "advertiser_id":110022,
                "member_id":4209,
                "active":false,
                "creative_custom_request_partner_id":22,
                "default_bid_currency": "EUR",
                "last_modified":"2014-04-18 23:37:01",
                "bid_count":0,
                "network_type":"mobile"
            },
            {
                "id":210,
                "name":"Amazon",
                "advertiser_id":110203,
                "member_id":4209,
                "active":false,
                "creative_custom_request_partner_id":25,
                "default_bid_currency": "EUR",
                "last_modified":"2014-04-18 23:32:36",
                "bid_count":1,
                "network_type":"mobile"
            }
      ]
  }
}
```

### View a specific mediated network

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/mediated-network?id=368' | json-pp

{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "mediated-network":{
            "id":368,
            "name":"Integration Test TEST1398457680380",
            "advertiser_id":110648,
            "member_id":4209,
            "active":true,
            "creative_custom_request_partner_id":1,
            "default_bid_currency": "USD",
            "last_modified":"2014-04-25 20:28:07",
            "bid_count":0,
            "network_type":"mobile"
        }
    }
}
```

### Delete a mediated network

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/mediated-network?id=371

{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null
    }
}
```

## Related topics

- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
- [Mediated Bid Service](./mediated-bid-service.md)
