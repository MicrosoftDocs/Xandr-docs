---
title: Query Engine Service
description: In this article, understand what query engine service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Query engine service

## Overview

The Yield Analytics API and services are exposed via a REST based interface. It is intended to make development of custom functionality comfortable to developers experienced with Web 2.0, AJAX, REST, and service oriented development platforms. Developers should have familiarity with web based application paradigms including AJAX, XML, JSON, and the HTTP(S) protocol prior to attempting development with the Yield Analytics API and services.

The Query Engine service permits the API developer access to a very flexible engine for querying data from the Yield Analytics system to accomplish use cases not accounted for with the Product Discovery and Inventory APIs. While the Query Engine Service’s flexibility and power permit many use cases to be accomplished, only deeply knowledgeable users should attempt to form a Query Engine query to insure valid data is extracted. Please contact your Yield Analytics customer service contact to help develop the query expressions required to achieve your data goal.

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

## Paths

### Execute saved analysis

```
GET /api/v1/rest/queryengine/analysis/{savedAnalysisId}
```

- **Description**

  Look up a saved analysis. These reports can be configured within the Yield Analytics UI or through the Yield Analytics API and then referenced by report ID.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | savedAnalysisId | savedAnalysisId | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**
  
  application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  Query Engine Resource


- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysis/100' 
  -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 
  'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/queryengine/analysis/100 HTTP/1.1
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
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute saved analysis with row count

```
GET /api/v1/rest/queryengine/analysis/{savedAnalysisId}/{rowCount}
```

- **Description**

  Look up a saved analysis with a row count. These reports can be configured within the Yield Analytics UI or through the Yield Analytics API and then referenced by report ID and the result can be limited to the desired number of rows.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | savedAnalysisId | savedAnalysisId | true | string |
  | PathParameter | rowCount | rowCount | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**
  
  application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysis/100/1' -i -H 'Content-Type: application/json' -H 
  'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/queryengine/analysis/100/1 HTTP/1.1
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
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute saved analysis with row count and row start

```
GET /api/v1/rest/queryengine/analysis/{savedAnalysisId}/{rowCount}/{startRow}
```

- **Description**

  Look up a saved analysis with a row count and start row. These reports can be configured within the Yield Analytics UI or through the Yield Analytics API and then referenced by report ID. The row count and row start parameters allow for paging through the report rows.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | savedAnalysisId | savedAnalysisId | true | string |
  | PathParameter | rowCount | rowCount | true | integer (int32) |
  | PathParameter | startRow | startRow | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  application/json

- **Produces**

  - application/xml
  - application/json

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysis/100/1/2' -i -H 'Content-Type: application/json' 
  -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/queryengine/analysis/100/1/2 HTTP/1.1
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
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute dynamic analysis

```
POST /api/v1/rest/queryengine/analysisdynamic
```

- **Description**

  Execute Dynamic Analysis.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamic' -i 
  -X POST -H 'Content-Type: application/json;charset=UTF-8' 
  -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamic HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute dynamic analysis

```
GET /api/v1/rest/queryengine/analysisdynamic/{reportDefinition}
```

- **Description**

  Execute Dynamic Analysis.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamic' -i 
  -X POST -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamic HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute dynamic analysis with row count

```
GET /api/v1/rest/queryengine/analysisdynamic/{reportDefinition}/{rowCount}
```

- **Description**

  Execute Dynamic Analysis with a Row Count.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | PathParameter | rowCount | rowCount | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamic/1' -i -X POST -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
    
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamic/1 HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute dynamic analysis with row count and row start

```
GET /api/v1/rest/queryengine/analysisdynamic/{reportDefinition}/{rowCount}/{startRow}
```

- **Description**

  Execute Dynamic Analysis with a Row Count and Row Start.

- **Parameters**

  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | PathParameter | rowCount | rowCount | true | integer (int32) |
  | PathParameter | startRow | startRow | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
   $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamic/1/2' -i -X POST 
     -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamic/1/2 HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute dynamic analysis with row count

```
POST /api/v1/rest/queryengine/analysisdynamic/{rowCount}
```

- **Description**

  Execute Dynamic Analysis with a Row Count.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | PathParameter | rowCount | rowCount | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamic/1' -i -X POST 
  -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamic/1 HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Execute dynamic analysis with row count and row start

```
POST /api/v1/rest/queryengine/analysisdynamic/{rowCount}/{startRow}
```

- **Description**

  Execute Dynamic Analysis with a Row Count and Row Start.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | PathParameter | rowCount | rowCount | true | integer (int32) |
  | PathParameter | startRow | startRow | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |  

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
   $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamic/1/2' -i -X POST 
  -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamic/1/2 HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Get a dynamic analyzer report by report definition using POST

```
POST /api/v1/rest/queryengine/analysisdynamicchart
```

- **Description**

  Reports defined by a reporting definition can be dynamically retrieved from the Target Analyzer.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |  

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

### Get a dynamic analyzer report by report definition using GET

```
GET /api/v1/rest/queryengine/analysisdynamicchart/{reportDefinition}
```

