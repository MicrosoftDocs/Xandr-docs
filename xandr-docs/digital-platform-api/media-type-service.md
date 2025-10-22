---
title: Media Type Service
description: Explore the read-only Media Type service and ways to view all of its supported media types.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Media Type service

The Xandr platform categorizes creatives by format, media type, and media subtype:

- Format defines the resource type of the creative (flash, image, etc.)
- Media type defines the general display style of the creative (banner, expandable, video, etc.)
- Media subtype defines the specific display style of the creative (standard banner, MediaMind expandable, Standard VAST, etc.)

This read-only service allows you to view all of the supported media types.

> [!TIP]
> To view all supported formats and media subtypes, you can use the [Creative Format Service](creative-format-service.md) and the [Media Subtype Service](media-subtype-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/media-type](https://api.appnexus.com/media-type) | View all media types. |
| `GET` | [https://api.appnexus.com/media-type?id=MEDIA_TYPE_ID](https://api.appnexus.com/media-type?id=MEDIA_TYPE_ID) | View a specific media type. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | A code-friendly version of the media type's name. For example, `"Image and Text"` becomes `"image_and_text"`. |
| `id` | int | The ID of the media type. |
| `last_modified` | timestamp | The date and time when Xandr last modified the media type. |
| `media_type_group_id` | int | The group to which a media type belongs. This information is relevant for setting allowed media types on placements (see [Placement Service](placement-service.md)). Only media types that belong to the same group can be allowed on a single placement. |
| `name` | string  | The name of the media type. For example, `"Banner"`, `"Interstitial"`, or `"Video"`. |
| `uses_sizes` | enum | The size requirement for creatives belonging to the media type. <br>Possible values:<br>- `"always"`: Width and height are required when adding creatives (Banner and Expandable).<br>- `"sometimes"`: Width and height are sometimes required when adding creatives (Pop and Text).<br>- `"never"`: Width and height are not required when adding creatives (Interstitial, Video, and Skin). |

## Examples

### View all media types

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/media-type'
{
    "response": {
        "status": "OK",
        "count": 8,
        "start_element": null,
        "num_elements": null,
        "media-types": [
            {
                "id": 1,
                "name": "Banner",
                "media_type_group_id": 1,
                "uses_sizes": "always",
                "last_modified": "2012-03-16 21:36:10"
            },
            {
                "id": 2,
                "name": "Pop",
                "media_type_group_id": 2,
                "uses_sizes": "sometimes",
                "last_modified": "2012-03-16 21:36:10"
            },
            {
                "id": 3,
                "name": "Interstitial",
                "media_type_group_id": 1,
                "uses_sizes": "never",
                "last_modified": "2012-06-26 17:18:54"
            },
            {
                "id": 4,
                "name": "Video",
                "media_type_group_id": 4,
                "uses_sizes": "never",
                "last_modified": "2012-03-16 21:36:10"
            },
            {
                "id": 5,
                "name": "Text",
                "media_type_group_id": 1,
                "uses_sizes": "sometimes",
                "last_modified": "2012-03-16 21:36:10"
            },
            {
                "id": 6,
                "name": "Expandable",
                "media_type_group_id": 1,
                "uses_sizes": "always",
                "last_modified": "2012-03-16 21:36:11"
            },
            {
                "id": 8,
                "name": "Skin",
                "media_type_group_id": 1,
                "uses_sizes": "never",
                "last_modified": "2012-06-26 17:18:54"
            },
            {
                "id": 9,
                "name": "Facebook",
                "media_type_group_id": 6,
                "uses_sizes": "always",
                "last_modified": "2012-06-27 18:53:17"
            }
        ]
    }
}
```

### View the `"Video"` media type (ID 4)

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/media-type?id=4'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "media-type": {
            "id": 4,
            "name": "Video",
            "media_type_group_id": 4,
            "uses_sizes": "never",
            "last_modified": "2012-03-16 21:36:10"
        }
    }
}
```

### View media types that always require creatives to have a width and height

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/media-type?uses_sizes=always'
{
    "response": {
        "status": "OK",
        "count": 4,
        "start_element": 0,
        "num_elements": 100,
        "media-types": [
            {
                "id": 1,
                "name": "Banner",
                "media_type_group_id": 1,
                "uses_sizes": "always",
                "last_modified": "2012-03-16 21:36:10",
                "code": "banner"
            },
            {
                "id": 6,
                "name": "Expandable",
                "media_type_group_id": 1,
                "uses_sizes": "always",
                "last_modified": "2012-03-16 21:36:11",
                "code": "expandable"
            },
            {
                "id": 9,
                "name": "Facebook",
                "media_type_group_id": 6,
                "uses_sizes": "always",
                "last_modified": "2012-06-27 18:53:17",
                "code": "facebook"
            },
            {
                "id": 10,
                "name": "Image and Text",
                "media_type_group_id": 1,
                "uses_sizes": "always",
                "last_modified": "2013-10-31 20:31:59",
                "code": "image_and_text"
            }
        ]
    }
    }
```

## Related topics

- [Creative Format Service](creative-format-service.md)
- [Media Subtype Service](media-subtype-service.md)
