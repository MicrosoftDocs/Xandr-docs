---
title: Bidders - API Semantics
description: In this article, learn how to work with our impression bus REST API.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - API semantics

This page explains how to work with our impression bus REST API. It includes information on:

- How to authenticate
- How to ask a service about itself - what fields it supports, which fields can be used to filter
- Response codes and errors

> [!NOTE]
> For more information about how to work with specific API services, see the links at [API Services](api-services.md).

## HTTP protocol

Xandr's impression bus API supports HTTP Protocol version 1.1 or later. While some calls may work with the deprecated 1.0 version, this is not guaranteed. Please ensure that your client communicates using at least version 1.1.

## API endpoints

| Environment | URL | Notes |
|---|---|---|
| Production | `https://api.adnxs.com` | We require using a secure endpoint (`https://`) for our production API to ensure the privacy of your data. Non-secure access to the product API (HTTP) is not available. |

## REST

Xandr API services are "RESTful." REST (Representational State Transfer) is a type of software architecture in which requests model the communication from a web browser to a web server. Below are the central REST methods used in Xandr's API Services and their uses:

| REST Method | Usage |
|--|--|
| POST | create/add |
| GET | read/retrieve |
| PUT | update/modify |
| DELETE | delete |

In our documentation we use [cURL](https://www.php.net/curl) to make REST requests. cURL is a command line tool for transferring files with URL syntax, supporting FTP, FTPS, HTTP, HTTPS, SCP, SFTP, TFTP, TELNET, DICT, LDAP, LDAPS, and FILE. The example scripts on each API wiki page will make clear the structure of the `cURL` commands you will need to run Xandr's API Services.

## Append on PUT

For `PUT` requests, only the fields included in the [JSON](http://json.org/) file will be updated, **except in the case of arrays**.

When updating an array using `PUT`, all fields in the array are overwritten with the contents of the new array you upload, unless you add this to your request's query string: `"append=true"`.

## Meta calls

All Bidder Services support meta calls, which will return the service's fields and the value type. Meta calls look like this:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/SERVICE/meta'
```
  
For example (partial output of a meta call):

```
            "bidder_id": {
                "type": "int"
            },
            "agent_id": {
                "type": "int"
            },
            "code": {
                "type": "string"
            },
            "active": {
                "type": "boolean"
            }
```

## Limiting `GET` request records

Adding this string to the end of any GET request to the API will limit the number of records retrieved:

```
?start_element=N&num_elements=N
```
  
### Examples

```
segment/1?start_element=0&num_elements=1000
member?start_element=0&num_elements=100
creative/1?start_element=0&num_elements=200
```

> [!NOTE]
> The maximum number of elements that can be returned regardless of your request is 100.

- The first element is element 0.
- All GET responses will have a "count" property showing the total number of elements matching that GET request.
- This will also apply to non-reporting services, such as the creative search service, that are requested with methods other than GETs.

## Filtering and sorting

Most API Services support filtering and sorting. Filtering allows you to specify a subset of objects to be returned. Sorting allows you to control the order of the objects returned.

### Get multiple objects by ID

You can get multiple specific objects by ID by passing a comma-separated list of IDs. The result object will contain an array holding just those specific objects. In the example below, we ask the [Creative Service](creative-service.md) for just the creatives with IDs 1, 2, and 3.

```
$ curl -bc -cc 'https://api.adnxs.com/creative?id=1,2,3
{ 
  "response" : {
     "count" : 3,
     "status" : "OK",
     "creatives" : [ ... ]
  }
}
      
```

### Filter by IDs

Pass a query string parameter for the field with a comma-separated list of IDs.

**Example**: Request all creatives for certain members

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?member_id=123,987' 
```

> [!NOTE]
> The maximum number of objects that can be returned per request, regardless of pagination, is 100. If you request over 100 objects, we will only return the first 100 and will not provide an error message.

### Filter by `Min` and `Max` Values

Fields that are of the type `int`, `double`, `date`, or `money` can be filtered by `min` and `max`. For example:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?min_id=47'
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?min_brand_id=20'
```

Fields of the type `date` can be filtered using the `min_last_modified` filter. Note the required date/time syntax: YYYY-MM-DD+HH:MM:SS

```
$ curl -b cookies 'https://api.adnxs.com/creative/114?min_last_activity=2017-10-27+21:00:00'
```

### Filter by field names

To limit the response to specific fields of an object, pass the `fields` query string parameter with a comma-separated list of field names. For example:

```
$ curl -b cookies "https://api.adnxs.com/user/current&fields=username,user_type,id"
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "user":{
            "id":14311,
             "username":"rloveland",
             "user_type":"admin"
        }
    }
}
  
```

### Misc filters on field

We support the following additional field-based filters on API responses:

- `not_*`
- `like_*`
- `min_*`
- `max_*`
- `nmin_*`
- `nmax_*`
- `having_*`
- `having_min_*`
- `having_max_*`

**Example**

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?like_[fieldName]=partialValue'
```

## JSON field values

`POST` and `PUT` requests require JSON-formatted data. `POST` request generally create objects in the database, and thus require all of the information about that object (unless it is subsequently modified by a PUT request). For `PUT` requests, only the JSON fields included in a request will be updated. All other fields will be unchanged.

Different fields require different types of values.

| Type | Description | Example |
|---|---|---|
| Array | More than one value allowed | [87,45] |
| Boolean | True/False | True |
| Double | Floating point number with twice the bit space of a float. | 3.12 |
| Enum | One element from an array of preassigned values only | male/female |
| Float | Floating point number | 3.12 |
| Int | Integer | 87 |
| String(100) | String of 100 characters or less | male_26_likes_cheese |
| Timestamp | Date and time string in the form YYYY-MM-DD HH:MM:SS | 2009-01-14 05:41:04 |
| Unsigned | Positive integers only | 745 |

## Authentication

Before you can use the APIs, you must authenticate yourself with your username and password. Please see [Authentication Service](authentication-service.md) for details.

## Response codes

All API Services return JSON-formatted data. When Service calls are successful, the JSON response will include a `"status"` field set to `"OK"`. The response to POST and PUT calls will also include the ID of the relevant object, such as bidder, member, tag, or creative, as well as any relevant attributes of that object. (In the example below, we are using cookies to store our authentication token and adding the file "tag" to the Tiny Tag Service.)

```
$ curl -b cookies -c cookies -X POST --data-binary @tag https://api.adnxs.com/tt/32/
{
    "response": {
        "status": "OK",
        "id": "242"
    }
}
```

## Errors

When invalid input is sent to the API - for example, an incorrect password - a JSON response will be returned with `"error"` and `"error_id"` fields. For some error conditions you may also see the optional `"error_description"` and `"error_code"` fields.

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/api/auth?username=admin&password=Wr0ngP@ss'
{
    "response": {
        "error": "No match found for user\/pass",
        "error_id": "NOAUTH"
    }
}
```

The `"error"` field is useful for debugging purposes, as it contains a verbose description of the error. The `"error_id"` field can be used programmatically as follows:

| Error_ID | Meaning | Logic |
|---|---|---|
| NOAUTH | Authentication information is either missing or invalid | Use /auth to get a valid token |
| UNAUTH | The user is not authorized to take the requested action | Check 'error' message and make sure logic is correct in code |
| SYNTAX | The syntax of the request is incorrect | Use the 'error' message to identify the issue and fix the code |
| SYSTEM | A system error has occurred | Contact Xandr |
| INTEGRITY | A client request is inconsistent; for example, an attempt to delete a default creative attached to an active TinyTag | Check the request for integrity |

## Related topic

[Bidder API Services](bidder-api-services.md)
