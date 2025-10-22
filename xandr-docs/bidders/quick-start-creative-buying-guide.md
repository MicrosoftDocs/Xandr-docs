---
title: Quick Start Creative Buying Guide
description: In this article, find information on getting a Xandr bidder customer started with creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Quick start creative buying guide

Here is a quick guide to help get you, as an Xandr bidder customer, up-and-running with creatives.

## Audit criteria

You will greatly increase the publishers you can reach if you have your creatives audited. Read the Creative Standards page in the UI to make sure your creatives are audited and ready to serve.

## Set up creatives

The way in which you set up creatives will depend on the type of creative you're working with.

### Third-party creatives

#### HTML URL

```
{ "creative":{
        "media_url":"[3RD_PARTY_HTML_URL]",
        "width":"980",
        "height":"120",
        "template": {
                "id": 1 } 
        } 
}
```

#### JavaScript URL

```
{ "creative": {
        "width": 320,
        "height": 50,
        "media_url": "[3RD_PARTY_JS_URL]",
        "template": {
                "id": 2 } 
        } 
}
```

### Third-party tag creatives

#### HTML

```
{ "creative": {
        "content": “[HTML_CREATIVE_CODE]",
        "width": "160",
        "height": "600",
        "template": {
        "id": 7 } 
        } 
}
```

#### JavaScript

```
{ "creative": {
        "content":”[JS_CREATIVE_CODE]",
        "width": "728",
        "height": "90",
        "template": {
                "id": 5 } 
        } 
}
```

### Dynamic creatives

For details on dynamic creatives, see [Submit Auditable Dynamic Creatives](submit-auditable-dynamic-creatives.md).

```
{"creative": {
        "content": "<script type='text/javascript' language='javascript'>
        if (${IS_PREVIEW}){
                document.write('<a href="[STATIC_URL_LANDING_PAGE]" target="_blank"><img src="[STATIC_URL_IMAGE]"></a>');}
        else{
                document.write('<a href=\"[DYNAMIC_URL_LANDING_PAGE_WITH_OPTIONAL_MACROS]" target=\"_blank\"><img src=\"[IMAGE_URL]"></a>');} </script>",
        "width": "320",
        "height": "50",
        "template": {
                "id": 7 } 
        } 
}
```

### Video

#### In-stream

```
{ "creative": {
        "width": "1280",
        "height": "720",
        "template": {
                "id": 6439 
        },
        "video_attribute": {
                "is_skippable": true,
                "duration_ms": 15000,
                "wrapper": {
                        "url": "[VAST_XML_URL]",
                        "secure_url": “[SECURE_ VAST_XML_URL]”
                        "elements": [
                                { "vast_element_type_id": 1, } ]
                        } 
                } 
        } 
}
```

#### Native

```
{
    "creative": {
        "brand_id": 1,
        "template": {
            "id": 39461
        },
        "native_attribute": {
            "link": {
                "url": "[YOUR_LANDING_PAGE]",
                "trackers": [{
                    "url": "[YOUR_CLICK_TRACKERS]",
                    "url_secure": "[YOUR_CLICK_TRACKERS_SECURE]"
                }]
            },
            "data_assets": [{
                "data_type": "title",
                "value": "[YOUR_TITLE]"
            }],
            "image_assets": [{
                "image_type": "main_image",
                "creative_asset_image": {
                    "url": "[URL_OF_IMAGE]",
                    "url_secure": "[URL_OF_IMAGE_SECURE]",
                    "height": 1,
                    "width": 1
                }
            }],
            "image_trackers": [{
                "url": "[YOUR_IMPRESSION_TRACKERS]",
                "url_secure": "[YOUR_IMPRESSION_TRACKERS_SECURE]"
            }],
            "javascript_trackers": [{
                "url": "[YOUR_JAVASCRIPT_TRACKERS]",
                "url_secure": "[YOUR_JAVASCRIPT_TRACKERS_SECURE]"
            }]
        }
    }
}
```

### Native video

In order to set up a native video creative, you must first register a video creative. You will then use the creative id from the video creative in the "video_assets.video_creative_id" field in the native creative.

#### Video registration

```
{ "creative": {
        "width": "1280",
        "height": "720",
        "template": {
                "id": 6439 
        },
        "video_attribute": {
                "is_skippable": true,
                "duration_ms": 15000,
                "wrapper": {
                        "url": "[VAST_XML_URL]",
                        "secure_url": “[SECURE_ VAST_XML_URL]”
                        "elements": [
                                { "vast_element_type_id": 1, } ]
                        } 
                } 
        } 
}
```

After POSTing the above video creative, you will use that creative id in the "video_assets.video_creative_id" field.

#### Native video registration

```
{
    "creative": {
        "brand_id": 1,
        "template": {
            "id": 39461
        },
        "native_attribute": {
            "link": {
                "url": "[YOUR_LANDING_PAGE]",
                "trackers": [{
                    "url": "[YOUR_CLICK_TRACKERS]",
                    "url_secure": "[YOUR_CLICK_TRACKERS_SECURE]"
                }]
            },
            "data_assets": [{
                "data_type": "title",
                "value": "[YOUR_TITLE]"
            }],
            "video_assets": [{
                                "video_creative_id": [VIDEO_CREATIVE_ID]
                        }],
            "image_trackers": [{
                "url": "[YOUR_IMPRESSION_TRACKERS]",
                "url_secure": "[YOUR_IMPRESSION_TRACKERS_SECURE]"
            }],
            "javascript_trackers": [{
                "url": "[YOUR_JAVASCRIPT_TRACKERS]",
                "url_secure": "[YOUR_JAVASCRIPT_TRACKERS_SECURE]"
            }]
        }
    }
}
```

### Audio

#### Use template ID 38745

```
{
    "creative": {
        "media_url": "[AUDIO_URL_XML_FILE]",
        "media_url_secure": "[SECURE_AUDIO_URL_FILE]",
                "click_target": "[URL_LINKED_TO_THE_BRAND]",
                "width": 1,
                "height": 1,
                "template": {
            "id": 38745
        },
        "video_attribute": {
                        "is_skippable": true,
                "duration_ms": 15000,
                "wrapper": {
                        "url": "[AUDIO_URL_XML_FILE]",
                                        "secure_url": "[SECURE_AUDIO_XML_URL_FILE]",
                        "elements": [
                                                {
                                        "vast_element_type_id": 1,
                                                        "type": "linear",
                                                        "trackers": null,
                                                        "media_files": [
                                                                {
                                                                        "mime_type": "audio"
                                                                }
                                                        ]
                                                }
                                        ]
                                }
                }
        }
}
```

## Macros

- You can use macros in the following fields:
  - `media_url`
  - `media_url_secure`
  - `content`
  - `content_secure`
  - `pixel_url`
- Macros don’t work inside a creative file.
- Nested macros (a macro within another macro) do not work with creatives.

## Related topics

- [Creative Service](creative-service.md)
- [Creative API Services](creative-api-services.md)
- [Xandr Macros](xandr-macros.md)
