---
title: Bidders - Creative Template Service
description: Learn how Xandr categorizes creatives by format, media type, and media subtype. For each format, media type, and media subtype combination, Xandr provides a standard creative or you can build your own.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Creative template service

Xandr categorizes creatives by format, media type, and media subtype. Format defines the resource type of creatives (flash, image, etc.); media type defines the general display style of creatives (banner, expandable, video, etc.); and media subtype defines the specific display style of creatives (standard banner, MediaMind expandable, or Standard VAST).

## Standard templates

For each format, media type, and media subtype combination, Xandr provides a standard creative template that ensures proper rendering on web pages when creatives are served. You cannot edit these templates, but the Creative Template Service allows you to view them and examine their rendering code.

## Custom templates

If you want to customize the way certain types of creatives render, you can build your own templates. With custom templates, you have complete control of the JavaScript, HTML, or XML rendering code, and you can define macros to prompt your traffickers to enter information and make decisions about the behavior of creatives when they are uploaded.

> [!NOTE]
> You can have up to 100 custom templates. Please note, however, that Xandr does not provide support for creatives that do not render correctly as a result of errors in custom template code.

## REST API

| HTTP method | End point | Description |
|--|--|--|
| `GET` | `https://api.adnxs.com/template` | To view all templates (standard and custom). |
| `GET` | `https://api.adnxs.com/template?member_id=null` | To view standard templates only. |
| `GET` | `https://api.adnxs.com/template?id=TEMPLATE_ID` | To view a specific template. |
| `POST` | `https://api.adnxs.com/template` <br>(template JSON) | To add a new custom template. |
| `PUT` | `https://api.adnxs.com/template?id=TEMPLATE_ID` <br>(template JSON) | To modify a custom template.<br><br>**Tip**: To modify a custom template, you need to use your member user rather than your bidder user. <br><br>**Warning**: When you modify a custom template, your changes immediately affect any creatives that are already using the template. If your changes cause these creatives to stop rendering properly, their audit status will be changed to "rejected," and they will stop serving on most third-party inventory. |
| `DELETE` | https://api.adnxs.com/template?id=TEMPLATE_ID | To delete a custom template.<br><br>**Tip**: You cannot delete a custom template that is used by one or more creatives, but you can archive the template to prevent future creatives from using it. See the [Archiving a custom template](#archiving-a-custom-template) example below for more details. |

## JSON fields

| Field | Type (Length) | Description |
|--|--|--|
| `id` | int | The ID of the creative template.<br>**Required On**: `PUT`/`DELETE`, in query string |
| `name` | string (30) | The name of the creative template.<br><br>**Required On**: `POST` |
| `description` | string | The description of the creative template. |
| `member_id` | int | **Read-only**. The ID of the member that owns the template. For standard Xandr templates, this is `null`. |
| `media_subtype` | object | The display style of creatives that can use this template. Each media subtype belongs to a superordinate media type, for example, the `"Standard Banner"` media subtype belongs to the `"Banner"` media type. <br><br>**Required On**: `POST` |
| `format` | object | The format of creatives that can use this template, for example, `"image"` or `"flash"`. <br><br>**Required On**: `POST` |
| `is_default` | Boolean | If `true`, the template is automatically assigned to creatives that match the template's media type, media subtype, and format. When the creatives are uploaded, this default assignment can be overridden, if necessary.<br><br>**Note**: There can be only one default creative template per media type, media subtype, and format combination.<br><br>**Default**: `false` |
| `is_archived` | Boolean | If `true`, the template is archived. Archiving a template prevents future creatives from using the template but does not affect creatives already using the template.<br><br>**Default**: `false` |
| `content_js` | string | The template's rendering code in JavaScript. The code can include both Xandr standard macros and your own custom macros. Xandr macros must begin with the $ symbol, and custom macros must begin with the # symbol. Each custom macro must be defined in the macros array.<br><br>**Required On**: `POST`, if `content_html` and `content_xml` are not provided |
| `content_html` | string | The template's rendering code in HTML. The code can include both Xandr standard macros and your own custom macros. Xandr macros must begin with the $ symbol, and custom macros must begin with the # symbol. Each custom macro must be defined in the macros array.<br><br>**Required On**: `POST`, if `content_js` and `content_xml` are not provided |
| `content_xml` | string | **Deprecated**. |
| `callback_content_html` | string | When `media_subtype` is `"Popup"` or `"Popunder"`, `content_js` defines the rendering code for the pop window, and this field defines the rendering code for the content in the pop window. |
| `macros` | array of objects | The custom macros used in the `content_js`, `content_html`, or `content_xml` fields. You can include up to 20 custom macros in a template. |
| `last_modified` | timestamp | **Read-only**. The date and time when the creative template was last modified. |

### Media subtype

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of media subtype.<br><br>**Required On**: `POST` |
| `name` | string | **Read-only**. The name of the media subtype. |
| `mediatype_id` | int | **Read-only**. The ID of the media type to which the subtype belongs. |
| `media_type_name` | string | **Read-only**. The name of the media type to which the subtype belongs. |

### Format

You can use the [Creative Format Service](creative-format-service.md) to view all supported creative formats.

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of creative format.<br><br>**Required On**: `POST` |
| `name` | string | **Read-only**. The name of the creative format. |

### Custom macros

You must define each custom macro used in the `content_js`, `content_html`, or `content_xml` field.

