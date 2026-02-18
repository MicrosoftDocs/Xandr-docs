---
title: Data Analytics API - Insertion Order Service
description: In this article, understand what insertion order service is and the various features and functions associated with it.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Data Analytics API - Insertion order service

## Overview

The Yield Analytics API and services are exposed via a REST based interface. It is intended to make development of custom functionality comfortable to developers experienced with Web 2.0, AJAX, REST, and service oriented development platforms. Developers should have familiarity with web-based application paradigms including AJAX, XML, JSON, and the HTTP(S) protocol prior to attempting development with the Yield Analytics API and services.

The Insertion Order Service currently exposes interfaces related to:

- Guaranteed Delivery and Capacity of Line Items at the Order Level
- Historical Delivery of Line Items at the Order Level

## Content types

The Service REST API is currently designed to support the following content type:

- JSON - using `Content-type: application/json`

Selecting the desired content type is a choice the API developer should make on a case by case basis. API functionality is symmetrical across content types. API developers may specify the desired content type in the HTTP GET or POST method parameters or via their AJAX or HTTP client library.

## Error checking and status codes

API developers should check the HTTP response codes returned from the service REST API to detect errors propagated from API calls. Successful calls to the service will result in 200 range response codes. 400 and 500 range http responses denote errors. The specific response codes and text will likely undergo change during BETA development of the API, however, the ranges will not.

## Security

The service API exposes application data in a secure manner. Use of API functionality is restricted to authenticated users and is exposed over secure transport protocols. Access to the API must take place within the following context:

### Authentication
For more infromation on authentication, see [Yield Analytics API - Authentication Process](api-authentication.md).


## Confidentiality

Confidentiality is maintained by using Secure Socket Layer based communication to interact with the Yield Analytics API. API developers should prefer use of HTTPS over HTTP insecure communication whenever possible. Consult your HTTP Client library on how to enable HTTP over SSL when developing outside of a web browser context.

## Host

```
https://api.appnexus.com/imf/
```

## Paths

### Get guaranteed capacity for single order

```
GET /api/v1/rest/order/capacity/future/{externalId}/{nbDays}
```

- **Description**

  Get guaranteed delivery dynamic capacity as CSV for a particular timezone.

