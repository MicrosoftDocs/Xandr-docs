---
title: Digital Platform API - Creative Macro Check Service
description: In this article, learn about the Digital Platform API's Creative Macro Check service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Creative Macro Check service

If you are running third party creatives, you can use this service to allow Xandr to check third party tags and append parameters in the query string, replace the domain, or insert Xandr click tracking macros in the appropriate place for you. We currently support the following ad servers: MediaMind, Atlas, Fetchback, and DoubleClick.

If we are able to insert the Xandr macros, then the new tag or URL will be returned in the response. If we are unable to ensure that the right macro was inserted (the value in the `existing_other_macros` or `unmatched` fields is not 0 within the response), then the value within the `new_content` or `new_media_url` field will not be displayed in the UI.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `PUT` | [https://api.appnexus.com/creative-macro-check](https://api.appnexus.com/creative-macro-check)<br>(replace_pattern_in_content_url JSON) | Replace content within a URL based on predefined patterns. |
| `PUT` | [https://api.appnexus.com/creative-macro-check?include_tests=1](https://api.appnexus.com/creative-macro-check?include_tests=1)<br>(replace_pattern_in_content_url JSON) | Replace content within a URL based on predefined patterns and test patterns. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `content` | string | **Field is used when modifying content.** The content that is being modified to include Xandr macros.<br>**Required On:** `PUT`, when transforming content. |
| `new_content` | string | **Field is populated when modifying content.** The updated content where all non-secure macros have been evaluated. This field will contain the same value as `content` unless all Xandr macros are successfully inserted. |
| `new_content_secure` | string | **Field is populated when modifying content.** The updated content where all macros, both secure and non-secure, have been evaluated. This field will contain the same value as `content` unless all Xandr macros are successfully inserted. |
| `media_url` | string | **Field is used when modifying a media URL.** The media URL that is being modified to include Xandr macros.<br>**Required On:** `PUT`, when transforming a media URL. |
| `new_media_url` | string | **Field is populated when modifying a media URL.** The updated media URL where all non-secure macros have been evaluated. This field will contain the same value as `media_url` unless all Xandr macros are successfully inserted. |
| `new_media_url_secure` | string | **Field is populated when modifying a media URL.** The updated media URL where all macros, secure and non-secure, have been evaluated. This field will contain the same value as `media_url` unless all Xandr macros are successfully inserted. |
| `recognized_servers` | array of strings | The names of the adservers that contain a URL pattern matching the value within the `content` or `media_url` field. For more information, see [Macro Replacements](#macro-replacements) below. |
| `found_urls` | int | The number of 'src=' or 'href=' URLs found in the creative content. |
| `matched_urls` | int | The number of `found_urls` that are from a recognized ad server. |
| `macro_replacements` | array | An array with information about replacements that were done, listed out by macro type (e.g., cachebuster). For more information, see [Macro Replacements](#macro-replacements) below. |
| `warning` | string | This field displays a warning message if the value within the `new_content_secure` or `new_media_url_secure` is not secure. |

## Macro replacements

| Field | Type | Description |
|:---|:---|:---|
| `type` | string | Specifies whether the object has information about the cachebuster or the `click_url`. |
| `replaced` | int | The number of URLs that had a macro for that `type` successfully inserted. |
| `existing_other_macro` | int | The number of URLs where we were able to determine where to insert the macro, but there was already something there, so we left it alone. If this value is not 0, then the value within the `new_content` or `new_media_url` field will not be displayed in the UI. |
| `existing_appnexus_macro` | int | The number of URLs where we were able to determine where to insert the macros. |
| `unmatched` | int | Number of URLs for which we could not determine how to insert the macros. If this value is not 0, then the value within the `new_content` or `new_media_url` field will not be displayed in the UI. |

## Recognized servers

| Field | Type | Description |
|:---|:---|:---|
| `adserver_name` | string | The name of the adserver. |

## Examples

### Replace macros within a third-party tag (content)

The content field can include multiple URLs, however in this example the content field only contains one URL.

```
{code}
$ cat /tmp/replace-macros-in-tag.json

{
    "creative-macro-check": {
        "content": "<a href=\"https://clk.atdmt.com/CCC/go/329458985/direct/01">test</a>"
    }
}

$ curl -b cookies -X PUT -d '@/tmp/replace-macros-in-tag.json' "https://api.appnexus.com/creative-macro-check"

{
  "response": {
    "status": "OK",
    "creative-macro-check": {
      "new_content": "<a href=\"${CLICK_URL}https:\/\/clk.atdmt.com\/CCC\/go\/329458985\/direct\/01\">test<\/a>",
      "new_content_secure": "<a href=\"${CLICK_URL}https:\/\/clk.atdmt.com\/CCC\/go\/329458985\/direct\/01\">test<\/a>",
      "content": "<a href=\"https:\/\/clk.atdmt.com\/CCC\/go\/329458985\/direct\/01\">test<\/a>",
      "media_url": null,
      "new_media_url": null,
      "new_media_url_secure": null,
      "recognized_servers": [
        "Atlas"
      ],
      "recognized_server": "Atlas",
      "found_urls": 1,
      "matched_urls": 1,
      "macro_replacements": [
        {
          "type": "click",
          "replaced": 1,
          "existing_other_macro": 0,
          "existing_appnexus_macro": 0,
          "unmatched": 0
        }
      ],
      "warning": "new_content_secure contains some non secure urls"
    },
    "count": 1,
    "start_element": null,
    "num_elements": null
  }
}
{code} 
```

### Replace macros within a third-party URL (media URL)

```
{code}
$ cat /tmp/replace-macros-in-url.json

{
    "creative-macro-check": {
        "media_url": "https://clk.atdmt.com/CCC/go/329458985/direct/01"
    }
}

$ curl -b cookies -c cookies -X PUT -d '@/tmp/replace-macros-in-url.json' 'https://api.appnexus.com/creative-macro-check'

{
  "response": {
    "status": "OK",
    "creative-macro-check": {
      "content": null,
      "new_content": null,
      "new_content_secure": null,
      "media_url": "https:\/\/clk.atdmt.com\/CCC\/go\/329458985\/direct\/01",
      "new_media_url": "${CLICK_URL}https:\/\/clk.atdmt.com\/CCC\/go\/329458985\/direct\/01",
      "matched_urls": 1,
      "new_media_url_secure": "${CLICK_URL}https:\/\/clk.atdmt.com\/CCC\/go\/329458985\/direct\/01",
      "recognized_servers": [
        "Atlas"
      ],
      "recognized_server": "Atlas",
      "found_urls": 1,
      "macro_replacements": [
        {
          "type": "click",
          "replaced": 1,
          "existing_other_macro": 0,
          "existing_appnexus_macro": 0,
          "unmatched": 0
        }
      ],
      "warning": "new_media_url_secure is not secure"
    },
    "count": 1,
    "start_element": null,
    "num_elements": null
  }
}
{code} 
```
