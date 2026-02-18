---
title: VaryBy Service
description: VaryBy functionality allows you to run availability lookups by varying one or more targeting attributes such as city, browser, or device, across a defined range of values.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.author: shsrinivasan
ms.date: 01/23/2026
---

# VaryBy service

## Overview

VaryBy functionality allows you to run availability lookups by varying one or more targeting attributes such as city, browser, and device, across a defined range of values. It allows you to vary base targeting criteria by selected variant targeting criteria. VaryBy helps build multiple targeting strings by combining each variant with the base targeting. Instead of checking availability for a single static target, VaryBy automatically generates and evaluates multiple combinations of attribute values, returning results for each combination in a single batch. This helps you better understand how different attribute variations influence availability, performance, or inventory. 
 
You can vary base targeting criteria by selected variant targeting criteria. It builds multiple targeting strings by combining each variant with the base targeting. This results in a set of targeting strings that represent all possible combinations, enabling more detailed and flexible analysis. 

VaryBy works in conjunction with Batch processing. While VaryBy defines the attributes and values that vary, Batch determines how those combinations are executed as a single request. The Batch workflow is where the final varyBy-based request structure is constructed and submitted.

For more details, see the [Batch section](#batch-method), which walks through the request structure and execution flow in detail.

## Prerequisites 

Before beginning this setup, familialize yourself with the foundational concepts outlined in the following pages:
- **[API Getting Started](../digital-platform-api/api-getting-started.md)** - It provides information on testing environments, usage constraints, API semantics (running commands, filtering, sorting, etc.), and best practices. 
- **[Authentication](api-authentication.md)** - is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use.

### Authentication
For more information on authentication, see [Yield Analytics API - Authentication Process](api-authentication.md).

<!--
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
> 'Authorization' is set to "No Auth"; the settings below are to be placed in the 'Headers' tab.


##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/0/100000/%2525 HTTP/1.1` 
Content-Type: application/json 
Authorization: {{auth-token}} 
```

**Example cURL request**

```
GET /api/imf/api/v1/rest/product/inventory/attributes/0/100000/%25
Headers:
{
  "Authorization": "{{auth-token}}"
}
```

**Example cURL response**

```
[
  {
    "adserver": [
      "APPNEXUS"
    ],
    "id": "38",
    "value": "a"
  },
  {
    "adserver": [
      "APPNEXUS"
    ],
    "id": "57",
    "value": "act_score"
  },
  {
    "adserver": [],
    "id": "1",
    "value": "ad_server"
  },
  {
    "adserver": [
      "APPNEXUS"
    ],
    "id": "104",
    "value": "ad_type"
  },
  {
    "adserver": [
      "APPNEXUS"
    ],
    "id": "2",
    "value": "age"
  }
]
```
-->


## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case-by-case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.


## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## REST API

> [!NOTE]
> Each of these endpoints return the attribute or value options needed to construct a Batch request body.

| HTTP method | Endpoint | Description |
|---|---|---|
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/{pageIndex}/{pageSize}/{attrNameQuery}` | Returns a list of attributes matching the given query. |
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributeValues/{pageIndex}/{pageSize}/attrId:{attributeId}` | Returns a paginated list of attribute values for a given attribute ID. |
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/operators/{attribute}` | Returns a list of operators for a given attribute. |
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/filters/{filter_name}` | Returns filter details to use in create batch body. |



## Paths

### Returns a list of attributes matching the given query (getAttributes) 

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/{pageIndex}/{pageSize}/{attrNameQuery}` 
```

#### JSON fields 

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| PathParameter | getAttributes | Returns a list of attributes matching the given query. | true | string |
| PathParameter | pageIndex | Specifies the page of results you want to retrieve. | true | integer |
| PathParameter | pageSize | Specifies how many items (or records) are included in each page of results. | true | integer |
| PathParameter | attrNameQuery | The name of the attribute you want to query. | true | string |
| HeaderParameter | content-type | Specifies your request body format. | true | string |

> [!Note] 
> These endpoints allow you to explore how to construct a varyBy query and explain the supported operators and attributes. Their usage is not limited to filters alone.

### Get attributes values 

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributeValues/{pageIndex}/{pageSize}/attrId:{attributeId}`
```

#### JSON fields 

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| PathParameter | getAttributeValues | Returns a paginated list of attribute values for a given attribute ID. | true | string |
| PathParameter | pageIndex | Specifies the page of results you want to retrieve. | true | integer |
| PathParameter | pageSize | Specifies how many items (or records) are included in each page of results. | true | integer |
| PathParameter | attributeId | The ID of the attribute for which you want to retrieve values. | true | integer |
| HeaderParameter | content-type | Specifies your request body format. | true | string |
| QueryParameter | query | Specifies your query parameter | true | string |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributeValues/0/1000/0/1000/attrId:{attributeID}?query={queryID}` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example cURL request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributeValues/0/1000/attrId:{attributeID}?query={queryID}`
```

**Example cURL response**

```
[
  {
    "adserver": [],
    "value": "1270x500"
  }
]
```

### Get operators 

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/operators/{attribute}` 
```

#### JSON fields 

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| PathParameter | getOperators | Returns a list of operators for a given attribute. | true | string |
| PathParameter | operators | Returns a list of operators for a specific `attributeId`. | true | integer |
| PathParameter | attribute | Enables you to understand the operators that are allowed for an attributeId. | true | integer |
| PathParameter | attributeId | The ID of the attribute for which you want to retrieve values. | true | integer |
| HeaderParameter | content-type | Specifies your request body format. | true | string |


##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/operators/size` -i -H 'Content-Type: application/json;charset=UTF-8'  
```


**Example cURL request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/operators/size`
```

**Example cURL response**

```json
[
  "IN",
  "NOT_IN",
  "LT",
  "GT",
  "LTE",
  "GTE"
]
```

### Get filters by name  

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/filters/{filter_name}`
```

#### JSON fields
| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| PathParameter | getFilters| Returns filter details to use in create batch body.| true | string |
| PathParameter | group_by | Specifies how the data is aggregated and displayed. <br> To see all possible values using GROUP_BY <br> `$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/filters/GROUP_BY` <br> **Example response:** <br> ```{ "total": 6, "name": "Group By", "options": [ { "name": "Daily", "value": "daily" }, { "name": "Weekly", "value": "weekly" }, { "name": "Monthly", "value": "monthly" }, { "name": "Quarterly", "value": "quarterly" }, { "name": "Yearly", "value": "yearly" }, { "name": "All", "value": "all" } ], "id": "GROUP_BY" } ``` <br> **NOTE:** This filter helps you identify the available GROUP_BY options and understand how to apply them. | true | string |
| PathParameter | priority  | Indicates the priority that you want to use for your lookup. For more information on filters see, [Lookup builder](../yield-analytics-ui/lookup-builder.md). <br> **Example response:** <br> ```{ "total": 20, "name": "Priority", "options": [ { "name": "20", "value": "20" }, { "name": "19", "value": "19" }, { "name": "18", "value": "18" }, { "name": "17", "value": "17" }, { "name": "16", "value": "16" }, { "name": "15", "value": "15" }, { "name": "14", "value": "14" }, { "name": "13", "value": "13" }, { "name": "12", "value": "12" }, { "name": "11", "value": "11" }, { "name": "10", "value": "10" }, { "name": "9", "value": "9" }, { "name": "8", "value": "8" }, { "name": "7", "value": "7" }, { "name": "6", "value": "6" }, { "name": "5", "value": "5" }, { "name": "4", "value": "4" }, { "name": "3", "value": "3" }, { "name": "2", "value": "2" }, { "name": "1", "value": "1" } ], "id": "PRIORITY" } ``` <br> **NOTE:** This filter helps you identify the available options and understand how they can be applied when the priority filter is used. | true | string |
| PathParameter | roadblock | Indicates whether to include roadblocked inventory in the lookup. <br> **Example response:** <br> ```{ "total": 4, "name": "Roadblock", "options": [ { "name": "All", "value": "all" }, { "name": "As Many", "value": "as_many" }, { "name": "Only One", "value": "only_one" }, { "name": "One Or More", "value": "one_or_more" } ], "id": "ROADBLOCK" } ``` <br> **NOTE:** This filter helps you identify the available options and understand how they can be applied when the roadblock filter is used. | true | string |
| PathParameter | page_effects | A flag indicating whether page-level constraints (such as “one impression per page” or displacement rules) should be applied during availability checks. When enabled, the forecast assumes stricter serving rules, reducing projected inventory. <br> **NOTE:** This filter helps you identify and return the available options when it’s used. | true | string |
| PathParameter | viewable | This setting allows you to run an availability check that includes additional viewability metrics. These are based on the historical viewable rate for a set of inventories that you are checking. <br> **Example response:** <br> ```{ "total": 2, "name": "Viewable", "options": [ { "name": "Yes", "value": "YES" }, { "name": "No", "value": "NO" } ], "id": "VIEWABLE" } ``` <br> **NOTE:** This filter helps you identify and return the available options when it's used. | true | string |
| PathParameter | frequency_cap | **Example response:** <br> ```{ "name": "Frequency Cap", "timePeriodOptions": [ "MINUTE", "HOUR", "DAY", "WEEK", "MONTH", "LIFETIME" ], "id": "FREQUENCY_CAP" } ``` <br> **NOTE:** This filter helps you identify and return the available options when a frequency cap is applied. | true | string |
| PathParameter | competitive_separation | This enables for refinements in availability lookup results by considering delivery restrictions due to advertiser and advertiser group restrictions. `competitive_separation` will exclude competitors' order lines from showing on the same page. For more information on filters see, [Lookup builder](../yield-analytics-ui/lookup-builder.md). <br> **NOTE:** This filter helps you identify and return the available options when it’s used. | true | string |
| PathParameter | order_line_exclusion | Allows exclusion of specific order lines from availability calculations or delivery. <br> NOTE: This filter helps you identify and return the available options when it’s used. | true | string |
| HeaderParameter | content-type | Specifies your request body format. | true | string |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/filters/GROUP_BY  \` -i -H 'Content-Type: application/json;charset=UTF-8'  
```

**Example cURL request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/filters/GROUP_BY
```

**Example cURL response**

```
{
  "total": 6,
  "name": "Group By",
  "options": [
    {
      "name": "Daily",
      "value": "daily"
    },
    {
      "name": "Weekly",
      "value": "weekly"
    },
    {
      "name": "Monthly",
      "value": "monthly"
    },
    {
      "name": "Quarterly",
      "value": "quarterly"
    },
    {
      "name": "Yearly",
      "value": "yearly"
    },
    {
      "name": "All",
      "value": "all"
    }
  ],
  "id": "GROUP_BY"
}
```

> [!NOTE]
> NOTE: This endpoint pattern can be used with any supported filter name, not just `GROUP_BY`. Use the following general format: 
> $ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/filters/{FILTER_NAME} 
> Supported filter names include: 
> - GROUP_BY 
> - PRIORITY 
> - FREQUENCY_CAP 
> - VIEWABLE 
> - PAGE_EFFECTS 
> - ROADBLOCK 
> - COMPETITIVE_SEPARATION 
> - ORDER_LINE_EXCLUSION 

## Batch method

Batch enables you to submit multiple inventory availability lookups in one request, each with different attribute variations (e.g. placement, size, priority, roadblock, etc.). 
Instead of making separate calls for each variation, you send them as a batch, and the system processes them concurrently for efficiency. Batch requests are constructed using the VaryBy endpoints, which define how specific attributes should vary across each lookup within the batch. This allows you to explore how different attribute combinations impact inventory availability in a single API call.

### REST API

| HTTP method | Endpoint | Description |
|---|---|---|
| POST | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/varyby` | Submits a batch request for varying by attributes. |
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/{batchqueueId}` | Fetches details of a specific batch by its ID. |
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch?take=100&skip=0&page=1&pageSize=100&sort=&filter=&noSpinner=true` | Lists all batches with summary information. |
| GET | `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/download?fileName={filename}` | Downloads a CSV or Excel file from ADLS. |

### Paths

#### Submit batch

```
POST /api/v1/rest/product/inventory/batch/varyby 
```

##### JSON fields

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| BodyParameter | targetExpression | Base targeting logic for inventory lookup. For example: browser in chrome, edge, safari. | true | string |
| BodyParameter | adServer | Optional field to specify ad server context. null means default. | false | string |
| BodyParameter | varybyExpression | Specifies which attribute(s) to vary by for multiple forecast slices. | true | array of objects |
| BodyParameter | batchRunFilters | Contains filters that you can apply to your lookup. | true | array of objects |
| BodyParameter | email | Email notification settings for batch completion. | true | array of objects |
| PathParameter | batch | Enables you to request groups multiple inventory availability checks into one API call for efficiency. | true | string |
| PathParameter | varyby | Enables you to request multiple inventory slices in one batch by varying specific attributes (For example, browser, device). | true | string |
| HeaderParameter | content-type | Specifies your request body format. | true | string | 

**varybyExpression object**

| Name | Description | Required | Schema |
|---|---|---|---|
| isNegated | Checks if the condition needs to be negated. <br> Supported values: <br> - False | true | boolean |
| attributeName | Attribute dimension to vary by. | true | string |
| operator | The operator specified by you, that’s used for the lookup. | true | string |
| attributeValues | Attributes to vary by in the lookup, provided by you. | true | strings |

**batchRunFilters object**

| Name | Description | Required | Schema |
|---|---|---|---|
| date_range | Defines the start and end date for the lookup. | true | string |
| group_by | Specifies how the results are displayed. This includes: <br> - Daily <br> - Weekly <br> - Monthly <br> - Quarterly <br> - Yearly <br> - All | true | string |
| priority | Indicates the priority you want to use for the lookup. Higher priority values mean the line item will compete more aggressively for impressions compared to lower-priority items. Used in filtering and forecasting to respect delivery hierarchy. | true | integer |
| multi_frequency_cap | Defines the frequency cap you want to apply to the lookup.| | true | string |
| viewable | Specifies if the forecast needs to be applied to the lookup or not. When set to true, only inventory meeting viewability criteria is included in availability. | true | string |
| roadblock | Indicates whether to include roadblocked inventory in the lookup. | true | string |
| page_effects | A flag indicating whether page-level constraints (such as “one impression per page” or displacement rules) should be applied during availability checks. | true | string |
| contracted_cpm | Refers to the minimum and maximum Cost per mille (CPM) | true | string |
| order_line_exclusion | Allows exclusion of specific order lines from availability calculations or delivery. Useful for avoiding conflicts with other campaigns or honoring contractual obligations. | true | string |
| competitive_separation | Specifies if you want to apply a competitive separation to your lookup. This enables for refinements in availability lookups results by considering delivery restrictions due to advertiser and advertiser group restrictions. Competitive Separation will exclude competitors' order lines from showing on the same page. For more information on filters see, [Lookup builder](../yield-analytics-ui/lookup-builder.md). | true | string |


**email object**

| Name | Description | Required | Schema |
|---|---|---|---|
| enabled | When set to true , it sends email notifications. | true | boolean |
| disablePrimary | Skips sending to primary user. <br> **NOTE:** when "disablePrimary": true email won't be sent to current user performing the lookup and instead will be sent to email address under "recipients". | true | boolean |
| recipients  | Array of email addresses. <br> **NOTE:** if disablePrimary is set to true, you will need to specify the alternative email address, instead.| true | strings |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/api/v1/rest/product/inventory/batch/varyby \ ` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example request**

```
POST /api/imf/api/v1/rest/product/inventory/batch/varyby
{
  "targetExpression": "placement in ('ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111')",
  "varybyExpression": {
    "terms": [
      {
        "isNegated": true,
        "attributeName": "size",
        "operator": "IN",
        "attributeValues": ["300x100", "320x50", "728x90"]
      }
    ]
  },
  "adServer": null,
  "batchRunFilters": {
    "configFilters": {
      "filters": [
        { "id": "DATE_RANGE", "startDate": "12/01/2025", "endDate": "12/30/2025" },
        { "id": "GROUP_BY", "value": "all" }
      ]
    },
    "advancedFilters": {
      "filters": [
        { "id": "PRIORITY", "value": "20" },
        {
          "id": "MULTI_FREQUENCY_CAP",
          "value": "MULTI_FREQUENCY_CAP",
          "data": [{ "value": "15", "numberOfPeriods": 1, "timePeriod": "WEEK" }]
        },
        { "id": "VIEWABLE", "value": "true" },
        { "id": "PAGE_EFFECTS", "value": "true" },
        { "id": "DISPLACEMENT", "value": "false" },
        { "id": "ROADBLOCK", "selectedOptions": [{ "name": "As Many", "value": "as many" }] },
        { "id": "CONTRACTED_CPM", "minVal": 1, "maxVal": 2 },
        {
          "id": "ORDER_LINE_EXCLUSION",
          "selectedOptions": [
            {
              "name": "ABC",
              "value": "11"
            }
          ]
        },
        {
          "id": "COMPETITIVE_SEPARATION",
          "selectedOptions": [
            { "name": "ABC Inc", "value": "ABC Inc" },
            { "name": "XYZ Insurance", "value": "XYZ Insurance" }
          ]
        }
      ]
    }
  },
  "email": {
    "enabled": true,
    "disablePrimary": true,
    "recipients": ["abc@contoso.com"]
  }
}
```

**Example response**

```
{ 
 { 
    "batchName": "{batchName}", 
    "queueId": {queryID} 
}  
} 
```

**Get batch details by queue ID**


```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/{queueId}` 
```

**JSON fields**

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| BodyParameter | fetchVaryByBatch | Fetches details of a specific batch by its ID. | true | string |
| PathParameter | queueId | Identifier for queued batch job. Used to fetch results later. | true | integer |
| HeaderParameter | content-type | Specifies your request body format. | true | string |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/api/v1/rest/product/inventory/batch/0  \ ` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/varyby
```

**Example HTTP response**

```
{ 
 "batchName": "ABC_rows", 
 "queueId": 0  
} 
```

**Get batch results by queue ID**


```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/results/{queueID}` 
```

**JSON fields**

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| BodyParameter | fetchVaryByBatch | Fetches details of a specific batch by its ID. | true | string |
| PathParameter | queueId | Identifier for queued batch job. Used to fetch results later. | true | integer |
| HeaderParameter | content-type | Specifies your request body format. | true | string |
| HeaderParameter | source | Your client source for accessing the Yield Analytics API. | true | string |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/results/3  \ ` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example HTTP request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/results/3 
```

**Example HTTP response**

```
{
  "count": 3,
  "results": [
    {
      "pageeffects": "Yes",
      "targetExpression": "placement in ('ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111')" and size in ('300x100')",
      "roadblockcapacity": 111,
      "viewabledeliverymultiplier": 0,
      "viewablecapacity": 111,
      "range": "12/01/25 - 12/30/25",
      "roadblockavailability": 111,
      "availability": 11,
      "priority": "20",
      "contractedcpm": "1 - 2",
      "capacity": 111,
      "viewable": 111,
      "name": placement in ('military_desktop_fparticle2 – 111', 'ABC – 111', 'DEF – 111', 'ABC – 111', 'DEF – 111', 'XYZ – 111', 'ABC – 111', 'XYZ – 111', 'ABC – 111') and size in ('300x100')",
      "roadblock": "As Many",
      "frequencycap": "15 per 1 Week(s)"
    },
    {
      "pageeffects": "Yes",
      "targetExpression": "placement in ('ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111')" and size in ('320x50')",
      "roadblockcapacity": 111,
      "viewabledeliverymultiplier": 0,
      "viewablecapacity": 111,
      "range": "12/01/25 - 12/30/25",
      "roadblockavailability": 111,
      "availability": 111,
      "priority": "20",
      "contractedcpm": "1 - 2",
      "capacity": 111,
      "viewable": 111,
      "name": placement in ('ABC – 111', 'XYZ – 111', 'DEF – 111', 'ABC – 111', 'ABC – 111', 'XYZ – 111', 'ABC – 111', 'XYZ – 111', 'ABC – 111') and size in ('320x50')",
      "roadblock": "As Many",
      "frequencycap": "15 per 1 Week(s)"
    },
    {
      "pageeffects": "Yes",
      "targetExpression": "placement in ('ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111', 'ABC - 111', 'XYZ - 111', 'DEF - 111')" and size in ('728x90')",
      "roadblockcapacity": 111,
      "viewabledeliverymultiplier": 0,
      "viewablecapacity": 111,
      "range": "12/01/25 - 12/30/25",
      "roadblockavailability": 111,
      "availability": 111,
      "priority": "20",
      "contractedcpm": "1 - 2",
      "capacity": 111,
      "viewable": 111,
      "name": placement in ('ABC – 111', 'DEF – 111', 'XYZ – 111', 'ABC – 111', 'DEF - 111', 'ABC – 111', 'DEF – 111', 'XYZ – 111', 'ABC - 111') and size in ('728x90')",
      "roadblock": "As Many",
      "frequencycap": "15 per 1 Week(s)"
    }
  ]
}
```

**Get multiple batches**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/` 
```

**JSON fields**

| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| BodyParameter | fetchVaryByBatches | Lists all batches with summary information. | true | string |
| QueryParameter | UriInfo | UriInfo is an object or field that provides the URI (Uniform Resource Identifier) details for the batch job or its associated resources. | true | integer |
| HeaderParameter | content-type | Specifies your request body format. | true | string |
| HeaderParameter | source | Your client source for accessing the Yield Analytics API. | true | string |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/api/v1/rest/product/inventory/ batch?take=100&skip=0&page=1&pageSize=100&sort=&filter=&noSpinner=true' \ ` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example HTTP request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/ batch?take=100&skip=0&page=1&pageSize=100&sort=&filter=&noSpinner=true`
```

**Example HTTP response**

```
[
  {
    "id": 0,
    "name": "{name}",
    "items": 3,
    "progress": 1,
    "startTime": "2025-10-27 20:48:47 UTC",
    "createdBy": "{createdBy}"
  },
  {
    "id": 1,
    "name": "{name}",
    "items": 3,
    "progress": 1,
    "startTime": "2025-10-27 20:53:38 UTC",
    "createdBy": "{createdBy}"
  }
]
```

**Download batch (CSV, xlsx)**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/download` 
```

**JSON fields**
| Type | Name | Description | Required | Schema |
|---|---|---| ---|---|
| QueryParameter | fileName | The name assigned to the output file containing batch results. | true | string |
| PathParameter | downloadFile | Downloads a CSV or Excel file from ADLS. | true | string |
| HeaderParameter | content-type | Specifies your request body format. | true | string |
| HeaderParameter | source | Your client source for accessing the Yield Analytics API. | true |

##### Example

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/attributes/api/v1/rest/product/inventory/ batch/download?fileName=Abc%40PL11716-Sep_02_2025_20_42_49PM%200000-3_rows.csv' \ ` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example HTTP request**

```
$ curl `https://api.appnexus.com/imf/api/v1/rest/product/inventory/batch/download?fileName=abc@contoso.com-Oct_27_2025_20_53_38PM+0000-3_rows.xlsx' \ ` -i -H 'Content-Type: application/json;charset=UTF-8' 
```

**Example HTTP response**

```
{Binary file content (XLSX or CSV format)}
```


## Related topics

- [Yield Analytics API](yield-analytics-api.md)
