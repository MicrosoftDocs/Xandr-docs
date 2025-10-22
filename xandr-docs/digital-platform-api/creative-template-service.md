---
title: Digital Platform API - Creative Template Service
description: In this article, learn about the Digital Platform API's Creative Template service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Creative Template service

The Xandr platform categorizes creatives by format, media type, and media subtype. Format defines the resource type of creatives (flash, image, etc.); media type defines the general display style of creatives (banner, expandable, video, etc.); and media subtype defines the specific display style of creatives (standard banner, MediaMind expandable, Standard VAST, etc.).

## Standard templates

For each format, media type, and media subtype combination, Xandr provides a standard creative template that ensures proper rendering on web pages when creatives are served. You cannot edit these templates, but the Creative Template Service allows you to view them and examine their rendering code.

## Custom templates

If you want to customize the way certain types of creatives render, you can build your own templates. With custom templates, you have complete control of the JavaScript, HTML, or XML rendering code, and you can define macros to prompt your traffickers to enter information and make decisions about the behavior of creatives when they are uploaded.

> [!NOTE]
> You can have up to 100 custom templates. However, Xandr does not provide support for creatives that do not render correctly as a result of errors in custom template code.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/template](https://api.appnexus.com/template) | View all templates (standard and custom). |
| `GET` | [https://api.appnexus.com/template?member_id=null](https://api.appnexus.com/template?member_id=null) | View standard templates only. |
| `GET` | [https://api.appnexus.com/template?id=TEMPLATE_ID](https://api.appnexus.com/template?id=TEMPLATE_ID) | View a specific template. |
| `POST` | [https://api.appnexus.com/template](https://api.appnexus.com/template)<br> (template JSON) | Add a new custom template. |
| `PUT` | [https://api.appnexus.com/template?id=TEMPLATE_ID](https://api.appnexus.com/template?id=TEMPLATE_ID)<br> (template JSON)<br><br>**Warning:**<br>When you modify a custom template, your changes immediately affect any creatives that are already using the template. If your changes cause these creatives to stop rendering properly, their audit status will be changed to "rejected," and they will stop serving on most third-party inventory. | Modify a custom template. |
| `DELETE` | [https://api.appnexus.com/template?id=TEMPLATE_ID](https://api.appnexus.com/template?id=TEMPLATE_ID)<br><br>**Note:**<br>You cannot delete a custom template that is used by one or more creatives, but you can archive the template to prevent future creatives from using it. For more details, see the [Archiving a custom template example](#archive-a-custom-template) below. | Delete a custom template. |

### Creating a Custom Template (iPhone only)

This functionality is for an ad to download a specific app from iTunes. A “direct-link” will not work in iPhone because of security. Therefore, it cannot access the Seller Tag (AST) Library directly. In lieu of this, we raise an event.

> [!WARNING]
> The user should have some prior familiarity with creating custom templates and macros.

To accomplish this:

Create a placement that has a default creative that uses a template. This lists the templates the member has access to. There’s a set of Xandr creative templates that are not standard templates. This situation would require a custom template.

The template needs to be associated with the default creative. When that creative is selected, it finds this template. It sends out an additional JavaScript function, along with the creative. It calls that function and then sends that event to the Seller Tag library. This will open the iTunes app store from the main page frame, where the Seller Tag library is running.

Summarizing:

1. The template takes in a urI.
1. It sends an event out to the Seller Tag library.
1. Seller Tag core has a listener for this custom event, and it launches iTunes.
1. We pass this event name and what app store url that we want to open. The url takes you to the specific resource in the iTunes app store.

### Example template

```
function iTunesClick(url)
{window.parent.document.dispatchEvent(new CustomEvent('apntag_iTunesLaunch', {
detail: { url: url }})); }
document.write('<a
href="#"
onclick="iTunesClick(\\\'${CLICK_URL}\\\');"><img
width="${CREATIVE_WIDTH}" height="${CREATIVE_HEIGHT}"
style="border-style: none" src="${MEDIA_URL}"/></a>');
```

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative template.<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `name` | string (30) | The name of the creative template.<br>**Required On:** `POST` |
| `description` | string | The description of the creative template. |
| `member_id` | int | The ID of the member that owns the template. For standard Xandr templates, this is null.<br>**Read Only.** |
| `ad_type` | string | **Note:**<br>This field only applies when you are associating creatives to [augmented line items](line-item-service---ali.md).<br>The type of creative used. Possible values:<br>- `"banner"`<br>- `"video"` (includes audio types)<br>- `"native"`<br>This value determines how auction items are tracked for the line item's buying strategy, paying strategy, optimization options, creative association, and targeting options.<br><br>**Note:**<br>All creatives associated to a line item must have the same ad type, which should match the `ad_type` selected in the [Line Item Service - ALI](line-item-service---ali.md). |
| `media_subtype` | object | The display style of creatives that can use this template. Each media subtype belongs to a superordinate media type, for example, the `"Standard Banner"` media subtype belongs to the `"Banner"` media type. For more details, see [Media Subtype](#media-subtype) below.<br>**Required On:** `POST` |
| `format` | object | The format of creatives that can use this template, for example, `"image"` or `"flash"`. For more details, see [Format](#format) below.<br>**Required On:** `POST` |
| `is_default` | boolean | If `true`, the template is automatically assigned to creatives that match the template's media type, media subtype, and format. When the creatives are uploaded, this default assignment can be overridden, if necessary. Note that there can be only one default creative template per media type, media subtype, and format combination.<br>**Default:** `false` |
| `is_archived` | boolean | If `true`, the template is archived. Archiving a template prevents future creatives from using the template but does not affect creatives already using the template.<br>**Default:** `false` |
| `content_js` | string | The template's rendering code in JavaScript. The code can include both Xandr standard macros and your own custom macros. Xandr macros must begin with the $ symbol, and custom macros must begin with the # symbol. Each custom macro must be defined in the `macros` array.<br>**Required On:** `POST`, if `content_html` and `content_xml` are not provided. |
| `content_html` | string | The template's rendering code in HTML. The code can include both Xandr standard macros and your own custom macros. Xandr macros must begin with the $ symbol, and custom macros must begin with the # symbol. Each custom macro must be defined in the `macros` array.<br>**Required On:** `POST`, if `content_js` and `content_xml` are not provided. |
| `content_xml` | string | **Deprecated** (as of October 17, 2016). |
| `callback_content_html` | string | When `media_subtype` is `"Popup"` or `"Popunder"`, `content_js` defines the rendering code for the pop window, and this field defines the rendering code for the content in the pop window. |
| `macros` | array of objects | The custom macros used in the `content_js`, `content_html`, or `content_xml` fields. You can include up to 20 custom macros in a template. For more details, see [Custom Macros](#custom-macros) below. |
| `last_modified` | timestamp | The date and time when the creative template was last modified.<br>**Read Only.** |

## Media subtype

You can use the [Media Subtype Service](media-subtype-service.md) and [Media Type Service](media-type-service.md) to view all supported media subtypes and the media types to which they belong.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of media subtype.<br>**Required On:** `POST` |
| `name` | string | The name of the media subtype.<br>**Read Only.** |
| `mediatype_id` | int | The ID of the media type to which the subtype belongs.<br>**Read Only.** |
| `media_type_name` | string | The name of the media type to which the subtype belongs.<br>**Read Only.** |

## Format

You can use the [Creative Format Service](creative-format-service.md) to view all supported creative formats.

| Field | Type | Description | Filter By? | Sort By? |
|:---|:---|:---|:---|:---|
| `id` | int | The ID of creative format.<br>**Required On:** `POST` | Yes | Yes |
| `name` | string | The name of the creative format.<br>**Read Only.** | Yes | Yes |

## Custom macros

You must define each custom macro used in the `content_js`, `content_html`, or `content_xml` field.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `code` | string (30) | The macro name exactly as it is used in the `content_js`, `content_html`, or `content_xml` field. For example, if `#{BORDER_SIZE}` is the macro in the `content_js` field, you would pass "BORDER_SIZE" here.<br>**Required On:** `POST` |
| `name` | string (50) | The user-friendly name for this macro that traffickers will see when they add creatives that use this template via the UI.<br>**Required On:** `POST` |
| `type` | enum | The type of value that traffickers will provide for this macro when they add creatives that use this template via the Creative Service or UI. Possible values: `"true/false"`, `"string"`, `"url"`, `"integer"`, `"decimal"`, `"string_list"`, `"select_from_list"` and `"file"`. For example, on the UI, if you set this to `"true/false"`, traffickers will see the macro name followed by a check box.<br>**Required On:** `POST` |
| `is_required` | boolean | If `true`, traffickers will be required to provide a value for the macro when adding creatives that use this template.<br>**Required On:** `POST` |
| `default_value` | string | If `is_required` is `false`, this is the default value that will be used when traffickers do not provide a value for the macro when adding creatives that use this template.<br>**Required On:** `POST`, if `is_required` is `false`. |
| `other_data` | string | The accepted values for the macro, if `type` is `"string_list"` or `"select_from_list"`. |

## Examples

### View all creative templates

```
{code}
$ curl -b cookies -c cookies 'https://api.appnexus.com/template'

{
    "response": {
        "status": "OK",
        "count": 74,
        "start_element": 0,
        "num_elements": 100,
        "templates": [
            {
                "id": 1,
                "name": "Standard",
                "description": null,
                "last_modified": "2012-02-20 21:36:13",
                "is_archived": false,
                "member_id": null,
                "is_default": true,
                "content_html": "<iframe frameborder=\"0\" width=\"${CREATIVE_WIDTH}\" height=\"
                 ${CREATIVE_HEIGHT}\"marginheight=\"0\" marginwidth=\"0\" target=\"_blank\"
                 scrolling=\"no\" src=\"${MEDIA_URL}\"></iframe>",
                "content_js": "document.write('<iframe frameborder=\"0\" width=\"${CREATIVE_WIDTH}\"
                 height=\"${CREATIVE_HEIGHT}\" marginheight=\"0\" marginwidth=\"0\" target=\"_blank\"
                 scrolling=\"no\" src=\"${MEDIA_URL}\"> </iframe>');",
                "content_xml": null,
                "callback_content_html": null,
                "media_subtype": {
                    "id": 1,
                    "name": "Standard Banner",
                    "media_type_name": "Banner",
                    "media_type_id": 1
                },
                "format": {
                    "id": 1,
                    "name": "url-html"
                },
                "macros": null
            },
            {
                "id": 2,
                "name": "Standard",
                "description": null,
                "last_modified": "2012-01-31 14:33:37",
                "is_archived": false,
                "member_id": null,
                "is_default": true,
                "content_html": "<html><body style=\"margin-left: 0%; margin-right: 0%; margin-top:
                 0%; margin-bottom: 0%\"><script type=\"text/javascript\" src=\"${MEDIA_URL}\">
                 </script></body></html>",
                "content_js": "document.write('<script type=\"text/javascript\" src=\"${MEDIA_URL}\">
                 </scr'+'ipt>');",
                "content_xml": null,
                "callback_content_html": null,
                "media_subtype": {
                    "id": 1,
                    "name": "Standard Banner",
                    "media_type_name": "Banner",
                    "media_type_id": 1
                },
                "format": {
                    "id": 2,
                    "name": "url-js"
                },
                "macros": null
            },
            {
                "id": 3,
                "name": "Standard",
                "description": null,
                "last_modified": "2012-01-31 14:33:37",
                "is_archived": false,
                "member_id": null,
                "is_default": true,
                "content_html": "\u000a<html><body style=\"margin-left: 0%; margin-right: 0%; margin-top:
                 0%;margin-bottom: 0%\"><script type=\"text/javascript\">\u000a<!--\u000a(function()\u000a\
                 u0009{\u000a\u0009var flashAd='<OBJECT id=\"${AUCTION_ID}\" data=\"${MEDIA_URL}\" classid=
                 \"clsid:D27CDB6E-AE6D-11cf-96B8-444553540000\" WIDTH=\"${CREATIVE_WIDTH}\" HEIGHT=\
                 "${CREATIVE_HEIGHT}\"flashvars=\"${FLASHVARS}\"><PARAM NAME=movie VALUE=\"${MEDIA_URL}\">
                 <PARAM NAME=loop VALUE=true><PARAM NAME=menu VALUE=false><PARAM NAME=quality VALUE=high>
                 <PARAM NAME=wmode VALUE=\"opaque\"><PARAM NAME=bgcolor VALUE=#FFFFFF><PARAM NAME=
                 allowscriptaccess VALUE=always><PARAM NAME=flashvarsVALUE=\"${FLASHVARS}\"><OBJECT TYPE=\
                 "application/x-shockwave-flash\" data=\"${MEDIA_URL}?${FLASHVARS}\"
                 ..."
                "content_js": "(function()\u000a\u0009{\u000a\u0009var flashAd='<OBJECT id=\"${AUCTION_ID}\"
                 data=\"${MEDIA_URL}\" classid=\"clsid:D27CDB6E-AE6D-11cf-96B8-444553540000\" WIDTH=
                 \"${CREATIVE_WIDTH}\"HEIGHT=\"${CREATIVE_HEIGHT}\" flashvars=\"${FLASHVARS}\"><PARAM NAME=movie
                 VALUE=\"${MEDIA_URL}\"><PARAM NAME=loop VALUE=true><PARAM NAME=menu VALUE=false><PARAM NAME=
                 quality VALUE=high><PARAM NAME=wmode VALUE=\"opaque\"><PARAM NAME=bgcolor VALUE=#FFFFFF>
                 <PARAM NAME=allowscriptaccess VALUE=always><PARAM NAME=flashvars VALUE=\"${FLASHVARS}\">
                 <OBJECT TYPE=\"application/x-shockwave-flash\" data=\"${MEDIA_URL}? ${FLASHVARS}\" width=\
                 "${CREATIVE_WIDTH}\" height=\"${CREATIVE_HEIGHT}\" wmode=\"opaque\" allowscriptaccess=
                 \"always\"></OBJECT></OBJECT>';\u000a\u0009var flashBackupUrl='${FLASH_BACKUP_URL}';\u000a\
                 u0009varalternate = '';\u000a\u0009if (flashBackupUrl)\u000a\u0009{\u000a\u0009\u0009alternate=
                 '<a href=\"${CLICK_URL}\" target=\"_blank\">\"<img width=\"${CREATIVE_WIDTH}\" height=
                 ..."
                "content_xml": null,
                "callback_content_html": null,
                "media_subtype": {
                    "id": 1,
                    "name": "Standard Banner",
                    "media_type_name": "Banner",
                    "media_type_id": 1
                },
                "format": {
                    "id": 3,
                    "name": "flash"
                },
                "macros": null
            },
            {
                "id": 4,
                "name": "Standard",
                "description": null,
                "last_modified": "2012-01-31 14:33:37",
                "is_archived": false,
                "member_id": null,
                "is_default": true,
                "content_html": "<a href=\"${CLICK_URL}\" target=\"_blank\"><img width=\"${CREATIVE_WIDTH}
                 \" height=\"${CREATIVE_HEIGHT}\" style=\"border-style: none\" src=\"${MEDIA_URL}\"/></a>",
                "content_js": "document.write('<a href=\"${CLICK_URL}\" target=\"_blank\"><img width=
                 \"${CREATIVE_WIDTH}\" height=\"${CREATIVE_HEIGHT}\" style=\"border-style: none\" src=
                 \"${MEDIA_URL}\"/></a>');",
                "content_xml": null,
                "callback_content_html": null,
                "media_subtype": {
                    "id": 1,
                    "name": "Standard Banner",
                    "media_type_name": "Banner",
                    "media_type_id": 1
                },
                "format": {
                    "id": 4,
                    "name": "image"
                },
                "macros": null
            },
            ...
        ]
    }
}
{code}
```

### View a specific creative template

In this example, the request gets details about the Xandr standard template for rendering creatives of the media type `"Banner"`, media subtype `"Standard Banner"`, and format `"flash"`.

```
{code}
$ curl -b cookies -c cookies 'https://api.appnexus.com/template?id=3'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "template": {
            "id": 3,
            "name": "Standard",
            "description": null,
            "last_modified": "2012-01-31 14:33:37",
            "is_archived": false,
            "member_id": null,
            "is_default": true,
            "content_html": "\u000a<html><body style=\"margin-left: 0%; margin-right: 0%; margin-top:
             0%;margin-bottom: 0%\"><script type=\"text/javascript\">\u000a<!--\u000a(function()\u000a\
             u0009{\u000a\u0009var flashAd='<OBJECT id=\"${AUCTION_ID}\" data=\"${MEDIA_URL}\" classid=
             \"clsid:D27CDB6E-AE6D-11cf-96B8-444553540000\" WIDTH=\"${CREATIVE_WIDTH}\" HEIGHT=\
             "${CREATIVE_HEIGHT}\"flashvars=\"${FLASHVARS}\"><PARAM NAME=movie VALUE=\"${MEDIA_URL}\">
             <PARAM NAME=loop VALUE=true><PARAM NAME=menu VALUE=false><PARAM NAME=quality VALUE=high>
             <PARAM NAME=wmode VALUE=\"opaque\"><PARAM NAME=bgcolor VALUE=#FFFFFF><PARAM NAME=
             allowscriptaccess VALUE=always><PARAM NAME=flashvarsVALUE=\"${FLASHVARS}\"><OBJECT TYPE=\
             "application/x-shockwave-flash\" data=\"${MEDIA_URL}?${FLASHVARS}\"
             ..."
            "content_js": "(function()\u000a\u0009{\u000a\u0009var flashAd='<OBJECT id=\"${AUCTION_ID}\"
             data=\"${MEDIA_URL}\" classid=\"clsid:D27CDB6E-AE6D-11cf-96B8-444553540000\" WIDTH=
             \"${CREATIVE_WIDTH}\"HEIGHT=\"${CREATIVE_HEIGHT}\" flashvars=\"${FLASHVARS}\"><PARAM NAME=movie
             VALUE=\"${MEDIA_URL}\"><PARAM NAME=loop VALUE=true><PARAM NAME=menu VALUE=false><PARAM NAME=
             quality VALUE=high><PARAM NAME=wmode VALUE=\"opaque\"><PARAM NAME=bgcolor VALUE=#FFFFFF>
             <PARAM NAME=allowscriptaccess VALUE=always><PARAM NAME=flashvars VALUE=\"${FLASHVARS}\">
             <OBJECT TYPE=\"application/x-shockwave-flash\" data=\"${MEDIA_URL}? ${FLASHVARS}\" width=\
             "${CREATIVE_WIDTH}\" height=\"${CREATIVE_HEIGHT}\" wmode=\"opaque\" allowscriptaccess=
             \"always\"></OBJECT></OBJECT>';\u000a\u0009var flashBackupUrl='${FLASH_BACKUP_URL}';\u000a\
             u0009varalternate = '';\u000a\u0009if (flashBackupUrl)\u000a\u0009{\u000a\u0009\u0009alternate=
             '<a href=\"${CLICK_URL}\" target=\"_blank\">\"<img width=\"${CREATIVE_WIDTH}\" height=
             ..."
            "content_xml": null,
            "callback_content_html": null,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "format": {
                "id": 3,
                "name": "flash"
            },
            "macros": null
        }
    }
}
{code} 
```

### Add a custom template

In this example, the `POST` request creates a custom creative template for rendering standard banner image creatives with a border. The template contains two custom macros for defining the border size and border color.

```
{code}$ cat template

{
    "template": {
        "name": "Image with border",
        "media_subtype":
            {
                "id": 1
            },
        "format":
            {
                "id": 4
            },
        "content_js": "document.write('<a href=${CLICK_URL}><img src=${MEDIA_URL} border=#{BORDER_SIZE}
         border_color=#{BORDER_COLOR}></img></a>');",
        "macros":[
            {
                "code": "BORDER_SIZE",
                "name": "Image Border Size",
                "type": "integer",
                "is_required": false,
                "default_value": "4"
            },
            {
                "code": "BORDER_COLOR",
                "name": "Image Border Color",
                "type": "string",
                "is_required": false,
                "default_value": "black"
            }
        ]
    }
}{code}
{code}
$ curl -b cookies -c cookies -X POST -d @template 'https://api.appnexus.com/template'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 222,
        "start_element": 0,
        "num_elements": 100,
        "template": {
            "id": 222,
            "name": "Image with border",
            "description": null,
            "last_modified": "2012-02-22 23:20:05",
            "is_archived": false,
            "member_id": 1066,
            "is_default": false,
            "content_html": null,
            "content_js": "document.write('<a href=${CLICK_URL}><img src=${MEDIA_URL} border=#{BORDER_SIZE}
             border_color=#{BORDER_COLOR}></img></a>');",
            "content_xml": null,
            "callback_content_html": null,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "format": {
                "id": 4,
                "name": "image"
            },
            "macros": [
                {
                    "code": "BORDER_COLOR",
                    "name": "Image Border Color",
                    "is_required": false,
                    "type": "string",
                    "default_value": "black",
                    "other_data": null
                },
                {
                    "code": "BORDER_SIZE",
                    "name": "Image Border Size",
                    "is_required": false,
                    "type": "integer",
                    "default_value": "4",
                    "other_data": null
                }
            ]
        }
    }
}
{code} 
```

### Modify a custom template

In this example, the `PUT` request updates the default values of the custom macros in custom template 222.

```
{code}$ cat template_update

{
    "template": {
        "macros":[
            {
                "code": "BORDER_SIZE",
                "name": "Image Border Size",
                "type": "integer",
                "is_required": false,
                "default_value": "6"
            },
            {
                "code": "BORDER_COLOR",
                "name": "Image Border Color",
                "type": "string",
                "is_required": false,
                "default_value": "blue"
            }
        ]
    }
}{code}
{code}
$ curl -b cookies -c cookies -X PUT -d @template_update 'https://api.appnexus.com/template?id=222'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "222",
        "start_element": 0,
        "num_elements": 100,
        "template": {
            "id": 222,
            "name": "Image with border",
            "description": null,
            "last_modified": "2012-02-22 23:49:39",
            "is_archived": false,
            "member_id": 1066,
            "is_default": false,
            "content_html": null,
            "content_js": "document.write('<a href=${CLICK_URL}><img src=${MEDIA_URL} border=#{BORDER_SIZE} border_color=#{BORDER_COLOR}></img></a>');",
            "content_xml": null,
            "callback_content_html": null,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "format": {
                "id": 4,
                "name": "image"
            },
            "macros": [
                {
                    "code": "BORDER_COLOR",
                    "name": "Image Border Color",
                    "is_required": false,
                    "type": "string",
                    "default_value": "blue",
                    "other_data": null
                },
                {
                    "code": "BORDER_SIZE",
                    "name": "Image Border Size",
                    "is_required": false,
                    "type": "integer",
                    "default_value": "6",
                    "other_data": null
                }
            ]
        }
    }
}
{code} 
```

### Archive a custom template

In this example, the `PUT` request sets the `is_archived` field to `true`, thus archiving the template and preventing future creatives from using it.

```
{code}$ cat template_archive

{
    "template": {
         "is_archived": true
    }
}{code}
{code}
$ curl -b cookies -c cookies -X PUT -d @template_archive 'https://api.appnexus.com/template?id=222'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "222",
        "start_element": 0,
        "num_elements": 100,
        "template": {
            "id": 222,
            "name": "Image with border",
            "description": null,
            "last_modified": "2012-02-22 23:57:52",
            "is_archived": true,
            "member_id": 1066,
            "is_default": false,
            "content_html": null,
            "content_js": "document.write('<a href=${CLICK_URL}><img src=${MEDIA_URL} border=#{BORDER_SIZE}
             border_color=#{BORDER_COLOR}></img></a>');",
            "content_xml": null,
            "callback_content_html": null,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "format": {
                "id": 4,
                "name": "image"
            },
            "macros": [
                {
                    "code": "BORDER_COLOR",
                    "name": "Image Border Color",
                    "is_required": false,
                    "type": "string",
                    "default_value": "blue",
                    "other_data": null
                },
                {
                    "code": "BORDER_SIZE",
                    "name": "Image Border Size",
                    "is_required": false,
                    "type": "integer",
                    "default_value": "6",
                    "other_data": null
                }
            ]
        }
    }
}
{code} 
```

### Re-activate an archived custom template

In this example, the `PUT` request sets the `is_archived` field to `false`, thus re-activating the template and allowing new creatives to use it.

```
{code}$ cat template_activate

{
    "template": {
         "is_archived": false
    }
}{code}
{code}
$ curl -b cookies -c cookies -X PUT -d @template_activate 'https://api.appnexus.com/template?id=222'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "222",
        "start_element": 0,
        "num_elements": 100,
        "template": {
            "id": 222,
            "name": "Image with border",
            "description": null,
            "last_modified": "2012-02-22 23:57:52",
            "is_archived": false,
            "member_id": 1066,
            "is_default": false,
            "content_html": null,
            "content_js": "document.write('<a href=${CLICK_URL}><img src=${MEDIA_URL} border=#{BORDER_SIZE}
             border_color=#{BORDER_COLOR}></img></a>');",
            "content_xml": null,
            "callback_content_html": null,
            "media_subtype": {
                "id": 1,
                "name": "Standard Banner",
                "media_type_name": "Banner",
                "media_type_id": 1
            },
            "format": {
                "id": 4,
                "name": "image"
            },
            "macros": [
                {
                    "code": "BORDER_COLOR",
                    "name": "Image Border Color",
                    "is_required": false,
                    "type": "string",
                    "default_value": "blue",
                    "other_data": null
                },
                {
                    "code": "BORDER_SIZE",
                    "name": "Image Border Size",
                    "is_required": false,
                    "type": "integer",
                    "default_value": "6",
                    "other_data": null
                }
            ]
        }
    }
}
{code} 
```

### Delete a custom template

In this example, the `DELETE` request removes the custom template from the system entirely.

```
{code}$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/template?id=222'

{
    "response": {
        "status": "OK"
    }
}
{code}
```
