---
title: Bidders - Pixel Template Service
description: In this article, learn about bidders Pixel Template service, their JSON fields, and REST API with a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Pixel template service

This read-only service allows you to view information about Xandr-approved creative pixels from trusted, commonly-used providers, such as Evidon and Brilig. Most Xandr-approved creative pixels can be added to creatives without causing re-audit.

Here's how it works:

1. You use the Pixel Template Service to find the Xandr-approved pixel that you want to add to your creative.
1. You note the ID of the pixel as well as its required parameters.
1. You use the pixels array in [Creative Service](creative-service.md) to add the pixel to your creative and define values for the required parameters.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.adnxs.com/pixel-template` | To view all Xandr-approved creative pixels. |
| `GET` | `https://api.adnxs.com/pixel-template/PIXEL_TEMPLATE_ID` | To view a specific Xandr-approved creative pixel. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the Xandr-approved creative pixel. |
| `name` | string | The name of the Xandr-approved creative pixel. |
| `format` | enum | The format of the Xandr-approved creative pixel. Possible values: `"raw-js"`, `"url-html"`, `"url-js"`, or `"url-image"`. |
| `content` | string | The HTML or JavaScript content of the creative pixel. This field is included if format is `"raw-js"`. |
| `secure_content` | string | The secure HTML or JavaScript content of the creative pixel. This field is included if format is `"raw-js"`. |
| `url` | string | The URL of the html, JavaScript, or image creative pixel. This field is included if format is `"url-html"`, `"url-js"`, or `"url-image"`. |
| `secure_url` | string | The secure URL of the html, JavaScript, or image creative pixel. This field is included if format is `"url-html"`, `"url-js"`, or `"url-image"`. |
| `num_required_params` | int | The number of parameters that must be defined when adding the pixel to a creative. |
| `require_reaudit` | boolean | If true, adding the pixel to a creative causes the creative to be resubmitted for audit. |

## Examples

### View all Xandr-approved creative pixels

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/pixel-template'
{
    "response": {
        "status": "OK",
        "count": 3,
        "start_element": 0,
        "num_elements": 100,
        "pixel-templates": [
            {
                "id": 1,
                "name": "Evidon AdChoices Icon",
                "format": "raw-js",
                "content": "(function() {document.write('<sc'+'ript type=\"text/javascript\"' + ((\"https:\"
                 == document.location.protocol) ? \"https://c.betrad.com\" : \"http://c.betrad.com\") +
                 '/surly.js?;ad_wxh=${CREATIVE_SIZE};coid=${P1};nid=${P2};${P3}\"></scr'+'ipt>');}());",
                "num_required_params": 2,
                "require_reaudit": false
            },
            {
                "id": 2,
                "name": "Brilig Impression Tracker",
                "format": "url-image",
                "num_required_params": 1,
                "require_reaudit": false,
                "url": "http://p.brilig.com/contact/bct?pid=${P1}&_ct=pixel&adid=${CP_ID}&action=1"
            },
            {
                "id": 3,
                "name": "Alenty Impression Tracker",
                "format": "raw-js",
                "content": "var lnte = window.document.createElement('SCRIPT');lnte.src = 'http://js.alenty.com/
                 apnxs/l/adtrk.js'+'#customer_id=${P1}'+';advertiser=${ADV_ID}'+';campaign=${CP_ID}'+';creative=
                 ${CREATIVE_ID}'+';dimension=${WIDTH}x${HEIGHT}'+';site=${INV_SOURCE_ID}'+';sitepage=${PUBLISHER_ID}
                 _${SITE_ID}'+';external_id=-a--${SSP_DATA}-b--${PRICE_PAID}'+';url=' + encodeURIComponent
                 ('${REFERER_URL_ENC}'); lnte.type = \"text/javascript\"; window.document.body.insertBefore(lnte,
                 window.document.body.lastChild);",
                "num_required_params": 1,
                "require_reaudit": false
            },
            ...
        ],
        "dbg": {
            ...
        }
    }
}
```

### View a specific Xandr-approved creative pixel

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/pixel-template/1'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "pixel-template": {
            "id": 1,
            "name": "Evidon AdChoices Icon",
            "format": "raw-js",
            "content": "(function() {document.write('<sc'+'ript type=\"text/javascript\"' + ((\"https:\"
             == document.location.protocol) ? \"https://c.betrad.com\" : \"http://c.betrad.com\") +
             /surly.js?;ad_wxh=${CREATIVE_SIZE};coid=${P1};nid=${P2};${P3}\"></scr'+'ipt>');}());",
            "num_required_params": 2,
            "require_reaudit": false
        },
        "dbg": {
            ...
        }
    }
}
```
