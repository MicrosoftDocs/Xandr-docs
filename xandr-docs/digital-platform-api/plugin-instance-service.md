---
title: Plugin Instance Service
description: Use the Plugin Instance service to create and manage umbrella and specific app instances for Apps marketplace.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Plugin Instance service

When you develop an app for the Apps Marketplace, you build an umbrella app and then one or more specific app instances that plug into the workflow in different places. The Plugin Instance Service allows you to create and control these instances. For information about creating and managing an umbrella app, see the [Plugin Service](./plugin-service.md).

## REST API

> [!NOTE]
> There are three different user roles, two of which that can make calls to this service:
>
> - **App Providers** - Members who develop apps in the Apps Marketplace.
> - **App Subscribers** - Members who subscribe to and use apps.
> - **Non-member Developers** - These app developers are not associated to members and cannot make calls to this service.
>
> Certain roles are restricted from making one or more calls. The roles that can make the calls are specified in the **Description** column in the table below.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/plugin-instance`<br>(plugin-instance JSON) | Add an app.<br> - App Providers.<br> - App Subscribers. |
| `PUT` | `https://api.appnexus.com/plugin-instance?id=PLUGIN_INSTANCE_ID`<br>(plugin-instance JSON) | Modify an app.<br> - App Providers. |
| `GET` | `https://api.appnexus.com/plugin-instance` | View all apps instances.<br> - App Providers.<br> - App Subscribers (will only see instances to which they are associated). |
| `GET` | `https://api.appnexus.com/plugin-instance?id=PLUGIN_INSTANCE_ID` | View a specific app instance.<br> - App Providers.<br> - App Subscribers (will only see an instance if they are associated to it). |
| `DELETE` | `https://api.appnexus.com/plugin-instance?id=PLUGIN_INSTANCE_ID` | Delete an app instance.<br> - App Providers |
| `DELETE` | `https://api.appnexus.com/plugin?id=PLUGIN_INSTANCE_ID` | Delete all apps installed by a subscriber. |
| `DELETE` | `https://api.appnexus.com/plugin-instance?id=PLUGIN_INSTANCE_ID` | Delete all apps created by a developer. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `description` | string | The tooltip that displays when you hover over the app instance.<br><br>**Default**: `null` |
| `flavor` | enum | The location where the app is integrated into the  workflow. Possible values:<br> - `"standalone"` - The app is available to network users in the main **Apps** tab.<br> - `"creative_action"` - The app is available to network users directly from the **Creative Manager** screen.<br> - `"advertiser_menu"` - The app is available to advertiser users in the **Advertisers** tab.<br> - `"publisher_menu"` - The app is available to publisher users in the **Publishers** tab.<br> - `"conversion_pixel"` - The app uses a tracking pixel to count the number of downloads of this app.<br><br>**Required On**: `POST` |
| `icon_url` | string | The URL of the icon that is displayed with the app instance.<br><br>**Default**: `null` |
| `id` | int | The ID of the app instance.<br><br>**Default**: Auto-generated number<br>**Required On**: `PUT`/`DELETE`, in query string |
| `iframe_url` | string | The URL pointing to the content of the app.<br><br>**Required On**: `POST` |
| `name` | string | The name that is displayed with the app instances.<br><br>**Required On**: `POST` |
| `plugin_id` | int | The ID of the app that the instance belongs to.<br><br>**Required On**: `POST` |
| `proxy_url` | string | The URL of the `proxy.md` file. This proxy file allows for cross-frame communication between and your app. It must be uploaded to a URL on the same domain as your app.<br><br>**Required On**: `POST` |

## Examples

### Add an app

```
$ cat plugin_instance.json
{
   "plugin-instance": {
       "name": "Test instance 1",
       "plugin_id": 45,
       "flavor": "standalone",
       "iframe_url": "https://www.iframe_url.com",
       "name": "Test Instance 1",
       "description": "This is the tooltip for Test Instance 1.",
       "icon_url": "https://www.icon_url.com",
       "proxy_url": "https://www.iframe_url.com/proxy.md"
   }
}
$ curl -b cookies -c cookies -X POST -d @plugin_instance 'https://api.appnexus.com/plugin-instance'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 65,
        "start_element": null,
        "num_elements": null,
        "plugin-instance": {
            "id": 65,
            "plugin_id": 45,
            "flavor": "standalone",
            "iframe_url": "https://www.iframe_url.com",
            "js_api_version": "",
            "name": "Test Instance 1",
            "description": "This is the tooltip for Test Instance 1.",
            "icon_url": "https://www.icon_url.com",
            "proxy_url": "https://www.iframe_url.com/proxy.md"
        },
        "dbg_info": {
            ...
        }
    }
}
```

### Modify an app

