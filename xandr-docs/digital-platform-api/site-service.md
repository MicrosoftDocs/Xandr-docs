---
title: Site Service
description: Use the Site service to group placements for management purposes, allowing ad quality and inventory categorization to be set at the site level.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Site service

A site (also called a placement group) provides a way of grouping [placements](./placement-service.md) for management purposes. Ad quality and inventory categorization can be set at the site level, so it doesn't have to be duplicated across placements. Each site belongs to a [publisher](./publisher-service.md), and each placement must belong to a site.

When you create a publisher, a site is automatically created. You can then modify that site however you wish or create more sites.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/site?publisher_id=PUBLISHER_ID`<br>(site JSON) | Add a site. |
| `PUT` | `https://api.appnexus.com/site?id=SITE_ID&publisher_id=PUBLISHER_ID`<br><br>`https://api.appnexus.com/site?id=SITE_ID`<br>(site JSON) | Modify an existing site. |
| `DELETE` | `https://api.appnexus.com/site?id=SITE_ID&publisher_id=PUBLISHER_ID`<br><br>`https://api.appnexus.com/site?code=SITE_CODE&publisher_code=PUBLISHER_CODE` | Delete a site. |
| `GET` | `https://api.appnexus.com/site` | View all sites for your publishers. |
| `GET` | `https://api.appnexus.com/site?publisher_id=PUBLISHER_ID` | View all of the sites for one of your publishers. |
| `GET` | `https://api.appnexus.com/site?id=SITE_ID&publisher_id=PUBLISHER_ID`<br><br>`https://api.appnexus.com/site?id=SITE_ID` | View a specific site for one of your publishers. |
| `GET` | `https://api.appnexus.com/site?id=1,2,3` | View multiple sites by ID using a comma-separated list. |

