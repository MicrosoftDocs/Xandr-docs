---
title: GraphQL Service
description: GraphQL is a query language for APIs and a runtime that executes queries against existing data. It enables you to request only the data you need, in a precise and efficient way.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.author: shsrinivasan
ms.date: 01/21/2026
---

# GraphQL service

## Overview

GraphQL is a query language for APIs and a runtime that executes queries against existing data. It enables you to request only the data you need, in a precise and efficient way. 

GraphQL also addresses several limitations of REST-based architectures, including: 

- Reducing the number of API calls by allowing you to retrieve all required data in a single query. 
- Preventing over-fetching, since REST endpoints typically return fixed field sets that may include unnecessary data. 
- Supporting multi-resource retrieval in one request, improving both efficiency and performance. 
- GraphQL ensures safer, more modern, and more scalable access patterns while preserving the flexibility you need.

## Prerequisites 

Before beginning this setup, familialize yourself with the foundational concepts outlined in the following pages:
- **[API Getting Started](../digital-platform-api/api-getting-started.md)** - It provides information on testing environments, usage constraints, API semantics (running commands, filtering, sorting, etc.), and best practices. 
- **[Authentication Service](../digital-platform-api/authentication-service.md)** - is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use.

### Authentication

- **Example cURL authentication**
> [!NOTE]
> The authentication username and password are the same credentials used for the Digital Platform API and/or Monetize.

Authentication occurs by passing credentials via http headers on each request.

  ```
  - username: curl -H "username:username"
  - password: curl -H "password:password"      
  ```

- **Example HTTPS authentication**

  ```
  GET /api/v1/rest/
  HTTPS/1.1
  Host: api.appnexus.com/imf
  Accept: application/xml, application/json
  Content-Type: application/json
  username: {{username}}
  password: {{password}}      
  ```

> [!NOTE]
>
> - 'Authorization' is set to "No Auth"; the settings below are to be placed in the 'Headers' tab.
> - For a more in depth tutorial of using Postman, see [Using Postman with the Yield Analytics API](using-postman-with-the-yield-analytics-api.md).

- **HTTPS authentication response**
The request returns a token that remains valid for 2 hours. We suggest using "-b cookies -c cookies" in the POST request to store the token in a cookie. For a more in-depth tutorial of using Postman, see Using Postman with the Yield Analytics API. 

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

## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case by case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.


## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## REST API

| HTTP method | Endpoint | Description |
|---|---|---|
| POST | `https://api.appnexus.com/imf/api/v1/rest/graphql` | Retrieve product names and ID listings according to the selected filter criteria. |
| POST | `https://api.appnexus.com/imf/api/v1/rest/graphql` | Create, modify, or update multiple products using file upload. |
| POST | `https://api.appnexus.com/imf/api/v1/rest/graphql` | Analyze product overlap and capacity relationships using simple queries (product IDs/names/groups) or dynamic targeting expressions. |
| POST | `https://api.appnexus.com/imf/api/v1/rest/graphql` | Manage Manual Forecast Adjustments (MFA) - List, Add, Edit, and Delete forecast overrides for ad inventory capacity. |



## Paths

### Product listing

The Product Listing service retrieves product names and IDs based on the filters you apply. The system returns only those products that meet the selected criteria, enabling efficient navigation and downstream use of product metadata.

#### JSON fields 

