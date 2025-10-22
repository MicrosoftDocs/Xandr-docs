---
title: Expandables and Rich Media
description: Enhance rich media support for supply platforms, integrating with exchanges like the Microsoft Advertising Exchange for adaptibility.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Expandables and rich media

## Overview

Xandr provides expandable rich media support on all supply from platform networks and Xandr-enabled exchanges, including the Microsoft Advertising Exchange.

## Creative specification

We have assembled a Xandr expandable specification based on the specs of our many supply sources. The goal is to have an "upload once, run everywhere" spec.

Creatives that do not meet this spec will still be allowed to run on the platform, but we expect publisher acceptance to be much lower.

**Allowed sizes and maximum expanded size**

| Base Size | Maximum Expanded Size |
|--|--|
| 120 x 600 | 240 x 600 |
| 160 x 600 | 320 x 600 |
| 300 x 250 | 500 x 300 |
| 468 x 60 | 468 x 210 |
| 728 x 90 | 728 x 300 |
| 234 x 60 | 300 x 250 |
| 120 x 60 | 120 x 240 |
| 180 x 150 | 300 x 300 |
| 300 x 600 | 560 x 600 |

## Media types

> [!TIP]
> For mobile interstitials, register creatives as standard banner and target interstitial sizes in the bid request.

Expandables are implemented through a broader "media type" system in Xandr. This system allows us to align placements and creatives so that all technical requirements are met for proper rendering.

Media types and subtypes are in a two-tiered hierarchy:

| Media Type | ID | Media Subtype | ID |
|--|--|--|--|
| **Banner** | 1 | Standard Banner | 1 |
|  |  | In-Banner Video | 3 |
| **Text** | 5 | Text | 9 |
| **Expandable** | 6 | Other Expandable | 10 |
|  |  | MediaMind | 11 |
|  |  | Pointroll | 12 |
|  |  | EyeWonder | 13 |
|  |  | eyeReturn | 14 |
|  |  | Pictela | 15 |
|  |  | Flashtalking | 16 |
|  |  | Doubleclick | 17 |
|  |  | Unicast | 18 |
|  |  | Spongecell | 19 |
|  |  | Adrime | 20 |
|  |  | Oggifinogi | 24 |
| **Skin** | 8 | Hi-Media Skin | 32 |
|  |  | IAB | 48 |
|  |  | Custom | 49 |
| **Image and Text** | 10 | Outlook.com | 52 |
| **High Impact** | 11 | ReactX Left/ Right | 53 |
|  |  | ReactX Top | 54 |
|  |  | ReactX Bottom | 55 |
|  |  | ReactX Custom | 56 |
|  |  | ReactX Over | 57 |
|  |  | ReactX Native | 58 |
|  |  | Lightbox | 59 |
|  |  | Foote | 60 |
|  |  | Slide-in | 61 |
|  |  | Peel | 62 |
|  |  | Custom | 63 |
| **Native** | 12 | In-Feed Standard | 65 |
|  |  | Content Marketing | 66 |
| **Audio** | 13 | 15-second | 67 |
|  |  | 30-second | 68 |
|  |  | Other | 69 |
|  |  | Standard VAST | 70 |
| **VAST** | 4 | **DEPRECATED** 15-second VAST | 7 |
|  |  | **DEPRECATED** 30-second VAST | 8 |
|  |  | **DEPRECATED** Other VAST | 23 |
|  |  | Standard VAST | 64 |

**Placements** may accept any combination of media types or subtypes. If they accept a media type, they accept all subtypes under the media type.

:::image type="content" source="media/placements.png" alt-text="Screenshot that display versatile placement information, allowing combinations of media types, automatically accepting associated subtypes.":::

**Templates** represent a media type and a creative format (Javascript, HTML, etc). They can be used to customize the rendering of your creatives, but in this case they simply specify the expandable vendor being used.

**Creatives** have one template, which specifies the format of the creative and the expandable vendor in use. A creative may serve only on placements that accept the creative template's media subtype or its parent media type.

:::image type="content" source="media/creatives.png" alt-text="Screenshot that details creative format and current expandable vendor. Creatives are limited to compatible placements based on media subtype or parent media type.":::

## Integration