> [!NOTE]
> `publisher_code` and `code` can be used interchangeably with `publisher_id` and `id`, respectively.

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | Xandr ID assigned by the API to reference this site.<br><br>**Required On**: `PUT`, in query string |
| `code` | string (100) | Optional code for this site. |
| `name` | string (100) | Name associated with the site.<br><br>**Required On**: `PUT`, `POST` |
| `state` | enum | State of this site. Possible values: `active` or `inactive`.<br><br>**Default**: `active` |
| `url` | string (255) | URL of this site. |
| `publisher_id` | int | ID of the publisher that this site belongs to.<br><br>**Required On**: `POST`/`PUT`, in query string |
| `primary_content_category_id` | int | Users can optionally specify a primary [content category](./content-category-service.md) for a placement (see [examples](#examples) below). This category can be used for targeting and will appear in reports. Content categories can be set either at the Site level or the Placement level, but not both. |
| `last_modified` | timestamp | The timestamp of last activity to this placement. |
| `placements` | array of objects | The IDs of placements associated with this site. See [Placements](#placements) below for more details. |
| `content_categories` | array | Users can optionally specify one or more content categories for a placement. These categories can be used for targeting, and can be set at both the Site and Placement level. At most 20 categories can be set on a site. See [Content Categories](#content-categories) below for more details. |
| `intended_audience` | enum | The intended audience of the site. Must not be `null` if `'audited'` is `true`. Possible values: <br> - `children` <br> - `young_adult` <br> - `general` <br> - `mature`<br><br>**Default**: `null` |
| `inventory_attributes` | array | The sensitive attributes contained by the site; if set at the site level, `inventory_attributes` will also influence objects at the placement level. The mapping of IDs to attributes can be found below. The format of the array is also contained below.<br><br>**Default**: `null` |
| `audited` | boolean | Whether the site has been audited. |
| `publisher_join` | array |  |
| `publisher_name` | string (100) | Name of the publisher the site is under |
| `supply_type` | string | **Deprecated**. While this field will continue to default to "web", its value is ignored as the supply type is detected automatically by Xandr in each auction. Users must rely on Xandr’s automatic detection rather than specifying the supply type manually. <br><br>**Default**: `web`<br>|
| `creative_format_action` | string | - `exclude`: Allow all creative formats to serve on this site except those specified in the `creative_formats` array<br> - `include`: Only all creatives to serve whose format is included in the list specified in `creative_formats`<br><br>**Default**: `exclude`. <br>Some mobile application supply sources do not support all creative formats available on Xandr. |
| `creative_formats` | array of strings | The creative formats to be excluded or included in this site.<br><br>**Default**: `text` |
| `allowed_click_actions` | array of strings | Tells the buyer what types of click actions on creatives are supported. Mobile web and apps often allow additional click actions beyond click to a website, such as click-to-call, click-to-sms, click-to-email, and click-to-map.<br><br>**Default**: `click-to-web only` |
| `marketplace_map` | object | Informs the buyer which types of marketplaces are accessible (performance, RTB, deals). See [Marketplace Map](#marketplace-map) below for internal field definitions. |
| `mobile_app_instance` | multi-object | The [Mobile App Instance](./mobile-app-instance-service.md) associated with this site. This field can only be set when `supply_type` is `mobile_app`. See [Mobile App Instance](#mobile-app-instance) below for the internal field definitions.<br><br>**Required On**: `POST`, for sites with a `supply_type` of `mobile_app`. |
| `mobile_app_instance_id` | int | The ID of the mobile app instance associated with this site. This field is only associated with sites with a `supply_type` of `mobile_app`. |

## Marketplace map

| Parameter | Type | Description |
|:---|:---|:---|
| `an_audit_perf_only` | Boolean | **Read-only**. Whether the site is only eligible for CPA/CPC demand based on our auditing. If `true`, then yes.<br><br>**Default**: `false` |
| `rtb` | Boolean | Designates whether the inventory associated with the site (and all of its placements) is part of the RTB Marketplace (i.e., eligible for CPM demand).<br> - If `true`, all inventory associated with this site's placements is to be resold within the RTB Marketplace.<br> - The field cannot be set to `true` if any of the placements within the site support the expandable media type. See the [Placement Service](./placement-service.md) for more information about media types and subtypes fields.<br> - If `false`, expandable placements within the site cannot be moved to a site where the field is `true`.<br> - If set to `false` all inventory associated with this site's placements is only available to direct campaigns. No inventory associated with this placement group's placements will be resold.<br><br>**Default**: `true` |
| `performance` | Boolean | Whether the site is eligible for CPA/CPC demand using the updated performance marketplace. If `true`, then yes.<br><br>**Default**: `false` |
| `deals_allowed` | Boolean | Specifies whether deals are allowed to serve on this site.<br><br>**Default**: `true` |
| `rtb_suspended` | Boolean | **Read-only**. Indicates that all inventory associated with this site and its placements is blocked from participating in the RTB Marketplace.<br><br>**Default**: `false` |
| `deals_suspended` | Boolean | **Read-only**. Indicates that all deals are suspended from serving on this site.<br><br>**Default**: `false` |

## Mobile app instance

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of this app instance. This field is optional on `POST`; if sent, it will be used to look up the `bundle_id` and `os_family_id`. If this field is not set on a `PUT` or `POST`, you must pass in the `bundle_id` and `os_family_id` fields, and a new mobile app instance ID will be created. |
| `bundle_id` | int | If no `id` field is passed on `POST`, this field is required. This field represents the bundle ID of the mobile app instance, and it's used to look up the mobile app instance ID. If there is no app instance ID associated with this bundle ID, a new one will be created. |
| `os_family_id` | int | If no `id` field is passed in on `PUT` or `POST`, this field is required. This field represents the unique ID of the operating system family this app instance is associated with. If there is no app instance ID associated with this OS family ID, a new one will be created. |

## Placements

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier of the placement. You can use the [Placement Service](./placement-service.md) to find placement IDs. |
| `code` | string | The internal code for the placement. |

## Content categories

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | ID of the content category. You can use the [Content Category Service](./category-service.md) to find category IDs. |
| `is_system` | Boolean | Whether or not the content category is a system (`"universal"`) category. |
| `name` | string (100) | The name of the category. |
| `site` | array | List of IDs which fall under this content category. |
| `primary` | Boolean | Whether the category is the primary category for the site. Only one category can be primary. |

## Inventory attributes

| Parameter | Type | Description |
|:---|:---|:---|
| `inventory_attribute_id` | int | The ID of the inventory attribute. |
| `name` | string (50) | **Read-only**. The name of the inventory attribute. |

## Inventory attributes ID

| Id | Attribute Name |
|:---|:---|
| `2` | Political |
| `4` | Social Media |
| `6` | Photo & video sharing |
| `8` | Forums (moderated) |
| `10` | Forums (unmoderated) |
| `12` | Incentivized clicks |
| `14` | Non-English languages |
| `16` | Streaming Media |
| `17` | Toolbars, plugins, or extensions |

## Examples

### Adding content categories to a site

```
$ cat site

{
    "site": {
        "content_categories": [
            {
                "id": 2561,
                "primary": true
            },
            {
                "id": 2558
            }
        ],
        "name": "Site 1"
    }
}

$ curl -b cookies -c cookies -X PUT -d @site 'https://api.appnexus.com/site?id=5822'
```

### Viewing all sites for your publishers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/site'

{
   "response":{
      "status":"OK",
      "sites":[
         {
            "id":2411,
            "code":null,
            "name":"[Default RTB Media Buy] - ROS",
            "state":"active",
            "url":"",
            "primary_content_category_id":null,
            "last_modified":"2010-05-12 22:46:42",
            "intended_audience":"general",
            "inventory_attributes":[
                {
                    "id":2,
                    "name":"Political"
                }
            ]
            "placements":[

            ],
            "content_categories": [
                {
                    "id": 2561,
                    "primary": true
                },
                {
                    "id": 2558
                }
            ],
         },
         {
            "id":2412,
            "code":null,
            "name":"[Weekdays Only] - ROS",
            "state":"active",
            "url":"",
            "media_buy_id":1559,
            "primary_content_category_id": 2561,
            "last_modified":"2010-05-12 23:28:40",
            "placements":[

            ],
            "content_categories":null
         },
         {
            "id":2413,
            "code":null,
            "name":"[Weekends Only] - ROS",
            "state":"active",
            "url":"",
            "media_buy_id":1560,
            "primary_content_category_id":null,
            "last_modified":"2010-05-12 23:28:52",
            "placements":[

            ],
            "content_categories":null
         },
         {
            "id":5775,
            "code":null,
            "name":"[Conversion Test] - ROS",
            "state":"active",
            "url":"",
            "media_buy_id":4732,
            "primary_content_category_id":null,
            "last_modified":"2010-06-15 20:09:38",
            "placements":[
               {
                  "id":"57851"
               }
            ],
            "content_categories":null
         }
      ],
      "count":4,
      "start_element":null,
      "num_elements":null
   }
}        
```

### Create a site with a mobile app supply type

In this example we create a site designed for mobile app supply. We'll use it in our next example as well:

```
$ cat the-site.json
 
{"site":{"name":"One site to rule them all", "supply_type":"mobile_app"}}
 
$ curl -b cookies -X POST -d @the-site.json 'https://api.appnexus.com/site?publisher_id=102306'
 
{
    "response":{,
         "site":{
            "allowed_click_actions":[
                "click-to-web"
            ],
             "creative_formats":[
                "text"
            ],
             "inventory_attributes":null,
             "content_categories":null,
             "placements":null,
             "mobile_app_instance":null,
             "member_id":1309,
             "creative_format_action":"exclude",
             "supply_type":"mobile_app",
             "publisher_name":"RICH'S CRAZY RESELLER",
             "audited":false,
             "intended_audience":null,
             "last_modified":"2014-02-20 20:56:03",
             "primary_content_category_id":null,
             "publisher_id":102306,
             "url":"",
             "state":"active",
             "name":"One site to rule them all",
             "code":null,
             "id":273205
        },
         "num_elements":100,
         "start_element":0,
         "id":273205,
         "count":1,
         "status":"OK"
    }
}
```

### Add a mobile app instance to a site

In this example, we have a pre-existing site with the required mobile app supply type. We make a `PUT` call to associate our site with an existing mobile app instance, and we can see that it worked by viewing the updated object in the response. For more details on mobile app instances, see the [Mobile App Instance Service](./mobile-app-instance-service.md).

```
$ cat update.json

{"site":{"supply_type":"mobile_app", "mobile_app_instance":{"id":62}}}
 
$ curl -b cookies -X PUT -d @update.json
 
{
    "response":{
        "site":{
            "allowed_click_actions":[
                "click-to-web"
            ],
            "creative_formats":[
                "text"
            ],
            "inventory_attributes":null,
            "content_categories":null,
            "placements":null,
            "mobile_app_instance":{
                "os_family_id":3,
                "bundle_id":"2342342345566666",
                "id":62
            },
            "member_id":1309,
            "creative_format_action":"exclude",
            "supply_type":"mobile_app",
            "publisher_name":"RICH'S CRAZY RESELLER",
            "audited":false,
            "intended_audience":null,
            "last_modified":"2014-02-20 21:18:15",
            "primary_content_category_id":null,
            "publisher_id":102306,
            "url":"",
            "state":"active",
            "name":"One site to rule them all",
            "code":null,
            "id":273205
        },
        "num_elements":100,
        "start_element":0,
        "id":"273205",
        "count":1,
        "status":"OK"
    }
}
```

## Related topics

- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
- [Mobile App Instance Service](./mobile-app-instance-service.md)
- [Mobile App Service](./mobile-app-service.md)
