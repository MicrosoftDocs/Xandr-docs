---
title: Supply Partners - Bid Request
description: Learn about a bid request, their JSON fields, the placement mapping sequence, and examples to help you understand better.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Supply Partners - Bid request

> [!WARNING]
> We have disabled the Supply Integration (ASI) protocol(formerly AppNexus Supply Integration) for server-side supply integrations beginning on October 1st, 2017. We strongly encourage that you migrate your supply to the [OpenRTB protocol](openrtb-specs.md). Everything in this section is legacy content.

To send a bid request to Xandr, you `POST` a JSON-formatted file containing the bid request details to the following endpoint:

```
https://ib.adnxs.com/asi?member_id=YOUR_PROD_MEMBER_ID
```

For testing in our client-testing environment, you `POST` to the endpoint:

```
https://ib.client-testing.adnxs.net/asi?member_id=YOUR_TESTING_MEMBER_ID
```

For guidance on formatting your request, see the [Examples](#examples) at the bottom of the page.

## JSON fields

Where fields are available for internal and external values (for example, `int_blocked_categories` and `ext_blocked_categories`), include only one of the fields in your JSON-formatted file. If both are included, the internal value will be used.

| Field | Type | Description |
|:---|:---|:---|
| `an_user_id` | int | The Xandr ID for the user viewing the page. You include this field if you store user ID mappings in your system. For more details, see [User ID Mapping](user-id-mapping.md).<br>**Required:** yes, if `ext_user_id` is not included. |
| `ext_user_id` | string | The supply partner ID for the user viewing the page. You include this field if you store user ID mappings with Xandr. For more details, see [User ID Mapping](user-id-mapping.md).<br>**Required:** yes, if `an_user_id` is not included. |
| `ext_auction_id` | string | The supply partner ID for the auction. <br> **Required:** yes |
| `width` | int | The width of the placement.<br>**Required:** yes |
| `height` | int | The height of the placement.<br>**Required:** yes |
| `ad_format` | enum | The format of the creative that should be returned. Possible values: "iframe", "javascript", or "vast". <br><br>**Note about VAST:** The "vast" format is **not supported**. However, see the VAST bid request in the [Examples](#examples) section of what a bid request for a VAST video creative is likely to look like.<br><br>**Required:** yes |
| `template_id` | int | **Not yet supported**. For VAST video creatives, you may want Xandr to include custom parameters in the `ad_tag` field of the bid response. To accomplish this, Xandr can create a "supply template" for you, which you then reference here when requesting VAST video. For more details, see [Supply Templates](bid-response.md#supply-templates) in the Bid Response documentation.<br>**Required:** no |
| `ip_address` | string | The IP address for the user viewing the page.<br>**Required:** no |
| `is_secure` | boolean | True or false. The supply partner can request an SSL version of the creative by setting this to true. |
| `page_url` | string | The full domain of the bid request (do not pass an encoded URL).<br>**Required:** no |
| `position` | enum | The position of the placement on the page. Possible values: "above" (above the fold), "below" (below the fold), or "unknown".<br>**Default:** "unknown"<br>**Required:** no |
| `ext_pub_code` | string | The supply partner code for the publisher.<br>**Required:** no |
| `ext_placement_code` | string | The supply partner code for the placement.<br>**Required:** no |
| `an_placement_id` | int | The Xandr ID for the placement. To retrieve placement IDs, use the [Placement Service](../digital-platform-api/placement-service.md).<br>**Required:** no |
| `language` | int | The X ID for the language of the page. To retrieve language IDs, use the [Language Service](../digital-platform-api/language-service.md).<br>**Default:** 0<br>**Required:** no |
| `user_agent` | string | The user agent for the request (i.e., the browser).<br>**Required:** no |
| `int_blocked_technical_attributes` | array of ints  | The Xandr IDs for the creative technical attributes that are not permitted. To retrieve technical attribute IDs, use the [Technical Attribute Service](../digital-platform-api/technical-attribute-service.md).<br>**Required:** no |
| `ext_blocked_technical_attributes` | array of ints | The supply partner IDs for the creative technical attributes that are not permitted.<br>**Required:** no |
| `int_blocked_categories` | array of ints | The Xandr IDs for the creative categories that are not permitted. To retrieve category IDs, use the [Category Service](../digital-platform-api/category-service.md).<br>**Required:** no |
| `ext_blocked_categories` | array of ints | The supply partner IDs for the creative categories that are not permitted.<br>**Required:** no |
| `int_content_categories` | array of ints | The Xandr IDs for the content categories applied to the placement. You can use the [Content Category Service](../digital-platform-api/content-category-service.md) to view all possible values. This includes custom content categories created by the supply partner under its Xandr member.<br>**Default:** 0<br>**Required:** no |
| `ext_content_categories` | array of ints | The supply partner IDs for the content categories applied to the placement.<br>**Default:** 0<br>**Required:** no |
| `blocked_urls` | array of strings | The creative landing page URLs that are not permitted. Up to 20 URLs can be blocked. See [Example formatting](#example-formatting-blocked_urls) below. <br>**Required:** no |
| `blocked_languages` | array of ints  | The creative languages that are not permitted. To retrieve language IDs, use the [Language Service](../digital-platform-api/language-service.md).<br>**Required:** no |
| `int_blocked_brands` | array of ints  | The Xandr IDs for the brands that are not permitted. To retrieve brand IDs, use the [Brand Service](../digital-platform-api/brand-service.md).<br>**Required:** no |
| `age` | int | The age of the user viewing the page.<br>**Default:** 0<br>**Required:** no |
| `gender` | enum | The gender of the user viewing the page. Possible values: "male", "female", or "unknown".<br>**Default:** "unknown"<br>**Required:** no |
| `supply_type` | enum | The display environment. Possible values: "web", "mobile_app", "mobile_web", "in-stream-video", or "other".<br><br>**Tip:** The value of `supply_type` will override the supply type set at the [site](../digital-platform-api/site-service.md) level.<br><br>**Note:** The "in-stream-video" format is **not yet supported**.<br><br>**Default:** "web"<br>**Required:** no |

### Example formatting: `blocked_urls`

```
{
"blocked_urls": [
"landingpage1.com",
"landingpage2.com"
]
}
```

## Placement mapping

Xandr will submit a bid only when we can map your request to a placement in Xandr. We are looking up the following in the following sequence:

1. `an_placement_id`
1. `ext_placement_code`
1. `ext_pub_code` (the publisher's default tag)
1. Your member's default placement (set up for your account by your Technical Account Manager before production login credentials are even assigned).

If none of the above are available, Xandr will not submit a bid. Note that each `ext_placement_code` can map to only one placement in Xandr, and each `ext_pub_code` can map to only one publisher in Xandr.

## Examples

### Sending a minimally acceptable bid request

1. Create a JSON-formatted file including the required fields only. This example uses the `an_user_id` field, but you could use `ext_user_id` instead.

    ```
    $ cat bid_request |
                   {
                   "an_user_id": 1089773736613054100,
                   "ext_auction_id": "395dj2j2j2dd",
                   "ad_format":"iframe",
                   "width": 300,
                   "height": 250
                   }
    ```

1. `POST` the JSON-formatted file. Be sure to include your member ID in the querystring.

    ```
    curl -X POST -d @bid_request 'https://ib.adnxs.com/asi?member_id=123'
    ```

### Sending a bid request that includes Xandr values only

1. Create a JSON-formatted file with the fields for Xandr values instead of supply partner values, for example, `an_user_id` instead of `ext_user_id` and `int_blocked_technical_attributes` instead of `ext_blocked_technical_attributes`.

    ``` 
    "$ cat bid_request"{
       "an_user_id":1089773736613054100,
       "ext_auction_id":"395dj2j2j2dd",
       "width":300,
       "height":250,
       "ad_format":"iframe",
       "ip_address":"38.108.249.106",
       "page_url":"publisher.com",
       "position":"above",
       "ext_pub_code":"203pub",
       "ext_site_code":"145site",
       "an_placement_id":40,
       "language":1,
       "user_agent":"Mozilla/5.0 (X11; U; Linux x86_64; en-US; rv:1.9.1.8) Gecko/20100214 Ubuntu/9.10 (karmic) Firefox/3.5.8",
       "int_blocked_technical_attributes":[
          6,
          10,
          11
       ],
       "int_blocked_categories":[
          16,
          17,
          19
       ],
       "int_content_categories":[
          5,
          6,
          7
       ],
       "blocked_urls":[
          "landingpage1.com",
          "landingpage2.com",
          "landingpage3.com",
          "landingpage4.com",
          "landingpage5.com"
       ],
       "blocked_languages":[
          2,
          3,
          4,
          5,
          6,
          7,
          8,
          9,
          10
       ],
       "age":25,
       "gender":"male",
       "supply_type":"web"
    }
    ```

1. `POST` the JSON-formatted file. Be sure to include your member ID in the querystring.

    ```
    curl -X POST -d @bid_request 'https://ib.adnxs.com/asi?member_id=123'
    ```

### Sending a bid request that includes external values only

1. Create a JSON-formatted file with the fields for supply partner values instead of Xandr values, for example, `ext_placement_code` instead of `an_placement_id` and `ext_blocked_categories` instead of `int_blocked_categories`.

    ```
    $ cat bid_request
    {
        "ext_user_id": 1089773736613054100,
        "ext_auction_id": "395dj2j2j2dd",
        "width": 300,
        "height": 250,
        "ad_format": "iframe",
        "ip_address": "38.108.249.106",
        "page_url": "publisher.com",
        "position": "above",
        "ext_pub_code": "203pub",
        "ext_site_code": "145site",
        "ext_placement_code": "40placement",
        "language": 1,
        "user_agent": "Mozilla/5.0 (X11; U; Linux x86_64; en-US; rv:1.9.1.8) Gecko/20100214 Ubuntu/9.10 (karmic) Firefox/3.5.8",
        "ext_blocked_technical_attributes": [
            3,
            5,
            8
        ],
        "ext_blocked_categories": [
            2,
            15,
            20
        ],
        "ext_content_categories": [
            2,
            9,
            13
        ],
        "blocked_urls": [
            "landingpage1.com",
            "landingpage2.com",
            "landingpage3.com",
            "landingpage4.com",
            "landingpage5.com"
        ],
        "blocked_languages": [
            2,
            3,
            4,
            5,
            6,
            7,
            8,
            9,
            10
        ],
        "age": 25,
        "gender": "male",
        "supply_type": "web"
    }
    ```

1. `POST` the JSON-formatted file. Be sure to include your member ID in the querystring.

    ```
    curl -X POST -d @bid_request 'https://ib.adnxs.com/asi?member_id=123'
    ```

### Sending a bid request that does not include blocking details

If you set up ad profiles to enforce your publishers' preferences, you do not need to specify blocking details in your bid request.

1. Create a JSON-formatted file excluding the fields for blocking technical attributes, creative categories, content categories, URLs, and languages.

    ```
    $ cat bid_request
    {
        "an_user_id": 1089773736613054100,
        "ext_auction_id": "395dj2j2j2dd",
        "width": 300,
        "height": 250,
        "ad_format": "iframe",
        "ip_address": "38.108.249.106",
        "page_url": "publisher.com",
        "position": "above",
        "ext_pub_code": "203pub",
        "ext_site_code": "145site",
        "an_placement_id": "40",
        "language": 1,
        "user_agent": "Mozilla/5.0 (X11; U; Linux x86_64; en-US; rv:1.9.1.8) Gecko/20100214 Ubuntu/9.10 (karmic) Firefox/3.5.8",
        "age": 25,
        "gender": "male",
        "supply_type": "web"
    }
    ```

1. `POST` the JSON-formatted file. Be sure to include your member ID in the querystring.

    ```
    curl -X POST -d @bid_request 'https://ib.adnxs.com/asi?member_id=123' 
    ```

### Sending a bid request for a VAST video creative (NOT YET SUPPORTED)

When requesting a VAST video creative:

- The `ad_format` must be set to "vast".
- The `width` must be set to 1.
- The `height` must be set to 1.
- The request must map to a placement in the Xandr system that allows creatives of the "Video" media type or any combination of the "15-Second VAST", "30-Second VAST", or "Other VAST" media subtypes. If the request maps to a non-video placement, AppNexus will respond with an error (Request ad format does not match the placement format). For details about how we look up the placement to use, see [Placement Mapping](#placement-mapping) above.
- Do not pass `int_blocked_technical_attributes` or `ext_blocked_technical_attributes` to define which VAST video durations you want. Instead, as mentioned above, the Xandr placement should define the allowed VAST video duration.
- If you have asked Xandr to set up a supply template to include custom parameters in the `ad_tag` field of our bid response, set `template_id` to the ID of that supply template. For more details, see Supply Templates in the Bid Response documentation.

1. Create a JSON-formatted file according to the requirements above. This example assumes that there is a specific placement in the Xandr system defined to allow VAST video creatives. The ID of this placement is passed in the `an_placement_id` field.

    ```
    $ cat bid_request
    {
        "an_user_id": 1089773736613054100,
        "ext_auction_id": "395dj2j2j2dd",
        "ad_format":"vast",
        "width": 1,
        "height": 1.
        "an_placement_id": 204,
        "tmpl_id": 4,
        "ip_address": "38.108.249.106",
        "page_url": "ibdo.com",
        "position": "unknown",
        "language": 0,
        "user_agent": "Mozilla/5.0 (X11; U; Linux x86_64; en-US; rv:1.9.1.8) Gecko/20100214 Ubuntu/9.10 (karmic) Firefox/3.5.8",
        "age": 25,
        "gender": "female"
    }
    ```

1. `POST` the JSON-formatted file. Be sure to include your member ID in the querystring.

    ```
    curl -X POST -d @bid_request 'https://ib.adnxs.com/asi?member_id=123'
    ```
