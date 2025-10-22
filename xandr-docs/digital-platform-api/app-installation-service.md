---
title: App Installation Service
description: The App Installation service allows app developers to install apps on client systems.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# App Installation service

This service allows app developers to install apps on client systems.

## REST API

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/app-installation` | View all installations |
| `GET`  | `https://api.appnexus.com/app-installation?id=ID` | View a specific installation |
| `POST` | `https://api.appnexus.com/app-installation` | Install an app for a client |
| `PUT` | `https://sand.api.appnexus.com/app-installation?id=ID` | Update an app installation |
| `DELETE` | `https://api.appnexus.com/app-installation?id=ID` | Delete an app installation  |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `accepted_permissions` | boolean | Indicates whether permission was received to access the areas required by the app for use. |
| `addendum` | string | This contains the text of the agreement that appears when a user installs the app. This field can be edited using the **Markdown** markup language. |
| `has_payment_access` | boolean | Indicates whether payment terms and fees can be applied to this app.<br>**Read-only**.<br>**Default**: `true` |
| `id` | int | The unique identification number of each installation instance.<br>**Required**: `PUT` and `DELETE` |
| `installed_on` | timestamp | The date and time that this app was installed by the user.<br>**Read-only** |
| `installer_user_id` | int | The unique identification of the user with permission to install apps from the Apps Marketplace. This is also the user who can accept or reject addendum agreements.<br>**Read-only** |
| `log_level_data_fee` | int | The fee being charged to the user to consume log-level data.<br>**Read-only** |
| `permissions` | array of objects | The operations that the app can perform on behalf of the currently logged in user. For more information, see [Permissions](#permissions) below. |
| `plugin_id` | int | The unique identification number of the plugin installed in this instance.<br>**Required**: `POST` |
| `subscriber_email` | string | The email address of the specified contact person at the app installer.<br>**Read-only** |
| `subscriber_entity_id` | int | The unique identification number of the parent of the user that installed the app.<br>**Required**: `POST` |
| `subscriber_entity_type` | enum | The parent organization of the user that installed the app. Possible values include `"member"` or `"bidder"`. When adding an installation, you must choose the correct option for the `subscriber_entity_id` (below). |
| `subscriber_name` | string | The name of the contact person at the app installer.<br>**Read-only** |
| `subscriber_phone` | string | The phone number of the specified contact person at the app installer.<br>**Read-only** |

### Permissions

Each object in the `permissions` array contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `privileges` | array of objects | The types of calls that the app can make to the API service and the specific fields that can be used. See [`privileges` example](#privileges-example).<br>Within each object, `method` defines the calls that can be made to the service (`"get"`, `"post"`, `"put"`, or `"delete"`), and `fields` restricts the permissions to particular fields in the service. If `fields` is `null`, the permissions apply to all fields in the service. Note that use of the `"delete"` method must be approved by a Xandr representative. |
| `service` | enum | The name of the API service that the app is permitted to use. |

#### `privileges` example

```
{
"method": "get",
"fields": null
}
```

## Examples

### View all installations

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/app-installation'
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "app-installations":[
            {
                "id":9,
                "plugin_id":47,
                "addendum":"This is test text to demonstrate the addendum functionality.",
                "subscriber_entity_type":"member",
                "subscriber_entity_id":3754,
                "accepted_permission":false,
                "installed_on":"2013-05-01 20:58:28",
                "installer_user_id":5447,
                "permissions":null,                     
                "has_payment_access":false   
                "log_level_data_fee":5500,
                "subscriber_phone":"",
                "subscriber_email":"zivester@appnexus.com",
                "subscriber_name":"Zach Ivester"
            }
        ],
        "dbg_info":{
            ...
        }
    }
}
```

### View a specific installation

```
$ curl -b cookies -c cookies 's://sand.api.appnexus.com/app-installation?id=868'
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null,
        "app-installation":{
            "id":868,
            "plugin_id":4,
            "entity_type":"bidder",
            "entity_id":226,
            "status":"installed"
        }
    }
}
```

### Install an app to a client

```
$ cat add-app-installation.json
{
    "app-installation":
        {
        "plugin_id": "20",
        "subscriber_entity_type": "member",
        "subscriber_entity_id":  "238"
        }
}
$ curl -b cookies -c cookies -X POST -d @add-app-installation.json 's://api.appnexus.com/app-installation' | json-pp
{
    "response":{
        "status":"OK",
        "count":1,
        "id":18716,
        "start_element":0,
        "num_elements":100,
        "app-installation":{
            "id":18716,
            "plugin_id":20,
            "addendum":null,
            "subscriber_entity_type":"member",
            "subscriber_entity_id":238,
            "accepted_permission":true,
            "installed_on":"2013-05-13 12:54:50",
            "installer_user_id":3052,
            "permissions":null,                     
            "has_payment_access":false   
            "log_level_data_fee":null,
            "subscriber_phone":null,
            "subscriber_email":null,
            "subscriber_name":"Netseer - member 238"
        },
        "dbg_info":{
            ...
        }
    }
}
```

### Update an app installation

```
$ cat update-app-installation.json
{
    "app-installation": 
        {
        "plugin_id": "19",
        "addendum": "www.site.com",
        "accepted_permission": false,
        "log_level_data_fee": "2000",
        "subscriber_phone": "914-555-1212",
        "subscriber_email": "JMS@live.com",
        "subscriber_name": "Ben Smith"
        }
} 
$ curl -b cookies -c cookies -X PUT -d @update-app-installation.json 's://api.appnexus.com/app-installation?id=23'
{
    "response":{
        "status":"OK",
        "count":1,
        "id":"23",
        "start_element":0,
        "num_elements":100,
        "app-installation":{
            "id":23,
            "plugin_id":50,
            "addendum":null,
            "subscriber_entity_type":"member",
            "subscriber_entity_id":185,
            "accepted_permission":false,
            "installed_on":"2013-05-07 15:05:45",
            "installer_user_id":43,
            "permissions":null,                     
            "has_payment_access":false   
            "log_level_data_fee":2500,
            "subscriber_phone":"",
            "subscriber_email":"PQ5ejohnson@appnexus.com",
            "subscriber_name":"Emily HB"
        },
        "dbg_info":{
            ...
        }
    }
}
```

### Delete an app installation

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/app-installation?id=121'
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
