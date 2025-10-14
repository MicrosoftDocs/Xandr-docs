---
title: Order Line Service
description: In this article, understand what order line service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Order line service

## Overview

The Yield Analytics API and services are exposed via a REST based interface. It is intended to make development of custom functionality comfortable to developers experienced with Web 2.0, AJAX, REST, and service oriented development platforms. Developers should have familiarity with web-based application paradigms including AJAX, XML, JSON, and the HTTP(S) protocol prior to attempting development with the Yield Analytics API and services.

The Order Service currently exposes interfaces related to:

- Delivery, Capacity, and Contention of Line Items

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

### Delete order lines by external IDs

```
DELETE /api/v1/rest/orderLine/delete/{sourceSystem}/{externalOrderLineIds}
```

- **Description**

  Delete (Cancel) orderLine in by source system and comma separated external orderLine IDs.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | sourceSystem | sourceSystem | true | string |
  | PathParameter | externalOrderLineIds | externalOrderLineIds | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [StringResponse](#stringresponse) |

- **Consumes**

  - application/xml
  - application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  OrderLine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/orderLine/delete/XFP/1,2' -i -X 
  DELETE -H 'Content-Type: application/json;charset=UTF-8'
  ```

- **Example HTTP request**

  ```
  DELETE /api/v1/rest/orderLine/delete/XFP/1,2 HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 35

  {
    "result" : "Deleted/Canceled"
  }
  ```

### Get order line inventory and contention by external ID batch

```
POST /api/v1/rest/orderLine/inventoryandcontention/batch/{aliasFunctions}/{consumptionFilter}
```

- **Description**

  Utilize batch processes to retrieve inventory and contention for an order line by referencing the order line’s External ID.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | batchOrderLineContentionQuery | batchOrderLineContentionQuery | false | [BatchOrderLineContentionQuery](#batchorderlinecontentionquery) |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | Object |

- **Consumes**

  - application/xml
  - application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  OrderLine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/orderLine/inventoryandcontention/batch/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED' -i -X POST -H 
  'Content-Type: application/json;charset=UTF-8' -d '{
    "batchOrderLineContentionQuery" : {
      "queryCriteria" : [ {
        "orderLineId" : "16471611",
        "startDate" : "2017-07-01",
        "endDate" : "2017-07-30"
      }, {
        "orderLineId" : "16471610",
        "startDate" : "2017-07-01",
        "endDate" : "2017-07-30"
      } ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/orderLine/inventoryandcontention/batch/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 286

  {
    "batchOrderLineContentionQuery" : {
      "queryCriteria" : [ {
        "orderLineId" : "16471611",
        "startDate" : "2017-07-01",
        "endDate" : "2017-07-30"
      }, {
        "orderLineId" : "16471610",
        "startDate" : "2017-07-01",
        "endDate" : "2017-07-30"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1652

  {
    "inventoryAndContentionBatchResponse" : {
      "batchResults" : [ {
        "identifier" : "sample identifier",
        "result" : {
          "productDetail" : {
            "active" : true,
            "reporting" : true,
            "sold" : false,
            "productExpression" : "size in ('300x250') and state in ('co')",
            "safeProductExpression" : "size in ('300x250') and state in ('co')",
            "productName" : "API Example Product Name",
            "productClass" : "REPORTING",
            "isReporting" : true,
            "isSold" : false,
            "rateCardCPM" : 0.0,
            "rateCardFloor" : 1.1,
            "exists" : true,
            "isActive" : true,
            "productId" : 12345,
            "externalId" : "54321",
            "state" : "ACTIVE",
            "resolved" : false,
            "targetExists" : false,
            "priority" : 8,
            "rateCardProductId" : 1,
            "baseRateCardPrice" : 12.0
          },
          "summaryData" : {
            "startDate" : "2020-03-19",
            "endDate" : "2020-06-19",
            "capacity" : 100,
            "available" : 100,
            "unmetDemand" : 100,
            "consumptionDetails" : [ {
              "detailName" : "sample name",
              "consumedImpressions" : 1
            } ],
            "exceededForecastWindow" : true,
            "evenAvailability" : false,
            "daysInForecast" : 0,
            "daysOutsideAvailabilityThreshold" : 0
          },
          "contendingData" : {
            "row" : [ {
              "columnData" : [ {
                "name" : "sample name",
                "value" : "sample value"
              } ]
            } ]
          }
        }
      } ]
    }
  }
  ```

### Retrieve inventory details for an order line by external order line ID

```
GET /api/v1/rest/orderLine/inventoryandcontention/{externalOrderLineId}/{startDate}/{endDate}
```

- **Description**

  Retrieve inventory details for an order line by external order line ID.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | externalOrderLineId | externalOrderLineId | true | string |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | Object |

- **Consumes**

  application/json

- **Produces**

  /

- **Tags**

  OrderLine Resource

### Retrieve inventory details for an order line by external order line ID with Alias Functions and Consumption Filters

```
GET /api/v1/rest/orderLine/inventoryandcontention/{externalOrderLineId}/{startDate}/{endDate}/{aliasFunctions}/{consumptionFilter}
```

- **Description**

  Retrieve inventory details for an order line by external order line ID with Alias Functions and Consumption Filters.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | externalOrderLineId | externalOrderLineId | true | string |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  | HeaderParameter | source | Your client source for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | Object |

- **Consumes**

  application/json

- **Produces**

  /

- **Tags**

  OrderLine Resource

## Definitions

### BatchOrderLineContentionQuery

| Name | Description | Required | Schema |
|---|---|---|---|
| batchOrderLineContentionQuery |  | false | [BatchOrderLineContentionQuery](#batchorderlinecontentionquery) |
| queryCriteria | A collection of order line contention query criteria | true | [OrderLineContentionQuery](#orderlinecontentionquery) array |

### ColumnData

A JSON object to hold the results of a column data.

| Name | Description | Required | Schema |
|---|---|---|---|
| name | The name of the column data | true | string |
| value | The value object of the column data | true | string |

### ConsumptionDetail

A JSON object to hold the results of a consumption detail.

| Name | Description | Required | Schema |
|---|---|---|---|
| consumedImpressions | The field contains consumed impressions | true | integer (int64) |
| detailName | The name of consumption detail | true | string |

### InventoryAndContention

A JSON object to hold the results of an inventory and contention.

| Name | Description | Required | Schema |
|---|---|---|---|
| contendingData | The contending query result data of the inventory and contention | true | [QueryResultData](#queryresultdata) |
| productDetail | The product detail of the inventory and contention | true | [ProductDetail](#productdetail) |
| summaryData | The inventory summary data of the inventory and contention | true | [InventoryData](#inventorydata) |

### InventoryAndContentionBatchResponse

A JSON object to hold the results of an inventory and contention batch response.

| Name | Description | Required | Schema |
|---|---|---|---|
| batchResults | A collection of inventory and contention batch results | true | [InventoryAndContentionBatchResult](#inventoryandcontentionbatchresult) array |

### InventoryAndContentionBatchResult

A JSON object to hold the results of an inventory and contention batch result.

| Name | Description | Required | Schema |
|---|---|---|---|
| identifier | The identifier of the inventory and contention batch result | true | string |
| result | The result of the inventory and contention batch result | true | [InventoryAndContention](#inventoryandcontention) |

### InventoryData

A JSON object to hold the results of an inventory data.

| Name | Description | Required | Schema |
|---|---|---|---|
| available | The field contains available | true | integer (int64) |
| capacity | The field contains capacity | true | integer (int64) |
| consumptionDetails | A collection of consumption details | false | [ConsumptionDetail](#consumptiondetail) array |
| daysInForecast | The days in forecast of the inventory data | true | integer (int32) |
| daysOutsideAvailabilityThreshold | The days outside availability threshold of the inventory data | true | integer (int32) |
| endDate | The end date of inventory data | true | string |
| evenAvailability | The even availability of the inventory data | true | boolean |
| exceededForecastWindow | The field indicates whether or not the inventory data exceeded forecast window | true | boolean |
| startDate | The start date of inventory data | true | string |
| unmetDemand | The field contains unmet demand | true | integer (int64) |

### OrderLineContentionQuery

A JSON object to hold the results of an order import response.

| Name | Description | Required | Schema |
|---|---|---|---|
| endDate | The end date of the order line contention query | true | string |
| orderLineId | The order line id of the order line contention query | true | string |
| startDate | The start date of the order line contention query | true | string |

### ProductDetail

A JSON object to hold the results of a product search.

| Name | Description | Required | Schema |
|---|---|---|---|
| active |  | false | boolean |
| baseRateCardPrice | The base rate card price of the product detail | false | number (double) |
| exists | The exists boolean field of the product detail | true | boolean |
| externalId | The external product ID of the product detail | false | string |
| isActive | The is active boolean field of the product detail | true | boolean |
| isReporting | The is reporting boolean field of the product detail | true | boolean |
| isSold | The is sold boolean field of the product detail | true | boolean |
| priority | The priority of the product detail | false | integer (int32) |
| productClass | The product class of the product detail | true | string |
| productExpression | The product expression of the product detail | true | string |
| productId | The product ID of the product detail | false | integer (int64) |
| productName | The product name of the product detail | true | string |
| rateCardCPM | The rate card cpm of the product detail | true | number (double) |
| rateCardFloor | The rate card floor of the product detail | true | number (double) |
| rateCardProductId | The rate card product id of the product detail | false | integer (int64) |
| reporting |  | false | boolean |
| resolved | The resolved boolean field of the product detail | true | boolean |
| safeProductExpression | The safe product expression of the product detail | true | string |
| sold |  | false | boolean |
| state | The state of the product detail | true | string |
| targetExists | The target exists boolean field of the product detail | true | boolean |

### QueryResultData

A JSON object to hold the results of a query result data.

| Name | Description | Required | Schema |
|---|---|---|---|
| row | A collection of row data | false | [RowData](#rowdata) array |

### RowData

A JSON object to hold the results of a row data.

| Name | Description | Required | Schema |
|---|---|---|---|
| columnData | A collection of column data | true | [ColumnData](#columndata) array |

### StringResponse

A JSON object to hold the string results of api queries.

| Name | Description | Required | Schema |
|---|---|---|---|
| result | Operation result | true | string |

## Related topic

[Yield Analytics API](yield-analytics-api.md)
