---
title: Primary Ad Server Service
description: Explore the Primary Ad Server service, which enables the creation, updating, and deletion of primary ad servers.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Primary Ad Server service

The Primary Ad Server Service returns all the primary ad servers for the caller's member. It enables the creation, updating and deleting of primary ad servers.

The primary ad server makes the ultimate decision of what ads will be shown on the publishers inventory. In the context of PSP, demand partners, usually supply-side platforms (SSPs) like, create adapters for Prebid Server that receive and interpret header bidding ad requests. Demand partners hold an auction among their demand sources (usually demand-side-platforms (DSPs)) to collect bids on those ad requests and send the bids back to PSP, which holds another auction. Monetize holds another auction across its demand sources, including PSP demand partner(s)'s bid(s). If Microsoft Monetize is not the primary ad server, the results of that auction are passed to the primary (external) ad server.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/prebid/primary-adserver](https://api.appnexus.com/prebid/primary-adserver) | Get all the primary ad servers. |
| `POST` | [https://api.appnexus.com/prebid/primary-adserver](https://api.appnexus.com/prebid/primary-adserver) | Create a new primary ad server. |
| `PUT` | [https://api.appnexus.com/prebid/primary-adserver/{id}](https://api.appnexus.com/prebid/primary-adserver/{id}) | Update an existing primary ad server. |
| `DELETE` | [https://api.appnexus.com/prebid/primary-adserver/{id}](https://api.appnexus.com/prebid/primary-adserver/{id}) | Delete an existing primary ad server. |

## `GET`

Returns the primary ad servers.

Example call using cURL:

```
curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/primary-adserver
```

### Response

A successful response will returns a JSON array of ad server objects.

| Property | Type | Description |
|:---|:---|:---|
| `id` | integer | A unique identifier for the ad server object. |
| `name` | string | The name of the ad server. |

### Response example

```
[
   {
      "id":1,
      "name":"freewheel"
   },
   {
      "id":2,
      "name":"google ad manager"
   }
]            
            
```

## `POST`

Enables creation of a new ad server.

Example call using cURL:

```
curl -d @adserver.json -X POST --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver'
```

### Parameters

| Name | Type | Scope | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the configuration. |

JSON file example:

```
{
   "name":"adserver-example-name"
}            
            
```

### `POST`: Response

On success, the created ad server object will be returned.

## `PUT`

Enables updating of an existing ad server object. Append the ad server id as the last path component of the URL.

Example call using cURL:

```
curl -d @adserver-update.json -X PUT --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver/{id}'
```

### `PUT`: Parameters

| Name | Type | Scope | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the ad server. |

JSON file example:

```
{
   "name":"adserver-example-new-name"
}            
            
```

### `PUT`: Response

On successful response, the updated ad server object will be returned.

## `DELETE`

Enables deletion of all or an existing ad server object. Append the ad server ID as the last path component of the URL.

Example call using cURL to delete all ad server objects:

```
curl  -X DELETE --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver'
```

Example call using cURL to delete an existing ad server object:

```
curl  -X DELETE --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver/{id}'
```

### `DELETE`: Response

A successful deletion notification object.