| Parameter | Field | Description |
|---|---|---|
| reportType | string | **Required** <br> Specifies the type of report to generate. This field should have one of the constants from the below list: <br> - ALL_CUSTOM_PRODUCTS <br> - ACTIVE_CUSTOM_PRODUCTS <br> - ALL_REPORTING_PRODUCTS <br> - ACTIVE_REPORTING_PRODUCTS <br> - ALL_SEASONAL_PRODUCTS <br> - ACTIVE_SEASONAL_PRODUCTS <br> - ALL_RATE_CARD_PRODUCTS <br> - ACTIVE_RATE_CARD_PRODUCTS <br> - PRODUCTS_BY_NAME <br> - ACTIVE_PRODUCTS_BY_NAME <br> - PRODUCTS_BY_CHARACTERISTICS <br> - PRODUCT_GROUP <br> - ACTIVE_PRODUCT_GROUP <br> - ACTIVE_PRODUCTS_BY_CHARACTERISTICS |
| startDate | string | **Required.** <br> The start date for the report data. |
| endDate | string | The end date for the report data. <br> **NOTE:** If not provided, it will pick the same date as `startDate`.|
| periodicity | integer | Defines the frequency or granularity of the results. Any of the following values can be used: <br> - DAILY <br> - WEEKLY <br> - MONTHLY <br> - QUARTERLY <br> - YEARLY <br> - ALL |
| characteristics | string | A list of key attributes that describe the product’s specifications or properties. <br> **NOTE:** Only required when report_type is `ACTIVE_PRODUCTS_BY_CHARACTERISTICS` or `PRODUCTS_BY_CHARACTERISTICS` |
| names | string | Human-readable names for individual products. <br> **NOTE:** Only required when report_type is `ACTIVE_PRODUCTS_BY_NAME` or `PRODUCTS_BY_NAME` |
| productGroupNames | string | Logical grouping or category to which the product belongs. <br> **NOTE:** Only required when report_type is `ACTIVE_PRODUCT_GROUP` or `PRODUCT_GROUP` |

##### **Example cURL request**

**All products, both active and inactive, with the product type set to Custom - ALL_CUSTOM_PRODUCTS**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ALL_CUSTOM_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**Active products with product type set to Custom - ACTIVE_CUSTOM_PRODUCTS**

> [!NOTE]
> All query responses use a consistent format rather than different variations of the sample answers.

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_CUSTOM_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All products, both active and inactive, with the product type set to Reporting - ALL_REPORTING_PRODUCTS**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ALL_REPORTING_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All active products with product type set to Reporting - ACTIVE_REPORTING_PRODUCTS**    

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_REPORTING_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All products, both active and inactive, with product type set to Seasonal Model - ALL_SEASONAL_PRODUCTS**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ALL_SEASONAL_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**Active products with product type set to Seasonal Model - ACTIVE_SEASONAL_PRODUCTS**
```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_SEASONAL_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All products, both active and inactive, with product type set to Rate Card - ALL_RATE_CARD_PRODUCTS**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ALL_RATE_CARD_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All active products with product type set to Rate Card - ACTIVE_RATE_CARD_PRODUCTS**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_RATE_CARD_PRODUCTS
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All products, both active and inactive, listed by name – PRODUCTS_BY_NAME**

> [!NOTE] 
> Names is a mandatory field for this request. 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: PRODUCTS_BY_NAME
      names: ["Display Banner 728x90", "Video Pre-Roll 30s"]
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All active products listed by name - ACTIVE_PRODUCTS_BY_NAME** 

> [!NOTE] 
> Names is a mandatory field for this request. 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_PRODUCTS_BY_NAME
      names: ["Display Banner 728x90", "Video Pre-Roll 30s"]
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All products, both active and inactive, matching the specified characteristics - PRODUCTS_BY_CHARACTERISTICS**

> [!NOTE]
> `characteristics` field is required for this request. The values in the array are evaluated using AND logic. For example: `WHERE size="780x320" AND duration=30`.

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: PRODUCTS_BY_CHARACTERISTICS
      characteristics: ["size=780x320", "duration=30"]
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All active products matching the specified characteristics - ACTIVE_PRODUCTS_BY_CHARACTERISTICS**

> [!NOTE]
> `characteristics` field is required for this request. The values in the array are evaluated using AND logic. For example: `WHERE size="780x320" AND duration=30`. 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_PRODUCTS_BY_CHARACTERISTICS
      characteristics: ["size=780x320", "duration=30"]
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All products, both active and inactive, with the specified product group - PRODUCT_GROUP**
> [!NOTE]
> `productGroupNames` is mandatory for this request. 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: PRODUCT_GROUP
      productGroupNames: ["Placement", "Video Inventory"]
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

**All active products with the specified product group - ACTIVE_PRODUCT_GROUP**
 
> [!NOTE] 
> `productGroupNames` is mandatory for this request. 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getProductListing(
      reportType: ACTIVE_PRODUCT_GROUP
      productGroupNames: ["Placement", "Video Inventory"]
      startDate: "2025-10-01"
      periodicity: DAILY
    ) {
      productId
      productName
    }
  }
}
```

