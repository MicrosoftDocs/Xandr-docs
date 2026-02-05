---
title: Product and Inventory Service
description: In this article, understand what product and inventory service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Product and inventory service

## Overview

The Yield Analytics Product and Inventory API exposes functionality for discovery of products from within the Yield Analytics environment and retrieval of product inventory and consumption data. When interacting with product related API functionality developers should understand that products may be either static or dynamic. These two types of products differ in the following ways:

- Static products exist in the Yield Analytics system when they have been imported in relation to order lines flowing into the Yield Analytics system, or have been created as rate card/reporting products in the system. Static products are always accessible throughout the Yield Analytics user interface and may be configured with rate card information and other metadata. They are persistent and may be viewed throughout the Yield Analytics UI.

- Dynamic products are ad-hoc in nature. Ad-hoc products result from inventory queries and there is currently no exact match product for the targeting criteria in the Yield Analytics system. Dynamic products may not have rate cards configured, do not have names, are not persistent, and are not visible in the Yield Analytics UI (with the exception of Product Creation where non-persisted products may be viewed).

Yield Analytics REST API functionality treats these two classes of products symmetrically whenever possible. However, there are certain API calls which apply strictly to static products. These static-product-only API calls are limited to interfaces requiring the use of either a Yield Analytics internal product ID or external product ID where the mapping looking is by nature persistent. Discovery functionality works primarily against static products, inventory data retrieval functionality works regardless of whether a product is static or dynamic.

## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case by case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.

## Security

The service API exposes application data in a secure manner. Use of API functionality is restricted to authenticated users and is exposed over secure transport protocols. Access to the API must take place within the following context:

### Authentication
The service API exposes application data in a secure manner. Use of API functionality is restricted to authenticated users and is exposed over secure transport protocols. Access to the API must take place within the following context:
- Authentication is performed by passing credentials (username and password) in the HTTP headers with each request. A successful authentication returns a token that remains valid for two hours. We recommend using `-b cookies -c cookies` in the POST request to store the token as a cookie.
- The issued token can then be used to access all endpoints available under the host endpoint `api.appnexus.com/imf`.



- **cURL authentication**

> [!NOTE]
> The authentication username and password are the same credentials used for the Digital Platform API and/or Monetize.



  ```
  - username: curl -H "username:username"
  - password: curl -H "password:password"
          
  ```

- **HTTPS authentication**

  ```
  GET /api/v1/rest/
  HTTPS/1.1
  Host: api.appnexus.com/imf
  Accept: application/xml, application/json
  Content-Type: application/json
  username: {{username}}
  password: {{password}}      
  ```

- **HTTPS authentication response**

```
$ curl -b cookies -c cookies -X POST -d @auth 'https://api.appnexus.com/auth'  
{  
   "response": {  

          "status": "OK",  

          "token": "h20hbtptiv3vlp1rkm3ve1qig0",  

          "dbg_info": {  

                ...  

        }  
    } 
} 
```

> [!NOTE]
> - 'Authorization' is set to "No Auth"; the settings below are to be placed in the 'Headers' tab.


## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## Paths

### Bulk product creation

```
POST /api/v1/rest/product/bulk/create
```

