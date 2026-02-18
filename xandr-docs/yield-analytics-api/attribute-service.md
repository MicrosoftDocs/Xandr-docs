---
title: Attribute Service
description: In this article, understand what attribute service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Attribute service

## Overview

The Yield Analytics API and services are exposed via a REST based interface. It is intended to make development of custom functionality comfortable to developers experienced with Web 2.0, AJAX, REST, and service oriented development platforms. Developers should have familiarity with web-based application paradigms including AJAX, XML, JSON, and the HTTP(S) protocol prior to attempting development with the Yield Analytics API and services.

The Attribute Service currently exposes interfaces related to:

- Attribute Translation creation
- Attribute Translation lookup

## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case by case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.

## Security

The service API exposes application data in a secure manner. Use of API functionality is restricted to authenticated users and is exposed over secure transport protocols. Access to the API must take place within the following context:

### Authentication
For more information on authentication, see [Yield Analytics API - Authentication Process](api-authentication.md).


## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## Host

```
https://api.appnexus.com/imf
```



## Paths

### Convert external IDs to Yield Analytics expression lexicon

```
POST /api/v1/rest/attributes/convert
```

- **Description**

  Pass in external ids for the attribute and attribute value(s) in order to convert to the Yield Analytics targeting lexicon.

- **Parameters**
  
  | Type | Name | Description | Required | Schema | Default |
  |---|---|---|---|---|---|
  | BodyParameter | attributeConverter | attributeConverter | true | [AttributeConverter](#attributeconverter) | NA |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string | NA |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string | NA |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [StringResponse](#stringresponse) |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Attribute Resource

- **Example cURL request**

  ```
  $ curl 'https://api.appnexus.com/imf/api/v1/rest/attributes/create' -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' -d '{
  "attributeTranslation" : {
  "inputAttribute" : "attribute1",
  "inputValue" : "value1",
  "targetAttribute" : "targetattribute1",
  "targetValue" : "targetValue1",
  "adServerType" : "XFP",
  "invincible" : false
  }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/attributes/create HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://api.appnexus.com/imf
  Content-Length: 235
          
  {
  "attributeTranslation" : {
  "inputAttribute" : "attribute1",
  "inputValue" : "value1",
  "targetAttribute" : "targetattribute1",
  "targetValue" : "targetValue1",
  "adServerType" : "XFP",
  "invincible" : false
  }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 26
  
  {
  "result" : "Created"
  }
  ```

### Create new attribute translation

```
POST /api/v1/rest/attributes/create
```

- **Description**

  This accepts only a JSON formatted file, parses it, and creates a new attribute in the Yield Analytics database.

- **Parameters**
  
  | Type | Name | Description | Required | Schema | Default |
  |---|---|---|---|---|---|
  | BodyParameter | attributeTranslation | attributeTranslation | true | [AttributeTranslation](#attributetranslation) | NA |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string | NA |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string | NA |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [StringResponse](#stringresponse) |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Attribute Resource

- **Example cURL request**

  ```
  $ curl 'https://api.appnexus.com/imf/api/v1/rest/attributes/create' -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' -d '{
  "attributeTranslation" : {
  "inputAttribute" : "attribute1",
  "inputValue" : "value1",
  "targetAttribute" : "targetattribute1",
  "targetValue" : "targetValue1",
  "adServerType" : "XFP",
  "invincible" : false
  }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/attributes/create HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://api.appnexus.com/imf
  Content-Length: 235

  {
  "attributeTranslation" : {
  "inputAttribute" : "attribute1",
  "inputValue" : "value1",
  "targetAttribute" : "targetattribute1",
  "targetValue" : "targetValue1",
  "adServerType" : "XFP",
  "invincible" : false
  }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 26
          
  {
  "result" : "Created"
  }
        
  ```

## Definitions

### AttributeConverter

| Name | Description | Required | Schema |
|---|---|---|---|
| attributeConverter |  | false | AttributeConverter |
| attributeName | The attribute name | true | string |
| dfpTargetingIds | Comma separated DFP ids to be translated. | true | string |
| operator | The operator either Inclusion or Exclusion. | true | string |

### AttributeTranslation

| Name | Description | Required | Schema |
|---|---|---|---|
| adServerType | The adServer type of the attribute translation | true | string |
| attributeTranslation |  |  | AttributeTranslation |
| inputAttribute | The input attribute of the attribute translation | true | string |
| inputValue | The input value of the attribute translation | true | string |
| invincible | The invincible field of the attribute translation | true | boolean |
| targetAttribute | The target attribute of the attribute translation | true | string |
| targetValue | The target value of the attribute translation | true | string |

### StringResponse

A JSON object to hold the string results of api queries.

| Name | Description | Required | Schema |
|---|---|---|---|
| result | Operation result. | true | string |

## Related topic

[Yield Analytics API](yield-analytics-api.md)