- **Parameters**

  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |  

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
  $ curl 'https://api.appnexus.com/imf/v1/rest/order/capacity/future/1/1' -i -H 'Content-Type: application/json' 
    -H 'Accept: application/json' -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/order/capacity/future/1/1 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://api.appnexus.com/imf/
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 2567
            
  [ {
  "externalId" : "1",
  "nextHours" : {
  "20200619T05:00+1000" : 1000,
  "20200619T12:00+1000" : 1000,
  "20200619T06:00+1000" : 1000,
  "20200619T13:00+1000" : 1000,
  "20200619T20:00+1000" : 1000,
  "20200619T04:00+1000" : 1000,
  "20200619T07:00+1000" : 1000,
  "20200619T21:00+1000" : 1000,
  "20200619T03:00+1000" : 1000,
  "20200619T10:00+1000" : 1000,
  "20200619T08:00+1000" : 1000,
  "20200619T11:00+1000" : 1000,
  "20200619T02:00+1000" : 1000,
  "20200619T17:00+1000" : 1000,
  "20200619T00:00+1000" : 1000,
  "20200619T09:00+1000" : 1000,
  "20200619T16:00+1000" : 1000,
  "20200619T23:00+1000" : 1000,
  "20200619T18:00+1000" : 1000,
  "20200619T15:00+1000" : 1000,
  "20200619T01:00+1000" : 1000,
  "20200619T19:00+1000" : 1000,
  "20200619T14:00+1000" : 1000,
  "20200619T22:00+1000" : 1000
  },
  "nextDays" : {
  "20200619T00:00+1000" : 240000
  },
  "targetings" : [ {
  "start" : "2020-03-19",
  "end" : "2020-06-19",
  "expression" : "country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') 
  and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
  site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') 
  or country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
  segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
  site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4860908 in ('true') and 
  segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and 
  segment-3222990 in ('true') and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and 
  size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4836884 in ('true') and 
  segment-4860908 in ('true') or country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and 
  segment-3222990 in ('true') and segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and 
  size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4860908 in ('true') and 
  segment-4860941 in ('true')",
  "impressionCap" : 5,
  "impressionCapPeriod" : 77,
  "dynamic" : false
  } ]
  } ]       
  ```

### Get guaranteed delivery dynamic capacity as CSV for single timezone

```
GET /api/v1/rest/order/capacity/guaranteed/future/csv/{nbDays}/{timeZone}
```

- **Description**

  Get guaranteed delivery dynamic capacity as CSV for a particular timezone.

- **Parameters**

  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | string |

- **Consumes**

  test/csv

- **Produces**

  test/csv

- **Tags**

  Insertion Order Service End Points

### Get guaranteed delivery dynamic capacity as CSV by group of order id for double timezone

```
POST /api/v1/rest/order/capacity/guaranteed/future/orderids/csv/{nbDays}/{timeZone}/{timeZoneSecond}
```

- **Description**

  Get guaranteed delivery dynamic capacity as CSV for a group of orders within a timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | timeZoneSecond | timeZoneSecond | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | string |

- **Consumes**

  test/csv

- **Produces**

  test/csv

- **Tags**

  Insertion Order Service End Points

### Get guaranteed delivery dynamic capacity as CSV by group of order id for single timezone

```
POST /api/v1/rest/order/capacity/guaranteed/future/orderids/csv/{nbDays}/{timeZone}
```

- **Description**

  Get guaranteed delivery dynamic capacity as CSV for a group of orders within a timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | string |

- **Consumes**

  application/json

- **Produces**

  test/csv

- **Tags**

  Insertion Order Service End Points

### Get guaranteed delivery dynamic capacity as CSV by group of order id for double timezone

```
POST /api/v1/rest/order/capacity/guaranteed/future/orderids/csv/{nbDays}/{timeZone}/{timeZoneSecond}
```

- **Description**

  Get guaranteed delivery dynamic capacity as CSV for a group of orders for double timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | timeZoneSecond | timeZoneSecond | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | string |

- **Consumes**

  application/json

- **Produces**

  test/csv

- **Tags**

  Insertion Order Service End Points

### Get guaranteed delivery dynamic capacity as CSV by group of order id for single timezone

```
POST /api/v1/rest/order/capacity/guaranteed/future/orderids/{nbDays}/{timeZone}
```

- **Description**

  Get guaranteed capacity for a group of orders within a timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |  

- **Consumes**

  application/json

- **Produces**

  test/csv

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
   $ curl 'https://api.appnexus.com/imf/v1/rest/order/capacity/guaranteed/future/orderids/1/EST' -i -X 
   POST -H 'Content-Type: application/json;charset=UTF-8' -d '{
   "externalOrderIdPool" : 
   {
   "orderIds" : [ "1" ]
   }
   }'     
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/order/capacity/guaranteed/future/orderids/1/EST HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://api.appnexus.com/imf/
  Content-Length: 60
            
  {
  "externalOrderIdPool" : {
  "orderIds" : [ "1" ]
  }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 2567
            
  [ {
  "externalId" : "1",
  "nextHours" : {
  "20200619T05:00+1000" : 1000,
  "20200619T12:00+1000" : 1000,
  "20200619T06:00+1000" : 1000,
  "20200619T13:00+1000" : 1000,
  "20200619T20:00+1000" : 1000,
  "20200619T04:00+1000" : 1000,
  "20200619T07:00+1000" : 1000,
  "20200619T21:00+1000" : 1000,
  "20200619T03:00+1000" : 1000,
  "20200619T10:00+1000" : 1000,
  "20200619T08:00+1000" : 1000,
  "20200619T11:00+1000" : 1000,
  "20200619T02:00+1000" : 1000,
  "20200619T17:00+1000" : 1000,
  "20200619T00:00+1000" : 1000,
  "20200619T09:00+1000" : 1000,
  "20200619T16:00+1000" : 1000,
  "20200619T23:00+1000" : 1000,
  "20200619T18:00+1000" : 1000,
  "20200619T15:00+1000" : 1000,
  "20200619T01:00+1000" : 1000,
  "20200619T19:00+1000" : 1000,
  "20200619T14:00+1000" : 1000,
  "20200619T22:00+1000" : 1000
  },
  "nextDays" : {
  "20200619T00:00+1000" : 240000
  },
  "targetings" : [ {
  "start" : "2020-03-19",
  "end" : "2020-06-19",
  "expression" : "country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') 
  and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
  site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
  country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
  segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
  site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true') or 
  country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
  segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
  site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
  country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
  segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
  site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true')",
  "impressionCap" : 5,
  "impressionCapPeriod" : 77,
  "dynamic" : false
  } ]
  } ]
  ```

