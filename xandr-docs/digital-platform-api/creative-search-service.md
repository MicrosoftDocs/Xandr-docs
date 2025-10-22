---
title: Digital Platform API - Creative Search Service
description: In this article, learn about the Digital Platform API's Creative Search service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Creative Search service

This read-only service allows you to search for **active** creatives ased on specific criteria, such as audit status, ID, size, etc. You may then wish to use these creative IDs in the [Ad Profile Service](ad-profile-service.md). To add creatives to the system, see the [Creative Service](creative-service.md).

> [!NOTE]
> Since this service searches all active creatives on the AppNexus platform (not just your own), a search that is too broad might cause an error. To ensure that you get results, narrow your search as much as possible.

This API also enables certain native fields searchable through creative search.

The searchable fields are as follows:

- title (1)
- description (2)
- call_to_action (3)
- additional_description (13)

The search will return a creative if the search term matches any text in any of the aforementioned fields.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/creative-search](https://api.appnexus.com/creative-search)<br> (creative_search JSON) | Search for creatives. |
| `POST` | [https://api.appnexus.com/creative-search?sort=FIELD_NAME.ASC_OR_DESC](https://api.appnexus.com/creative-search?sort=FIELD_NAME.ASC_OR_DESC)<br>(creative_search JSON) | Search for creatives and sort results. |

> [!NOTE]
> The fields used to search for creatives are not exactly the same as the fields returned. This is because the returned objects are drawn from the [Creative Service](creative-service.md) and formatted accordingly.

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `creative_ids` | array of integers | Search for creatives by their IDs.<br>**Sortable:** Yes, use "id" in query string. |
| `description` | string | Search for creatives by terms in their descriptions.<br>**Sortable:** No |
| `audit_status` | array of enums | Search for creatives by their audit status. Possible values: `"no_audit"`, `"pending"`, `"rejected"`, `"audited"`.<br>**Sortable:** Yes |
| `ad_profile_id` | int | **Must be used with `brand_status`.** Search for a creative by the ID of its ad profile.<br>**Sortable:** No |
| `brand_status` | array of enums | **Must be used with `ad_profile_id`.** Search for creatives by their brand status. For example, if this is set to `"trusted"`, all trusted brands within the ad profiles specified in `ad_profile_id` will be returned in the response. Possible values: `"trusted"`, `"case-by-case"`, `"banned"`. The brand status field is only returned in the response when you use this filter.<br>**Sortable:** No |
| `review_status` | array of enums | Search for creatives based on their review status (from the associated ad profiles). Possible values: `"reviewed"`, `"unreviewed"`. The review status field is only returned in the response when you use this filter.<br>**Sortable:** No |
| `uploaded_since` | timestamp | Search for creatives that were uploaded since this date. <br>Format: "YYYY-MM-DD HH:MM:SS".<br>**Sortable:** No |
| `modified_since` | timestamp | Search for creatives that were modified since this date. <br>Format: "YYYY-MM-DD HH:MM:SS".<br>**Sortable:** No |
| `formats` | array of enums | Search for creatives by their formats. Possible values: `"url-html"`, `"url-js"`, `"flash"`, `"image"`, `"raw-js"`, `"raw-html"`, `"iframe-html"`, `"url-vast"`, `"text"`.<br>**Sortable:** Yes, use "format" in query string. |
| `media_subtype` | array of enums | **Deprecated, use `media_subtype_ids` instead.** Search for creatives by their media subtypes. Possible values: `"Banner"`, `"Popup"`, `"Popunder"`.<br>**Sortable:** No |
| `media_subtype_ids` | array of integers | Search for creatives by their media subtype via ID. You can use the [Media Subtype Service](media-subtype-service.md) to look up the desired ID's.<br>**Sortable:** Yes, use `"media_subtype_id"` in query string. |
| `media_url` | string | Search for a creative by its URL.<br>**Sortable:** Yes |
| `media_content` | string | Search for a creative by the data in its original_content field (see [Creative Service](creative-service.md)).<br>**Sortable:** No |
| `sizes` | array of strings | Search for creatives by their sizes, for example, "728x90".<br>**Sortable:** Yes, use `"width"` and `"height"` in query string. |
| `brand_ids` | array of integers | Search for creatives by the IDs of their brands.<br>**Sortable:** No |
| `member_ids` | array of integers | **Must be used with `member_action`.** Search for creatives by the IDs of their members.<br>**Sortable:** Yes, use `"member_id"` in query string. |
| `member_action` | enum | **Must be used with `member_ids`.** If this is set to `"exclude"`, you exclude the members specified in `member_ids` from the search. Otherwise, the specified IDs are included.<br>**Sortable:** No |
| `template_id` | int | Search for creatives by their creative template IDs.<br>**Sortable:** Yes |
| `size_in_bytes` | string | **Not a filter.** Sort results in ascending/descending size order.<br>**Sortable:** Yes |
| `click_url` | string | **Not a filter.** Sort results in ascending/descending alphabetical click URL order.<br>**Sortable:** Yes |
| `landing_page_url` | string |**Not a filter.** Sort results in ascending/descending alphabetical landing page URL order.<br>**Sortable:** Yes |

## Examples

### Search for all banner creatives that have passed AppNexus audit

```
$ cat creative_search
{
   "creative-search": {
      "audit_status": [
         "audited"
      ],
      "media_subtype": [
         "banner"
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X POST -d @creative_search 'https://api.appnexus.com/creative-search'

{
   "response": {
      "status": "OK",
      "creatives": [
         {
            "id": "48652",
            "width": "300",
            "height": "250",
            "media_url": "https:\/\/cdn.adnxs.com\/p\/05\/d1\/cd\/fe\/05d1cxxxxxx221db2ba8b.png",
            "content": null,
            "format": "image",
            "member_id": "408",
            "brand_id": "1",
            "click_url": "https:\/\/www.sample.com",
            "audit_status": "audited",
            "size_in_bytes": "14545",
            "landing_page_url": null,
            "last_activity": "2010-07-23 16:40:41",
            "created_on": "2010-04-30 07:20:23",
            "media_subtypes": [
               "banner"
            ],
            "pop_values": null
            },
         {
            "id": "73163",
            "width": "300",
            "height": "250",
            "media_url": null,
            "content": "<iframe src=\"https:\/\/xxxx.net\/udm\/img.fetch?sid=2773;tid=2;ev=1;dt=1;\" width=300
             height=250 Marginwidth=0 Marginheight=0 Hspace=0 Vspace=0 Frameborder=0 Scrolling=No><\/iframe>
             <noscript><a href=\"https:\/\/fletcher.net\/udm\/clk.cpx?sid=2773;ev=2;tid=2;dt=3\"><img src=\
             "https:\/\/sample.net\/udm\/img.fetch?sid=2773;ev=1;tid=2;dt=3\" width=300 height=250 border=0>
             <\/a><\/noscript>",
            "format": "iframe-html",
            "member_id": "333",
            "brand_id": "17",
            "click_url": "",
            "audit_status": "audited",
            "size_in_bytes": "0",
            "landing_page_url": "https:\/\/www.appleblueberry.com",
            "last_activity": "2010-09-07 23:33:45",
            "created_on": "2010-08-25 16:31:43",
            "media_subtypes": [
               "banner"
            ],
            "pop_values": null
         },
         ...
      ]
   }
}
```

### Search for all flash creatives that have been uploaded since 2012-01-01 00:00:00

```
$ cat creative_search
{
   "creative-search": {
      "formats": [
         "flash"
      ],
      "uploaded_since": "2012-01-01 00:00:00"
   }
}
```

```
$ curl -b cookies -c cookies -X POST -d @creative_search 'https://api.appnexus.com/creative-search'

{
   "response": {
      "status": "OK",
      "creatives": [
         {
            "id": "1207858",
            "width": "160",
            "height": "600",
            "media_url": "https:\/\/cdn.adnxs.com\/p\/c7\/6d\/5b\/bd\/c76d5bbdxxxxx8b9e1507c07cbe61.swf",
            "content": null,
            "format": "flash",
            "member_id": "326",
            "brand_id": "4467",
            "click_url": "https:\/\/clickclick.com\/witness\/p=28xxx96\/c=6sxd3",
            "audit_status": "audited",
            "size_in_bytes": "40077",
            "landing_page_url": "https:\/\/www.destination.com",
            "last_activity": "2012-01-01 15:56:59",
            "created_on": "2012-01-01 02:34:14",
            "media_subtypes": [
               "banner"
            ],
            "pop_values": null
         },
         {
            "id": "1207859",
            "width": "160",
            "height": "600",
            "media_url": "https:\/\/cdn.adnxs.com\/p\/3b\/d6\/f6\/1d\/3bd6f61dkdh4473djfb579430ed.swf",
            "content": null,
            "format": "flash",
            "member_id": "326",
            "brand_id": "4467",
            "click_url": "https:\/\/clickclick.com\/witness\/p=2ddssd6\/c=3423",
            "audit_status": "audited",
            "size_in_bytes": "32094",
            "landing_page_url": "https:\/\/www.destination.com",
            "last_activity": "2012-01-01 15:57:36",
            "created_on": "2012-01-01 02:35:52",
            "media_subtypes": [
               "banner"
            ],
            "pop_values": null
         },
         ...
      ]
   }
}
```

### Search for all 728x90 and 300x250 image creatives that belong to member 333

```
$ cat creative_search
{
   "creative-search": {
      "sizes": [
         "728x90", 
         "300x250"
      ],
      "formats": [
         "image"
      ],
      "member_ids": [
         333
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X POST -d @creative_search 'https://api.appnexus.com/creative-search'

{
   "response": {
      "status": "OK",
      "creatives": [
         {
            "id": "61967",
            "width": "300",
            "height": "250",
            "media_url": "https://cdn.adnxs.com/p/c8/fb/12/56/c8fb125634xxxx2e67a783d91cf.png",
            "content": null,
            "format": "image",
            "member_id": "333",
            "brand_id": "1",
            "click_url": "https://www.clickplace.com/",
            "audit_status": "no_audit",
            "size_in_bytes": "29433",
            "landing_page_url": null,
            "last_activity": "2011-05-13 02:34:47",
            "created_on": "2010-07-28 20:44:22",
            "media_subtypes": [
               "banner"
            ],
            "pop_values": null
         },
         {
            "id": "291801",
            "width": "728",
            "height": "90",
            "media_url": "https://cdn.adnxs.com/p/54/62/87/d1/546287aasxxx8e6431960ad2b1fb.png",
            "content": null,
            "format": "image",
            "member_id": "333",
            "brand_id": "2450",
            "click_url": "https://thatplace.com/careers",
            "audit_status": "audited",
            "size_in_bytes": "24091",
            "landing_page_url": "https://thatplace.com/careers",
            "last_activity": "2011-05-13 03:30:00",
            "created_on": "2011-04-05 18:28:29",
            "media_subtypes": [
               "banner"
            ],
            "pop_values": null
         },
         ...
      ]
   }
}
```