##### Example cURL response

```
{
  "data": {
    "getProductListing": [
      {
        "productId": "11",
        "productName": "desktop native placement slot 1 - 11"
      },
      {
        "productId": "12",
        "productName": "native_featured_discount_details_page_tracker - 111"
      },
      {
        "productId": "-13",
        "productName": "Analyzed Network"
      },
      {
        "productId": "14",
        "productName": "hour_17"
      },
      {
        "productId": "15",
        "productName": "desktop native placement slot 2 - 1111"
      },
      {
        "productId": "-16",
        "productName": "Non-Analyzed Network"
      },
      {
        "productId": "17",
        "productName": "tracker - 112"
      }
    ]
  }
}
```


### File based product creation

The File Based Product Creation feature allows you to create or update products in bulk using a file upload workflow. 

To create or update products: 

- Create a .txt file containing the required product data. Please click here for the sample .txt file. 
- Upload the file through the designated endpoint. 
- Once uploaded, the system saves the file contents to the appropriate database table. 
- The data is then processed, and the products are created instantly or updated during the next nightly processing run. 

#### JSON fields

| Parameter | Field | Description |   
|---|---|---|
| productId | string | Valid product ID from the application. <br> **NOTE:** This field is required only within the file, when an existing product is being updated. |
| mutation UploadFile | string | Refers to a GraphQL mutation operation used to upload a file to a server or API endpoint.|
| validateOnly | boolean | If set to true, GraphQL app will only validate the text file. It will not insert the data from the text file into the table, so product creation will not occur. This process is solely for validating the data in the text file. If set to false, the products would be queued to be created during the next nightly processing run. Other fields however, in the query, for example, like mutation or UploadFile do not change and will always be the same in the query. <br> **NOTE:** The only inputs allowed are: <br> - validateOnly: true or false <br> - processNow: true or false <br>  - 0: file |
| processNow | boolean | If set to true, the product creation job will immediately trigger the creation of products in the actual table. Instead of waiting for the next processing run, which causes a delay, this will create the product right away. If set to false, the products would be queued to be created during the next nightly processing run. Other fields however, in the query, for example, like mutation or UploadFile do not change and will always be the same in the query. <br> **NOTE:** The only inputs allowed are: <br> - validateOnly: true or false <br> - processNow: true or false <br>  - 0: file |
| map | string | Refers to the variable in the GraphQL operation that should receive the uploaded file(s).<br> **NOTE:** The value here will always be `{ "0": ["variables.input.file"] }` |


##### Example cURL request 
 
**`validateOnly":true,"processNow":false`**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: multipart/form-data' \
  operations: {"query":"mutation UploadFile($input: CustomSeasonalModelInput!) { uploadCustomSeasonalModels(input: $input) { success messages { lineNumber message } } }","variables":{"input":{"file":null,"validateOnly":true,"processNow":false}}}
  map: { "0": ["variables.input.file"] }
  0: upload the file here
```

**`validateOnly":false,"processNow":true`**

