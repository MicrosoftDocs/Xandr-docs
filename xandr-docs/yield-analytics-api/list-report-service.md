---
title: Reporting Service - List Reports 
description: In this article, understand what reporting service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 02/26/2026
---

# Reporting service - List reports 

## Overview
The List report endpoint helps you retrive all Yield Analytics saved reports, including each report’s ID, name, description, and report definition. 

## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case by case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.

## Security

The service API exposes application data in a secure manner. Use of API functionality is restricted to authenticated users and is exposed over secure transport protocols. Access to the API must take place within the following context:

## Authentication
For more information on authentication, see [Yield Analytics API - Authentication Process](api-authentication.md)


## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## Host

```
https://api.appnexus.com/imf/
```

## Endpoint    

```
GET /api/v1/rest/reporting/reports 
```

- **Parameters**
  | HTTP method | Endpoint | Description | 
  |---|---|---|
  | GET | `https://api.appnexus.com/imf/api/v1/rest/reporting/reports` | Retrieves all Yield Analytics saved reports, including report ID, name, description, and report definition. |


- **Example cURL request**

  ```
  $ curl --request GET \
    --url https://api.appnexus.com/imf/api/v1/rest/reporting/reports \
    --header 'Authorization: {{auth-token}}' \
    --header 'content-type: application/json'
  ```

- **Example HTTP request**

  ```
  GET /imf/api/v1/rest/reporting/reports HTTP/1.1
  Content-Type: application/json
  Authorization: {{auth-token}}
  Host: api.appnexus.com
  ```

- **Example HTTP response**

  ```
  [
    {
      "reportId": 316,
      "reportName": "Sample Capacity Trend - Actuals",
      "description": "",
      "reportDefinition": "{\"report\":{\"selectedTab\":\"tab1\",\"view\":\"TABLE_VIEW\"}}"
    },
    {
      "reportId": 317,
      "reportName": "Sample Delivery Summary",
      "description": "Example report for documentation",
      "reportDefinition": "{\"report\":{\"selectedTab\":\"tab1\",\"view\":\"TABLE_VIEW\"}}"
    }
  ]
  ```



## Related topic

See [Query Engine Service](query-engine-service.md) to execute a saved report via the API using report ID. 
