---
title: App Asset Service
description: Use the App Asset service to add app-related images to Akamai.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# App Asset service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This is an admin-only service that allows Xandr personnel to add app-related images to Akamai. This service is not available to any Apps Marketplace subscribers or developers.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/app-asset` | Add an image |
| `GET` | `https://api.appnexus.com/app-asset` | View all images |
| `GET` | `https://api.appnexus.com/app-asset?id=ID` | View a specific image |
| `GET` | `https://api.appnexus.com/app-asset?plugin_id=PLUGIN_ID` | View all images associated to a specific app |
| `DELETE` | `https://api.appnexus.com/app-asset?id=ID` | Delete an image |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of each image.<br>**Required On**: `PUT` and `DELETE`, in querystring. |
| `plugin_id` | int | The unque ID value of the plugin to which this image is associated.<br>**Required On**: `POST` |
| `description` | string | Text which describes the app asset.<br>**Default**: `null` |
| `category` | enum | The category in which the app asset belongs. The possible values: <br> - `"big_icon"` <br> - `"icon"` <br> - `"favicon"` <br> - `"screenshot"`<br><br>**Default**: `null`<br>**Required On**: `POST` |
| `width` | int | The width of the app asset, in pixels.<br>**Default**: `null` |
| `height` | int | The height of the app asset, in pixels. This must be at least **400**.<br>**Default**: `null` |
| `file_type` | enum | **Read only**. The image type of the app asset. Possible values are <br> - `"png"` <br> - `"jpg"` <br> - `"gif"`.<br><br>**Default**: `null` |
| `last_modified` | timestamp | **Read Only**. The date and time when the image was last modified. |
| `media_url` | string | **Read Only**. The URL to the hosted app asset. <br>**Default**: `null` |
| `content` | string  | The base 64 encoded content of the app asset. This field does not appear when you execute a `GET` command. <br>**Required On**: `POST` |
| `size_in_bytes` | int | **Read Only**. The size of the app asset in bytes. This cannot exceed **2 MB**.<br>**Default**: `0` |

## Image requirements

1. The `plugin_id` must be a valid one from the plugin service.
2. The number of app assets for each plugin_id cannot exceed the limit given by `allowed_asset_count` in the [Plugin Service](./plugin-service.md). The default is **5**.
3. The image size cannot exceed **2MB**.
4. The image type must be either **.jpg**, **gif**, or **.png**.
5. The image must be **base 64 encoded**.
6. The image height must be at least **400px**.
7. The following dimensions are required for these `category` types:
    - **big_icon:** 150 x 175
    - **icon:** 96 x 96
    - **favicon:** 16 x 16
    - **screenshot:** 640 x 400

## Examples

### Add an image

```
$ cat add-image.json
             {
             "app-asset": {
             "id":  "3466",
             "plugin_id": "91"
             }
             }
             $ curl -b cookies -c cookies -X PUT -d @add-image.json 'https://api.appnexus.com/app-asset'
             {
             "response":{
             "status":"OK",
             "count":1,
             "id":"3467",
             "start_element":null,
             "num_elements":null,
             "app-asset":{
             "id":3467,
             "plugin_id":92,
             "description":null,
             "category":"screenshot",
             "width":640,
             "height":400,
             "file_type":"jpeg",
             "media_url":"http:\/\/cdn.sand-08.adnxs.net\/s\/app_asset\/11\/d7\/55\/bc\/11d755bce0f9e7539b57408de1799204.jpeg",
             "size_in_bytes":49354
             },
             }
             }
```

### View a specific image

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/app-asset?id=3464'
             {
             "response":{
             "status":"OK",
             "count":1,
             "start_element":null,
             "num_elements":null,
             "app-asset":{
             "id":3467,
             "plugin_id":92,
             "description":null,
             "category":"screenshot",
             "width":640,
             "height":400,
             "file_type":"jpeg",
             "media_url":"http:\/\/cdn.sand-08.adnxs.net\/s\/app_asset\/11\/d7\/55\/bc\/11d755bce0f9e7539b57408de1799204.jpeg",
             "size_in_bytes":49354
             }
             }
             }
```

### View all images

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/app-asset'
             {
             "response":{
             "status":"OK",
             "count":3,
             "start_element":null,
             "num_elements":null,
             "app-assets":[
             {
             "id":3467,
             "plugin_id":92,
             "description":null,
             "category":"screenshot",
             "width":640,
             "height":400,
             "file_type":"jpeg",
             "media_url":"http:\/\/cdn.sand-08.adnxs.net\/s\/app_asset\/11\/d7\/55\/bc\/11d755bce0f9e7539b57408de1799204.jpeg",
             "size_in_bytes":49354
             },
             {
             "id":3468,
             "plugin_id":91,
             "description":"This is a description of the screenshot",
             "category":"screenshot",
             "width":640,
             "height":400,
             "file_type":"jpeg",
             "media_url":"http:\/\/cdn.sand-08.adnxs.net\/s\/app_asset\/11\/d7\/55\/bc\/11d755bce0f9e7539b57408de1799204.jpeg",
             "size_in_bytes":49354
             },
             {
             "id":3469,
             "plugin_id":47,
             "description":null,
             "category":"icon",
             "width":96,
             "height":96,
             "file_type":"png",
             "media_url":"http:\/\/cdn.sand-08.adnxs.net\/s\/app_asset\/1b\/65\/02\/14\/1b6502147d7fa34f5a75d722fb46e4f3.png",
             "size_in_bytes":15250
             }
             ]
             }}
```

### View all images associated to a specific app

```
$ curl -b cookies -c cookies 'http://sand.api.appnexus.com/app-asset?plugin_id=91' | json-pp
             {
             "response":{
             "status":"OK",
             "count":1,
             "start_element":null,
             "num_elements":null,
             "app-assets":[
             {
             "id":3468,
             "plugin_id":91,
             "description":"This is a description of the screenshot",
             "category":"screenshot",
             "width":640,
             "height":400,
             "file_type":"jpeg",
             "media_url":"http:\/\/cdn.sand-08.adnxs.net\/s\/app_asset\/11\/d7\/55\/bc\/11d755bce0f9e7539b57408de1799204.jpeg",
             "size_in_bytes":49354
             }
             ]
             }
             }
```

### Delete an image

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/app-asset?id=3468' |
             {
             "response":{
             "status":"OK",
             }
             }
```