```
curl `https://api.appnexus.com/imf/api/v1/rest/graphql`
-H 'Authorization: Bearer <token>' \
-H 'Content-Type: multipart/form-data' \
operations: {"query":"mutation UploadFile($input: CustomSeasonalModelInput!) { uploadCustomSeasonalModels(input: $input) { success messages { lineNumber message } } }","variables":{"input":{"file":null,"validateOnly":false,"processNow":true}}}
map: { "0": ["variables.input.file"] }
0: upload the file here
```

**`validateOnly":false,"processNow":false`**

```
curl `https://api.appnexus.com/imf/api/v1/rest/graphql`
-H 'Authorization: Bearer <token>' \
-H 'Content-Type: multipart/form-data' \
operations: {"query":"mutation UploadFile($input: CustomSeasonalModelInput!) { uploadCustomSeasonalModels(input: $input) { success messages { lineNumber message } } }","variables":{"input":{"file":null,"validateOnly":false,"processNow":false}}}
map: { "0": ["variables.input.file"] }
0: upload the file here
```


#### Example cURL response 
 
**`validateOnly":false,"processNow":true`**

```
{ 
  "data": { 
    "uploadCustomSeasonalModels": { 
      "success": true, 
      "messages": [ 
      { 
        "lineNumber": null, 
            "message": "[INFO] Loaded 1 lines. Checking Line Operations...”        
                           }, 
      { 
        "lineNumber": 1, 
        "message": "[INFO] Line parsed successfully" 
      }, 
      { 
        "lineNumber": null, 
        "message": "[INFO] Line parsed successfully" 
      }, 
      { 
        "lineNumber": null, 
        "message": "[INFO] *** 1 products to process ***" 
      }, 
      { 
        "lineNumber": null, 
        "message": "[INFO] Validation completed successfully. 1 line processed." 
      }, 
      { 
        "lineNumber": null, 
        "message": "[INFO] Products have been successfully created" 
      }, 
      { 
        "lineNumber": null, 
        "message": "[INFO] PDI job triggered successfully " 
      } 
     ] 
    } 
  } 
}
```

**`validateOnly":false,"processNow":false`**

```
{
  "data": {
    "uploadCustomSeasonalModels": {
      "success": true,
      "messages": [
        {
          "lineNumber": null,
          "message": "[INFO] Loaded 1 lines. Checking Line Operations..."
        },
        {
          "lineNumber": 1,
          "message": "[INFO] Line parsed successfully"
        },
        {
          "lineNumber": null,
          "message": "[INFO] *** 1 products to process ***"
        },
        {
          "lineNumber": null,
          "message": "[INFO] Validation completed successfully. 1 lines processed."
        },
        {
          "lineNumber": null,
          "message": "[INFO] Products have been successfully queued for creation"
        }
      ]
    }
  }
}
```

### Product or overlap analysis query 

The product or overlap analysis query in Yield Analytics examines how impressions overlap across products. By analyzing these overlapping impressions, you can compare how impressions are shared between a selected focus product. or a set of target attributes, and the products that overlap with it. 

The service supports two query methods:
- **Simple queries:** Compare product names or IDs with other product names or IDs. 
- **Dynamic queries:** Compare a target expression with a product ID. 
 

#### Json fields

