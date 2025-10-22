---
title: Developer Service
description: Use the Developer service to get the address and billing information for each developer as reference information.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Developer service

This service contains the address and billing information for each developer as reference information. While developers can modify or delete their entries, only administrative users can create a new developer with this service. For help creating a developer entry, contact your Xandr representative.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/developer` | View all developers |
| `GET` | `https://api.appnexus.com/developer?id=15` | View a specific developer |
| `POST` | `https://api.appnexus.com/developer` | Add a developer: (Xandr admin only) |
| `PUT` | `https://api.appnexus.com/developer?id=19` | Modify a developer |
| `DELETE` | `https://api.appnexus.com/developer?id=19` | Delete an developer |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `billing_address_1` | string | The first line of the developer address.<br>**Required on**: `POST` |
| `billing_address_2` | string | The second line of the developer address.<br>**Default**: `null` |
| `billing_city` | string | The city in which the developer resides.<br>**Required on**: `POST` |
| `billing_country` | string | The country in which the developer lives.<br>**Required on**: `POST` |
| `billing_region` | string | The region in which the developer resides.<br>**Required on**: `POST` |
| `billing_postal_code` | string | The developer ZIP code.<br>**Required on**: `POST` |
| `email` | string | The developer email address.<br>**Required on**: `POST` |
| `last_modified` | date | The date and time on which this information was last modified. |
| `phone` | string | The developer contact phone number.<br>**Required on**: `POST` |

## Examples

### Add a developer

```
$ cat add-developer.json
{
    "developer":
        {
        "id": 3535,
        "name": "John Smith" ,
        "entity_id": 32 ,
        "phone": "914-555-1212" ,
        "email": "JSmith@aol.com" ,
        "billing_address_1": "1 No Way" ,
        "billing_city": "New York" ,
        "billing_region": "Northeast" ,
        "billing_postal_code": "10010" ,
        "billing_country": "United States"
        }
}
$ curl -b cookies -c cookies -X POST -d @add-developer.json 'https://api.appnexus.com/developer'
{
    "response":{
        "status":"OK",
        "count":1,
        "id":19,
        "start_element":0,
        "num_elements":100,
        "developer":{
            "id":19,
            "name":"John Smith",
            "entity_id":32,
            "phone":"914-555-1212",
            "email":"JSmith@aol.com",
            "billing_address_1":"1 No Way",
            "billing_address_2":null,
            "billing_city":"New York",
            "billing_region":"Northeast",
            "billing_postal_code":"10010",
            "billing_country":"United States",
            "last_modified":"2013-05-03 17:58:02"
        },
        "dbg_info":{
            ...
        }
    }
}
```

### Modify a developer

```
$ cat update-developer.json
{
    "developer":
        {
        "name": "John Smith" ,
        "phone": "914-555-2222"
        }
}
$ curl -b cookies -c cookies -X PUT -d @update-developer.json 'https://api.appnexus.com/developer?id=19'
{
    "response":{
        "status":"OK",
        "count":1,
        "id":"19",
        "start_element":0,
        "num_elements":100,
        "developer":{
            "id":19,
            "name":"John Smith",
            "entity_id":32,
            "phone":"914-555-2222",
            "email":"JSmith@aol.com",
            "billing_address_1":"1 No Way",
            "billing_address_2":null,
            "billing_city":"New York",
            "billing_region":"Northeast",
            "billing_postal_code":"10010",
            "billing_country":"United States",
            "last_modified":"2013-05-03 18:04:03"
        },
        "dbg_info":{
            ...
        }
    }
}
```

### View all developers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/developer'                                             
{
    "response":{
        "status":"OK",
        "count":17,
        "start_element":0,
        "num_elements":100,
        "developers":[
            {
                "id":1,
                "name":"AppNexus,
                 Inc.",
                "entity_id":null,
                "phone":null,
                "email":null,
                "billing_address_1":null,
                "billing_address_2":null,
                "billing_city":null,
                "billing_region":null,
                "billing_postal_code":null,
                "billing_country":null,
                "last_modified":"2011-09-16 15:38:16"
            },
            {
                "id":3,
                "name":"eXelate",
                "entity_id":246,
                "phone":null,
                "email":"jhackett@exelate.com",
                "billing_address_1":null,
                "billing_address_2":null,
                "billing_city":null,
                "billing_region":null,
                "billing_postal_code":null,
                "billing_country":null,
                "last_modified":"2012-05-22 15:20:58"
            },
        ],
        "dbg_info":{
            ...
        }
    }
}
```

### View a specific developer

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/developer?id=15'
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "developer":{
            "id":15,
            "name":"FlxOne",
            "entity_id":null,
            "phone":null,
            "email":null,
            "billing_address_1":null,
            "billing_address_2":null,
            "billing_city":null,
            "billing_region":null,
            "billing_postal_code":null,
            "billing_country":null,
            "last_modified":"2013-03-08 15:03:06"
        },
        "dbg_info":{
            ...
        }
    }
}
```

### Delete a developer

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/developer?id=19'
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "dbg_info":{
            ...
        }
    }
}
```

## Related topic

[App Installation Service](./app-installation-service.md)