There are two touch points for our expandable integration: a change to the RTB protocol, and a change to creative upload.

### RTB protocol

There will be two new fields in the bid request to indicate the availability of expandables on an impression.

| Field | Description | Notes |
|--|--|--|
| `allowed_media_types` | Array of media type IDs | This field is optional. If it appears, creatives of the specified media types may serve on this impression. |
| `allowed_media_subtypes` | Array of media subtype IDs | This field is optional. If it appears, creatives of the specified media subtypes may serve on this impression. |
| `media_subtypes` | Array of media subtype in string format | This field is optional. If it appears, it will list the allowed media in string format. |

These fields will be on each "tag" object in the bid request:

```
{
  "bid_request": {
    "tags": [
      {
        "allowed_media_types": [1,7,20],
        "allowed_media_subtypes": [5,23,40]
      }
    ]
  }
}
```

To determine if your expandable creative will serve:

- First, check if `allowed_media_types` contains the `Expandable` Media Type.
- If `Expandable` is not in `allowed_media_types`, check if the `media_subtype` ID is allowed in `allowed_media_subtypes`.

### Creative upload

When expandable creatives are uploaded to the **Creative Service**, you will need to denote the expandable ad server being used.

| Field | Description | Notes |
|--|--|--|
| template | JSON object with the ID of the associated template. | To denote an expandable, select the template that corresponds to the expandable vendor in use, and the creative format used by your bidder. If the vendor in use is not listed, use "Other Expandable". |

This field is **required** on expandable creatives.

**Example**:

```
{
  "creative": {
    "content": "<script src=...></script>",
    "template": {"id": 1}
  }
}
```

> [!NOTE]
>
> - You are not required to set the template ID on standard creatives (non-expandable). Continue uploading those creatives as you did before.
> - Traffic Skin creatives as a standard banner. We recommend using 1800 X 1000 dimensions.
   >   - Use template ID **6** for HTML, and **5** for Javascript.

**Template IDs**

The following table lists the available templates and their associated IDs.

> [!TIP]
> Expandables for bidders will only work with the templates listed below. Please do not use custom templates for expandables.
> [!WARNING]
> Creatives that are of the media type Expandable will not serve on external mobile supply. If it's a mobile expandable creative, use a template with the banner media type and non-iframe html format, and set up `alternative_landing_page_url` in your creative.

| Expandable Media Subtype | Creative Format | Template ID |
|--|--|--|
| Adrime | raw-html | 167 |
| Adrime | raw-js | 129 |
| Adrime | url-js | 117 |
| Doubleclick | raw-html | 164 |
| Doubleclick | raw-js | 126 |
| Doubleclick | url-js | 114 |
| EyeReturn | raw-html | 161 |
| EyeReturn | raw-js | 123 |
| EyeReturn | url-js | 111 |
| EyeWonder | raw-html | 160 |
| EyeWonder | raw-js | 122 |
| EyeWonder | url-js | 110 |
| Flashtalking | raw-html | 163 |
| Flashtalking | raw-js | 125 |
| Flashtalking | url-js | 113 |
| MediaMind | raw-html | 158 |
| MediaMind | raw-js | 120 |
| MediaMind | url-js | 108 |
| Oggifinogi | raw-html | 168 |
| Oggifinogi | raw-js | 130 |
| Oggifinogi | url-js | 118 |
| Other Expandable | raw-html | 157 |
| Other Expandable | raw-js | 119 |
| Other Expandable | url-js | 107 |
| Pictela | raw-html | 162 |
| Pictela | raw-js | 124 |
| Pictela | url-js | 112 |
| Pointroll | raw-html | 159 |
| Pointroll | raw-js | 121 |
| Pointroll | url-js | 109 |
| Spongecell | raw-html | 166 |
| Spongecell | raw-js | 128 |
| Spongecell | url-js | 116 |
| Unicast | raw-html | 165 |
| Unicast | raw-js | 127 |
| Unicast | url-js | 115 |

### Questions?

Please contact your Xandr account representative with any questions about expandable or video integration.

## Related topics

- [Rich Media Creatives on Mobile](rich-media-creatives-on-mobile.md)
- [Creative Service](creative-service.md)
- [Creative Template Service](creative-template-service.md)