| Parameter | Field | Description |
|---|---|---|
| focusProductIds | array | Array of product IDs that represent the primary products for which overlap analysis is requested. |
| focusProductNames | array | Array of names corresponding to the focus product IDs. . |
| focusProductGroupNames | string | Names of product groups (e.g., bundles or categories) that the focus products belong to. |
| focusProductIdsOrTargetExpressions | string | It enables you to define the focus of an overlap analysis either by listing product IDs or by providing a targeting expression. |
| overlapsToAnalyzeProductIds | array | Array of product IDs that should be compared against the focus products for overlap. |
| overlapsToAnalyzeProductNames | string | Names corresponding to the related product IDs. |
| overlapsToAnalyzeProductGroupNames | string | Names of product groups for the related products. |
| startDate | string | The beginning date for the overlap analysis (format: YYYY-MM-DD). |
| endDate | string | The ending date for the overlap analysis (format: YYYY-MM-DD). |
| RELATED_PRODUCT_ID | string | The unique identifier of another product that is being compared against the focus product for overlap analysis. |
| RELATED_PRODUCT_NAME | string | The name of the related product in the overlap comparison. |
| FOCUS_PRODUCT_CAPACITY | integer | The total available impression capacity for the related product within the same date range. |
| RELATED_PRODUCT_CAPACITY | integer | The total available impression capacity for the related product within the same date range. |
| OVERLAPPING_CAPACITY | integer | The number of impressions that both products share (i.e., inventory that qualifies for both targeting sets). |
| PERCENT_OVERLAP | float | The percentage of the related product’s capacity that overlaps with the focus product. |
| TargetExpressions | string | The set of targeting criteria or conditions that define which inventory qualifies for a product or target in the context of IMF/Yield Analytics and ad forecasting. |
| PERCENT_OVERLAP_FOCUS | float | The percentage of the focus product’s capacity that overlaps with the related product. |


##### Simple query 

**Example cURL request**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getOverlapAnalysis(
      focusProductIds: ["focusproduct ID"]
      overlapsToAnalyzeProductIds: ["product ID1", "productID2", "productID3"]
      startDate: "2025-12-15"
      endDate: "2025-12-18"
    ) {
      data {
        FOCUS_PRODUCT_ID
        FOCUS_PRODUCT_NAME
        RELATED_PRODUCT_ID
        RELATED_PRODUCT_NAME
        FOCUS_PRODUCT_CAPACITY
        RELATED_PRODUCT_CAPACITY
        OVERLAPPING_CAPACITY
        PERCENT_OVERLAP
        PERCENT_OVERLAP_FOCUS
      }
    }
  }
}
```

**Example cURL response**

```
{
  "data": {
    "getOverlapAnalysis": {
      "data": [
        {
          "FOCUS_PRODUCT_ID": "focus_product_id",
          "FOCUS_PRODUCT_NAME": "focus_product_name",
          "RELATED_PRODUCT_ID": "related_product_id1",
          "RELATED_PRODUCT_NAME": "related_product_name",
          "FOCUS_PRODUCT_CAPACITY": "focus_product_capacity",
          "RELATED_PRODUCT_CAPACITY": "related_product_capacity1",
          "OVERLAPPING_CAPACITY": "overlapping_capacity1",
          "PERCENT_OVERLAP": "percent_overlap",
          "PERCENT_OVERLAP_FOCUS": "percent_overlap_focus"
        },
        {
          "FOCUS_PRODUCT_ID": "focus_product_id",
          "FOCUS_PRODUCT_NAME": "focus_product_name",
          "RELATED_PRODUCT_ID": "related_product_id2",
          "RELATED_PRODUCT_NAME": "related_product_name",
          "FOCUS_PRODUCT_CAPACITY": "focus_product_capacity",
          "RELATED_PRODUCT_CAPACITY": "related_product_capacity2",
          "OVERLAPPING_CAPACITY": "overlapping_capacity2",
          "PERCENT_OVERLAP": "percent_overlap",
          "PERCENT_OVERLAP_FOCUS": "percent_overlap_focus"
        },
        {
          "FOCUS_PRODUCT_ID": "focus_product_id",
          "FOCUS_PRODUCT_NAME": "focus_product_name",
          "RELATED_PRODUCT_ID": "related_product_id3",
          "RELATED_PRODUCT_NAME": "related_product_name",
          "FOCUS_PRODUCT_CAPACITY": "focus_product_capacity",
          "RELATED_PRODUCT_CAPACITY": "related_product_capacity3",
          "OVERLAPPING_CAPACITY": "overlapping_capacity3",
          "PERCENT_OVERLAP": "percent_overlap",
          "PERCENT_OVERLAP_FOCUS": "percent_overlap_focus"
        }
      ]
    }
  }
}
```

##### Dynamic query 

**Example cURL request**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  query {
    getOverlapAnalysis(
      focusProductIdsOrTargetExpressions: ["publisher in ('ABC')"]
      overlapsToAnalyzeProductNames: ["ProductName1", "ProductName2"]
      startDate: "2025-12-15"
      endDate: "2025-12-31"
    ) {
      data {
        FOCUS_PRODUCT_ID
        FOCUS_PRODUCT_NAME
        RELATED_PRODUCT_ID
        RELATED_PRODUCT_NAME
        FOCUS_PRODUCT_CAPACITY
        RELATED_PRODUCT_CAPACITY
        OVERLAPPING_CAPACITY
        PERCENT_OVERLAP
        PERCENT_OVERLAP_FOCUS
      }
    }
  }
}
```

