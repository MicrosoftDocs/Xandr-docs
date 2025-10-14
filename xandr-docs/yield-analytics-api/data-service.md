---
title: Data Service
description: In this article, understand what data service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Data service

## Overview

The Yield Analytics Data API exposes functionality for searching of available data and configs from within the Yield Analytics environment.

## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case by case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.

## Security

The service API exposes application data in a secure manner. Use of API functionality is restricted to authenticated users and is exposed over secure transport protocols. Access to the API must take place within the following context:

- **Example cURL authentication**

  Authentication occurs by passing credentials via http headers on each request.

  ```
  - username: curl -H "username:username"
  - password: curl -H "password:password"
  - source: curl -H "source:client_id"
          
  ```

- **Example HTTPS authentication**

  ```
  GET /api/v1/rest/
  HTTPS/1.1
  Host: yieldanalytics.xandr.com
  Accept: application/xml, application/json
  Content-Type: application/json
  username: {{username}}
  password: {{password}}
  source: {{client_id}}        
  ```

- **Example POSTMAN authentication**

  Find an example of header settings in Postman below:

    > [!NOTE]
    >
    > - 'Authorization' is set to "No Auth"; the settings below are to be placed in the 'Headers' tab.
    > - For a more in depth tutorial of using Postman, see [Using Postman with the Yield Analytics API](using-postman-with-the-yield-analytics-api.md).

  :::image type="content" source="media/postman-header-variables.png" alt-text="A screenshot of the Headers tab with standard keys and values in Postman.":::

## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## Paths

### Get alias columns

```
GET /api/v1/rest/data/aliasColumns
```

- **Description**

  Get request to read a collection of alias columns.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [AliasColumns](#aliascolumns) |

- **Consumes**

  application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  Data Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/data/aliasColumns' -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 
  'username: {{username}}' -H 'password: {{password}}' -H 'source: {{source}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/data/aliasColumns HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  source: {{source}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 187

  {
    "aliasColumns" : [ {
      "aliasKey" : "TARGET_OVERLAPPING_PRODUCT",
      "dateSourceType" : "TARGET"
    }, {
      "aliasKey" : "BOOKED_VALUE",
      "dateSourceType" : "ORDER_LINE"
    } ]
  }
  ```

### Get alias functions

```
GET /api/v1/rest/data/aliasFunctions
```

- **Description**

  Get request to read a collection of alias functions.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [AliasFunctions](#aliasfunctions) |

- **Consumes**

  application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  Data Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/data/aliasColumns' -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 
  'username: {{username}}' -H 'password: {{password}}' -H 'source: {{source}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/data/aliasColumns HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  source: {{source}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 187

  {
    "aliasColumns" : [ {
      "aliasKey" : "TARGET_OVERLAPPING_PRODUCT",
      "dateSourceType" : "TARGET"
    }, {
      "aliasKey" : "BOOKED_VALUE",
      "dateSourceType" : "ORDER_LINE"
    } ]
  }
  ```

### Get consumption filters

```
GET /api/v1/rest/data/consumptionFilters
```

- **Description**

  Get request to read a collection of consumption filters.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [ConsumptionFilters](#consumptionfilters) |

- **Consumes**

  application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  Data Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/data/consumptionFilters' -i -H 'Content-Type: application/json' -H 
  'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' -H 'source: {{source}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/data/consumptionFilters HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  source: {{source}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 82

  {
    "consumptionFilters" : [ "CONSUMPTION_TYPE", "INVENTORY_CLASS", "PRIORITY" ]
  }
  ```

## Definitions

### AliasColumn

A JSON object to hold the request for AliasColumn.

| Name | Required | Schema |
|---|---|---|
| aliasKey | false | string |
| dateSourceType | false | string |

### AliasColumns

A JSON object to hold the request for AliasColumns.

| Name | Required | Schema |
|---|---|---|
| aliasColumns | false | [AliasColumn](#aliascolumn) array |

### AliasFunction

A JSON object to hold the request for AliasFunction.

| Name | Required | Schema |
|---|---|---|
| inputs | false | string array |
| name | false | string |

### AliasFunctions

A JSON object to hold the request for AliasFunctions.

| Name | Required | Schema |
|---|---|---|
| aliasFunctions | false | [AliasFunction](#aliasfunction) array |

### ConsumptionFilters

A JSON object to hold the request for ConsumptionFilters.

| Name | Required | Schema |
|---|---|---|
| consumptionFilters | false | string array |

## Related topic

[Yield Analytics API](yield-analytics-api.md)
