---
title: VAST Extension Template Service
description: Explore the VAST Extension Template service, offering a template for entering and saving custom extensions from a VAST file.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# VAST Extension Template service

This service provides a template to enter and save custom extensions from a VAST file. Extensions are custom XML snippets added to the VAST file. Video players must be specially programmed to recognize and handle the data provided. Since an extension must be added manually, and to avoid having to add the same extension multiple times, you can use this service and enter the template ID.

In addition, custom and impbus macros are supported in the extension templates.

Once you have created an extension, you must then associate it with a creative.

## Example extension XML

```
<Ad>
  <InLine|Wrapper>
    <Extensions>
       <Extension type="X">
          <MyCustomization>ABC</MyCustomization>
          <AnotherCustomization>123</AnotherCustomization>
       </Extension>
    </Extensions>
  </InLine|Wrapper>
</Ad>
```

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/vast-extension-template](https://api.appnexus.com/vast-extension-template) | View VAST Extension Templates. |
| `POST` | [https://api.appnexus.com/vast-extension-template](https://api.appnexus.com/vast-extension-template) | Add a VAST extension template and custom macros. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `name` | string (1000) | The name of the VAST extension.<br>**Required On:** `POST` |
| `member_id` | int | The member ID of the member associated with this VAST extension. |
| `content` | string | The XML content to output when rendering the creative's VAST document.<br>**Required On:** `POST` |
| `created_on` | timestamp | The date and time the VAST extension template was created.<br>**Read Only.** |
| `last_activity` | timestamp | The date and time the template was last modified.<br>**Read Only.** |
| `macros` | array of objects | The custom macros used in the `content` field. For more details, see [Custom Macros](#custom-macros) below. |

### Custom macros

You must define each custom macro used in the `content` field.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `code` | string (30) | The macro name exactly as it is used in the `content` field. For example, if `#{BORDER_SIZE}` is the macro in the `content` field, you would pass `"BORDER_SIZE"` here.<br>**Required On:** `POST` |
| `name` | string (50) | The user-friendly name for this macro that traffickers will see when they add creatives that use this template via the UI.<br>**Required On:** `POST` |
| `is_required` | boolean | If true, traffickers will be required to provide a value for the macro when using this template.<br>**Required On:** `POST` |
| `type` | enum | The type of value that traffickers will provide for this macro when they add creatives that use this template. <br>Possible values:<br> - `"true/false"`<br> - `"string"`<br> - `"url"`<br> - `"integer"`<br> - `"decimal"`<br> - `"string_list"`<br> - `"select_from_list"` <br> - `"file"`<br>For example, on the UI, if you set this to `"true/false"`, traffickers will see the macro name followed by a check box.<br><br>**Required On:** `POST` |
| `default_value` | string | If `is_required` is `false`, this is the default value that will be used when traffickers do not provide a value for the macro when using this template.<br>**Required On:** `POST`, if `is_required` is `false`. |
| `other_data` | string | The accepted values for the macro, if `type` is `"string_list"` or `"select_from_list"`. |

## Examples

### Add a custom VAST extension and associate with a creative

#### Step 1: Add a custom VAST extension

```
$ cat vast-extension-template
 
{
    "vast-extension-template": {
     
      "name": "First Template",
      "member_id": 2,
      "content": "<hello>world #{FIRST} #{SECOND}</hello>",
      "created_on": "2017-05-21 13:15:17",
      "last_activity": "2017-05-21 13:15:17",
      "macros": [
        {
          "code": "FIRST",
          "name": "first",
          "is_required": false,
          "type": "string",
          "default_value": null,
          "other_data": null
        },
        {
          "code": "SECOND",
          "name": "second",
          "is_required": false,
          "type": "string",
          "default_value": null,
          "other_data": null
        }
      ]
    }
}


$ curl -b cookies -c cookies -X POST -d @vast-extension-template 'https://api.appnexus.com/vast-extension-template'
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 3,
    "start_element": 0,
    "num_elements": 100,
    "vast-extension-template": {
      "id": 3,
      "name": "First Template",
      "member_id": 2,
      "content": "<hello>world #{FIRST} #{SECOND}</hello>",
      "created_on": "2017-05-21 13:15:17",
      "last_activity": "2017-05-21 13:15:17",
      "macros": [
        {
          "code": "FIRST",
          "name": "first",
          "is_required": false,
          "type": "string",
          "default_value": null,
          "other_data": null
        },
        {
          "code": "SECOND",
          "name": "second",
          "is_required": false,
          "type": "string",
          "default_value": null,
          "other_data": null
        }
      ]
    },
   ...
  }
```

In the **`video_attribute`** object for the creative, assign the template ID in the **`vast_extension_template_id`** field and ensure that you define the macros in the **`custom_macros`** object.

#### Step 2: Associate it with a creative

```
{
    "creative-vast": {
        "id": 145,
        "template_id": 6439,
        "video_attribute": {
            "is_skippable": true,
            "duration_ms": 21000,
        “extensions”: [
                {
                    "vast_extension_template_id": 3
                }
            ],
            "wrapper": {
                "url": "http://www.doubleclick.net/...",
                "secure_url": "https://www.doubleclick.net/...",
                "elements": [
                    {
                        "vast_element_type_id": 1,
                        "name": "linear",
                        "trackers": [
                            {
                                "name": "startTracker",
                                "vast_event_type_id": 2,
                                "url": "http://tracker.com/...",
                                "secure_url": "https://tracker.com/...",
                                "event_type": "start"
                            },
                            {
                                "name": "completionTracker",
                                "vast_event_type_id": 8,
                                "url": "http://tracker.com/...",
                                "secure_url": "https://tracker.com/...",
                                "event_type": "completion"
                            }
                        ]
                    }
                ]
            }
        }
    }
}
```

### Update a custom VAST extension

```
$ cat vast-extension-template-update
 
{
    "vast-extension-template": {
     
      "name": "Second Template",
      "member_id": 4,
      "content": "<hello>world #{THIRD} #{FOURTH}</hello>",
      "created_on": "2017-05-21 13:15:17",
      "last_activity": "2017-05-21 13:15:17",
      "macros": [
        {
          "code": "THIRD",
          "name": "third",
          "is_required": true,
          "type": "string",
          "default_value": null,
          "other_data": null
        },
        {
          "code": "FOURTH",
          "name": "fourth",
          "is_required": false,
          "type": "string",
          "default_value": null,
          "other_data": null
        }
      ]
    }
}

{
    "creative":{
        "video_attribute":{
            "extensions":[
                {
                    "vast_extension_template_id": 3
                }
            ]
        }
        "custom_macros": [
            {
                "code": "FIRST"
                "value": "FirstVALUE"
            },
           {
                "code": "SECOND"
                "value": "SecondVALUE"
            } 
        ]
    }
}
```
