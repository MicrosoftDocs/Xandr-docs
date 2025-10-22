---
title: Privacy Service
description: Explore the Privacy Service, which enables customers to create personalized consumer privacy experiences and respond to data subject access requests.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Privacy service

The Xandr Privacy Service permits Xandr clients to delete and access personal data (personal information) to support complying with privacy regulations related to the provision and deletion of personal information such as the GDPR or CCPA. This enables Xandr customers to build custom consumer privacy experiences and reply to data subject access requests.

There are two capabilities exposed by this API: Access and Delete. In both cases, only data that is related to your account for the given user is impacted. Deletion means the given ID will be disassociated from your segments; it does not imply forward-looking suppression.

> [!NOTE]
> This service is only available to `member` users. For more information about user types, see the [User Service](user-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/privacy/consumer-request](https://api.appnexus.com/privacy/consumer-request) | Create a new `"delete"` or `"access"` request. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `identifier` | string | The identifier for the end user.<br>For example, `"123e4567-e89b-12d3-a456-426655440000"` or `"7738918429796999062"`.<br>**Required On:** `POST` |
| `identifier_type` | string enum | The identifier type for the end user. May be either the Mobile Advertising ID or the Xandr user ID for the user.<br>**Required On:** `POST`<br>**Accepted values:** `"maid"` or `"uuid2"`. |
| `request_type` | string | The type of privacy request. Currently, Xandr only supports `"delete"` and `"access"` requests.<br>**Required On:** `POST` |

## Examples

> [!NOTE]
> A 200 status code response indicates success. A 422 status code response indicates a problem with the input.

### Create a `"delete"` request using a Xandr UUID

```
$ cat privacy.json
{
  "identifier": "7738918429796999062", 
  "identifier_type": "uuid2", 
  "request_type":"delete"
}
$ curl -X POST -d @privacy.json 'https://api.appnexus.com/privacy/consumer-request'
```

### Create a `"delete"` request using an external Mobile Advertising ID

```
$ cat privacy.json
{
   "identifier": "123e4567-e89b-12d3-a456-426655440000", 
   "identifier_type": "maid", 
   "request_type":"delete"
}
$ curl -X POST -d @privacy.json 'https://api.appnexus.com/privacy/consumer-request'
```

### Create an `"access"` request using a Xandr UUID

```
$ cat privacy.json
{
  "identifier": "7738918429796999062", 
  "identifier_type": "uuid2", 
  "request_type":"access"
}
$ curl -X POST -d @privacy.json 'https://api.appnexus.com/privacy/consumer-request'
{
  "response": {
    "status": "OK",
    "segments": [
      {
        "id": 789,
        "name": "Customer Segment 1"
      },
      {
        "id": 1234567,
        "name": "customer_segment_2"
      }
    ]
  }
} 
```

### Create an `"access"` request using an external Mobile Advertising ID

```
$ cat privacy.json
{
   "identifier": "123e4567-e89b-12d3-a456-426655440000", 
   "identifier_type": "maid", 
   "request_type":"access"
}
$ curl -X POST -d @privacy.json 'https://api.appnexus.com/privacy/consumer-request'
{
  "response": {
    "status": "OK",
    "segments": [
      {
        "id": 123,
        "name": "Customer Segment 1"
      },
      {
        "id": 456,
        "name": "customer_segment_2"
      }
    ]
  }
}  
```

## Related topics

- [CCPA Client Overview (Part of Privacy Policies)](../policies-regulations/index.yml)
- [CCPA Publisher Controls Provided by Xandr (Part of Privacy Policies)](../policies-regulations/index.yml)
