---
title: Native Layout Service
description: The Native Layout service allows sellers to specify and retrieve layouts for native creatives from a database using renderer and layout IDs.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Native Layout service

This service allows the seller to specify the layout for a native creative. Once the layout is in our database, it can be retrieved using the `renderer_id`, and subsequently the `layout_id`.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/native-layout?member_id=456` | Create a new layout. |
| `PUT` | `https://api.appnexus.com/native-layout?id=16&member_id=456` | Edit an existing layout. |
| `DELETE` | `https://api.appnexus.com/native-layout?id=123&member_id=456` | Delete a layout. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `data_assets` | array of objects | Attributes of the native creative. See [Data Assets](#data-assets) below for more details. |
| `image_assets` | array of objects | Specify the required attributes of each individual image. See [Image Assets](#image-assets) for more details. |
| `renderer` | object | The renderer ID of the seller. Enter the `id` in this array. Example:<br>`"renderer":{"id":1}` |

### Image assets

The `image_assets` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `aspect_ratios` | array of objects | Define the aspect ratios required for the `icon` image type. Required values are `min_width`, `ratio_width` and `ratio_height`. See [Example](#example-for-aspect_ratios).|
| `image_type` | string | The format of the image. Possible values include:<br> - `main_image`<br> - `icon_image` |
| `required` | int | Specify if the image is required.<br>Possible values: `1` - Required |
| `sizes` | array of objects | The size of the image. Specify both `width` and `height`. See [Example](#example-for-sizes). |

#### Example for `aspect_ratios`

```
"aspect_ratios": [
{
"min_width" : 100,
"ratio_width": 1,
"ratio_height": 2
}
]
```

#### Example for `sizes`

```
Example:
"sizes": [
{
"width": 300,
"height": 500
}
]
```

### Data assets

The `data_assets` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `data_type` | string | The asset type for the native creative. Possible values:<br> - `sponsored_by`<br> - `title`<br> - `description`<br> - `rating`<br> - `call_to_action`<br> - `display_url`<br> - `likes`<br> - `downloads`<br> - `price`<br> - `sale_price`<br> - `phone`<br> - `address`<br> - `additional_description` |
| `required` | int | If required then the value should be `1`. |
| `maximum_length` | int | The maximum length of the data asset. |

## Examples

### Create a new native layout protocol

```
$ cat native_layout

{
    "native-layout": {
        "renderer": {
            "id": 1
        },
        "image_assets":[
            {
                "image_type": "main_image", //depends on api.native_asset_image_type.name
                "required": 1,
                "sizes": [
                    {
                        "width": 300,
                        "height": 500
                    }
                ]
            },
            {
                "image_type": "icon_image",
                "aspect_ratios": [
                    {
                        "minimum_width" : 100,
                        "ratio_width": 1,
                        "ratio_height": 2
                    }
                ]
            }
        ],
        "data_assets": [
            {
                "data_type": "title", //depends on api.native_asset_data_type.name
                "required": 1,
                "maximum_length": 100
            }
        ]
    }
} 

$ curl -b cookies -c cookies -X POST -d @native_layout 'https://api.appnexus.com/native-layout?member_id=456'

{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "native-layout": {
            "id": 2,
            "member_id": 7,
            "renderer": {
                "id": 1
            },
            "data_assets": [
                {
                    "required": true,
                    "data_type": "title",
                    "maximum_length": 100
                }
            ],
            "image_assets": [
                {
                    "required": true,
                    "image_type": "main_image",
                    "sizes": [
                        {
                            "width": 300,
                            "height": 500
                        }
                    ],
                    "aspect_ratios": null
                },
                {
                    "required": false,
                    "image_type": "icon_image",
                    "sizes": null,
                    "aspect_ratios": [
                        {
                            "minimum_width": 100,
                            "ratio_width": 1,
                            "ratio_height": 2
                        }
                    ]
                }
            ]
        },
        ...
    }
}
```
