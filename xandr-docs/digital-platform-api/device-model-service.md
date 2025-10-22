---
title: Digital Platform API - Device Model Service
description: Use the read-only Device Model service to view the registered models of mobile devices in the system, the make, device type, device screen size, and other details.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Device Model service

Mobile devices are categorized by make and model, where make is generally the manufacturer of the device (such as Apple) and model is generally the specific product (such as iPhone). The read-only Device Model Service allows you to see what models of mobile devices are registered in the Xandr system, as well as the make, device type (phone, tablet, or other device), device screen size, and supported capabilities (such as JavaScript creatives, Flash creatives, cookies) for each model. You can use this service to retrieve this data for targeting in mobile campaigns.

> [!NOTE]
> You can target mobile campaigns based on mobile carrier as well. For more details, see the [Carrier Service](./carrier-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/device-model` | View all device models |
| `GET` | `https://api.appnexus.com/device-model?device_type=DEVICE_TYPE` | View all device models of a specific type (i.e., `pc`, `phone`, or `tablet`) |
| `GET` | `https://api.appnexus.com/device-model?id=DEVICE_MODEL_ID` | View a specific device model |
| `GET` | `https://api.appnexus.com/device-model/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `codes` | array of objects | Third-party representations for the device model. See [Codes](#codes) below for more details. |
| `device_make_id` | int | The ID of the device make to which the model belongs. For example, the `iPhone` device model would belong to the `Apple` device make. |
| `device_make_name` | string | The name of the device make to which the model belongs. |
| `device_type` | enum | The type of device. Possible values: <br> - `pc` <br> - `phone` <br> - `tablet` <br> - `tv` <br> - `gameconsole` <br> - `stb` <br> - `mediaplayer` |
| `id` | int | The ID of the device model. |
| `name` | string | The name of the device model (such as `iPhone`). |
| `screen_height` | int | The height of the screen on the device. |
| `screen_width` | int | The width of the screen on the device. |
| `supports_cookies` | Boolean | **Not yet available**. If `true`, the device supports cookies. If `null`, Xandr does not know whether or not the device supports cookies. |
| `supports_flash` | Boolean | **Not yet supported**. If `true`, the device supports Flash creatives. If `null`, Xandr does not know whether or not the device supports Flash. |
| `supports_geo` | Boolean | **Not yet available**. If `true`, the device can pass the latitude and longitude of users, when GPS data is available.  |
| `supports_html_audio` | Boolean | **Not yet available**. If `true`, the device supports HTML audio creatives. If `null`, Xandr does not know whether or not the device supports HTML audio. |
| `supports_html_video` | Boolean | **Not yet available**. If `true`, the device supports HTML video creatives. If `null`, Xandr does not know whether or not the device supports HTML video. |
| `supports_js` | Boolean | **Not yet available**. If `true`, the device supports JavaScript creatives. If `null`, Xandr does not know whether or not the device supports JavaScript. |

### `Codes`

Each object in the `codes` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID for the device model. |
| `code` | string | The third-party representation for the device model. |
| `notes` | string | Identification information about the third-party. |
| `device_model_id` | int | The ID for the device model. |

## Examples

### View all models of mobile devices

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/device-model'
{
    "response": {
        "status": "OK",
        "count": 9033,
        "start_element": null,
        "num_elements": null,
        "device-models": [
            {
                "id": 1,
                "name": "Onetab XST2",
                "device_make_id": 1,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "4G Systems",
                "codes": [
                    {
                        "id": 1,
                        "code": "da-3499464",
                        "notes": "4G Systems:Onetab XST2",
                        "device_model_id": 1
                    }
                ]
            },
            {
                "id": 2,
                "name": "PAD7",
                "device_make_id": 2,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "A-Link",
                "codes": [
                    {
                        "id": 2,
                        "code": "da-3924965",
                        "notes": "A-Link:PAD7",
                        "device_model_id": 2
                    }
                ]
            },
            {
                "id": 3,
                "name": "A101",
                "device_make_id": 3,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "Acer",
                "codes": [
                    {
                        "id": 3,
                        "code": "da-3318996",
                        "notes": "Acer:A101",
                        "device_model_id": 3
                    }
                ]
            },
            {
                "id": 4,
                "name": "A200",
                "device_make_id": 3,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "Acer",
                "codes": [
                    {
                        "id": 4,
                        "code": "da-3334186",
                        "notes": "Acer:A200",
                        "device_model_id": 4
                    }
                ]
            },
            ...
        ]
    }
}
```

### View a specific model of mobile device

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/device-model?id=2'
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "device-model": {
            "id": 2,
            "name": "PAD7",
            "device_make_id": 2,
            "device_type": "tablet",
            "screen_width": null,
            "screen_height": null,
            "is_aggregated": false,
            "supports_js": null,
            "supports_cookies": null,
            "supports_flash": null,
            "supports_geo": null,
            "supports_html_video": null,
            "supports_html_audio": null,
            "device_make_name": "A-Link",
            "codes": [
                {
                    "id": 2,
                    "code": "da-3924965",
                    "notes": "A-Link:PAD7",
                    "device_model_id": 2
                }
            ]
        }
    }
}
```

### View all models of `"tablet"` devices

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/device-model?device_type=tablet'
{
    "response": {
        "status": "OK",
        "count": 547,
        "start_element": null,
        "num_elements": null,
        "device-models": [
            {
                "id": 1,
                "name": "Onetab XST2",
                "device_make_id": 1,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "4G Systems",
                "codes": [
                    {
                        "id": 1,
                        "code": "da-3499464",
                        "notes": "4G Systems:Onetab XST2",
                        "device_model_id": 1
                    }
                ]
            },
            {
                "id": 2,
                "name": "PAD7",
                "device_make_id": 2,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "A-Link",
                "codes": [
                    {
                        "id": 2,
                        "code": "da-3924965",
                        "notes": "A-Link:PAD7",
                        "device_model_id": 2
                    }
                ]
            },
            {
                "id": 3,
                "name": "A101",
                "device_make_id": 3,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "Acer",
                "codes": [
                    {
                        "id": 3,
                        "code": "da-3318996",
                        "notes": "Acer:A101",
                        "device_model_id": 3
                    }
                ]
            },
            {
                "id": 4,
                "name": "A200",
                "device_make_id": 3,
                "device_type": "tablet",
                "screen_width": null,
                "screen_height": null,
                "is_aggregated": false,
                "supports_js": null,
                "supports_cookies": null,
                "supports_flash": null,
                "supports_geo": null,
                "supports_html_video": null,
                "supports_html_audio": null,
                "device_make_name": "Acer",
                "codes": [
                    {
                        "id": 4,
                        "code": "da-3334186",
                        "notes": "Acer:A200",
                        "device_model_id": 4
                    }
                ]
            },
            ...
        ]
    }
}
```