| Field | Type (Length) | Description |
|--|--|--|
| `code` | string (30) | The macro name exactly as it is used in the `content_js`, `content_html`, or `content_xml` field. For example, if `#{BORDER_SIZE}` is the macro in the `content_js` field, you would pass `"BORDER_SIZE"` here. <br><br>**Required On**: `POST` |
| `name` | string (50) | The user-friendly name for this macro that traffickers will see when they add creatives that use this template via the Creative Service or UI. <br><br>**Required On**: `POST` |
| `type` | enum | The type of value that traffickers will provide for this macro when they add creatives that use this template via the Creative Service or UI. Possible values: `"true/false"`, `"string"`, `"url"`, `"integer"`, `"decimal"`, `"string_list"`, `"select_from_list"`. For example, on, if you set this to `"true/false"`, traffickers will see the macro name followed by a check box.<br><br>**Required On**: `POST` |
| `is_required` | boolean | If `true`, traffickers will be required to provide a value for the macro when adding creatives that use this template.<br><br>**Required On**: `POST` |
| `default_value` | string | If `is_required` is `false`, this is the default value that will be used when traffickers do not provide a value for the macro when adding creatives that use this template.<br><br>**Required On**: `POST`, if `is_required` is `false` |
| `other_data` | string | The accepted values for the macro, if type is `"string_list"` or `"select_from_list"`. |

## Examples

### Viewing all creative templates

``` 
{code}
$ curl -b cookies -c cookies 'https:api.adnxs.com/template'
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
        ],
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": true,
            "db": "06.mysql.sand-08.nym2",
            "reads": 2,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 0,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "time": 71.73490524292,
            "start_microtime": 1329952251.6778,
            "version": "1.11.12",
            "s1ave_lag": 0,
            "member_last_modified_age": 2979
        }
    }
}
{code}
```

### Viewing a specific creative template

In this example, the request gets details about the Xandr standard template for rendering creatives of the media type "Banner", media subtype "Standard Banner", and format "flash".

``` 
{code}
$ curl -b cookies -c cookies 'https:api.adnxs.com/template?id=3'
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
        },
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": false,
            "db": "master",
            "time": 684.47399139404,
            "start_microtime": 1329858928.9459,
            "version": "1.11.11.2",
            "s1ave_miss": "no_service_index"
        }
    }
}
{code}
```

### Adding a custom template

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
                "is_required": false
                "default_value": "black"
            }
        ]
    }
}{code}
{code}
$ curl -b cookies -c cookies -X POST -d @template 'https://api.adnxs.com/template'
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
        },
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": false,
            "db": "master",
            "reads": 0,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 1,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "time": 1270.6458568573,
            "start_microtime": 1329952805.2524,
            "version": "1.11.12",
            "master_instance": "04.hbapi.sand-08.lax1",
            "proxy": true,
            "master_time": 1084.1600894928
        }
    }
}
{code}
```

### Modifying a custom template

In this example, the `PUT` request updates the default values of the custom macros in custom template `222`.

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
$ curl -b cookies -c cookies -X PUT -d @template_update 'https://api.adnxs.com/template?id=222'
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
        },
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": false,
            "db": "master",
            "reads": 0,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 1,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "time": 1860.7339859009,
            "start_microtime": 1329954578.4409,
            "version": "1.11.12",
            "master_instance": "05.hbapi.sand-08.lax1",
            "proxy": true,
            "master_time": 1082.7260017395
        }
    }
}
{code}
```

### Archiving a custom template

In this example, the `PUT` request sets the `is_archived` field to `true`, thus archiving the template and preventing future creatives from using it.

``` 
{code}$ cat template_archive
{
    "template": {
         "is_archived": true
    }
}{code}
{code}
$ curl -b cookies -c cookies -X PUT -d @template_archive 'https://api.adnxs.com/template?id=222'
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
        },
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": false,
            "db": "master",
            "reads": 0,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 1,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "time": 1709.9781036377,
            "start_microtime": 1329955072.2898,
            "version": "1.11.12",
            "master_instance": "05.hbapi.sand-08.lax1",
            "proxy": true,
            "master_time": 890.67912101746
        }
    }
}
{code}
```

### Re-activating an archived custom template

In this example, the PUT request sets the is_archived field to false, thus re-activating the template and allowing new creatives to use it.

```
{code}$ cat template_activate
{
    "template": {
         "is_archived": false
    }
}{code}
{code}
$ curl -b cookies -c cookies -X PUT -d @template_activate 'https://api.adnxs.com/template?id=222'
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
        },
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": false,
            "db": "master",
            "reads": 0,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 1,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "time": 1709.9781036377,
            "start_microtime": 1329955072.2898,
            "version": "1.11.12",
            "master_instance": "05.hbapi.sand-08.lax1",
            "proxy": true,
            "master_time": 890.67912101746
        }
    }
}
{code}
```

### Deleting a custom template

In this example, the DELETE request removes the custom template from the system entirely.

```
{code}$ $ curl -b cookies -c cookies -X DELETE 'https://api.adnxs.com/template?id=222'
{
    "response": {
        "status": "OK",
        "dbg_info": {
            "instance": "02.hbapi.sand-08.nym2",
            "s1ave_hit": false,
            "db": "master",
            "reads": 0,
            "read_limit": 100,
            "read_limit_seconds": 60,
            "writes": 1,
            "write_limit": 60,
            "write_limit_seconds": 60,
            "time": 1454.5428752899,
            "start_microtime": 1329955347.807,
            "version": "1.11.12",
            "master_instance": "05.hbapi.sand-08.lax1",
            "proxy": true,
            "master_time": 1018.196105957
        }
    }
}
{code}
```