### Get guaranteed delivery dynamic capacity by group of order id for double timezone

```
POST /api/v1/rest/order/capacity/guaranteed/future/orderids/{nbDays}/{timeZone}/{timeZoneSecond}
```

- **Description**

  Get guaranteed capacity for a group of orders for double timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | timeZoneSecond | timeZoneSecond | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
  $ curl 'https://api.appnexus.com/imf/v1/rest/order/capacity/guaranteed/future/orderids/1/Australia/Sydney' -i -X 
    POST -H 'Content-Type: application/json;charset=UTF-8' -d '{
    "externalOrderIdPool" : 
    {
      "orderIds" : [ "1" ]
    }
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/order/capacity/guaranteed/future/orderids/1/Australia/Sydney HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://api.appnexus.com/imf/
  Content-Length: 60

  {
    "externalOrderIdPool" : {
      "orderIds" : [ "1" ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 2567

  [ {
    "externalId" : "1",
    "nextHours" : {
      "20200619T05:00+1000" : 1000,
      "20200619T12:00+1000" : 1000,
      "20200619T06:00+1000" : 1000,
      "20200619T13:00+1000" : 1000,
      "20200619T20:00+1000" : 1000,
      "20200619T04:00+1000" : 1000,
      "20200619T07:00+1000" : 1000,
      "20200619T21:00+1000" : 1000,
      "20200619T03:00+1000" : 1000,
      "20200619T10:00+1000" : 1000,
      "20200619T08:00+1000" : 1000,
      "20200619T11:00+1000" : 1000,
      "20200619T02:00+1000" : 1000,
      "20200619T17:00+1000" : 1000,
      "20200619T00:00+1000" : 1000,
      "20200619T09:00+1000" : 1000,
      "20200619T16:00+1000" : 1000,
      "20200619T23:00+1000" : 1000,
      "20200619T18:00+1000" : 1000,
      "20200619T15:00+1000" : 1000,
      "20200619T01:00+1000" : 1000,
      "20200619T19:00+1000" : 1000,
      "20200619T14:00+1000" : 1000,
      "20200619T22:00+1000" : 1000
    },
    "nextDays" : {
      "20200619T00:00+1000" : 240000
    },
    "targetings" : [ {
      "start" : "2020-03-19",
      "end" : "2020-06-19",
      "expression" : "country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
       segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
       segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4860908 in ('true') and 
       segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and 
       segment-3222990 in ('true') and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and 
       size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4836884 in ('true') and 
       segment-4860908 in ('true') or country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and 
       segment-3222990 in ('true') and segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and 
       size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4860908 in ('true') and 
       segment-4860941 in ('true')",
      "impressionCap" : 5,
      "impressionCapPeriod" : 77,
      "dynamic" : false
    } ]
  } ]
  ```

### Get guaranteed delivery dynamic capacity by group of order id for single timezone

```
GET /api/v1/rest/order/capacity/guaranteed/future/{nbDays}/{timeZone}
```

- **Description**

  Get guaranteed capacity for a group of orders within a timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
   $ curl 'https://api.appnexus.com/imf/v1/rest/order/capacity/guaranteed/future/orderids/1/EST' -i -X POST 
     -H 'Content-Type: application/json;charset=UTF-8' -d '{
     "externalOrderIdPool" : 
    {
      "orderIds" : [ "1" ]
    }
  }'  
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/order/capacity/guaranteed/future/orderids/1/EST HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://api.appnexus.com/imf/
  Content-Length: 60

  {
    "externalOrderIdPool" : {
      "orderIds" : [ "1" ]
    }
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 2567

  [ {
    "externalId" : "1",
    "nextHours" : {
      "20200619T05:00+1000" : 1000,
      "20200619T12:00+1000" : 1000,
      "20200619T06:00+1000" : 1000,
      "20200619T13:00+1000" : 1000,
      "20200619T20:00+1000" : 1000,
      "20200619T04:00+1000" : 1000,
      "20200619T07:00+1000" : 1000,
      "20200619T21:00+1000" : 1000,
      "20200619T03:00+1000" : 1000,
      "20200619T10:00+1000" : 1000,
      "20200619T08:00+1000" : 1000,
      "20200619T11:00+1000" : 1000,
      "20200619T02:00+1000" : 1000,
      "20200619T17:00+1000" : 1000,
      "20200619T00:00+1000" : 1000,
      "20200619T09:00+1000" : 1000,
      "20200619T16:00+1000" : 1000,
      "20200619T23:00+1000" : 1000,
      "20200619T18:00+1000" : 1000,
      "20200619T15:00+1000" : 1000,
      "20200619T01:00+1000" : 1000,
      "20200619T19:00+1000" : 1000,
      "20200619T14:00+1000" : 1000,
      "20200619T22:00+1000" : 1000
    },
    "nextDays" : {
      "20200619T00:00+1000" : 240000
    },
    "targetings" : [ {
      "start" : "2020-03-19",
      "end" : "2020-06-19",
      "expression" : "country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') 
       and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
       segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
       segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
       segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true')",
      "impressionCap" : 5,
      "impressionCapPeriod" : 77,
      "dynamic" : false
    } ]
  } ]
  ```

### Get guaranteed delivery dynamic capacity for double timezone

```
GET /api/v1/rest/order/capacity/guaranteed/future/{nbDays}/{timeZone}/{timeZoneSecond}
```

- **Description**

  Get guaranteed capacity for a group of orders for double timezone.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | timeZone | timeZone | true | string |
  | PathParameter | timeZoneSecond | timeZoneSecond | true | string |
  | PathParameter | nbDays | nbDays | true | integer (int32) |
  | BodyParameter | externalOrderIdPool | externalOrderIdPool | true | [ExternalOrderIdPool](#externalorderidpool) |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |


- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
  $ https://api.appnexus.com/imf/v1/rest/order/capacity/guaranteed/future/1/Australia/Sydney' 
  -i -H 'Content-Type: application/json' -H 'Accept: application/json' 
  -H 'username: {{username}}' -H 'password: {{password}}' 
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/order/capacity/guaranteed/future/1/Australia/Sydney HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://api.appnexus.com/imf/
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 2567

  [ {
    "externalId" : "1",
    "nextHours" : {
      "20200619T05:00+1000" : 1000,
      "20200619T12:00+1000" : 1000,
      "20200619T06:00+1000" : 1000,
      "20200619T13:00+1000" : 1000,
      "20200619T20:00+1000" : 1000,
      "20200619T04:00+1000" : 1000,
      "20200619T07:00+1000" : 1000,
      "20200619T21:00+1000" : 1000,
      "20200619T03:00+1000" : 1000,
      "20200619T10:00+1000" : 1000,
      "20200619T08:00+1000" : 1000,
      "20200619T11:00+1000" : 1000,
      "20200619T02:00+1000" : 1000,
      "20200619T17:00+1000" : 1000,
      "20200619T00:00+1000" : 1000,
      "20200619T09:00+1000" : 1000,
      "20200619T16:00+1000" : 1000,
      "20200619T23:00+1000" : 1000,
      "20200619T18:00+1000" : 1000,
      "20200619T15:00+1000" : 1000,
      "20200619T01:00+1000" : 1000,
      "20200619T19:00+1000" : 1000,
      "20200619T14:00+1000" : 1000,
      "20200619T22:00+1000" : 1000
    },
    "nextDays" : {
      "20200619T00:00+1000" : 240000
    },
    "targetings" : [ {
      "start" : "2020-03-19",
      "end" : "2020-06-19",
      "expression" : "country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') 
       and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
       segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
       segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4836884 in ('true') and 
       segment-4860908 in ('true') or country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and 
       segment-3222990 in ('true') and segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and 
       size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4860908 in ('true') 
       and segment-4860941 in ('true')",
      "impressionCap" : 5,
      "impressionCapPeriod" : 77,
      "dynamic" : false
    } ]
  } ]
  ```

### Get guaranteed delivery historical capacity as JSON

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
  | 200 | OK | [OrderDeliveryInfo](#orderdeliveryinfo) |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
  $ curl 'https://api.appnexus.com/imf/v1/rest/order/delivery/1/2016-06-01/2016-07-01' -i -H 
  'Content-Type: application/json' -H 'Accept: application/json' 
  -H 'username: {{username}}' -H 'password: {{password}}'
  ```

- **Example HTTP request**

  ```
  GET /api/v1/rest/order/delivery/1/2016-06-01/2016-07-01 HTTP/1.1
  Content-Type: application/json
  Accept: application/json
  username: {{username}}
  password: {{password}}
  Host: https://api.appnexus.com/imf/
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 241

  {
    "externalOrderId" : "1",
    "impressions" : 20,
    "orderLineDeliveryDetail" : {
      "1" : [ {
        "impressions" : 10,
        "date" : "05/19/2020"
      } ],
      "2" : [ {
        "impressions" : 10,
        "date" : "06/19/2020"
      } ]
    }
  }
  ```

### Get insertion order inventory with JSON

```
POST /api/v1/rest/order/inventory/apas/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  Get insertion order inventory with JSON.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | BodyParameter | body | body | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

### Get insertion order inventory and contention with JSON

```
POST /api/v1/rest/order/inventoryandcontention/apas/{startDate}/{endDate}/{consumptionFilter}
```

- **Description**

  Get insertion order inventory and contention with JSON.

- **Parameters**
  
  | Type | Name | Description | Required | Schema |
  |---|---|---|---|---|
  | PathParameter | startDate | startDate | true | string |
  | PathParameter | endDate | endDate | true | string |
  | PathParameter | consumptionFilter | consumptionFilter | true | string |
  | PathParameter | matrixVars | matrixVars | false | object |
  | BodyParameter | body | body | true | string |
  | HeaderParameter | username | Your username for accessing the Yield Analytics API | true | string |
  | HeaderParameter | password | Your password for accessing the Yield Analytics API | true | string |

- **Responses**

  | HTTP Code | Description | Schema |
  |---|---|---|
  | 200 | OK | [InsertionOrderResponse](#insertionorderresponse) array |

- **Consumes**

  application/json

- **Produces**

  application/json

- **Tags**

  Insertion Order Service End Points

- **Example cURL request**

  ```
  $ curl 'https://api.appnexus.com/imf/v1/rest/order/inventoryandcontention/apas/2017-03-01/2017-03-31/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5' -i -X POST -H 
  'Content-Type: application/json;charset=UTF-8' -d 
  '{
    "expression" : "ad_server in ('TEST')"
  }'
  ```

- **Example HTTP request**

  ```
  POST /api/v1/rest/order/inventoryandcontention/apas/2017-03-01/2017-03-31/consumptionFilter;
  INVENTORY_CLASS=GUARANTEED;CONSUMPTION_TYPE=DIRECT;CONSUMPTION_TYPE=CONTAINED;PRIORITY%3E=5 HTTP/1.1
  Content-Type: application/json;charset=UTF-8
  Host: https://api.appnexus.com/imf/
  Content-Length: 44

  {
    "expression" : "ad_server in ('TEST')"
  }
  ```

- **Example HTTP response**

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json;charset=UTF-8
  Content-Length: 2567

  [ {
    "externalId" : "1",
    "nextHours" : {
      "20200619T05:00+1000" : 1000,
      "20200619T12:00+1000" : 1000,
      "20200619T06:00+1000" : 1000,
      "20200619T13:00+1000" : 1000,
      "20200619T20:00+1000" : 1000,
      "20200619T04:00+1000" : 1000,
      "20200619T07:00+1000" : 1000,
      "20200619T21:00+1000" : 1000,
      "20200619T03:00+1000" : 1000,
      "20200619T10:00+1000" : 1000,
      "20200619T08:00+1000" : 1000,
      "20200619T11:00+1000" : 1000,
      "20200619T02:00+1000" : 1000,
      "20200619T17:00+1000" : 1000,
      "20200619T00:00+1000" : 1000,
      "20200619T09:00+1000" : 1000,
      "20200619T16:00+1000" : 1000,
      "20200619T23:00+1000" : 1000,
      "20200619T18:00+1000" : 1000,
      "20200619T15:00+1000" : 1000,
      "20200619T01:00+1000" : 1000,
      "20200619T19:00+1000" : 1000,
      "20200619T14:00+1000" : 1000,
      "20200619T22:00+1000" : 1000
    },
    "nextDays" : {
      "20200619T00:00+1000" : 240000
    },
    "targetings" : [ {
      "start" : "2020-03-19",
      "end" : "2020-06-19",
      "expression" : "country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') 
       and segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222986 in ('true') and 
       segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222986 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
       segment-4836884 in ('true') and segment-4860903 in ('true') or country in ('australia') and size in ('160x600') and    
       site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4836884 in ('true') and segment-4860908 in ('true') or 
       country in ('australia') and size in ('160x600') and site in ('outlook au desktop') and segment-3222990 in ('true') and 
       segment-4860903 in ('true') and segment-4860941 in ('true') or country in ('australia') and size in ('160x600') and 
       site in ('outlook au desktop') and segment-3222990 in ('true') and segment-4860908 in ('true') and segment-4860941 in ('true')",
      "impressionCap" : 5,
      "impressionCapPeriod" : 77,
      "dynamic" : false
    } ]
  } ]
  ```

## Definitions

### ExternalOrderIdPool

| Name | Description | Required | Schema |
|---|---|---|---|
| externalOrderIdPool |  | false | ExternalOrderIdPool |
| orderIds | A collection of order IDs | true | string array |

### InsertionOrderResponse

A JSON object to hold the results of insertion order execution.

| Name | Description | Required | Schema |
|---|---|---|---|
| externalId | The external ID of the insertion order response | true | string |
| nextDays | A map of key to next days | true | object |
| nextHours | A map of key to next hours | true | object |
| targetings | A collection of insertion order targeting response | true | [InsertionOrderTargetingResponse](#insertionordertargetingresponse) array |

### InsertionOrderTargetingResponse

A JSON object to hold the results of a targeting in Insertion Order Response.

| Name | Description | Required | Schema |
|---|---|---|---|
| dynamic | The dynamic of the insertion order targeting response | true | boolean |
| end | The end of the insertion order targeting response | true | string |
| expression | The expression of the insertion order targeting response | true | string |
| impressionCap | The impression cap of the insertion order targeting response | false | integer (int64) |
| impressionCapPeriod | The impression cap period of the insertion order targeting response | false | integer (int64) |
| start | The start of the insertion order targeting response | true | string |

### OrderDeliveryInfo

A JSON object to hold the order delivery info.

| Name | Description | Required | Schema |
|---|---|---|---|
| externalOrderId | The external order ID of the order delivery info | true | string |
| impressions | The impressions of the order delivery info | true | integer (int64) |
| orderLineDeliveryDetail | A map of key to a set of order line delivery details | false | object |

### OrderLineDeliveryDetail

A JSON object to hold the orderline delivery detail info.

| Name | Description | Required | Schema |
|---|---|---|---|
| date | The date of the order line delivery detail | true | string |
| impressions | The impression of the order line delivery detail | true | integer (int64) |

## Related topic

[Yield Analytics API](yield-analytics-api.md)
