---
title: Plugin Service
description: Developing an app for Apps Marketplace involves building an umbrella app and specific app instances, which can be controlled through the Plugin service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Plugin service

When you develop an app for the Apps Marketplace, you build an umbrella app and then one or more specific app instances that plug into the workflow in different places. The Plugin Service allows you to create and control the umbrella app. For information about creating and managing app instances, see the [Plugin Instance Service](./plugin-instance-service.md).

## REST API

> [!NOTE]
> There are three different user roles that can make calls to this service:
>
> - **App Providers** - Members who develop apps in the Apps Marketplace
> - **App Subscribers** - Members who subscribe to and use apps
> - **Non-member Developers** - App providers who are not associated to any member
>
> Certain roles are restricted from making one or more calls. The roles that can make the calls are specified in the **Description** column in the table below.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/plugins`<br>(plugin JSON) | Add an app.<br> - App providers. |
| `PUT` | `https://api.appnexus.com/plugin?id=PLUGIN_ID`<br>(plugin JSON) | Modify an app.<br> - App providers. |
| `GET` | `https://api.appnexus.com/plugin` | View all apps.<br> - App Providers.<br> - App Subscribers (will only see apps to which they are associated).<br> - Non-member Developers (will only see apps to which they are associated).<br><br>**Note**: To view all apps that a member has installed, execute a `GET` call against the **Member** service. Locate the `id` field under **plugins**. All plugins that this member has installed (regardless of whether they are associated) are listed by plugin number. |
| `GET` | `https://api.appnexus.com/plugin?id=PLUGIN_ID` | View a specific app.<br> - App Providers.<br> - App Subscribers (will only see apps to which they are associated).<br> - Non-member Developers (will only see app if they are associated to it). |
| `GET` | `https://api.appnexus.com/plugin?developer_id=DEVELOPER_ID` | View all apps created by a specific subscriber, developer, or non-member developer.<br> - App Subscribers.<br> - App Providers.<br> - Non-member Developers.<br><br>**Note**: If you cannot see apps that you have created, contact your Xandr representative. |
| `DELETE` | `https://api.appnexus.com/plugin` | Delete an app.<br> - App Providers |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `addendum` | string |**Read-only**. Contains the text of the addendum terms for the app.<br><br>**Default**: `null` |
| `allowed_asset_count` | int | **Read-only**. Indicates the number of images that can be associated to an app. This cannot exceed five (5). These images are defined in the App-Asset service (**Admin only**). |
| `author_display_name` | string | The author name that is displayed below the name of the app on the main **Apps Marketplace** page and in the More Info dialog.<br><br>**Default**: `null` <br><br> See [Images](#images-for-author_display_name). |
| `click_to_install` | boolean | Indicates whether the install option on the **Apps Marketplace UI** screen is functional.<br><br>**Default**: `false` |
| `contact_email` | string | The email address that you can use to contact the app developer. This appears on the **Fee Details** screen.<br><br>**Default**: `null` |
| `contact_name` | string | The name of the app developer. This appears on the **Fee Details** screen.<br><br>**Default**: `null` |
| `contact_phone` | string | The phone number that you can use to contact the app developer. This appears on the **Fee Details** screen.<br><br>**Default**: `null` |
| `contact_text` | string | This is any additional text that usually providers more information about the app developer. This appears on the **Fee Details** screen.<br><br>**Default**: `null` |
| `description` | string | The description of the app that is displayed in the **More Info** dialog. |
| `developer` | object | The developer of the app. For more information, see [Developer](#developer) below.<br><br>**Required On**: `POST` |
| `domains` | array of objects | The sites to which Apps Marketplace will look to see if a user is already logged into. For more information, see [Domains](#domains) below.<br><br> **Default**: `null` |
| `featured` | boolean | **Read-only**. Indicates whether the app is listed in the carousel area of the available apps.<br><br>**Default**: `false` |
| `has_payment_access` | boolean | **Read-only**. Indicates whether payment terms and fees can be applied to this app.<br><br>**Default**: `true` |
| `id` | int | The ID of the app.<br><br>**Default**: Auto-generated number<br>**Required On**: `PUT`/`DELETE`, in query string |
| `is_available` | boolean | If `true`, the app is exposed to members in the Apps Marketplace by default. You can use the `member_availabilities` field to override this setting for specific members. For example, if you wanted to expose the app only to specific clients, you would set `is_available` to `false` and then use `member_availabilities` to expose the app to those specific clients. For more details, see [Member Availabilities](#member-availabilities) below.<br><br>**Default**: `false` |
| `log_level_data_fee` | int | **Read-only**. The dollar amount charged to the member consuming log-level data.<br><br>**Default**: `null`<br>**Required On**: This field can only be updated through the [App Contract Service](./app-contract-service.md). |
| `member_availabilities` | array of objects | This setting indicates if this app is available to certain members or restricted from certain members. This value will override the setting `is_available`. For more information, see [Member Availabilities](#member-availabilities) below. |
| `moreinfo_url` | string | The URL of the app used for demo purposes.<br><br>**Default**: `null` |
| `name` | string | The name of the app that is displayed on the main **Apps Marketplace** page and in the **More Info** dialog.<br><br>**Required On**: `POST` |
| `permissions` | array of objects | The operations that the app can perform on behalf of the currently logged in user. For more information, see [Permissions](#permissions) below.<br><br>**Default**: `null` |
| `plugin_category_id` | int | The identification number of the category to which this app will be assigned. Note that if you select a number that is a sub-level category, this app will automatically be assigned to both this category and the associate parent category. If you enter a parent category, however, the app belongs only to that one and not to any sub-level category.<br><br>**Default**: `null` |
| `plugin-instances` | array of objects | **Read-only**. The specific instances associated to the app. For more information about app instances, see the [Plugin Instance Service](./plugin-instance-service.md).<br><br>**Default**: `null` |
| `public_key` | string | The public key of the public/private key pair for authenticating the app. |
| `recommended` | boolean | **Read-only**. Indicates whether the app is listed in the **Recommended Apps** row of the **Apps Marketplace** screen.<br><br>**Default**: `false` |
| `summary` | string | The description of the app that is displayed on the main **Apps Marketplace** page.<br><br>**Default**: `null` |
| `video_url` | string | The URL of the tutorial video for this app. Must be Vimeo hosted.<br><br>**Default**: `null` |

#### Images for `author_display_name`

:::image type="content" source="media/plugin-service-a.png" alt-text="Screenshot one showing the author name displayed in the selected app on the main Apps Marketplace page.":::

:::image type="content" source="media/plugin-service-b.png" alt-text="Screenshot two showing the author name displayed in the app's Description panel.":::

### Developer

The `developer` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the developer that built the app. You can use the Developer Service to retrieve this ID.<br><br>**Required On**: `POST` |
| `name` | string | **Read-only**. The name of the developer that built the app. |

### Domains

The `domains` object contains the following field:

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | The domain name of the site to which Apps Marketplace will look to see if a user is logged on.<br><br>**Default**: `null` |

### Permissions

Each object in the `permissions` array contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `privileges` | array of objects | The types of calls that the app can make to the API service and the specific fields that can be used. See [Example](#example-for-privileges) <br>Within each object, method defines the calls that can be made to the service (`"get"`, `"post"`, `"put"`, or `"delete"`), and fields restricts the permissions to particular fields in the service. If fields are `null`, the permissions apply to all fields in the service. Note that use of the `"delete"` method must be approved by an Xandr representative. |
| `service` | enum | The name of the API service that the app is permitted to use. |

#### Example for `privileges`

```
{
"method": "get",
"fields": null
}
```

### Member availabilities

The main `is_available` field defines whether or not the app is exposed to all members by default. You can use the `member_availabilities` field to override this default for specific members. For example, if you wanted to expose the app only to select members, you would set `is_available` to `false` and then use `member_availabilities` to expose the app to those specific members.

Each object in the `member_availabilities` array contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the member.<br><br>**Required On**: `POST`/`PUT`, if passing main `is_available` field. |
| `is_available` | boolean | If `true`, the app is exposed to the member.<br><br>**Required On**: `POST`/`PUT`, if passing `id`. |

## Examples

### Add an app

```
$ cat add-plugin.json
{
    "plugin":
 {
        "name": "JMS November App",
        "description": "This is a test for an app created by another user.",
        "public_key": "-----BEGIN PUBLIC KEY-----\nMFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBAL88J0hPSmfYfKmWw\/y4xwdeTZsbwDeU\n\ 
                 /vkE+r88KaVJ0gG7K8BT+0nhfeOalrw\/EfX\/ta0YWxRb\/\/Yco39MbssCAwEAAQ==\n-----END PUBLIC KEY-----",
        "moreinfo_url": null,
        "is_available": "true",
        "summary": "The Test App does something great.",
        "contact_name": "The Test Application",
        "contact_phone": "1-800-TESTAPP",
        "contact_email": "hello@testapp.com",
        "contact_text": "Support email: support@testapp.com",
        "author_display_name": "Test App #2555",
        "developer":
 {
            "id": 7
        },
        "permissions":
[
            {
                "service": "segment",
                "privileges":
[
                    {
                        "method": "post",
                        "fields": null
                    }
                ]
            }
        ]
    }
}
$ curl -b cookies -c cookies -X POST -d @add-plugin.json 'https://api.appnexus.com/plugin' | json-pp
{
    "response":{
        "status":"OK",
        "count":1,
        "id":142,
        "start_element":0,
        "num_elements":100,
                "plugin":{
            "id":142,
            "name":"JMS November App",
            "description":"This is a test for an app created by another user.",
            "public_key":"-----BEGIN PUBLIC KEY-----             
                         \nMFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBAL88J0hPSmfYfKmWw\/y4xwdeTZsbwDeU\n\/
                         vkE+r88KaVJ0gG7K8BT+0nhfeOalrw\/EfX\/ta0YWxRb\/\/Yco39MbssCAwEAAQ==\n-----END PUBLIC KEY-----",
            "moreinfo_url":null,
            "log_level_data_fee":null,
            "plugin_category_id":null,
            "is_available":false,
            "summary":"The Test App does something great.",
            "contact_name":"The Test Application",
            "contact_phone":"1-800-TESTAPP",
            "contact_email":"hello@testapp.com",
            "contact_text":"Support email: support@testapp.com",
            "author_display_name":"Test App #2555",
            "recommended":false,
            "featured":false,
            "has_payment_access":false,
            "is_frozen":false,
            "allowed_asset_count":5,
            "addendum":null,
            "click_to_install":false,
            "video_url":null,
            "developer":{
                "id":14,
                "name":"taylortest"
            },
            "domains":null,
            "permissions":[
                {
                    "service":"segment",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        }
                    ],
                    "methods":[
                        "post"
                    ]
                }
            ],
            "plugin-instances":null,
            "member_availabilities":null
        },
        "dbg_info":{
            ...
        }
    }
}
```

### Modify an app

```
$ cat modify-plugin2.json
{
    "plugin": {
       "plugin_category_id": "33",
       "flavor": "converson_pixel"
    }
}
$ curl -b cookies -c cookies -X PUT -d @modify-plugin2.json 'https://api.appnexus.com/plugin?id=104' | json-pp
{
    "response":{
        "status":"OK",
        "count":1,
        "id":"104",
        "start_element":0,
        "num_elements":100,
        "plugin":{
            "id":104,
            "name":"JMS app",
            "description":"This is a test for an app created by a user.",
            "public_key":"",
            "moreinfo_url":null,
            "log_level_data_fee":null,
            "plugin_category_id":33,
            "is_available":false,
            "summary":"The Test App does something great.",
            "contact_name":"The Test Application",
            "contact_phone":"1-800-TESTAPP",
            "contact_email":"hello@testapp.com",
            "contact_text":"Support email: support@testapp.com",
            "author_display_name":"Test App #2000",
            "recommended":true,
            "featured":false,
            "has_payment_access":false,
            "is_frozen":false,
            "allowed_asset_count":5,
            "addendum":null,
            "click_to_install":false,
            "video_url":null,
            "developer":{
                "id":7,
                "name":"John Smith"
            },
            "domains":null,
            "permissions":[
                {
                    "service":"advertiser",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"campaign",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"insertion-order",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"line-item",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"publisher",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"site",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                }
            ],
            "plugin-instances":[
                {
                    "id":167,
                    "plugin_id":104,
                    "flavor":"standalone",
                    "iframe_url":"https:\/\/localhost\/app\/",
                    "js_api_version":"1.1",
                    "name":"testy test",
                    "description":"TBD",
                    "icon_url":"https:\/\/localhost\/app\/",
                    "proxy_url":"https:\/\/google.com"
                }
            ],
            "member_availabilities":[
                {
                    "id":185,
                    "is_available":true
                },
                {
                    "id":324,
                    "is_available":true
                },
                {
                    "id":1066,
                    "is_available":true
                }
            ]
        },
        "dbg_info":{
            ...
        }
    }
}
```

### View all apps

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/plugin' | json-pp
{
    "response":{
        "status":"OK",
        "count":14,
        "start_element":0,
        "num_elements":100,
        "plugins":[
            {
                "id":2,
                "name":"Example Plugin 1",
                "description":"This is an example full description.  It should support <span style='color: green'>HTML<\/span>.
                                 <br><br>\nThis plugin does the following when installed:\n<ul><li>Nothing.<\/li><\/ul>",
                "public_key":"-----BEGIN PUBLIC KEY-----\nMEwwDQYJKoZIhvcNAQEBBQADOwAwOAIxAL7yOpVHyI0JnHZxa4UKJrenZpjNFLV0\      
                                 nBaAfRbmp5xMrHYIHZXdYplyEOeLw8\/y2TQIDAQAB\n-----END PUBLIC KEY-----",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"Manage first party data, buy third party data and build custom audiences that are immediately 
                                 available to target 
                                 inventory.",
                "contact_name":"Sam",
                "contact_phone":"",
                "contact_email":"smati@example.com",
                "contact_text":"",
                "author_display_name":"Mr. Example",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":1,
                    "name":"Xandr,
                     Inc."
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"user",
                        "privileges":[
                            {
                                "method":"get",
                                "fields":[
                                    "entity_name"
                                ]
                            }
                        ],
                        "methods":[
                            "get"
                        ]
                    },
                    {
                        "service":"profile",
                        "privileges":[
                            {
                                "method":"get",
                                "fields":[
                                    "daypart_timezone"
                                ]
                            }
                        ],
                        "methods":[
                            "get"
                        ]
                    },
                    {
                        "service":"campaign",
                        "privileges":[
                            {
                                "method":"put",
                                "fields":[
                                    "profile_id"
                                ]
                            }
                        ],
                        "methods":[
                            "put"
                        ]
                    },
                    {
                        "service":"saved-report",
                        "privileges":[
                            {
                                "method":"get",
                                "fields":[
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "get"
                        ]
                    },
                    {
                        "service":"not-real-service",
                        "privileges":[
                            {
                                "method":"get",
                                "fields":[
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "get"
                        ]
                    }
                ],
                "plugin-instances":[
                    {
                        "id":7,
                        "plugin_id":2,
                        "flavor":"standalone",
                        "iframe_url":"https:\/\/xandr.com\/contact\/",
                        "js_api_version":"",
                        "name":"Plugin 1",
                        "description":"",
                        "icon_url":"https:\/\/abc.example.com\/download\/attachments\/34406872\/an-labs-symbol.png?
                                                 version=1&modificationDate=1327610813446",
                        "proxy_url":"https:\/\/www.xandr.com"
                    }
                ],
                "member_availabilities":[
                    {
                        "id":185,
                        "is_available":true
                    },
                    {
                        "id":326,
                        "is_available":true
                    },
                    {
                        "id":709,
                        "is_available":true
                    },
                    {
                        "id":884,
                        "is_available":true
                    }
                ]
            },
            {
                "id":3,
                "name":"Example Plugin 2",
                "description":"Lorem ipsum...",
                "public_key":"-----BEGIN PUBLIC KEY-----\nMEwwDQYJKoZIhvcNAQEBBQADOwAwOAIxANoHW5tUyLrWXo0fBe6KuxQFLgcyIU1X\ 
                                 n6hW9OUPU1vFBITj7LcCVg5RbRM7wV+TClwIDAQAB\n-----END PUBLIC KEY-----",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"",
                "contact_name":"",
                "contact_phone":"",
                "contact_email":"",
                "contact_text":"",
                "author_display_name":"",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":1,
                    "name":"Xandr,
                     Inc."
                },
                "domains":null,
                "permissions":null,
                "plugin-instances":[
                    {
                        "id":8,
                        "plugin_id":3,
                        "flavor":"standalone",
                        "iframe_url":"https:\/\/xandr.com\/contact\/",
                        "js_api_version":"",
                        "name":"Plugin 2",
                        "description":"",
                        "icon_url":"https:\/\/www.xandr.com\/favicon.ico",
                        "proxy_url":"https:\/\/www.xandr.com"
                    }
                ],
                "member_availabilities":[
                    {
                        "id":185,
                        "is_available":true
                    },
                    {
                        "id":326,
                        "is_available":true
                    },
                    {
                        "id":709,
                        "is_available":true
                    },
                    {
                        "id":884,
                        "is_available":true
                    }
                ]
            },
```

### View a specific app

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/plugin?id=104' | json-pp
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "plugin":{
            "id":104,
            "name":"JMS app",
            "description":"This is a test for an app created by a user.",
            "public_key":"",
            "moreinfo_url":null,
            "log_level_data_fee":null,
            "plugin_category_id":33,
            "is_available":false,
            "summary":"The Test App does something great.",
            "contact_name":"The Test Application",
            "contact_phone":"1-800-TESTAPP",
            "contact_email":"hello@testapp.com",
            "contact_text":"Support email: support@testapp.com",
            "author_display_name":"Test App #2000",
            "recommended":true,
            "featured":false,
            "has_payment_access":false,
            "is_frozen":false,
            "allowed_asset_count":5,
            "addendum":null,
            "click_to_install":false,
            "video_url":null,
            "developer":{
                "id":7,
                "name":"John Smith"
            },
            "domains":null,
            "permissions":[
                {
                    "service":"advertiser",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"campaign",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"insertion-order",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"line-item",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"publisher",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                },
                {
                    "service":"site",
                    "privileges":[
                        {
                            "method":"post",
                            "fields":null
                        },
                        {
                            "method":"delete",
                            "fields":[
                                "code",
                                "id"
                            ]
                        }
                    ],
                    "methods":[
                        "post",
                        "delete"
                    ]
                }
            ],
            "plugin-instances":[
                {
                    "id":167,
                    "plugin_id":104,
                    "flavor":"standalone",
                    "iframe_url":"https:\/\/localhost\/app\/",
                    "js_api_version":"1.1",
                    "name":"testy test",
                    "description":"TBD",
                    "icon_url":"https:\/\/localhost\/app\/",
                    "proxy_url":"https:\/\/google.com"
                }
            ],
            "member_availabilities":[
                {
                    "id":185,
                    "is_available":true
                },
                {
                    "id":324,
                    "is_available":true
                },
                {
                    "id":1066,
                    "is_available":true
                }
            ]
        },
        "dbg_info":{
            ...
        }
    }
}
```

### View all apps created by a specific subscriber, developer, or non-member developer

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/plugin?developer_id=7' | json-pp
{
    "response":{
        "status":"OK",
        "count":13,
        "start_element":0,
        "num_elements":100,
        "plugins":[
            "id":89,
                "name":"John M. Schneider III App",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"Test App person",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App Creator",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"segment",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            }
                        ],
                        "methods":[
                            "post"
                        ]
                    }
                ],
                "plugin-instances":null,
                "member_availabilities":[
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            },
            {
                "id":99,
                "name":"John M. Schneider Jr",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"The Test App JMS",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App JMS",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"segment",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            }
                        ],
                        "methods":[
                            "post"
                        ]
                    }
                ],
                "plugin-instances":null,
                "member_availabilities":[
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            },
            {
                "id":100,
                "name":"Napoleon Boneparte",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"The Test App JMS",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App JMS",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"segment",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            }
                        ],
                        "methods":[
                            "post"
                        ]
                    }
                ],
                "plugin-instances":null,
                "member_availabilities":[
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            },
            {
                "id":101,
                "name":"November Test App",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"The Test Application",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App JMS",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"segment",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            }
                        ],
                        "methods":[
                            "post"
                        ]
                    }
                ],
                "plugin-instances":null,
                "member_availabilities":[
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            },
            {
                "id":102,
                "name":"JMS app",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"The Test Application",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App for John",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"segment",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            }
                        ],
                        "methods":[
                            "post"
                        ]
                    }
                ],
                "plugin-instances":null,
                "member_availabilities":[
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            },
            {
                "id":104,
                "name":"JMS app",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":33,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"The Test Application",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App #2000",
                "recommended":true,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"advertiser",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            },
                            {
                                "method":"delete",
                                "fields":[
                                    "code",
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "post",
                            "delete"
                        ]
                    },
                    {
                        "service":"campaign",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            },
                            {
                                "method":"delete",
                                "fields":[
                                    "code",
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "post",
                            "delete"
                        ]
                    },
                    {
                        "service":"insertion-order",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            },
                            {
                                "method":"delete",
                                "fields":[
                                    "code",
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "post",
                            "delete"
                        ]
                    },
                    {
                        "service":"line-item",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            },
                            {
                                "method":"delete",
                                "fields":[
                                    "code",
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "post",
                            "delete"
                        ]
                    },
                    {
                        "service":"publisher",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            },
                            {
                                "method":"delete",
                                "fields":[
                                    "code",
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "post",
                            "delete"
                        ]
                    },
                    {
                        "service":"site",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            },
                            {
                                "method":"delete",
                                "fields":[
                                    "code",
                                    "id"
                                ]
                            }
                        ],
                        "methods":[
                            "post",
                            "delete"
                        ]
                    }
                ],
                "plugin-instances":[
                    {
                        "id":167,
                        "plugin_id":104,
                        "flavor":"standalone",
                        "iframe_url":"https:\/\/localhost\/app\/",
                        "js_api_version":"1.1",
                        "name":"testy test",
                        "description":"TBD",
                        "icon_url":"https:\/\/localhost\/app\/",
                        "proxy_url":"https:\/\/google.com"
                    }
                ],
                "member_availabilities":[
                    {
                        "id":185,
                        "is_available":true
                    },
                    {
                        "id":324,
                        "is_available":true
                    },
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            },
            {
                "id":111,
                "name":"JMS December App",
                "description":"This is a test for an app created by a user.",
                "public_key":"",
                "moreinfo_url":null,
                "log_level_data_fee":null,
                "plugin_category_id":null,
                "is_available":false,
                "summary":"The Test App does something great.",
                "contact_name":"The Test Application",
                "contact_phone":"1-800-TESTAPP",
                "contact_email":"hello@testapp.com",
                "contact_text":"Support email: support@testapp.com",
                "author_display_name":"Test App #2555",
                "recommended":false,
                "featured":false,
                "has_payment_access":false,
                "is_frozen":false,
                "allowed_asset_count":5,
                "addendum":null,
                "click_to_install":false,
                "video_url":null,
                "developer":{
                    "id":7,
                    "name":"John Smith"
                },
                "domains":null,
                "permissions":[
                    {
                        "service":"segment",
                        "privileges":[
                            {
                                "method":"post",
                                "fields":null
                            }
                        ],
                        "methods":[
                            "post"
                        ]
                    }
                ],
                "plugin-instances":null,
                "member_availabilities":[
                    {
                        "id":1066,
                        "is_available":true
                    }
                ]
            }
        ],
        "dbg_info":{
            ...
        }
    }
}
```

### Delete an app

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/plugin?id=80' | json-pp
{
    "response":{
        "status":"OK",
        "dbg_info":{
            ...
        }
    }
}
```