**Example cURL response**

```
{
  "data": {
    "getOverlapAnalysis": {
      "data": [
        {
          "FOCUS_PRODUCT_ID": "focus_product_id1",
          "FOCUS_PRODUCT_NAME": "focus_product_name1",
          "RELATED_PRODUCT_ID": "related_product_id1",
          "RELATED_PRODUCT_NAME": "related_product_name1",
          "FOCUS_PRODUCT_CAPACITY": "focus_product_capacity1",
          "RELATED_PRODUCT_CAPACITY": "related_product_capacity1",
          "OVERLAPPING_CAPACITY": "overlapping_capacity1",
          "PERCENT_OVERLAP": "percent_overlap1",
          "PERCENT_OVERLAP_FOCUS": "percent_overlap_focus1"
        },
        {
          "FOCUS_PRODUCT_ID": "focus_product_id2",
          "FOCUS_PRODUCT_NAME": "focus_product_name2",
          "RELATED_PRODUCT_ID": "related_product_id2",
          "RELATED_PRODUCT_NAME": "related_product_name2",
          "FOCUS_PRODUCT_CAPACITY": "focus_product_capacity2",
          "RELATED_PRODUCT_CAPACITY": "related_product_capacity2",
          "OVERLAPPING_CAPACITY": "overlapping_capacity2",
          "PERCENT_OVERLAP": "percent_overlap2",
          "PERCENT_OVERLAP_FOCUS": "percent_overlap_focus2"
        }
      ]
    }
  }
}
```
### Manual forecast adjustment (MFA)

Manual Forecast Adjustment (MFA) enables you enables you to make one-time changes to the forecast for specific events that will impact traffic for a particular product. 
The GraphQL API supports the following MFA operations: 

- List MFAs 
- Add an MFA 
- Edit an existing MFA 
- Delete an MFA 

#### JSON fields

| Parameter | Field | Description |
|---|---|---|
| manualForecastAdjustmentId | integer | Unique identifier for the manual forecast adjustment entry. |
| name | string |  Descriptive name for the adjustment (e.g., “Holiday Boost Q4”). |
| productId | integer | The ID of the product to which the adjustment applies. |
| adjustmentStatus | string | Current status of the adjustment. <br> The values included are: <br> - ACTIVE: The change takes effect on the dates you select.  <br> - INACTIVE: The change doesn't take effect until you edit and set the adjustment status to “active”.  |
| adjustmentType | string | Type of adjustment applied, such as: <br> - Absolute: Adds/subtracts a specific number of impressions to the Yield Analytics generated forecast. It changes the forecast by adding or subtracting the value you enter. <br> - Relative: Adds/subtracts a percentage of impressions to the Yield Analytics generated forecast. It changes the forecast based on the percentage that you enter. <br> - Replace: Replaces the Yield Analytics forecast with a manually supplied forecast value. It changes the actual forecast value (number of impressions) with the value you enter. <br> - Ceiling: Caps the Yield Analytics forecast at a supplied forecast value. It creates an impressions cap over a period of time, above and beyond spike detection and mitigation. |
| adjustmentValue | integer | The numeric value of the adjustment (e.g., +10% or 500000 impressions). |
| creationDate | string | Timestamp when the adjustment was created.  |
| lastModifiedDate | string | Timestamp of the most recent update to the adjustment. |
| fromDate | string | Start date for the adjustment’s effective period. |
| toDate | string | End date for the adjustment’s effective period. |
| productName | string | Human-readable name of the product (e.g., “Homepage Banner”). |
| externalId | integer | External reference ID for integration with other systems (e.g., OMS or ad server). |
| priority | string | Indicates the product’s priority level in forecasting or delivery (e.g., High, Medium, Low) |

