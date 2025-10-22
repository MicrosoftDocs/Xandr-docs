---
title: Media Subtype Service
description: Explore the Media Subtype service, its supported media subtypes, along with information about the media types they are associated with.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Media Subtype service

The Xandr platform categorizes creatives by format, media type, and media subtype. Format defines the resource type of creatives (flash, image, etc.); media type defines the general display style of creatives (banner, expandable, video, etc.); and media subtype defines the specific display style of creatives (standard banner, MediaMind expandable, Standard VAST, etc.).

This read-only service allows you to view all of the supported media subtypes and the media types to which they belong.

> [!TIP]
> To view all supported formats and media types, you can use the [Creative Format Service](creative-format-service.md) and the [Media Type Service](media-type-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/media-subtype](https://api.appnexus.com/media-subtype) | View all media subtypes. |
| `GET` | [https://api.appnexus.com/media-subtype?id=MEDIA_SUBTYPE_ID](https://api.appnexus.com/media-subtype?id=MEDIA_SUBTYPE_ID) | View a specific media subtype. |
| `GET` | [https://api.appnexus.com/media-subtype?media_type.id=MEDIA_TYPE_ID](https://api.appnexus.com/media-subtype?media_type.id=MEDIA_TYPE_ID) | View media subtypes that belong to a specific media type. |

## JSON fields

| Field | Type (length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the media subtype. |
| `last_modified` | timestamp | The date and time when Xandr last modified the media subtype. |
| `media_type` | object | The media type to which the subtype belongs. For more details, see [Media Type](#media-type) below. |
| `name` | string | The name of the media subtype. For example, `"Standard Banner"`, `"In-Banner Video"`, or `"15-Second VAST"`. |
| `native_assets` | array of objects | An array describing constraints on elements of native ads for this media subtype. Elements of a native ad can include the title, body content, and more. The format's constraints could be whether body content is required or recommended, or how long the text may be. For more details, see [Native Assets](#native-assets) below. |
| `permitted_sizes` | array of objects | The permitted sizes for creatives of the media subtype. For more details, see [Permitted Sizes](#permitted-sizes) below. <br><br>**Note:** Not all media subtypes have permitted size requirements. |

### Media type

The `media_type` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of media type. |
| `media_type_group_id` | int | The group to which a media type belongs. This information is relevant for setting allowed media types on placements (see [Placement Service](placement-service.md)). Only media types that belong to the same group can be allowed on a single placement. |
| `name` | string | The name of the media type. For example, `"Banner"` or `"Video"`. |
| `uses_sizes` | enum | The size requirement for creatives belonging to the media type. Possible values:<br>- `"always"`: Width and height are required when adding creatives (Banner and Expandable).<br>- `"sometimes"`: Width and height are sometimes required when adding creatives (Pop and Text).<br>- `"never"`: Width and height are not required when adding creatives (Interstitial, Video, and Skin). |

### Permitted sizes

Each object in the `permitted_sizes` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `aspect_ratio_tolerance` | double | If `validate_image_size` and `scaling_permitted` are both `true`, the image can deviate from the aspect ratio of `platform_width` and `platform_height` by this amount. For example, the aspect ratio for a `platform_width` and `platform_height` of 254x133 is 1.19:1. If the `aspect_ratio_tolerance` is 0.03, an aspect ratio between 1.16:1 and 1.22:1 would be acceptable. |
| `max_image_height` | int | If `validate_image_size` is `true`, the maximum acceptable image height, in pixels, for creatives of this media subtype. |
| `min_image_height` | int | If `validate_image_size` is `true`, the minimum acceptable image height, in pixels, for creatives of this media subtype. |
| `max_image_width` | int | If `validate_image_size` is `true`, the maximum acceptable image width, in pixels, for creatives of this media subtype. |
| `min_image_width` | int | If `validate_image_size` is `true`, the minimum acceptable image width, in pixels, for creatives of this media subtype. |
| `platform_height` | int | The actual rendering height, in pixels, for creatives of this media subtype. This is also the height that appears in reporting. |
| `platform_width` | int | The actual rendering width, in pixels, for creatives of this media subtype. This is also the width that appears in reporting. |
| `scaling_permitted` | boolean | If `true`, the image for creatives of this media subtype must have the same aspect ratio as `platform_width`/`platform_height`.<br>If `false`, the image for creatives of this media subtype must have a width and height exactly matching `platform_width` and `platform_height`. |
| `validate_image_size` | boolean | If `true`, the image for creatives of this media subtype will be validated against the requirements defined by the following fields in this object: <br> - `scaling_permitted`<br> -  `aspect_ratio_tolerance`<br> - `min_image_width`<br> -  `max_image_width`<br> -  `min_image_height`<br> - `max_image_height` |

### Native assets

| Field | Type | Description |
|:---|:---|:---|
| `max_text_length` | int | The maximium allowable length of the text of the native asset for this media subtype, in characters. |
| `min_text_length` | int | The minimum allowable length of the text of the native asset for this media subtype, in characters. |
| `native_asset_name` | enum | The name of the native asset. This can be one of:<br> - `"title"`<br> - `"content"`<br> - `"description"`<br> - `"full_text"`<br> - `"context"`<br> - `"icon_img_url"`<br> - `"main_media"`<br> - `"cta"`<br> - `"rating"`<br> - `"click_fallback_url"` |
| `requirement` | enum | Whether this asset is required by this particular media subtype. This field can contain several levels of `"requiredness"`:<br>- `"required"`<br>- `"recommended"`<br>- `"optional"` |

## Examples

### View all media subtypes

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/media-subtype'
{
    "response": {
        "status": "OK",
        "count": 26,
        "start_element": null,
        "num_elements": null,
        "media-subtypes": [
            {
                "id": 1,
                "name": "Standard Banner",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 1,
                    "name": "Banner",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 2,
                "name": "Popup",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 2,
                    "name": "Pop",
                    "media_type_group_id": 2,
                    "uses_sizes": "sometimes"
                }
            },
            {
                "id": 3,
                "name": "In-Banner Video",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 1,
                    "name": "Banner",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 4,
                "name": "Popunder",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 2,
                    "name": "Pop",
                    "media_type_group_id": 2,
                    "uses_sizes": "sometimes"
                }
            },
            {
                "id": 5,
                "name": "Standard Interstitial",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 3,
                    "name": "Interstitial",
                    "media_type_group_id": 1,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 7,
                "name": "15-second VAST",
                "last_modified": "2012-02-17 22:58:10",
                "media_type": {
                    "id": 4,
                    "name": "Video",
                    "media_type_group_id": 4,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 8,
                "name": "30-second VAST",
                "last_modified": "2012-02-17 22:58:10",
                "media_type": {
                    "id": 4,
                    "name": "Video",
                    "media_type_group_id": 4,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 9,
                "name": "Text",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 5,
                    "name": "Text",
                    "media_type_group_id": 1,
                    "uses_sizes": "sometimes"
                }
            },
            {
                "id": 10,
                "name": "Other Expandable",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 11,
                "name": "MediaMind",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 12,
                "name": "Pointroll",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 13,
                "name": "EyeWonder",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 14,
                "name": "EyeReturn",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 15,
                "name": "Pictela",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 16,
                "name": "Flashtalking",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 17,
                "name": "Doubleclick",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 18,
                "name": "Unicast",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 19,
                "name": "Spongecell",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 20,
                "name": "Adrime",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 21,
                "name": "Layer",
                "last_modified": "2012-02-01 18:49:36",
                "media_type": {
                    "id": 3,
                    "name": "Interstitial",
                    "media_type_group_id": 1,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 22,
                "name": "Slide-in",
                "last_modified": "2012-02-01 18:49:37",
                "media_type": {
                    "id": 3,
                    "name": "Interstitial",
                    "media_type_group_id": 1,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 23,
                "name": "Other VAST",
                "last_modified": "2012-02-17 22:58:11",
                "media_type": {
                    "id": 4,
                    "name": "Video",
                    "media_type_group_id": 4,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 24,
                "name": "Oggifinogi",
                "last_modified": "2012-02-20 19:07:46",
                "media_type": {
                    "id": 6,
                    "name": "Expandable",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                }
            },
            {
                "id": 48,
                "name": "IAB",
                "last_modified": "2012-04-30 16:39:35",
                "media_type": {
                    "id": 8,
                    "name": "Skin",
                    "media_type_group_id": 1,
                    "uses_sizes": "never"
                }
            },
            {
                "id": 49,
                "name": "Custom",
                "last_modified": "2012-04-30 16:39:35",
                "media_type": {
                    "id": 8,
                    "name": "Skin",
                    "media_type_group_id": 1,
                    "uses_sizes": "never"
                }
            }
            }
        ]
    }
}
```

### View the `"Standard VAST"` media subtype (ID 64)

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/media-subtype?id=64'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "media-subtype": {
            "id": 64,
            "name": "Standard VAST",
            "last_modified": "2014-09-04 13:06:04",
            "media_type": {
                "id": 4,
                "name": "Video",
                "media_type_group_id": 4,
                "uses_sizes": "never"
            },
            "permitted_sizes": null,
            "native_assets": null
        }
    }
}
```

### View the media subtypes that belong to the `"Banner"` media type

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/media-subtype?media_type.id=1'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "media-subtypes": [
            {
                "id": 1,
                "name": "Standard Banner",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 1,
                    "name": "Banner",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                },
                "permitted_sizes": null
            },
            {
                "id": 3,
                "name": "In-Banner Video",
                "last_modified": "2012-01-27 16:14:43",
                "media_type": {
                    "id": 1,
                    "name": "Banner",
                    "media_type_group_id": 1,
                    "uses_sizes": "always"
                },
                "permitted_sizes": null
            }
        ]
    }
}
```