- **Description**

  Reports defined by a reporting definition can be dynamically retrieved from the Target Analyzer.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | reportDefinition | reportDefinition | true | [Report](#report) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [CountResponse](#countresponse) |
  
- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/analysisdynamicchart/' -i -X POST 
  -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/analysisdynamicchart/ HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 1889

  {
    "report" : {
      "additionalDimensions" : [ {
        "additionalDimension" : {
          "key" : "CHANNEL"
        }
      } ],
      "additionalMetrics" : [ {
        "additionalMetric" : {
          "key" : "CHANNEL_EARNED_REVENUE_PRODUCT"
        }
      } ],
      "dimensionFilters" : [ {
        "filter" : {
          "name" : "TARGET_TYPE",
          "value" : "REPORTING",
          "operator" : "include"
        }
      } ],
      "leftYAxis" : "IMPRESSION_CAPACITY",
      "metricFilters" : [ {
        "entry" : {
          "string" : "tab1",
          "list" : {
            "filter" : [ {
              "name" : "INVENTORY_CLASS",
              "value" : "Guaranteed",
              "operator" : "include"
            } ]
          }
        }
      } ],
      "pageSize" : 25,
      "rightYAxis" : "None",
      "selectedTab" : "tab1",
      "sortBy" : "DESCENDING_LEFT_Y_AXIS",
      "stackBy" : "",
      "dashboardDateRange" : {
        "type" : "last",
        "rangeLength" : 1,
        "rangeUnits" : "months",
        "customPeriod" : false,
        "trimToRemainderOfCustomPeriod" : false
      },
      "widgetFilter" : {
        "reportParamType" : "MULTI_REPORT",
        "defaultSelections" : "PRODUCT",
        "selectionLabels" : "By Product,By Advertiser",
        "selectionValues" : "PRODUCT,ADVERTISER"
      },
      "tabDateRanges" : [ {
        "entry" : {
          "string" : "tab1",
          "dateRange" : {
            "type" : "current",
            "customPeriod" : false,
            "trimToRemainderOfCustomPeriod" : false
          }
        }
      } ],
      "tablePageSize" : 25,
      "tableState" : {
        "ascending" : false,
        "columnOrdering" : {
          "string" : [ "string" ]
        },
        "sortBy" : "IMPRESSION_CAPACITY"
      },
      "tabs" : [ {
        "tab" : {
          "displayName" : "Dataset1",
          "id" : "tab1",
          "name" : "Dataset1",
          "selected" : true
        }
      } ],
      "xAxis" : "FOCUSED_EARNED_REVENUE"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 118

  {
    "successfulStatements" : [ "sample successful statement" ],
    "failedStatements" : [ "sample failed statement" ]
  }
  ```

### Batch query POST

```
POST /api/v1/rest/queryengine/batch
```

- **Description**

  The Query Engine Service batch call can run an arbitrary sequence of SQL statements and return a result set. These may be used to perform CRUD operations and or selects.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | queryStringRequest | queryStringRequest | true | [QueryStringRequest](#querystringrequest) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [CountResponse](#countresponse) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/batch' -i 
  -X POST -H 'Content-Type: application/json;charset=UTF-8' -d 
  '{
    "query" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2010-07-01','2010-07-31') 
     group by consumption_date order by consumption_date asc",
    "batchQueryParams" : [ {
      "first" : "INVENTORY_CLASS",
      "second" : [ "GUARANTEED" ]
    } ]
  }'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/batch HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 268

  {
    "query" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2010-07-01','2010-07-31') 
     group by consumption_date order by consumption_date asc",
    "batchQueryParams" : [ {
      "first" : "INVENTORY_CLASS",
      "second" : [ "GUARANTEED" ]
    } ]
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 326

  {
    "queryString" : "SELECT * FROM TABLE",
    "batchQueryResults" : [ {
      "batchId" : "1",
      "batchParams" : "sample batch param",
      "resultData" : {
        "row" : [ {
          "columnData" : [ {
            "name" : "sample name",
            "value" : "sample value"
          } ]
        } ]
      },
      "resultCode" : 1
    } ]
  }
  ```

### Batch query GET

```
GET /api/v1/rest/queryengine/batch/{queries}/{query}
```

- **Description**

  The Query Engine Service batch call can run an arbitrary sequence of SQL statements and return a result set. These may be used to perform CRUD operations and or selects.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | queries | queries | true | string |
  | BodyParameter | queryVars | queryVars | false | object |
  | PathParameter | query | query | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [BatchQueryResponse](#batchqueryresponse) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/batch/select%20consumption_date,
  %20sum(consumed)%20from%20OLPCS(network_products(),'2010-07-01','2010-07-31')
  %20group%20by%20consumption_date%20order%20by%20consumption_date%20ascconsumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5/select%20consumption_date,
  %20sum(consumed)%20from%20OLPCS(network_products(),'2010-07-01','2010-07-31')%20group%20by%20
  consumption_date%20order%20by%20consumption_date%20asc' -i -H 'Content-Type: application/json;charset=UTF-8' 
  -d '"{\"relativeDate\":\"2020-03-19\", \"title\":\"test\"}"'
  ```

- **Example HTTP Request**

  ```
  GET /api/v1/rest/queryengine/batch/select%20consumption_date,%20sum(consumed)%20from%20OLPCS(network_products(),
  '2010-07-01','2010-07-31')%20group%20by%20consumption_date%20order%20by%20consumption_date%20ascconsumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5/select%20consumption_date,
  %20sum(consumed)%20from%20OLPCS(network_products(),'2010-07-01','2010-07-31')%20group%20by%20consumption_date%
  20order%20by%20consumption_date%20asc HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 55

  "{\"relativeDate\":\"2020-03-19\", \"title\":\"test\"}"
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 326

  {
    "queryString" : "SELECT * FROM TABLE",
    "batchQueryResults" : [ {
      "batchId" : "1",
      "batchParams" : "sample batch param",
      "resultData" : {
        "row" : [ {
          "columnData" : [ {
            "name" : "sample name",
            "value" : "sample value"
          } ]
        } ]
      },
      "resultCode" : 1
    } ]
  }
  ```

### Execute statement using GET

```
GET /api/v1/rest/queryengine/execute/{statement}
```

- **Description**

  Execute an SQL statement passed through via the API.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | statement | statement | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [CountResponse](#countresponse) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/execute/select%20*%20from%20list_aliases()%20where%
  20data_source_type%20=%20'ORDER_LINE'' -i -H 'Content-Type: application/json' -H 'Accept: application/json' 
  -H 'username: {{username}}' -H 'password: {{password}}'

- **Example HTTP Request**

  ```
  GET /api/v1/rest/queryengine/execute/select%20*%20from%20list_aliases()%20where%20data_source_type%20=%20'ORDER_LINE' 
  HTTP/1.1
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
  Content-Length: 118

  {
    "successfulStatements" : [ "sample successful statement" ],
    "failedStatements" : [ "sample failed statement" ]
  }
  ```

### Execute statement using POST

```
POST /api/v1/rest/queryengine/execute/{statement}
```

- **Description**

  Execute an SQL statement passed through via the API.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | statement | statement | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  
- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [CountResponse](#countresponse) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/execute/select%20*%20from%20list_aliases()%20
  where%20data_source_type%20=%20'ORDER_LINE'' -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' 
  -H 'username: {{username}}' -H 'password: {{password}}'

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/execute/select%20*%20from%20list_aliases()%20where%20data_source_type%20=%20'ORDER_LINE' 
  HTTP/1.1
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
  Content-Length: 118

  {
    "successfulStatements" : [ "sample successful statement" ],
    "failedStatements" : [ "sample failed statement" ]
  }
  ```

### Execute SQL query statement by request object

```
POST /api/v1/rest/queryengine/executerequest
```

- **Description**

  Execute an SQL statement by passing in a Query Request object.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | statementHolder | statementHolder | true | [QueryRequest](#queryrequest) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [CountResponse](#countresponse) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/executerequest' -i 
  -X POST -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "queryRequest" : {
      "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
    }
  }'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/executerequest HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 194

  {
    "queryRequest" : {
      "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 118

  {
    "successfulStatements" : [ "sample successful statement" ],
    "failedStatements" : [ "sample failed statement" ]
  }
  ```

### Query by body statement

```
POST /api/v1/rest/queryengine/query
```

- **Description**

  Pass an SQL like statement as part of the body of a post.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | query | query | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |
  
- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/query' -i -X POST 
  -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
  }'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/query HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 167

  {
    "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Query by statement using GET

```
GET /api/v1/rest/queryengine/query/{query}
```

- **Description**

  Pass an SQL query as a path parameter. In order to execute multiple statements your statements need to be delimited by a semi-colon. In the case where data contains a semi-colon utilize the POST version of this call.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | query | query | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |
  
- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/query/select%20consumption_date,%20sum(consumed)%20
  from%20OLPCS(network_products(),'2010-07-01','2010-07-31')%20group%20by%20consumption_date%20order%20by%20consumption_date%20asc' 
  -i -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'username: {{username}}' 
  -H 'password: {{password}}'
  ```

- **Example HTTP Request**

  ```
  GET /api/v1/rest/queryengine/query/select%20consumption_date,%20sum(consumed)%20from%20OLPCS(network_products(),'2010-07-01',
  '2010-07-31')%20group%20by%20consumption_date%20order%20by%20consumption_date%20asc HTTP/1.1
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
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Query by statement using POST

```
POST /api/v1/rest/queryengine/query/{query}
```

- **Description**

  Pass an SQL query as a path parameter. In order to execute multiple statements your statements need to be delimited by a semi-colon. In the case where data contains a semi-colon utilize the POST version of this call.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | query | query | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |
  
- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/query/select%20consumption_date,
  %20sum(consumed)%20from%20OLPCS(network_products(),'2010-07-01','2010-07-31')%20group%20by%20consumption_date%20order%20by
  %20consumption_date%20asc' -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' 
  -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/query/select%20consumption_date,%20sum(consumed)%20from%20OLPCS(network_products(),
  '2010-07-01','2010-07-31')%20group%20by%20consumption_date%20order%20by%20consumption_date%20asc HTTP/1.1
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
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Query by query request

```
POST /api/v1/rest/queryengine/queryrequest/{decode}
```

- **Description**

  Pass a Query Request object to query the engine.

- **Parameters**
  
  | Type | Name | Description | Required | Schema | Default |
  |---|---|---|---|---|---|
  | BodyParameter | query | query | true | [QueryRequest](#queryrequest) |  |
  | QueryParameter | decode | decode | false | boolean | true |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |  |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |  |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/queryrequest/true' -i -X POST -H 
  'Content-Type: application/json;charset=UTF-8' -d '{
    "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
  }'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/queryrequest/true HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 167

  {
    "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') group by 
  consumption_date order by consumption_date asc"
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Query set using GET

```
GET /api/v1/rest/queryengine/queryset
```

- **Description**

  The Query Engine Service queryset call can run an arbitrary sequence of SQL statements and return a result set. These may be used to perform CRUD operations and or selects.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | querySet | querySet | true | [QuerySet](#queryset) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/queryset' -i -H 'Content-Type: application/json;
  charset=UTF-8' -d '{
    "querySet" : {
      "title" : "test",
      "relativeDate" : "2020-03-19",
      "requests" : [ {
        "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
      } ]
    }
  }'
  ```

- **Example HTTP Request**

  ```
  GET /api/v1/rest/queryengine/queryset HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 278

  {
    "querySet" : {
      "title" : "test",
      "relativeDate" : "2020-03-19",
      "requests" : [ {
        "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Query set using POST

```
POST /api/v1/rest/queryengine/queryset
```

- **Description**

  The Query Engine Service queryset call can run an arbitrary sequence of SQL statements and return a result set. These may be used to perform CRUD operations and or selects.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | BodyParameter | querySet | querySet | true | [QuerySet](#queryset) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryResultData](#queryresultdata) |

- **Consumes**

  - application/json
  - application/xml

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

- **Example cURL request**

  ```
  $ curl 'https://{{client_url}}/api/v1/rest/v1/rest/queryengine/queryset' -i -X POST -H 
  'Content-Type: application/json;charset=UTF-8' -d '{
    "querySet" : {
      "title" : "test",
      "relativeDate" : "2020-03-19",
      "requests" : [ {
        "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
      } ]
    }
  }'
  ```

- **Example HTTP Request**

  ```
  POST /api/v1/rest/queryengine/queryset HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://{{client_url}}/api/v1/rest
  Content-Length: 278

  {
    "querySet" : {
      "title" : "test",
      "relativeDate" : "2020-03-19",
      "requests" : [ {
        "sql" : "select consumption_date, sum(consumed) from OLPCS(network_products(),'2020-03-19','2020-06-19') 
  group by consumption_date order by consumption_date asc"
      } ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 115

  {
    "row" : [ {
      "columnData" : [ {
        "name" : "sample name",
        "value" : "sample value"
      } ]
    } ]
  }
  ```

### Reports defined and saved in the target analyzer may be executed as a REST based service

```
GET /api/v1/rest/queryengine/xml/{query}
```

- **Description**

  Get a saved Analyzer Report by ID.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | query | query that needs to be run | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**
  
  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [QueryEngineXML](#queryenginexml) |

- **Consumes**

  application/json

- **Produces**

  - application/json
  - application/xml

- **Tags**

  Query Engine Resource

## Functions

The Query Engine supports a large quantity of built-in generic database Functions. Yield Analytics functions are also in place to facilitate working with the Inventory Model.

| Function | Description | Example |
|---|---|---|
| ACTIVE_RATE_CARD_PRODUCTS | returns all the active rate card product ids (PIDs) in the system | TEST EXAMPLE |
| ACTIVE_REPORTING_PRODUCTS | returns all the active reporting products ids (PIDs) in the system | TEST EXAMPLE |
| ALL_RATE_CARD_PRODUCTS | returns all the rate card products ids (PIDs) in the system | TEST EXAMPLE |
| ALL_RATE_CARD_PRODUCTS | returns all the reporting products ids (PIDs) in the system | TEST EXAMPLE |
| PRODUCT_GROUP | groupNames<br>returns all the product ids in the target group with the given name | TEST EXAMPLE |
| PRODUCTS_BY_CHARACTERISTICS | characteristics - e.g. size=120x90, size=460x80, sex=male, behavioral!=political<br>return all the product ids matching the given characteristics | TEST EXAMPLE |
| PRODUCTS_BY_MATCHPRASE | matchphrases | TEST EXAMPLE |
| PRODUCTS_BY_NAME | names | TEST EXAMPLE |

## Aliases

| ALIAS_KEY | DATASOURCE_TYPE |
|---|---|
| ACTIONS | <ACTION_NAME>_TOTAL_ACTIONS_POST_IMPRESSIONS |
| ACTIONS | <ACTION_NAME>_TOTAL_ACTIONS |
| ACTIONS | <ACTION_NAME>_ECPA |
| ADVERTISER | ORDER_LINE |
| AGENCY | ORDER_LINE |
| AVAILABILITY | PRODUCT |
| AVERAGE_FREQUENCY_DAILY | PRODUCT |
| AVERAGE_FREQUENCY_WEEKLY | PRODUCT |
| AVERAGE_UNIQUES_DAILY | PRODUCT |
| AVERAGE_UNIQUES_WEEKLY | PRODUCT |
| BOOKED_CPM | ORDER_LINE |
| BOOKED_IMPRESSIONS | ORDER_LINE |
| BOOKED_VALUE | ORDER_LINE |
| BOOKING_TYPE | OLP_IMPRESSIONS |
| CAMPAIGN_NAME | ORDER_LINE |
| CLOSE_DATE | ORDER_LINE |
| CONSUMED_IMPRESSIONS | OLP_IMPRESSIONS |
| CONSUMED_IMPRESSIONS_LIFETIME | OLP_IMPRESSIONS |
| CONSUMED_VALUE | ORDER_LINE |
| CONSUMPTION_DATE | OLP_IMPRESSIONS |
| CONSUMPTION_TYPE | OLP_IMPRESSIONS |
| CONTRACT_TYPE | ORDER_LINE |
| CONTRACTED_CPD | ORDER_LINE |
| CONTRACTED_CPD_OLTP | OLTP |
| CONTRACTED_CPM | ORDER_LINE |
| CONTRACTED_IMPRESSIONS | ORDER_LINE |
| CONTRACTED_IMPRESSIONS_CPM_ONLY | ORDER_LINE |
| CONTRACTED_IMPRESSIONS_CPM_ONLY_OLTP | OLTP |
| CONTRACTED_IMPRESSIONS_GOAL_BASED_ONLY | ORDER_LINE |
| CONTRACTED_IMPRESSIONS_LIFETIME | ORDER_LINE |
| CONTRACTED_IMPRESSIONS_OLTP | OLTP |
| CONTRACTED_IMPRESSIONS_TOTAL | ORDER_LINE |
| CONTRACTED_IMPRESSIONS_UNDERDELIVERY_CALCULABLE | ORDER_LINE |
| CONTRACTED_RATE | ORDER_LINE |
| CONTRACTED_REVENUE | ORDER_LINE |
| CONTRACTED_REVENUE_CPD_ONLY | ORDER_LINE |
| CONTRACTED_REVENUE_CPD_ONLY_FULL | ORDER_LINE |
| CONTRACTED_REVENUE_CPD_ONLY_OLTP | OLTP |
| CONTRACTED_REVENUE_CPM_ONLY | ORDER_LINE |
| CONTRACTED_REVENUE_CPM_ONLY_FULL | ORDER_LINE |
| CONTRACTED_REVENUE_CPM_ONLY_OLTP | OLTP |
| CONTRACTED_REVENUE_FULL | ORDER_LINE |
| CONTRACTED_REVENUE_LIFETIME | ORDER_LINE |
| CONTRACTED_REVENUE_OLTP | OLTP |
| CONTRACTED_REVENUE_SALES_DISCOUNT_CALCULABLE | ORDER_LINE |
| CONTRACTED_REVENUE_SALES_DISCOUNT_CALCULABLE_FULL | ORDER_LINE |
| CONTRACTED_REVENUE_SALES_DISCOUNT_CALCULABLE_OLTP | OLTP |
| CONTRACTED_REVENUE_UNDERDELIVERY_CALCULABLE | ORDER_LINE |
| CONTRACTED_REVENUE_UNDERDELIVERY_CALCULABLE_OLTP | OLTP |
| CONTRACTED_REVENUE_UNDERDELIVERY_CALCULABLE_OLTP_LIFETIME | OLTP |
| CURRENT_PRODUCT_ID | ORDER_LINE |
| DATA_ELEMENTS_UNDERDELIVERY_CALCULABLE_OLTP_LIFETIME | OLTP |
| DAYS_IN_CPD_ONLY | ORDER_LINE |
| DAYS_IN_CPD_ONLY_OLTP | OLTP |
| DAYS_TO_DELIVERY | OLP_IMPRESSIONS |
| DAYS_TO_DELIVERY_CUM | OLP_IMPRESSIONS |
| DELIVERABLE_GUARANTEED_IMPRESSIONS | ORDER_LINE |
| DELIVERABLE_IMPRESSIONS | ORDER_LINE |
| DELIVERABLE_IMPRESSIONS_LIFETIME | ORDER_LINE |
| DELIVERABLE_IMPRESSIONS_UNDERDELIVERY_CALCULABLE | OLP_IMPRESSIONS |
| DELIVERABLE_IMPRESSIONS_UNDERDELIVERY_CALCULABLE_OLTP | OLTP |
| DELIVERABLE_IMPRESSIONS_UNDERDELIVERY_CALCULABLE_OLTP_LIFETIME | OLTP |
| DELIVERED_CLICKS | OLP_CLICKS |
| DELIVERED_CLICKS_LIFETIME | OLP_CLICKS |
| DIRECT_AVERAGE_FREQUENCY_DAILY | ORDER_LINE |
| DIRECT_AVERAGE_FREQUENCY_WEEKLY | ORDER_LINE |
| DIRECT_AVERAGE_UNIQUES_DAILY | ORDER_LINE |
| DIRECT_AVERAGE_UNIQUES_WEEKLY | ORDER_LINE |
| DIRECT_LIFETIME_UNIQUES | ORDER_LINE |
| EARNED_IMPRESSIONS | ORDER_LINE |
| EARNED_IMPRESSIONS_UNDERDELIVERY_CALCULABLE | ORDER_LINE |
| EARNED_REVENUE | ORDER_LINE |
| EARNED_REVENUE_LIFETIME | ORDER_LINE |
| EARNED_REVENUE_UNDERDELIVERY_CALCULABLE | ORDER_LINE |
| EARNED_REVENUE_UNDERDELIVERY_CALCULABLE_OLTP | OLTP |
| EARNED_REVENUE_UNDERDELIVERY_CALCULABLE_OLTP_LIFETIME | OLTP |
| END_DATE | ORDER_LINE |
| ESTABLISHED_ASP | PRODUCT |
| EXTERNAL_ID | ORDER_LINE |
| FLOOR | PRODUCT |
| FOCUSED_CONSUMED_VALUE | OLP_IMPRESSIONS |
| FOCUSED_EARNED_IMPRESSIONS | OLP_IMPRESSIONS |
| FOCUSED_EARNED_REVENUE | OLPEVENT |
| HARD_CUTOFF | ORDER_LINE |
| IMPRESSION_CAP_PER_DAY | ORDER_LINE |
| IMPRESSION_CAPACITY | PRODUCT |
| IN_NETWORK | ORDER_LINE |
| INDUSTRY | ORDER_LINE |
| INVENTORY_CLASS | ORDER_LINE |
| MASTER_ID | ORDER_LINE |
| MC_TYPE | ORDER_LINE |
| NETWORK_STATUS | PRODUCT |
| ORDER | ORDER_LINE |
| ORDER_EXTERNAL_ID | ORDER_LINE |
| ORDER_LINE | ORDER_LINE |
| ORDER_LINE_DELIVERY_SCOPE_TARGET | ORDER_LINE |
| ORDER_LINE_ID | ORDER_LINE |
| ORDER_LINE_SITE_NAME | ORDER_LINE |
| ORDER_LINE_SIZE | ORDER_LINE |
| ORDER_LINE_STATUS | ORDER_LINE |
| ORDER_LINE_TARGET | ORDER_LINE |
| ORDER_LINE_TARGET_ATTRIBUTE | ORDER_LINE |
| ORDER_LINE_TARGET_EXPRESSION | ORDER_LINE |
| ORDER_LINE_TARGET_EXTERNAL_ID | ORDER_LINE |
| ORDER_LINE_TARGET_ID | ORDER_LINE |
| ORDER_NAME | ORDER_LINE |
| ORDER_STATE | ORDER_LINE |
| PACKAGE_ID | ORDER_LINE |
| PARENT_TARGET | PRODUCT |
| PRICING_TYPE | ORDER_LINE |
| PRIORITY | ORDER_LINE |
| PRODUCT | PRODUCT |
| PRODUCT | RATE_CARD |
| PRODUCT | REPORTING_TYPE |
| PRODUCT | REVENUE_CAPACITY |
| PRODUCT | SELL_STATUS |
| PRODUCT | STATUS |
| PRODUCT | TARGET_ATTRIBUTE |
| PRODUCT | TARGET_CREATION_DATE |
| PRODUCT | TARGET_GROUP |
| PRODUCT | TARGET_ID |
| PRODUCT | TARGET_OVERLAP |
| PRODUCT | TARGET_TYPE |
| PRODUCT | UNMET_DEMAND |
| PRODUCT | WEIGHTED_RATE_CARD |
| PRODUCT | <ACTION_NAME>_TOTAL_ACTIONS_POST_CLICKS |
| PRODUCT_EXPRESSION PRODUCT | PRODUCT_EXTERNAL_ID |
| RANGE_END | ORDER_LINE |
| RANGE_START | ORDER_LINE |
| RATE_CARD_REVENUE | ORDER_LINE |
| RATE_CARD_REVENUE_CPM_ONLY | ORDER_LINE |
| RATE_CARD_REVENUE_CPM_ONLY_OLTP | OLTP |
| RATE_CARD_REVENUE_SALES_DISCOUNT_CALCULABLE | ORDER_LINE |
| RATE_CARD_REVENUE_SALES_DISCOUNT_CALCULABLE_FULL | OLTP |
| RATE_CARD_REVENUE_SALES_DISCOUNT_CALCULABLE_OLTP | OLTP |
| SALES_PERSON | ORDER_LINE |
| SALES_TEAM_MEMBER | ORDER_LINE |
| SCHEDULED_IMPRESSIONS | ORDER_LINE |
| SCHEDULED_IMPRESSIONS_LIFETIME | ORDER_LINE |
| SCHEDULED_IMPRESSIONS_OLTP | OLTP |
| SCHEDULED_IMPRESSIONS_UNDERDELIVERY_CALCULABLE | OLP_IMPRESSIONS |
| SCHEDULED_IMPRESSIONS_UNDERDELIVERY_CALCULABLE_OLTP | OLTP |
| SCHEDULED_IMPRESSIONS_UNDERDELIVERY_CALCULABLE_OLTP_LIFETIME | OLTP |
| SOLD_AS_PRODUCT | ORDER_LINE |
| SOLD_AS_PRODUCT_ID | ORDER_LINE |
| START_DATE | ORDER_LINE |
| SYSTEM_OF_RECORD | ORDER_LINE |
| TILE_IDS | ORDER_LINE |
| TILE_NAMES | ORDER_LINE |

## Definitions

### AdditionalDimension

A JSON object to hold the results of AdditionalDimension of Analyzer Report.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| groupingModifier | The grouping modifier of additional dimension | true | string |
| key | The key of additional dimension | true | string |
  
### AdditionalMetric

A JSON object to hold the results of AdditionalMetric of Analyzer Report.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| key | The key of additional dimension | true | string |

### AnalyzerReport

A JSON object to hold the results of AnalyzerReport.
  
| Name | Description | Required | Schema |
|---|---|---|---|
| additionalDimensions | A collection of additional dimensions | false | MapOfstringAndAdditionalDimension array |
| additionalMetrics | A collection of additional metrics | false | MapOfstringAndAdditionalMetric array |
| dashboardDateRange | The dashboard date rage of the analyzer report | false | [DateRangeData](#daterangedata) |
| dashboardDimension | The dashboard dimension of the analyzer report | false | string |
| dashboardTableData | The dashboard table data of the analyzer report | false | [TableState](#tablestate) |
| dateRange | The date range of the analyzer report | false | [DateRangeData](#daterangedata) |
| dateRangeFilters | A collection of report date range filters | false | MapOfstringAndReportDateRangeFilter array |
| dimensionFilters | A collection of dimension filters | false | MapOfstringAndFilter array |
| includeZeroValues | The include zero values field of the analyzer report | false | string |
| keyValueFilters | A collection of report key value filters | false | MapOfstringAndReportKeyValueFilter array |
| leftYAxis | The left Y axis of the analyzer report | true | string |
| metricFilters | The map of name to a list of metric filters | true | MapOfstringAndMetricFilterEntry array |
| numericRangeFilters | The field contains a list of numeric range filters | false | MapOfstringAndReportNumericRangeFilter array |
| orderBy | The order by field of the analyzer report | false | string |
| pageSize | The page size of the analyzer report | false | integer (int32) |
| rightYAxis | The right Y axis of the analyzer report | false | string |
| selectedTab | The selected tab of the analyzer report | false | string |
| sizeBy | The size by field of the analyzer report | false | string |
| sortBy | The sort by field of the analyzer report | false | string |
| stackBy | The stack by field of the analyzer report | false | string |
| stackbyIncrement | The stack by increment field of the analyzer report | false | string |
| tabDateRanges | The map of name to table date ranges | true | MapOfstringAndDateRangeEntry array |
| tablePageSize | The table page size of analyzer report | false | integer (int32) |
| tableState | The table state of the analyzer report | false | [TableState](#tablestate) |
| tabs | The field contains a list of tabs | true | MapOfstringAndTab array |
| trendPoints | A collection of trend point | false | MapOfstringAndTrendPoint array |
| view | The view of the analyzer report | false | string |
| widgetCacheWarm | The widget cache warm field of the analyzer report | false | string |
| widgetFilter | The widget filter of the analyzer report | false | [WidgetFilter](#widgetfilter) |
| widgetNumericType | The widget numeric type of the analyzer report | false | enum (NEGATIVE_ONLY, POSITIVE_ONLY) |
| widgetView | The widget view of the analyzer report | false | string |
| xAxis | The x Axis of the analyzer report | true | string |
| xAxisIncrement | The x Axis increment of the analyzer report | false | string |

### BatchQueryParams

A JSON object to hold the batch query params.

| Name | Description | Required | Schema |
|---|---|---|---|
| first | The first field of the batch query params | true | string |
| second | A collection of second fields | true | string array |

### BatchQueryResponse

A JSON object to hold the results of a batch query response.

| Name | Description | Required | Schema |
|---|---|---|---|
| batchQueryResults | A collection of batch query results | false | [BatchQueryResult](#batchqueryresult) array |
| queryString | The query string of the batch query response | true | string |

### BatchQueryResult

A JSON object to hold the results of a batch query result.

| Name | Description | Required | Schema |
|---|---|---|---|
| batchId | The batch ID of the batch query result | true | string |
| batchParams | The batch params of the batch query result | true | string |
| resultCode | The result code of the batch query result | true | integer (int32) |
| resultData | The query result data of the batch query result | true | [QueryResultData](#queryresultdata) |

### Column

| Name | Description | Required | Schema |
|---|---|---|---|
| name | The name of header | false | string |
| value | The value of header | false | string |

### ColumnData

A JSON object to hold the results of a column data.

| Name | Description | Required | Schema |
|---|---|---|---|
| name | The name of the column data | true | string |
| value | The value object of the column data | true | string |

### ColumnFilter

A JSON object to hold the results of ColumnFilter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| field | The field of the column filter | true | string |
| logic | The logic of the column filter | true | string |
| operator | A collection of operators | true | string array |
| value | A collection of values | true | string array |

### ColumnSort

A JSON object to hold the results of ColumnSort of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| direction | The direction of the column sort | true | string |
| field | The field of the column sort | true | string |

### CountResponse

A JSON object to hold the results of a count response.

| Name | Description | Required | Schema |
|---|---|---|---|
| failedStatements | The count of failed statements | false | string array |
| successfulStatements | The count of succesful statements | false | string array |

### DateRangeData

A JSON object to hold the results of DateRangeData of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| customCalendarId | The custom calendar id of the date range data | false | string |
| customPeriod | THe custom period field of the date range data | false | boolean |
| endDate | The end date of the date range data | false | string |
| rangeLength | The range length of the date range data | false | integer (int32) |
| rangeUnits | The range units of the date range data | false | string |
| startDate | The start date of the date range data | false | string |
| trimToRemainderOfCustomPeriod | The trim to remainder of custom period field of the date range data | false | boolean |
| type | The type of the date range data | true | string |

### DateRangeEntry

A JSON object to hold DateRangeEntry.

| Name | Description | Required | Schema |
|---|---|---|---|
| dateRange | The dateRange field of the DateRangeEntry | false | [DateRangeData](#daterangedata) |
| string | The string field of the DateRangeEntry | true | string |

### Filter

A JSON object to hold the results of Filter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| name | The name of the filter | true | string |
| operator | The operator of the filter | true | string |
| value | The value of the filter | true | string |

### Header

A JSON object to hold the results of Filter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| generated | The generated string of header | false | string |
| query | The query string of header | false | string |

### MetricFilterEntry

A JSON object to hold MetricFilterEntry.

| Name | Description | Required | Schema |
|---|---|---|---|
| list | A collection of filters | false | object |
| string | The string field of the MetricFilterEntry | true | string |

### QueryEngineXML

A JSON object to hold the query result.

| Name | Description | Required | Schema |
|---|---|---|---|
| header | The header of query engine xml | true | [Header](#header) |
| resultSet | The result set of query engine xml | true | [ResultSet](#resultset) |

### QueryRequest

A JSON object to hold the query result.

| Name | Description | Required | Schema |
|---|---|---|---|
| queryRequest |  | false | [QueryRequest](#queryrequest) |
| sql | The SQL input to the query engine | true | string |

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

### QuerySet

A JSON object to hold the results of a query result data.

| Name | Description | Required | Schema |
|---|---|---|---|
| querySet |  | false | QuerySet |
| relativeDate | The relative data of the query set | true | string |
| requests | A collection of query requests | false | [QueryRequest](#queryrequest) array |
| title | The title of the query set | true | string |

### QueryStringRequest

A JSON object to hold the query string request.

| Name | Description | Required | Schema |
|---|---|---|---|
| batchQueryParams | A collection of batch query params | true | [BatchQueryParams](#batchqueryparams) array |
| query | The query field of the query string request | true | string |

### Report

A JSON object to hold the query string request.

| Name | Description | Required | Schema |
|---|---|---|---|
| report |  | false | [AnalyzerReport](#analyzerreport) |

### ReportDateRangeFilter

A JSON object to hold the results of ReportDateRangeFilter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| dataSetKey | The data set key of the report date range filter | true | string |
| dateRange | The date range data of the report date range filter | true | [DateRangeData](#daterangedata) |
| key | The key of the report date range filter | true | string |

### ReportKeyValueFilter

A JSON object to hold the results of ReportKeyValueFilter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| dataSetKey | The data set key of the report key value filter | true | string |
| key | The key of the report key value filter | true | string |
| name | The name of the report key value filter | true | string |
| operator | The operator of the report key value filter | true | string |
| value | The value of the report key value filter | true | string |
| valueMatchTypeValue | The value match type value of the report key value filter | true | string |

### ReportNumericRangeFilter

A JSON object to hold the results of ReportNumericRangeFilter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| dataSetKey | The data set key of the report numeric range filter | true | string |
| highValue | The high value of the report numeric range filter | true | number (double) |
| id | The ID of the report numeric range filter | true | integer (int32) |
| key | The key of the report numeric range filter | true | string |
| lowValue | The low value of the report numeric range filter | true | number (double) |

### ResultSet

A JSON object to hold the results of ReportNumericRangeFilter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| rows | A collection of rows | false | [Row](#row) array |

### Row

| Name | Description | Required | Schema |
|---|---|---|---|
| columns | A collection of columns | false | [Column](#column-1) array |

### Column

| Name | Description | Required | Schema |
|---|---|---|---|
| name | The name of header | false | string |
| value | The value of header | false | string |

### RowData

A JSON object to hold the results of a row data.

| Name | Description | Required | Schema |
|---|---|---|---|
| columnData | A collection of column data | true | [ColumnData](#columndata) array |

### Tab

A JSON object to hold the results of Tab of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| displayName | The display name of the tab | true | string |
| id | The ID of the tab | true | string |
| name | The name of the tab | true | string |
| selected | The selected field of the tab | true | boolean |

### TableState

A JSON object to hold the results of TableState of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| ascending | The ascending field of the table state | true | boolean |
| columnFilters | A collection of column filters | false | [ColumnFilter](#columnfilter) array |
| columnOrdering | A collection of column ordering | true | object |
| columnSorts | A collection of column sorts | false | [ColumnSort](#columnsort) array |
| key | The key of the table state | false | string |
| sortBy | The sort by field of the table state | true | string |

### TrendPoint

A JSON object to hold the results of TrendPoint of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| key | The key of the trend point | true | string |

### WidgetFilter

A JSON object to hold the results of WidgetFilter of Analyzer Report.

| Name | Description | Required | Schema |
|---|---|---|---|
| defaultSelections | The default selections of the widget filter | true | string |
| reportParamType | The report param type of the widget filter | true | string |
| selectionLabels | The selection labels of the widget filter | true | string |
| selectionValues | The selection values of the widget filter | true | string |

## Related topic

[Yield Analytics API](yield-analytics-api.md)