##### Example cURL request

**Listing all the MFA's without product id filter**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  "query": "query {
    "getManualForecastAdjustments": [
      {
        manualForecastAdjustmentId
        name
        productId
        adjustmentStatus
        adjustmentType
        adjustmentValue
        creationDate
        lastModifiedDate
        fromDate
        toDatex
        product: {
          productId
          productName
          externalId
          priority
        }
      },
      {
        manualForecastAdjustmentId
        name
        productId
        adjustmentStatus
        adjustmentType
        adjustmentValue
        creationDate
        lastModifiedDate
        fromDate
        toDate
        product: {
          productId
          productName
          externalId
          priority
        }
      }
    ]
  }"
}
```

**Listing all the MFA's with product id filter**

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  "query": "query {
    getManualForecastAdjustments(productId: \"538\") [
      {
        manualForecastAdjustmentId
        name
        productId
        adjustmentStatus
        adjustmentType
        adjustmentValue
        creationDate
        lastModifiedDate
        fromDate
        toDate
        product: {
          productId
          productName
          externalId
          priority
        }
      }
    ]
  }"
}
```

**Adding a new MFA under a product**


> [!NOTE]
> `productId` is required field for adding a new row. 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  "query": "mutation {
    addManualForecastAdjustment (
      productId: 538,
      name: \"Test\",
      adjustmentStatus: \"Active\",
      adjustmentType: \"Absolute\",
      adjustmentValue: 1.0,
      fromDate: \"2025-12-21\",
      toDate: \"2025-12-25\"
    ) {
    manualForecastAdjustmentId
      productId
      adjustmentStatus
      adjustmentType
      adjustmentValue
      fromDate
      toDate
    }
  }"
}
```

**Edit an MFA**
 
> [!NOTE] 
> When editing an MFA, you are not required to include all fields in the request payload. You may provide only the fields you want to update—for example, adjustmentStatus—and omit all others. Existing database values remain unchanged except for the lastUpdatedDate field. 
> The following fields are required when editing an MFA: 
- manualForecastAdjustmentId 
- productId 

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  "query": "mutation {
    updateManualForecastAdjustment(
      manualForecastAdjustmentId: \"6c45e5e3-3759-463a-815f-0a2ad900f362\"
      productId: 538,
      name: \"Test MFA Edited\",
      adjustmentStatus: \"Active\",
      adjustmentType: \"Relative\",
      adjustmentValue: 100.0,
      fromDate: \"2025-10-25\",
      toDate: \"2025-10-26\"
    ) {
      manualForecastAdjustmentId
      productId
      adjustmentStatus
      adjustmentType
      adjustmentValue
      fromDate
      toDate
    }
  }"
}
```

**Delete an MFA**

> [!NOTE]
> `manualForecastAdjustmentId` is required for deleting an MFA.

```
$ curl 'https://api.appnexus.com/imf/api/v1/rest/graphql'
{
  mutation {
    deleteManualForecastAdjustment(manualForecastAdjustmentId: "111")
  }
} 
```

##### Example cURL response 

```
{ 
  "data": { 
    "deleteManualForecastAdjustment": true 
  } 
} 
```


## Related topic

- [Yield Analytics API](yield-analytics-api.md)