```
$ cat modify-plugin.json
{
    "plugin-instance": {
       "name": "Napoleon Bonaparte"
    }
}
$ curl -b cookies -c cookies -X PUT -d @modify-plugin.json 'https://sand.api.appnexus.com/plugin-instance?id=146' | json-pp
{
    "response":{
        "status":"OK",
        "count":1,
        "id":"146",
        "start_element":null,
        "num_elements":null,
        "plugin-instance":{
            "id":146,
            "plugin_id":101,
            "flavor":"advertiser_menu",
            "iframe_url":"https:\/\/www.myadgent.com\/logos",
            "js_api_version":"",
            "name":"Napoleon Boneparte",
            "description":null,
            "icon_url":null,
            "proxy_url":"https:\/\/www.myadgent.com\/logos\/video-appnexus-96-96.png"
        },
        "dbg_info":{
            ...
        }
    }
}
```

### View all apps

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/plugin-instance'
{
    "response": {
        "status": "OK",
        "count": 58,
        "start_element": null,
        "num_elements": null,
        "plugin-instances": [
            {
                "id": 2,
                "plugin_id": 1,
                "flavor": "campaign_profile_segment",
                "iframe_url": "https://host.appnexus/segment-targeting/boolean/",
                "js_api_version": "",
                "name": "Advanced Segment Chooser",
                "description": "Allows you to select groups of segments and perform boolean comparison of them.",
                "icon_url": "https://console.appnexus.com/favicon.ico",
                "proxy_url": "https://host.appnexus/proxy_new.md"
            },
            {
                "id": 3,
                "plugin_id": 2,
                "flavor": "standalone",
                "iframe_url": "https://my.evidon.com/tag?i=17",
                "js_api_version": "",
                "name": "Evidon",
                "description": "Evidon InForm enables businesses to comply with privacy laws and self-regulatory programs  across North America and Europe.",
                "icon_url": "https://betteradblog.files.wordpress.com/2011/11/adchoices14x16.png",
                "proxy_url": "https://my.evidon.com/client_plugins/proxy.md"
            },
            {
                "id": 4,
                "plugin_id": 3,
                "flavor": "standalone",
                "iframe_url": "https://agents.proximic.com/appnexus/v1/index.jsp",
                "js_api_version": "",
                "name": "Agents",
                "description": "Add powerful contextual and brand safety data to your media buy.",
                "icon_url": "https://static.proximic.com/img/proximic_appnexus_16x16.png",
                "proxy_url": "https://agents.proximic.com/appnexus/v1/proxy.md"
            },
            {
                "id": 5,
                "plugin_id": 4,
                "flavor": "standalone",
                "iframe_url": "https://audexp.apps.exelate.com",
                "js_api_version": "",
                "name": "Audience eXplorer",
                "description": "eXelate provides data on online purchase intent, household demographics and behavioral propensities that enable digital advertisers to make optimal marketing decisions.",
                "icon_url": "https://www.exelate.com/favicon.ico",
                "proxy_url": "https://audexp.apps.exelate.com/AppNexusPluginProxy"
            },
            {
                "id": 6,
                "plugin_id": 5,
                "flavor": "standalone",
                "iframe_url": "https://e1.targusinfo.com/plugin/e1anx.md",
                "js_api_version": "",
                "name": "Audience Wizard",
                "description": "Create customized audience groups based on TARGUSinfos offline data  including thousands of demographic, branding, product, lifestyle/lifestage and consumer behavior profiles.",
                "icon_url": "https://targusinfo.com/files/images/16x16_T.png",
                "proxy_url": "https://e1.targusinfo.com/plugin/e1anxproxy.md"
            },
            {
                "id": 7,
                "plugin_id": 6,
                "flavor": "standalone",
                "iframe_url": "https://marketplace.brilig.com/brilig-webapp/loginAppNexusOuterFrame.jsp",
                "js_api_version": "",
                "name": "Audience DataMizer",
                "description": "Access recommended audience buys and the ability to shop for and deploy 15 billion data points, encompassing 7,500 audience segments from 200 million profiles.",
                "icon_url": "https://cdn.adnxs.com/applogos/brilig16_16.png",
                "proxy_url": "https://marketplace.brilig.com/brilig-webapp/proxy.md"
            },
            ...
        ],
        "dbg_info": {
            ...
        }
    }
}
```

### View a specific app

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/plugin-instance?id=32'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "plugin-instance": {
            "id": 32,
            "plugin_id": 27,
            "flavor": "standalone",
            "iframe_url": "https://apps.eyereturn.com/appnexus-app/",
            "js_api_version": "",
            "name": "eyeReturn",
            "description": "Build a rich media banner featuring multiple products and messages  No experience needed!",
            "icon_url": "https://www.eyereturnmarketing.com/img/logos/erm_app_logo_16x16.png",
            "proxy_url": "https://apps.eyereturn.com/appnexusproxy.md"
        },
        "dbg_info": {
            ...
        }
    }
}
```

### Delete an app

```
$ curl -b cookies -c cookies -X DELETE 'https://sand.api.appnexus.com/plugin-instance?id=20' | json-pp
{
    "response":{
        "status":"OK",
        "dbg_info":{
            ...
        }
    }
}
```
