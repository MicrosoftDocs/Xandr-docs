---
title: Creative Custom Request Template Service
description: In this article, learn about the Creative Custom Request Template service, their JSON fields, and REST API with thorough examples.
ms.date: 10/04/2024
ms.custom: digital-platform-api
---

# Creative Custom Request Template service

> [!NOTE]
> Mediation is only available to Microsoft Monetize Ad Server customers.

For context on mediation, see [Selling Your Inventory through Mediation](../monetize/mediation-selling-your-inventory-through-mediation.md).

Mediation partners, also known as custom request partners, can be identified and defined through the [Creative Custom Request Partner Service](creative-custom-request-partner-service.md). These partners are assigned to customer-specific Networks via the [UI](../monetize/mediation-networks.md) or [Mediated Network Service](mediated-network-service.md).

To support mobile ad server mediation, Monetize uses a mediated creative type. Unlike standard creatives, which reside as static content on a server, mediated creatives are configurable containers that fetch server-side content. The Creative Custom Request Template Service is used to build the requests that populate these mediated creatives. The service does this by managing a set of custom templates, each of which corresponds to a different creative custom request partner, and which is associated with a template "type" defined by the [Creative Custom Request Template Type Service](./creative-custom-request-template-type-service.md).

This document describes the fields made available by this API service, as well as providing usage examples. See the [Examples](#examples) section below.

> [!NOTE]
>
> For more information about mediated creatives, see the [Creative Service](creative-service.md).

## REST API

> [!NOTE]
> This information is for Xandr employees. If you are an employee and an admin user, your permissions are as follows:
>
> - You will see the global templates.
> - You can view member-specific templates by appending `a =member_id=field` to the query string of your request.
>
> **Template Viewing Permissions:**
>
> If you are a member you will be able to view the following templates:
>
> - Global templates (those belonging to `member_id`=0).
> - Your own templates, i.e., those associated with your `member_id`.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET`  | [https://api.appnexus.com/creative-custom-request-template?id=123](https://api.appnexus.com/creative-custom-request-template?id=123) | View a specific custom request template. |
| `GET` | - [https://api.appnexus.com/creative-custom-request-template?member_id=0](https://api.appnexus.com/creative-custom-request-template?member_id=0)<br> - [https://api.appnexus.com/creative-custom-request-template?member_id=MEMBER_ID](https://api.appnexus.com/creative-custom-request-template?member_id=MEMBER_ID) | View all custom request templates available to the member. |
| `GET` |  [https://api.appnexus.com/creative-custom-request-template/meta](https://api.appnexus.com/creative-custom-request-template/meta) | View available fields to filter and sort. |
| `POST` |  [https://api.appnexus.com/creative-custom-request-template](https://api.appnexus.com/creative-custom-request-template) | Create a custom request template. |
| `PUT` |  [https://api.appnexus.com/creative-custom-request-template](https://api.appnexus.com/creative-custom-request-template) | Update a custom request template. |
| `DELETE` |  [https://api.appnexus.com/creative-custom-request-template?id=123](https://api.appnexus.com/creative-custom-request-template?id=123) | Delete a custom request template. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `macros` | array of objects | These are the macros (or query string parameters) that will be sent on the request. See [Macros](#macros).<br>**Sort by:** No<br>**Filter by:** No |
| `id` | int | The ID of this template.<br>**Required On:** `PUT`  <br>**Sort by:** Yes<br>**Filter by:** Yes |
| `type_id` | int | The ID from the [Creative Custom Request Template Type Service](creative-custom-request-template-type-service.md).<br>**Default:** `null` <br>**Required On:** `POST` <br>**Sort by:** Yes<br>**Filter by:** Yes |
| `member_id` | int | The member ID whose mediation creatives will be associated with this template. For more information see the [Creative Service](creative-service.md) and the [Member Service](member-service.md).<br>**Default:** `0` <br>**Sort by:** Yes<br>**Filter by:** Yes |
| `media_subtype_id` | int | The media subtype ID for this template. Derived from the [Media Subtype](#media-subtype) object below.<br>**Default:** `null`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `hostname` | string | The mediation partner host to be called for demand.<br>**Default:** `null`<br>**Required On:** `POST` <br>**Sort by:** Yes<br>**Filter by:** Yes |
| `uri` | string | The mediation partner host endpoint to be called for demand.<br>**Default:** `null`<br>**Required On:** `POST`, `PUT` if `is_client` is `false`. <br>**Sort by:** Yes<br>**Filter by:** Yes |
| `port` | int | The mediation partner host port to be called for demand.<br>**Default:** `80`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `is_post` | Boolean | Whether the request for demand is a `POST`.<br>**Default:** `false`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `content` | string | The payload included in the request. Examples: JSON, XML.<br>**Default:** `null`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `timeout_ms` | int | The timeout either given by the partner or to be enforced by Microsoft Monetize.<br>**Default:** `0`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `is_client` | Boolean | Whether the request originates from the client-side. Example: An SDK.<br>**Default:** `false`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `media_subtype` | array | The display style of creatives that can use this template. Each media subtype belongs to a superordinate media type. For example, the "Standard Banner" media subtype belongs to the "Banner" media type. For more details, see [Media Subtype](#media-subtype) below.<br>**Sort by:** No<br>**Filter by:** No |
| `last_modified` | date | The date and time at which this object was last updated.<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `integration_type` | string | The type of integration with the mediation partner. Examples: SDK, Server-side, Sync-web-client. |
| `creative_custom_request_partner_id` | int | The ID of the mediation partner. For more information, see [Creative Custom Request Partner Service](creative-custom-request-partner-service.md). |
| `active` | boolean | Whether the template is available for use. |
| `supply_types` | array | The type of demand available from the mediation partner (`web`, `mobile_web`, `mobile_app`). |
| `passback` | object | If no acceptable bid is received for a request, this `passback` can be added to the ad tag to allow the next system in line to bid. Add the Network's passback, listed here, to an ad tag to use this option. |

## Macros

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of this macro.<br>**Default:** `null` <br>**Sort by:** Yes<br>**Filter by:** Yes |
| `template_id` | int | The Creative Custom Request Template this macro is associated with.<br>**Default:** `null`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `code` | string | The query string parameter that will be built into the url, e.g., `send_referer`.<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `name` | string | A description of what the macro does, e.g., "Toggle if referer should be sent".<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `type` | string | The type of value the parameter will accept. <br><br>**Note:** The default value of `"string"` is also the most common. Allowed values include:<br> - `true_false`<br> - `string`<br> - `url`<br> - `integer`<br> - `decimal`<br> - `string_list`<br> - `select_from_list`<br> **Default:** `string`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `is_required` | Boolean | Whether this macro is required in a call to the external ad server.<br>**Default:** `true`<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `last_modified` | date | The date and time at which this macro object was last updated.<br>**Sort by:** Yes<br>**Filter by:** Yes |

### Media subtype

All available options can be viewed in the [Media Subtype Service](media-subtype-service.md) and [Media Type Service](media-type-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the media subtype. |
| `name` | string | **Read Only.** The name of the media subtype. |
| `media_type_name` | string | **Read Only.** The name of the media type to which the subtype belongs. |
| `mediatype_id` | int | **Read Only.** The ID of the media type to which the subtype belongs. |

## Examples

### View all creative request templates

In the example below, note the difference between how standard Microsoft Monetize macros are displayed in the `uri` field, e.g., `* $\{USER_IP\}` and how the custom macros defined on a per-ad-server basis by this service are displayed: `* \#\{MK_SITEID\}`. Definitions for each macro are in the macros array of objects below.

```

{code}
$ curl -b cookies https://api.appnexus.com/creative-custom-request-template?member_id=0
{
    "response": {
        "status": "OK",
        "count": 4,
        "start_element": 0,
        "num_elements": 100,
        "creative-custom-request-templates": [
            {
                "id": 1,
                "type_id": 2,
                "member_id": 0,
                "media_subtype_id": 1,
                "hostname": "w.inmobi.com",
                "uri": "/showad.asm?mk-siteid=#{MK_SITEID}&mk-carrier=${USER_IP}&h-user-agent=${USER_AGENT_ENC}&h-referer=${REFERER_URL_ENC}&u-id-map=${INMOBI_UID_MAP}&u-latlong-accu=${INMOBI_LAT_LONG_ACCU}&u-age=${AGE}&u-gender=${GENDER}&d-localization=${USER_LOCALE}&d-nettype=${INMOBI_NETTYPE}&d-orientation=${INMOBI_ORIENTATION}",
                "port": 80,
                "is_post": false,
                "content": "",
                "timeout_ms": 200,
                "is_client": false,
                "last_modified": "2013-07-10 19:27:41",
                "media_subtype": {
                    "id": 1,
                    "name": "Standard Banner",
                    "media_type_name": "Banner",
                    "mediatype_id": 1
                },
                "macros": [
                    {
                        "id": 1,
                        "template_id": 1,
                        "code": "MK_SITEID",
                        "name": "MK_SITEID",
                        "type": "string",
                        "is_required": true,
                        "last_modified": "2013-07-10 19:27:41"
                    }
                ]
            },
            {
                "id": 2,
                "type_id": 3,
                "member_id": 0,
                "media_subtype_id": 1,
                "hostname": "ads.mydas.mobi",
                "uri": "/getAd?apid=#{APID}&auid=${DEVICE_MD5}&ua=${USER_AGENT_ENC}&uip=${USER_IP}&age=${AGE}&gender=${GENDER}&zip=${POSTAL_CODE}&lat=${GEO_LAT}&long=${GEO_LON}",
                "port": 80,
                "is_post": false,
                "content": "",
                "timeout_ms": 200,
                "is_client": false,
                "last_modified": "2013-07-10 19:27:50",
                "macros": [
                    {
                        "id": 2,
                        "template_id": 2,
                        "code": "APID",
                        "name": "APID",
                        "type": "string",
                        "is_required": true,
                        "last_modified": "2013-07-10 19:27:50"
                    }
                ]
            },
            {
                "id": 3,
                "type_id": 4,
                "member_id": 0,
                "media_subtype_id": 5,
                "hostname": "ads.mojiva.com",
                "uri": "/ad?zone=#{ZONE}&ip=${USER_IP}&ua=${USER_AGENT_ENC}&url=${REFERER_URL_ENC}&udid=${DEVICE_MD5}&lat=${GEO_LAT}&long=${GEO_LON}&country=${USER_COUNTRY}&region=${USER_STATE}&city=${USER_CITY}&dma=${USER_DMA}&zip=${POSTAL_CODE}",
                "port": 80,
                "is_post": false,
                "content": "",
                "timeout_ms": 200,
                "is_client": false,
                "media_subtype": {
                    "id": 1,
                    "name": "Standard Banner",
                    "media_type_name": "Banner",
                    "media_type_id": 1
                },
                "last_modified": "2013-07-10 19:28:00",
                "macros": [
                    {
                        "id": 3,
                        "template_id": 3,
                        "code": "ZONE",
                        "name": "ZONE",
                        "type": "string",
                        "is_required": true,
                        "last_modified": "2013-07-10 19:28:00"
                    }
                ]
            },
            {
                "id": 4,
                "type_id": 5,
                "member_id": 0,
                "media_subtype_id": 5,
                "hostname": "a.jumptap.com",
                "uri": "/a/ads?hid_sha1=${DEVICE_SHA1}&idfa=${DEVICE_APPLE_IDA}&pub=#{PUB}&site=#{SITE}&spot=#{SPOT}&url=${REFERER_URL_ENC}&ua=${USER_AGENT_ENC}&client-ip=${USER_IP}&country=${USER_COUNTRY}&ll=${JUMPTAP_LAT_LONG_ENC}&mt-age=${AGE}&mt-gender=${GENDER}",
                "port": 80,
                "is_post": false,
                "content": "",
                "timeout_ms": 200,
                "is_client": false,
                "media_subtype": {
                    "id": 5,
                    "name": "Interstitial",
                    "media_type_name": "Interstitial",
                    "media_type_id": 3
                },
                "last_modified": "2013-07-10 19:28:10",
                "macros": [
                    {
                        "id": 4,
                        "template_id": 4,
                        "code": "PUB",
                        "name": "PUB",
                        "type": "string",
                        "is_required": true,
                        "last_modified": "2013-07-10 19:28:10"
                    },
                    {
                        "id": 5,
                        "template_id": 4,
                        "code": "SITE",
                        "name": "SITE",
                        "type": "string",
                        "is_required": true,
                        "last_modified": "2013-07-10 19:28:10"
                    },
                    {
                        "id": 6,
                        "template_id": 4,
                        "code": "SPOT",
                        "name": "SPOT",
                        "type": "string",
                        "is_required": true,
                        "last_modified": "2013-07-10 19:28:10"
                    }
                ]
            }
        ],
        "dbg_info": {
            "instance": "28.bm-hbapi.prod.nym1",
            "s1ave_hit": true,
            "db": "141.bm-mysql.prod.nym1",
            "reads": 1,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 0,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [],
            "time": 66.461801528931,
            "start_microtime": 1373651335.4519,
            "version": "1.13.52",
            "s1ave_lag": 1,
            "member_last_modified_age": 68896
        }
    }
}
{code}
```

### View a single creative custom request template

```
{code}
$ curl -b cookies https://api.appnexus.com/creative-custom-request-template?id=2
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "creative-custom-request-template": {
            "id": 2,
            "type_id": 3,
            "member_id": 0,
            "media_subtype_id": 1,
            "hostname": "ads.mydas.mobi",
            "uri": "/getAd?apid=#{APID}&auid=${DEVICE_MD5}&ua=${USER_AGENT_ENC}&uip=${USER_IP}&age=${AGE}&gender=${GENDER}&zip=${POSTAL_CODE}&lat=${GEO_LAT}&long=${GEO_LON}",
            "port": 80,
            "is_post": false,
            "content": "",
            "timeout_ms": 200,
            "is_client": false,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "last_modified": "2013-07-10 18:57:43",
            "macros": [
                {
                    "id": 2,
                    "template_id": 2,
                    "code": "APID",
                    "name": "APID",
                    "type": "string",
                    "is_required": true,
                    "last_modified": "2013-07-02 00:50:53"
                }
            ]
        },
        "dbg_info": {
            "instance": "05.hbapi.sand-08.lax1",
            "s1ave_hit": false,
            "db": "master",
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [],
            "time": 68.688154220581,
            "start_microtime": 1373910064.7161,
            "version": "1.13.53.1",
            "s1ave_miss": "no_service_index",
            "s1ave_lag": 0,
            "member_last_modified_age": 1373910064
        }
    }
}
{code}
```

### Create a request template

Create a JSON file specifying the fields of the request template.

> [!NOTE]
> The `type_id` field is required on `POST`.

For more information about the request template types, see the [Creative Custom Request Template Type Service](creative-custom-request-template-type-service.md).

```
{code}
$ cat create.json
{
    "creative-custom-request-template": {
        "hostname": "ads.light-vs-wily.com",
        "uri": "/a/ads?hid_sha1=${DEVICE_SHA1}&idfa=${DEVICE_APPLE_IDA}&enemy=#{ENEMY}&light_or_wily=#{LIGHT_OR_WILY}&megaman_version=#{MEGAMAN_VERSION}&url=${REFERER_URL_ENC}&ua=${USER_AGENT_ENC}&client-ip=${USER_IP}&country=${USER_COUNTRY}&ll=${JUMPTAP_LAT_LONG_ENC}&mt-age=${AGE}&mt-gender=${GENDER}",
        "port": 49995,
        "is_post": false,
        "content": "",
        "timeout_ms": 2,
        "is_client": false,
        "type_id": 1
    }
}
{code}
```

Make a `POST` call to the API with the JSON payload included.

```
{code}
$ curl -b cookies -X POST -d @create.json https://api.appnexus.com/creative-custom-request-template
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "creative-custom-request-template": {
            "id": 13,
            "type_id": 1,
            "member_id": 0,
            "media_subtype_id": 1,
            "hostname": "ads.light-vs-wily.com",
            "uri": "/a/ads?hid_sha1=${DEVICE_SHA1}&idfa=${DEVICE_APPLE_IDA}&enemy=#{ENEMY}&light_or_wily=#{LIGHT_OR_WILY}&megaman_version=#{MEGAMAN_VERSION}&url=${REFERER_URL_ENC}&ua=${USER_AGENT_ENC}&client-ip=${USER_IP}&country=${USER_COUNTRY}&ll=${JUMPTAP_LAT_LONG_ENC}&mt-age=${AGE}&mt-gender=${GENDER}",
            "port": 49995,
            "is_post": false,
            "content": "",
            "timeout_ms": 2,
            "is_client": false,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "last_modified": "2013-07-15 19:02:02",
            "macros": ""
        },
        "dbg_info": {
            "instance": "07.hbapi.sand-08.lax1",
            "s1ave_hit": false,
            "db": "master",
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [],
            "time": 67.02995300293,
            "start_microtime": 1373914957.1776,
            "version": "1.13.53.1",
            "s1ave_miss": "no_service_index",
            "s1ave_lag": 0,
            "member_last_modified_age": 1373914957
        }
    }
}
{code}
```

### Update a request template

First, create a JSON file with only the parameters to be updated.

> [!NOTE]
> You must include the `id` of the request template being updated.

```
{code}
$ cat update.json
{"creative-custom-request-template":{"id":13, "type_id":2, "timeout_ms":250}}
{code}
```

Make the `PUT` call, including the JSON update.

A successful `PUT` call requires:

- Specifying the ID of the request template in the JSON file.
- Not adding any query string parameters (like `?id=123`) to the request (see example below).

<!-- 
> [!NOTE]
> In order to make a successful `PUT` call, you must do the following:
>
> - Specify the ID of the request template in the JSON file
> - Do not add any query string parameters (like `?id=123`) to your request (see the example below).

```
{code}
$ curl -b cookies -X PUT -d @update.json https://api.appnexus.com/creative-custom-request-template
{code}
```

> [!NOTE]
> A successful `PUT` call will not return any JSON response. -->

### Delete a request template

Deleting a request simply requires the template ID in the query string.

```
{code}
$ curl -b cookies -X DELETE https://api.appnexus.com/creative-custom-request-template?id=123
{code}
```

## Related topics

- [Mediated Bid Service](mediated-bid-service.md)
- [Mediated Network Service](mediated-network-service.md)
- [Creative Custom Request Partner Service](./creative-custom-request-partner-service.md)
- [Creative Custom Request Template Type Service](creative-custom-request-template-type-service.md)
- [Creative Template Service](creative-template-service.md)
- [Creative Service](creative-service.md)