- **Description**

  Uniqueness of records is defined by productId and externalId. If neither of those is present then the row will result in a NEW product
  record (possibly with a new [generated] product name).

  If productId is provided then it MUST correspond to a product id in our system; otherwise an error is returned.

  In this scenario we will UPDATE the designated product.

  > [!NOTE]
  > We do not check the externalId, we simply update this record. This means if an externalId was provided in the request but does not match the product found by this productId, we will update the externalId on this product with the new value provided. If externalId conflicts with a pre-existing externalId from another product, this update will fail and an error message will be generated.

  - If productId is NOT provided then we will check for externalId.
  - If externalId is provided and a product with that externalId exists in our system then that product will be UPDATED.
  - If externalId is provided and a product with that externalId does NOT exist in our system, the product will be CREATED.
  - If neither productId nor externalId is provided then we will create a new product.

  > [!NOTE]
  > Product Name is not required to be unique when creating or updating products, but a post-process will run that renames products which overlap. Any product name which conflicts with another product in the system is renamed to productName-{productId} (our internal product id); thereby creating a unique name for that product.

  For each uploaded set of products our system will generate a hash based on the contents of the file (and/or post-body) (using MD5 algorithm) and stored with the product data. This protects against duplicate uploads of the exact same data (or file). Duplicate posts will result in an error message that the request is a duplicate.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | bulkProductCreation | bulkProductCreation | true | [BulkProductCreation](#bulk-product-creation) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  
  application/json

- **Tags**
  
  Product Resource

- **Example cURL request**
  
  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/bulk/create' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' -d '{
    "bulkProductCreation" : {
      "products" : [ {
        "productName" : "Test Product",
        "state" : "ACTIVE",
        "externalId" : "1",
        "rateCardCPM" : 1.0,
        "productClass" : "RATE_CARD",
        "originatingTarget" : "TEST in ('TEST')"
      } ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/bulk/create HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 264

  {
    "bulkProductCreation" : {
      "products" : [ {
        "productName" : "Test Product",
        "state" : "ACTIVE",
        "externalId" : "1",
        "rateCardCPM" : 1.0,
        "productClass" : "RATE_CARD",
        "originatingTarget" : "TEST in ('TEST')"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 459

  {
    "bulkProductCreationResponse" : {
      "products" : [ {
        "productName" : "Failed Creation Test",
        "externalId" : null,
        "productId" : null,
        "status" : "FAILED",
        "errors" : [ {
          "field" : "Failed Field",
          "error" : "Failed Reason"
        } ]
      }, {
        "productName" : "Successful Creation Test",
        "externalId" : null,
        "productId" : null,
        "status" : "PENDING",
        "errors" : null
      } ]
    }
  }
  ```

### Bulk product creation by date

```
GET /api/v1/rest/product/bulk/create/{date}
```

- **Description**

  Send a GET request to obtain the status of products pending creation or having been created for a particular date. Date is required. If not specified we return the current set of PENDING products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | date | date | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  
  application/json

- **Tags**
  
  Product Resource

- **Example cURL request**
  
  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/bulk/create/2017-06-15' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}'
  ```

- **Example HTTP request**
  
  ```
  GET /api/v1/rest/product/bulk/create/2017-06-15 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**
  
  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 211

  {
    "bulkProductCreationResponse" : {
      "products" : [ {
        "productName" : "Test Product",
        "externalId" : "1",
        "productId" : "1",
        "status" : "PENDING",
        "errors" : null
      } ]
    }
  }
  ```

### Get consumption detail by external ID batch

```
GET /api/v1/rest/product/consumption/batch/externalids/{queries}/{groupingInfo}
```

- **Description**

  The External ID Product Consumption API call can also be called in a batch mode, where more than one combination of external ID, start date, and end date can be queried for in a single call. In this case, the Inventory Batch Lookup Response structure will be returned from the call. This structure wraps multiple Inventory Detail structures, one for each query made to the batch API call. In case an invalid External ID is passed in, the API will return a NOT_FOUND constant for all string values in the ProductDetail structure.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | queries | queries | true | string |
  | BodyParameter | queryVars | queryVars | false | object |
  | PathParameter | groupingInfo | groupingInfo | true | string |
  | BodyParameter | groupingInfoVars | groupingInfoVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/consumption/batch/externalids/queries;q=321,2017-03-01,
  2017-03-31;q=322,2017-03-01,2017-03-31/groupInfo;groupBy=salesperson' -i -H 'Content-Type: application/json' -H 
  'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**
  
  ```
  GET /api/v1/rest/product/consumption/batch/externalids/queries;q=321,2017-03-01,2017-03-31;q=322,2017-03-01,
  2017-03-31/groupInfo;groupBy=salesperson HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1767

  {
    "inventoryBatchLookupResponse" : {
      "inventoryDetails" : [ {
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
        "summary" : {
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
        "dailyDetail" : [ {
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
        } ]
      } ]
    }
  }
  ```

### Get consumption detail by external ID

```
GET /api/v1/rest/product/consumption/externalid/{externalId}/{startDate}/{endDate}/{groupingInfo}
```

- **Description**

  The use of the External ID Product Consumption API is limited to lookups where a static product has been configured with an external ID. This allows API developers to use an external correlating identifier to lookup Yield Analytics Product Consumption information. In order to use the External ID a persistent mapping must be specified, configured, and maintained in the Yield Analytics system. Contact your Yield Analytics Administrator to setup this mapping.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | externalId | externalId | true | string |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | groupingInfo | groupingInfo | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**
  
  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/consumption/externalid/321/2017-03-01/2017-03-31/groupinfo;
  groupBy=salesperson' -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}'
  ```

- **Example HTTP request**
  
  ```
  GET /api/v1/rest/product/consumption/externalid/321/2017-03-01/2017-03-31/groupinfo;groupBy=salesperson HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Create product by originating target string

```
GET /api/v1/rest/product/create/target/{target}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Analysis Target Creation. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | target | target | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [ProductDetail](#productdetail) |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/create/target/ad_server%20in%20('TEST')' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/create/target/ad_server%20in%20('TEST') HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 603

  {
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
  }
  ```

### Create product by originating target expression

```
POST /api/v1/rest/product/create/targetexpression
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Analysis Target Creation. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | targetExpression | targetExpression | true | [TargetExpression](#targetexpression) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [ProductDetail](#productdetail) |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/create/targetexpression' -i -X POST -H 
  'Content-Type: application/json;charset=UTF-8' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/create/targetexpression HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 603

  {
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
  }
  ```

### Find products by match phrase

```
GET /api/v1/rest/product/discover/matchphrase/{matchphrase}
```

- **Description**

  Match Phrase functionality is the easiest Product Discovery functionality to use. It may be used to retrieve static-only products from the Yield Analytics API. The Match Phrase specifies a text string to be matched in a case-insensitive manner against both product names and included-only Product Targeting criteria term values. The specified text matches anywhere in the name or included term values but not against the attribute names or excluded term values. For example when specifying a match phrase; 'Food', both a product named ROS Food and a product having category=FOODLOVER would match.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | matchphrase | matchphrase | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/discover/matchphrase/testingMatchphrase' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/discover/matchphrase/testingMatchphrase HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1470

  {
    "productLookupResponse" : {
      "exactMatch" : {
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
      "candidateMatches" : [ {
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
      } ]
    }
  }
  ```

### Find products by targeting characteristics

```
GET /api/v1/rest/product/discover/targetingcharacteristics/{characteristics}
```

- **Description**

  Targeting Criteria current functionality allows the API developer to interact with static products. A future API release may allow for the exact match in the `ProductLookupResponse` to be created from the specific Targeting Criteria passed. Targeting Criteria is used to provide more exact matching than the Match Phrase functionality. When using the Targeting Criteria functionality, API developers may specify the specific attribute names and values to match. Both inclusion '=' or exclusion '!=" may be specified. Multiple term values for the same attribute may also be supplied. The above example will match any product having category=food and category=cooking where the size is 350x200. Note that the matched products will usually have other targeting attributes defined.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | characteristics | characteristics | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/discover/targetingcharacteristics/target;category=food;
  size=350x200;category=cooking' -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 
  'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/discover/targetingcharacteristics/target;category=food;size=350x200;category=cooking HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1470

  {
    "productLookupResponse" : {
      "exactMatch" : {
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
      "candidateMatches" : [ {
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
      } ]
    }
  }
  ```

### Find products

```
GET /api/v1/rest/product/discover/{productLocator}
```

- **Description**

  The Product Discovery interfaces allow the API developer to find products in the Yield Analytics system and retrieve product related meta-data. The identifiers returned in the Product Detail response data types allow for subsequent retrieval of Product Inventory. All Product Discovery interfaces return the `ProductLookupResponse` data type. Depending on the use case, one of the following API calls may be used to discover products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | productLocator | productLocator | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/discover/%7B%22productId%22:%221%22,%22externalId%22:%221%22%7D' -i 
  -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/discover/%7B%22productId%22:%221%22,%22externalId%22:%221%22%7D HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1470

  {
    "productLookupResponse" : {
      "exactMatch" : {
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
      "candidateMatches" : [ {
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
      } ]
    }
  }
  ```

### Get forecast adjustments

```
GET /api/v1/rest/product/forecast/{targets}/{date}
```

- **Description**

  Get forecast adjustment.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | targets | targets | true | string |
  | PathParameter | date | date | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**

  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/forecast/1/2017-03-01' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/forecast/1/2017-03-01 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 58

  {
    "forecastDebugResponse" : {
      "result" : "foo"
    }
  }
  ```

### Get inventory detail by external ID batch

```
GET /api/v1/rest/product/inventory/batch/externalids/{queries}
```

- **Description**

  The External ID Product Inventory API call can also be called in a batch mode, where more than one combination of external ID, start date, and end date can be queried for in a single call. In this case, the Inventory Batch Lookup Response structure will be returned from the call. This structure wraps multiple Inventory Detail structures, one for each query made to the batch API call. In case an invalid External ID is passed in, the API will return a NOT_FOUND constant for all string values in the `ProductDetail` structure.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | queries | queries | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/batch/externalids/queries;
  q=12345,2017-03-01,2017-03-31;q=23456,2017-03-01,2017-03-31' -i -H 'Content-Type: application/json' 
  -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/batch/externalids/queries;q=12345,2017-03-01,2017-03-31;q=23456,
  2017-03-01,2017-03-31 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1767

  {
    "inventoryBatchLookupResponse" : {
      "inventoryDetails" : [ {
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
        "summary" : {
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
        "dailyDetail" : [ {
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
        } ]
      } ]
    }
  }
  ```

### Get inventory details by target expression batch

```
POST /api/v1/rest/product/inventory/batch/{consumptionFilter}
```

- **Description**

  Inventory Details can be dynamically looked up in batch mode by passing url based alias function and consumption filters. The body of this call can contain a collection of lookup queries that are defined by the presence of a well-formed target expression and the date range for the lookup.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | batchInventoryQuery | batchInventoryQuery | true | [BatchInventoryQuery](#batchinventoryquery) |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/batch/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST 
  -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' -d '{
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('300x250') and state in ('co')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      }, {
        "targetExpression" : "size in ('300x250') and state in ('ca')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      } ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/batch/consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;
  CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 348

  {
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('300x250') and state in ('co')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      }, {
        "targetExpression" : "size in ('300x250') and state in ('ca')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1767

  {
    "inventoryBatchLookupResponse" : {
      "inventoryDetails" : [ {
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
        "summary" : {
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
        "dailyDetail" : [ {
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
        } ]
      } ]
    }
  }
  ```

### Get inventory details by target expression with displacement batch

```
POST /api/v1/rest/product/inventory/displacement/batch/{consumptionFilter}
```

- **Description**

  Inventory Details can be dynamically looked up in batch mode by passing url based alias function and consumption filters. The body of this call can contain a collection of lookup queries that are defined by the presence of a well-formed target expression and the date range for the lookup.

- **Parameters**

  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | batchInventoryQuery | batchInventoryQuery | true | [BatchInventoryQuery](#batchinventoryquery) |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/displacement/batch/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}'
  ' -d '{
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('300x250') and state in ('co')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      }, {
        "targetExpression" : "size in ('300x250') and state in ('ca')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      } ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/displacement/batch/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 348

  {
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('300x250') and state in ('co')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      }, {
        "targetExpression" : "size in ('300x250') and state in ('ca')",
        "startDate" : "2017-01-01",
        "endDate" : "2030-09-01"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1869

  {
    "inventoryWithDisplacementBatchLookupResponse" : {
      "inventoryDetails" : [ {
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
        "summary" : {
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
          "daysOutsideAvailabilityThreshold" : 0,
          "availableWithDisplacement" : 150
        },
        "dailyDetail" : [ {
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
          "daysOutsideAvailabilityThreshold" : 0,
          "availableWithDisplacement" : 150
        } ]
      } ]
    }
  }
  ```

### Get inventory detail by target expression with displacement

```
POST /api/v1/rest/product/inventory/displacement/targetexpression/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Product Inventory lookup. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | targetExpression | targetExpression | true | [TargetExpression](#targetexpression) |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/displacement/targetexpression/
  2017-03-01/2017-03-01/consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;
  PRIORITY%3E=5' -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' ' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/displacement/targetexpression/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1693

  {
    "inventoryDetail" : {
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
      "summary" : {
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
        "daysOutsideAvailabilityThreshold" : 0,
        "availableWithDisplacement" : 150
      },
      "dailyDetail" : [ {
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
        "daysOutsideAvailabilityThreshold" : 0,
        "availableWithDisplacement" : 150
      } ]
    }
  }
  ```

### Get inventory detail by external ID

```
GET /api/v1/rest/product/inventory/externalid/{externalId}/{startDate}/{endDate}
```

- **Description**

  The use of the External ID Product Inventory API is limited to inventory lookups where a static product has been configured with an external ID. This allows API developers to use an external correlating identifier to lookup Yield Analytics Product Inventory. In order to use the external ID a persistent mapping must be specified, configured, and maintained in the Yield Analytics system. Contact your Yield Analytics Administrator to setup this mapping.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | externalId | externalId | true | string |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/externalid/12345/2017-03-01/2017-03-31' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/externalid/12345/2017-03-01/2017-03-31 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by external ID with consumption filter

```
GET /api/v1/rest/product/inventory/externalid/{externalId}/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  The use of the External ID Product Inventory API is limited to inventory lookups where a static Product has been configured with an external ID. This allows API developers to use an external correlating identifier to lookup Yield Analytics Product Inventory. In order to use the external ID a persistent mapping must be specified, configured, and maintained in the Yield Analytics system. Contact your Yield Analytics Administrator to setup this mapping.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | externalId | externalId | true | string |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/externalid/12345/2017-03-01/2017-03-31/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/externalid/12345/2017-03-01/2017-03-31/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by operative adapter targeting

```
POST /api/v1/rest/product/inventory/operativeadapter/targeting/{startDate}/{endDate}
```

- **Description**

  The Operative Adapter Targeting Product Inventory API call allows Inventory Details to be retrieved for static or dynamic products via Operative Targeting Structures syntax combined with Consumption Filter inputs.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | targeting | targeting | true | [OperativeTargetingOptions](#operativetargetingoptions) |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**

  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/operativeadapter/targeting/2017-03-01/2017-03-01' 
  -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}' ' -d '{
    "targetingOptionFlatList" : [ {
      "mappedField" : "",
      "mappedValue" : "",
      "mappedValueExternalId" : "",
      "productionSystemIds" : [ ],
      "productionSystemName" : "",
      "rank" : 0,
      "status" : "",
      "targetingId" : 0,
      "targetingName" : "TEST",
      "targetingOptionId" : 0,
      "targetingOptionValue" : "",
      "productionSystemId" : 0
    } ]
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/operativeadapter/targeting/2017-03-01/2017-03-01 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 370

  {
    "targetingOptionFlatList" : [ {
      "mappedField" : "",
      "mappedValue" : "",
      "mappedValueExternalId" : "",
      "productionSystemIds" : [ ],
      "productionSystemName" : "",
      "rank" : 0,
      "status" : "",
      "targetingId" : 0,
      "targetingName" : "TEST",
      "targetingOptionId" : 0,
      "targetingOptionValue" : "",
      "productionSystemId" : 0
    } ]
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by operative adapter targeting with consumption filter

```
POST /api/v1/rest/product/inventory/operativeadapter/targeting/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  The Operative Adapter Targeting Product Inventory API call allows Inventory Details to be retrieved for static or dynamic products via Operative Targeting Structures syntax combined with Consumption Filter inputs.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | targeting | targeting | true | [OperativeTargetingOptions](#operativetargetingoptions) |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**

  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/operativeadapter/targeting/2017-03-01/2017-03-01/
  consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X 
  POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' -H ' -d '{
    "targetingOptionFlatList" : [ {
      "mappedField" : "",
      "mappedValue" : "",
      "mappedValueExternalId" : "",
      "productionSystemIds" : [ ],
      "productionSystemName" : "",
      "rank" : 0,
      "status" : "",
      "targetingId" : 0,
      "targetingName" : "TEST",
      "targetingOptionId" : 0,
      "targetingOptionValue" : "",
      "productionSystemId" : 0
    } ]
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/operativeadapter/targeting/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 370

  {
    "targetingOptionFlatList" : [ {
      "mappedField" : "",
      "mappedValue" : "",
      "mappedValueExternalId" : "",
      "productionSystemIds" : [ ],
      "productionSystemName" : "",
      "rank" : 0,
      "status" : "",
      "targetingId" : 0,
      "targetingName" : "TEST",
      "targetingOptionId" : 0,
      "targetingOptionValue" : "",
      "productionSystemId" : 0
    } ]
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by product ID with consumption filter

```
GET /api/v1/rest/product/inventory/productid/{productId}/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  Product Inventory may also be retrieved using the Yield Analytics internal Product ID combined with Consumption Filter inputs.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | productId | productId | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/productid/-2147483646/2017-03-01/2017-03-01/
  consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' 
  -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/productid/-2147483646/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get roadblock detail with consumption filter

```
POST /api/v1/rest/product/inventory/roadblock/product/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  Roadblock Detail would be retrieved with roadblock Consumption Filter.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | BodyParameter | roadblock | roadblock | true | [Roadblock](#roadblock) |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/roadblock/product/2017-03-01/2017-03-01/consumptionFilter;
  ROADBLOCK=all' -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}' ' -d '{
    "roadblock" : {
      "targetExpressions" : [ "ad_server in ('TEST') and size in ('180x70'), ad_server in ('TEST') and size in ('1010x150')" ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/roadblock/product/2017-03-01/2017-03-01/consumptionFilter;ROADBLOCK=all HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 150

  {
    "roadblock" : {
      "targetExpressions" : [ "ad_server in ('TEST') and size in ('180x70'), ad_server in ('TEST') and size in ('1010x150')" ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 78

  {
    "roadblockDetail" : {
      "availability" : 100,
      "capacity" : 100
    }
  }
  ```

### Get inventory detail by target string

```
GET /api/v1/rest/product/inventory/target/{target}/{startDate}/{endDate}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Product Inventory lookup. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | target | target | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/target/city=Boulder;country=USA/2017-03-01/2017-03-01' -i 
  -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' 
  
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/target/city=Boulder;country=USA/2017-03-01/2017-03-01 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  } 
  ```

### Get inventory detail by target string with consumption filter

```
GET /api/v1/rest/product/inventory/target/{target}/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Product Inventory lookup. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | target | target | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/target/city=Boulder;country=USA/2017-03-01/2017-03-01/
  consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/target/city=Boulder;country=USA/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by target expression

```
POST /api/v1/rest/product/inventory/targetexpression/{startDate}/{endDate}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Product Inventory lookup. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | BodyParameter | targetExpression | targetExpression | true | [TargetExpression](#targetexpression) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/targetexpression/2017-03-01/2017-03-01' -i -X 
  POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}' ' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/targetexpression/2017-03-01/2017-03-01 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by target expression with consumption filter

```
POST /api/v1/rest/product/inventory/targetexpression/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Product Inventory lookup. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | BodyParameter | targetExpression | targetExpression | true | [TargetExpression](#targetexpression) |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/targetexpression/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' 
  ' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/targetexpression/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get combined inventory detail by target expression

```
POST /api/v1/rest/product/inventory/targetexpressioncombined/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  The use of a Yield Analytics Originating Target targeting expression in Yield Analytics targeting syntax is supported for Product Inventory lookup. These expressions are returned in the `ProductLookupResponse ProductDetail` data structure as well as displayed in the Yield Analytics UI. This syntax allows for the richest targeting expressions to be built and defined. The use of Originating Target works for both static and dynamic products. This API returns a `CombinedInventoryDetail` object that contains an InventoryDetail including the effects of frequency capping and another one without capping effects. If the consumption filter has no frequency capping
  component, both InventoryDetail results are the same.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | BodyParameter | targetExpression | targetExpression | true | [TargetExpression](#targetexpression) |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/targetexpressioncombined/2017-03-01/2017-03-01/
  consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' ' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventory/targetexpressioncombined/2017-03-01/2017-03-01/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 3472

  {
    "combinedInventoryDetail" : {
      "uncappedDetail" : {
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
        "summary" : {
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
        "dailyDetail" : [ {
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
        } ]
      },
      "cappedDetail" : {
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
        "summary" : {
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
        "dailyDetail" : [ {
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
        } ]
      }
    }
  }
  ```

### Get inventory detail by targeting characteristics

```
GET /api/v1/rest/product/inventory/targetingcharacteristics/{characteristics}/{startDate}/{endDate}
```

- **Description**

  The Targeting Characteristics Product Inventory API call allows Inventory Detail to be retrieved for static or dynamic products via the loosely formed Targeting Criteria syntax.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | characteristics | characteristics | true | string |
  | BodyParameter | characteristicsVars | characteristicsVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/targetingcharacteristics/characteristics;city=Boulder;
  country=USA/2017-03-01/2017-03-01' -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 
  'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/targetingcharacteristics/characteristics;city=Boulder;
  country=USA/2017-03-01/2017-03-01 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get inventory detail by targeting characteristics with consumption filter

```
GET /api/v1/rest/product/inventory/targetingcharacteristics/{characteristics}/{startDate}/{endDate}
```

- **Description**

  The Targeting Characteristics Product Inventory API call allows Inventory Detail to be retrieved for static or dynamic products via the loosely formed Targeting Criteria syntax.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | characteristics | characteristics | true | string |
  | BodyParameter | characteristicsVars | characteristicsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventory/targetingcharacteristics/characteristics;
  city=Boulder;country=USA/2017-03-01/2017-03-01/consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;
  CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 
  'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventory/targetingcharacteristics/characteristics;city=Boulder;
  country=USA/2017-03-01/2017-03-01/consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;
  CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1611

  {
    "inventoryDetail" : {
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
      "summary" : {
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
      "dailyDetail" : [ {
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
      } ]
    }
  }
  ```

### Get batch inventory and contention

```
POST /api/v1/rest/product/inventoryandcontention/batch/{aliasFunctions}/{consumptionFilter}
```

- **Description**

  A batch related interface is also available to retrieve multiple product - date range pairings' inventory and contention data concurrently. The batch interface should be preferred in cases where several sets of inventory and contention data must be retrieved for display as a grouping. The batch interface performs internal multi-threading to greatly increase overall throughput and performance
  as batch items are not run serially.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | batchInventoryQuery | batchInventoryQuery | true | [BatchInventoryQuery](#batchinventoryquery) |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventoryandcontention/batch/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' 
  ' -d '{
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('TEST')",
        "startDate" : "2017-01-01",
        "endDate" : "2017-03-01"
      } ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventoryandcontention/batch/aliasFunctions;INVENTORY_CLASS=GUARANTEED;
  CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5/consumptionFilter;INVENTORY_CLASS=GUARANTEED;
  CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 181

  {
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('TEST')",
        "startDate" : "2017-01-01",
        "endDate" : "2017-03-01"
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

### Get batch inventory and contention with displacement

```
POST /api/v1/rest/product/inventoryandcontention/displacement/batch/{aliasFunctions}/{consumptionFilter}
```

- **Description**

  A batch related interface is also available to retrieve multiple product - date range pairings' inventory and contention data concurrently. The batch interface should be preferred in cases where several sets of inventory and contention data must be retrieved for display as a grouping. The batch interface performs internal multi-threading to greatly increase overall throughput and performance as batch items are not run serially.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | batchInventoryQuery | batchInventoryQuery | true | [BatchInventoryQuery](#batchinventoryquery) |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventoryandcontention/displacement/batch/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' 
  ' -d '{
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('TEST')",
        "startDate" : "2017-01-01",
        "endDate" : "2017-03-01"
      } ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventoryandcontention/displacement/batch/aliasFunctions;INVENTORY_CLASS=GUARANTEED;
  CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5/consumptionFilter;INVENTORY_CLASS=GUARANTEED;
  CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 181

  {
    "batchInventoryQuery" : {
      "queryCriteria" : [ {
        "targetExpression" : "size in ('TEST')",
        "startDate" : "2017-01-01",
        "endDate" : "2017-03-01"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1713

  {
    "inventoryAndContentionWithDisplacementBatchResponse" : {
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
            "daysOutsideAvailabilityThreshold" : 0,
            "availableWithDisplacement" : 150
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

### Get inventory and contention by target expression with displacement

```
POST /api/v1/rest/product/inventoryandcontention/displacement/targetexpression/{startDate}/{endDate}/{aliasFunctions}
/{consumptionFilter}
```

- **Description**

  In cases where both inventory forecast data and contender data is required, overall performance and throughput can be maximized by leveraging the Inventory and Contention based APIs. There are both single call and batch invocation options. When multiple inventory and contention is being retrieved for a variety of products or targets, the batch option should be preferred or the API should be accessed in a multithreaded manner. Calls to the Inventory and Contention APIs may be filtered using the Yield Analytics API consumptionFilter filter specification syntax.

  Additionally, the Inventory and Contention API offers flexible extraction of order line dimensional data using Query Engine aliases.

  The Inventory And Consumption API may be invoked via both GET and POST http methods. The use of POST is strongly recommended as this lessens the escaping required due to conflicting characters between the supplied target expression and URL legal characters.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | target | target | true | [TargetExpression](#targetexpression) |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventoryandcontention/displacement/targetexpression/
  2017-03-01/2017-03-01/aliasFunctions;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/
  consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED' -i -X POST -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' -H 
  'password: {{password}}' ' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventoryandcontention/displacement/targetexpression/2017-03-01/2017-03-01/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/consumptionFilter;INVENTORY_CLASS=GUARANTEED;
  CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1410

  {
    "inventoryAndContentionWithDisplacement" : {
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
        "daysOutsideAvailabilityThreshold" : 0,
        "availableWithDisplacement" : 150
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
  }
  ```

### Get inventory and contention by target string

```
GET /api/v1/rest/product/inventoryandcontention/target/{target}/{startDate}/{endDate}/{aliasFunctions}/{consumptionFilter}
```

- **Description**

  In cases where both inventory forecast data and contender data is required, overall performance and throughput can be maximized by leveraging the Inventory and Contention based APIs. There are both single call and batch invocation options. When multiple inventory and contention is being retrieved for a variety of products or targets, the batch option should be preferred or the API should be accessed in a multithreaded manner. Calls to the Inventory and Contention APIs may be filtered using the Yield Analytics API consumptionFilter filter specification syntax.

  Additionally, the Inventory and Contention API offers flexible extraction of order line dimensional data using Query Engine aliases.

  The Inventory And Consumption API may be invoked via both GET and POST http methods. The use of POST is strongly recommended as this lessens the escaping required due to conflicting characters between the supplied target expression and URL legal characters.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | target | target | true | [TargetExpression](#targetexpression) |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  
  application/json

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventoryandcontention/target/ad_server%20in%20('TEST')
  /2017-03-01/2017-03-01/aliasFunctions;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/
  consumptionFilter;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/product/inventoryandcontention/target/ad_server%20in%20('TEST')/2017-03-01/2017-03-01/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/consumptionFilter;INVENTORY_CLASS=GUARANTEED;
  CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1353

  {
    "inventoryAndContention" : {
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
  }
  ```

### Get inventory and contention by target expression

```
POST /api/v1/rest/product/inventoryandcontention/targetexpression/{startDate}/{endDate}/{aliasFunctions}/{consumptionFilter}
```

- **Description**

  In cases where both inventory forecast data and contender data is required, overall performance and throughput can be maximized by leveraging the Inventory and Contention based APIs. There are both single call and batch invocation options. When multiple inventory and contention is being retrieved for a variety of products or targets, the batch option should be preferred or the API should be accessed in a multithreaded manner. Calls to the Inventory and Contention APIs may be filtered using the Yield Analytics API consumptionFilter filter specification syntax.

  Additionally, the Inventory and Contention API offers flexible extraction of order line dimensional data using Query Engine aliases.

  The Inventory And Consumption API may be invoked via both GET and POST http methods. The use of POST is strongly recommended as this lessens the escaping required due to conflicting characters between the supplied target expression and URL legal characters.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | target | target | true | [TargetExpression](#targetexpression) |
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | aliasFunctions | aliasFunctions | true | string |
  | PathParameter | aliasFunctionsVars | aliasFunctionsVars | false | object |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | consumptionFilterVars | consumptionFilterVars | false | object |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | object |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/inventoryandcontention/targetexpression/2017-03-01/
  2017-03-01/aliasFunctions;INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED' -i -X POST -H 'Content-Type: application/json' 
  -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}' ' -d '{
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/inventoryandcontention/targetexpression/2017-03-01/2017-03-01/aliasFunctions;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 75

  {
    "targetExpression" : {
      "expression" : "ad_server in ('TEST')"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 1353

  {
    "inventoryAndContention" : {
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
  }
  ```

### Get operative adapter targeting expression

```
POST /api/v1/rest/product/targeting/operativeadapter
```

- **Description**

  Get operative adapter targeting expression.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | targets | targets | true | [OperativeTargetingOptions](#operativetargetingoptions) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [TargetExpression](#targetexpression) |

- **Consumes**
  - application/json
  - application/xml

- **Produces**
  - application/json
  - application/xml

- **Tags**
  
  Product Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/product/targeting/operativeadapter' -i -X POST 
  -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}' ' -d '{
    "targetingOptionFlatList" : [ {
      "mappedField" : "",
      "mappedValue" : "",
      "mappedValueExternalId" : "",
      "productionSystemIds" : [ ],
      "productionSystemName" : "",
      "rank" : 0,
      "status" : "",
      "targetingId" : 0,
      "targetingName" : "TEST",
      "targetingOptionId" : 0,
      "targetingOptionValue" : "",
      "productionSystemId" : 0
    } ]
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/product/targeting/operativeadapter HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 370

  {
    "targetingOptionFlatList" : [ {
      "mappedField" : "",
      "mappedValue" : "",
      "mappedValueExternalId" : "",
      "productionSystemIds" : [ ],
      "productionSystemName" : "",
      "rank" : 0,
      "status" : "",
      "targetingId" : 0,
      "targetingName" : "TEST",
      "targetingOptionId" : 0,
      "targetingOptionValue" : "",
      "productionSystemId" : 0
    } ]
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 46

  {
    "expression" : "ad_unit in ('sf video')"
  }
  ```

## Definitions

### BatchInventoryQuery
  
| Name | Description | Required | Schema |
|---|---|---|---|
| batchInventoryQuery |  | false | BatchInventoryQuery |
| queryCriteria | A collection of inventory query criteria | true | [InventoryQueryCriteria](#inventoryquerycriteria) array |

### BulkProductCreation

| Name | Description | Required | Schema |
|---|---|---|---|
| bulkProductCreation |  | false | BulkProductCreation |
| products | A collection of product creation data types holding the relevant data for each product to be added to the system | true | [ProductCreation](#productcreation) array |

### BulkProductCreationResponse

A JSON object to hold the request for Bulk Product Creation Response.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| products | A collection of product creation detail of the bulk product creation response | false | [ProductCreationDetail](#productcreationdetail) array |

### ColumnData

A JSON object to hold the results of a column data.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| name | The name of the column data | true | string |
| value | The value object of the column data | true | string |

### CombinedInventoryDetail

A JSON object to hold the results of a combined inventory detail.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| cappedDetail | The capped inventory detail of the combined inventory detail | true | [InventoryDetail](#inventorydetail) |
| uncappedDetail | The uncapped inventory detail of the combined inventory detail | true | [InventoryDetail](#inventorydetail) |

### ConsumptionDetail

A JSON object to hold the results of a consumption detail.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| consumedImpressions | The field contains consumed impressions | true | integer (int64) |
| detailName | The name of consumption detail | true | string |

### ForecastDebugResponse

A JSON object to hold the results of a forecast debug response.

| Name | Description | Required | Schema |
|---|---|---|---|
| result | The result of the forecast debug response | true | string |

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

### InventoryAndContentionWithDisplacement

A JSON object to hold the results of an inventory and contention detail with displacement enabled.

| Name | Description | Required | Schema |
|---|---|---|---|
| contendingData |  | false | [QueryResultData](#queryresultdata) |
| productDetail |  | false | [ProductDetail](#productdetail) |
| summaryData |  | false | [InventoryDataWithDisplacement](#inventorydatawithdisplacement) |  

### InventoryAndContentionWithDisplacementBatchResponse

A JSON object to hold the results of an inventory and contention with displacement enabled batch response.

| Name | Description | Required | Schema |
|---|---|---|---|
| batchResults |  | false | [InventoryAndContentionWithDisplacementBatchResult](#inventoryandcontentionwithdisplacementbatchresult) array |

### InventoryAndContentionWithDisplacementBatchResult

A JSON object to hold the results of an inventory and contention with displacement enabled batch result.

| Name | Description | Required | Schema |
|---|---|---|---|
| identifier |  | false | string |
| result |  | false | [InventoryAndContentionWithDisplacement](#inventoryandcontentionwithdisplacement) |

### InventoryBatchLookupResponse

A JSON object to hold the results of an inventory batch lookup response.

| Name | Description | Required | Schema |
|---|---|---|---|
| inventoryDetails | A collection of inventory details | false | [InventoryDetail](#inventorydetail) array |

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

### InventoryDataWithDisplacement

A JSON object to hold the results of an inventory data with displacement enabled.

| Name | Description | Required | Schema |
|---|---|---|---|
| available | The field contains available | true | integer (int64) |
| availableWithDisplacement |  | false | integer (int64) |
| capacity | The field contains capacity | true | integer (int64) |
| consumptionDetails | A collection of consumption details | false | [ConsumptionDetail](#consumptiondetail) array |
| daysInForecast | The days in forecast of the inventory data | true | integer (int32) |
| daysOutsideAvailabilityThreshold | The days outside availability threshold of the inventory data | true | integer (int32) |
| endDate | The end date of inventory data | true | string |
| evenAvailability | The even availability of the inventory data | true | boolean |
| exceededForecastWindow | The field indicates whether or not the inventory data exceeded forecast window | true | boolean |
| startDate | The start date of inventory data | true | string |
| unmetDemand | The field contains unmet demand | true | integer (int64) |

### InventoryDetail

A JSON object to hold the results of an inventory detail.

| Name | Description | Required | Schema |
|---|---|---|---|
| dailyDetail | A collection of daily inventory detail data | true | [InventoryData](#inventorydata) array |
| productDetail | The product detail of the inventory detail | true | [ProductDetail](#productdetail) |
| summary | The inventory data of the inventory detail | true | [InventoryData](#inventorydata) |

### InventoryDetailWithDisplacement

A JSON object to hold the results of an inventory detail with displacement enabled.

| Name | Description | Required | Schema |
|---|---|---|---|
| dailyDetail |  | false | [InventoryDataWithDisplacement](#inventorydatawithdisplacement) array |
| productDetail |  | false | [ProductDetail](#productdetail) |
| summary |  | false | [InventoryDataWithDisplacement](#inventorydatawithdisplacement) |

### InventoryQueryCriteria

A JSON object to hold the results of an inventory query criteria.

| Name | Description | Required | Schema |
|---|---|---|---|
| endDate | The end date of the inventory query criteria | true | string |
| identifier | The identifier of the inventory query criteria | true | string |
| startDate | The start date of the inventory query criteria | true | string |
| targetExpression | The target expression of the inventory query criteria | true | string |

### InventoryWithDisplacementBatchLookupResponse

A JSON object to hold the results of an inventory with displacement enabled batch lookup response.

| Name | Description | Required | Schema |
|---|---|---|---|
| inventoryDetails |  | false | [InventoryDetailWithDisplacement](#inventorydetailwithdisplacement) array |

### OperativeTargetingOptions

A JSON object to hold the OperativeTargetingOptions.

| Name | Description | Required | Schema |
|---|---|---|---|
| operativeProductId |  | false | string |
| targetingOptionFlatList |  | false | [TargetingOptionFlat](#targetingoptionflat) array |
| yxProductId |  | false | string |  

### ProductCreation

A JSON object to hold the request for Product Creation.

| Name | Description | Required | Schema |
|---|---|---|---|
| externalId | rim then: not empty and length < 200 <br><br> If productId exist and found in system, check for existence of externalId. If externalId also exist violates uniqueness of external ids. raise error: "Unable to update an existing product with product id: XXX that changes externalId to one: XXX that already exist" | false | string |
| originatingTarget | trim then: length > 0, parsable, and attributes and values exist in our system | true | string |
| productClass | CUSTOM or RATE_CARD or REPORTING or SEASONAL_MODEL | true | string |
| productGroupNames | Comma separated list of user group names. User groups must exist or an error will be generated, new user groups are not created. | false | string array |
| productId | If present must be Long and must correspond to a product in our system. | false | integer (int64) |
| productName | check for null, trim then: not empty and length < 4000 | true | string |
| rateCardCPM | if present must be double - If omitted default value of 0 will be used. | false | number (double) |
| state | ACTIVE or INACTIVE | true | string |
| userGroupNames | Comma separated list of user group names. User groups must exist or an error will be generated, new user groups are not created. | false | string array |  

### ProductCreationDetail

A JSON object to hold the results for Product Creation.

| Name | Description | Required | Schema |
|---|---|---|---|
| errors | The a collection of validation constraints that were not met during creation scheduling | false | [ProductCreationError](#productcreationerror) array |
| externalId | The ID of the product from it’s system of record | false | string |
| productId | The ID of the product within the Yield Analytics platform | false | string |
| productName | The name of the product within the Yield Analytics platform | true | string |
| status | The status of the product creation job: PENDING, COMPLETED, FAILED | true | string |  

### ProductCreationError

A JSON object to hold the error for product creation.

| Name | Description | Required | Schema |
|---|---|---|---|
| error | The error msg of the product creation field | true | string |
| field | The field of the product creation | true | string |  

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

### ProductLookupResponse

A JSON object to hold the results of a product search.

| Name | Description | Required | Schema |
|---|---|---|---|
| candidateMatches | Details of the products matched in the search | false | [ProductDetail](#productdetail) array |
| exactMatch | The total count of matched products in the search | false | [ProductDetail](#productdetail) |
  
### QueryResultData

A JSON object to hold the results of a query result data.

| Name | Description | Required | Schema |
|---|---|---|---|
| row | A collection of row data | false | [RowData](#rowdata) array |

### Roadblock

| Name | Description | Required | Schema |
|---|---|---|---|
| products | A list of products | true | string array |
| roadblock |  | false | Roadblock |
| targetExpressions | A list of target expressions | true | string array |

### RoadblockDetail

A JSON object to hold the results of an roadblock detail.

| Name | Description | Required | Schema |
|---|---|---|---|
| availability | The availability of roadblock | true | integer (int64) |
| capacity | The capacity of roadblock | true | integer (int64) |

### RowData

A JSON object to hold the results of a row data.

| Name | Description | Required | Schema |
|---|---|---|---|
| columnData | A collection of column data | true | [ColumnData](#columndata) array |

### TargetExpression

| Name | Description | Required | Schema |
|---|---|---|---|
| expression | The expression field of the target expression | true | string |
| targetExpression |  | false | TargetExpression |

### TargetingOptionFlat

A JSON object to hold the TargetingOptionFlat.

| Name | Description | Required | Schema |
|---|---|---|---|
| mappedField |  | false | string |
| mappedValue |  | false | string |
| mappedValueExternalId |  | false | string |
| productionSystemId |  | false | integer (int64) |
| productionSystemIds |  | false | string array |
| productionSystemName |  | false | string |
| rank |  | false | integer (int64) |
| status |  | false | string |
| targetingId |  | false | integer (int64) |
| targetingName |  | false | string |
| targetingOptionId |  | false | integer (int64) |
| targetingOptionValue |  | false | string |

## Related topic

[Yield Analytics API](yield-analytics-api.md)
