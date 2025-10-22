---
title: Ad Server Category Mapping Service
description: Learn about Ad Server Category Mapping service. It returns all or a specific ad server category mapping.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Ad Server Category Mapping service

The Ad Server Category Mapping Service returns all or a specific ad server category mapping. It enables creation, update and deletion of ad server category mappings. These map Monetize content categories to [IAB subcategory codes](https://www.iab.com/guidelines/iab-quality-assurance-guidelines-qag-taxonomy/) for the ad server category mapping. The IAB subcategory code is part of the [IAB Content Taxonomy](https://www.iab.com/guidelines/content-taxonomy/) that helps buyers understand seller inventory, and in turn, helps sellers better monetize their supply.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/prebid/adserver-category-mapping` | Get all ad server category mappings. |
| `POST` | `https://api.appnexus.com/prebid/adserver-category-mapping` | Create a new ad server category mapping. |
| `PUT` | `https://api.appnexus.com/prebid/adserver-category-mapping/{id}` | Update an existing ad server category mapping. |
| `DELETE` | `https://api.appnexus.com/prebid/adserver-category-mapping/{id}` | Delete an existing ad server category mapping. |

## `GET`

Returns all ad server category mappings. To return a specific ad server category mapping, append the ad server category mapping's ID as the last path component of the URL.

### Example call using curl

```
curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/adserver-category-mapping
```

### Example call using curl to return a specific ad server category mapping

```
curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/adserver-category-mapping/{id}
```

### Response

A successful response will return a JSON object containing an array of ad server category mapping objects.

| Property | Type | Description |
|:---|:---|:---|
| `mappings` | array | An array of ad server category mapping objects. |
| `member_id` | integer | The unique identifier of the caller's member. |

#### Example response

```
{
  "mappings": [
    {
      "adserver_category_code": "financial",
      "iab_subcategory_code": "IAB13-4",
      "id": 8
    },
    {
      "adserver_category_code": "movies",
      "iab_subcategory_code": "IAB1-5",
      "id": 5
    },
    {
      "adserver_category_code": "pets",
      "iab_subcategory_code": "IAB16-5",
      "id": 7
    },
    {
      "adserver_category_code": "beauty",
      "iab_subcategory_code": "IAB18-1",
      "id": 3
    },
    {
      "adserver_category_code": "electronics",
      "iab_subcategory_code": "IAB19-8",
      "id": 6
    },
    {
      "adserver_category_code": "travel",
      "iab_subcategory_code": "IAB20-7",
      "id": 11
    },
    {
      "adserver_category_code": "auto",
      "iab_subcategory_code": "IAB2-3",
      "id": 9
    },
    {
      "adserver_category_code": "health",
      "iab_subcategory_code": "IAB7-32",
      "id": 12
    },
    {
      "adserver_category_code": "food",
      "iab_subcategory_code": "IAB8-7",
      "id": 10
    },
    {
      "adserver_category_code": "games",
      "iab_subcategory_code": "IAB9-5",
      "id": 4
    }
  ],
  "member_id": 9325
}
```

## `POST`

Enables creation of a new ad server category mapping object.

### Example call using curl

```
curl -d @adserver-category-mapping.json -X POST --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver-category-mapping'
```

### Parameters

| Name | Type | Scope | Description |
|:---|:---|:---|:---|
| `adserver_category_code` | string | Required | Which ad server category that will be associated with the ad server category mapping. |
| `iab_subcategory_code` | string | Required | The IAB subcategory code for the ad server category mapping. The [IAB subcategory code](https://www.iab.com/guidelines/content-taxonomy/) is part of the [IAB Content Taxonomy](https://www.iab.com/guidelines/content-taxonomy/) that helps buyers understand seller inventory, and in turn, helps sellers better monetize their supply. |

### Example JSON file

```
{
    "adserver_category_code":"bowling shoes"
    "iab_subcategory_code":"IAB9-11000"
}
```

### Response

On success, the created ad server category mapping object will be returned.

## `PUT`

Enables updating of an existing ad server category mapping object. Append the ad server category mapping ID as the last path component of the URL.

### Example call using curl

```
curl -d @adserver-category-mapping-update.json -X PUT --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver-category-mapping/{id}'
```

### Parameters

| Name | Type | Scope | Description |
|:---|:---|:---|:---|
| name | string | Required | The name of the ad server category mapping. |

### Example JSON file

```
{
    "name":"adserver-category-mapping-example-new-name"
}
```

### Response

On a successful response, the updated ad server category mapping object will be returned. Append the ad server category mapping ID as the last path component of the URL.

## `DELETE`

Enables the deletion of an existing ad server category mapping object.

### Example call using curl

```
curl  -X DELETE --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/adserver-category-mapping/{id}'
```

### Response

A successful deletion notification object.
