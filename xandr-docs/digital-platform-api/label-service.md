---
title: Label Service
description: Discover the Label service, providing the ability to view and apply labels to your advertisers, insertion orders, line items, campaigns, and publishers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Label service

This read-only service allows you to view the labels that can be applied to your advertisers, insertion orders, line items, campaigns, and publishers. It also allows you to view the labels that have already been applied.

An example of an advertiser label is `"Salesperson"`. You might use this label to specify the name of the salesperson responsible for each of your advertisers. You might then run the Network Analytics report filtered by `"salesperson_for_advertiser"` to focus on the advertisers that a particular salesperson is responsible for, or grouped by `"salesperson_for_advertiser"` to rank the performance of your salespeople.

The following reports currently support labels: [Network Analytics](network-analytics.md), [Network Advertiser Analytics](network-advertiser-analytics.md), and [Advertiser Analytics](advertiser-analytics.md). For the full list of report columns associated with labels, see `"report_field"` below.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/label](https://api.appnexus.com/label) | View all available labels. |
| `GET` | [https://api.appnexus.com/label?id=LABEL_ID](https://api.appnexus.com/label?id=LABEL_ID) | View a specific label. |
| `GET` | [https://api.appnexus.com/label?show_values=true&object_type=OBJECT_TYPE](https://api.appnexus.com/label?show_values=true&object_type=OBJECT_TYPE) | View the labels that are applied to a specific object type.<br><br>**Note:**<br>The following object types are available: `advertiser`, `publisher`, `line_item`, `campaign`, and `insertion_order`. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the label.<br>Possible values: `1`, `2`, `3`, `4`, `5`, `7`, `8`, `9`, `11`, `12`, `14`, `15`, `16`. |
| `is_user_associated` | boolean | This field is specific to. If `true`, the label is associated with a person (i.e. `"Salesperson"` or `"Account Manager"`) and will allow for auto-completion of the label value by the firstname, lastname of a user. |
| `is_reporting_enabled` | boolean | If `true`, the label is available for use in reporting. |
| `last_modified` | timestamp | The date and time when the label was last modified. |
| `member_id` | int | Since all labels are currently available to all members, this field will always be `NULL`. In the future, it may become possible for a member to create unique labels, in which case this field would return the ID of the owning member.  |
| `name` | string | The name of the label. Possible values: `"Salesperson"`, `"Account Manager"`, `"Trafficker"`, `"Sales Rep"`, `"Test/Control"`, `"Campaign Type"`, or `"Advertiser Type"`. For `id`/`name`/`object_type` mappings, see the [first example](#view-all-available-labels) below. |
| `object_type` | enum | The type of object to which the label can be applied. <br>Possible values: `"advertiser"`, `"insertion_order"`, `"line_item"`, `"campaign"`, or `"publisher"`. For `id`/`name`/`object_type` mappings, see the [first example](#view-all-available-labels) below. |
| `report_field` | string  | The report column with which you can report on the label. Possible report columns (with corresponding reports):<br> - `salesperson_for_advertiser` (Network Analytics)<br> - `salesperson_for_publisher` (Network Analytics)<br> - `account_manager_for_advertiser` (Network Analytics)<br> - `account_manager_for_publisher` (Network Analytics)<br> - `trafficker_for_line_item` (Network Analytics, Network Advertiser Analytics)<br> - `salesrep_for_line_item` (Network Analytics, Network Advertiser Analytics)<br> - `user_group_for_campaign` (Network Analytics, Network Advertiser Analytics, Advertiser Analytics)<br> - `advertiser_type` (Network Analytics, Network Advertiser Analytics)<br> - `line_item_type` (Network Analytics, Network Advertiser Analytics)<br> - `insertion_order_type` (Network Analytics, Network Advertiser Analytics) |
| `values` | array of objects | This field is return when using the request `GET` [https://api.appnexus.com/label?show_values=true&object_type=OBJECT_TYPE](https://api.appnexus.com/label?show_values=true&object_type=OBJECT_TYPE). For more details, see [Values](#values) and the [second example](#view-the-labels-that-are-applied-to-your-advertisers) below. |

### Values

| Field | Type | Description |
|:---|:---|:---|
| `object_id` | int | The ID of the object to which the label is applied. For example, if `object_type` is `"advertiser"`, `object_id` would be the `ID` of the advertiser. |
| `value` | string | The value assigned to the label. For example, for the publisher `"Salesperson"` label, this would be a name such as `"Michael Sellers"`. |

## Examples

### View all available labels

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/label'
{
    "response": {
        "status": "OK",
        "labels": [
            {
                "id": 1,
                "name": "Salesperson",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "advertiser",
                "report_field": "salesperson_for_advertiser",
                "last_modified": "2010-09-14 22:12:38"
            },
            {
                "id": 2,
                "name": "Salesperson",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "publisher",
                "report_field": "salesperson_for_publisher",
                "last_modified": "2010-09-14 22:12:43"
            },
            {
                "id": 3,
                "name": "Account Manager",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "advertiser",
                "report_field": "account_manager_for_advertiser",
                "last_modified": "2010-09-14 22:12:47"
            },
            {
                "id": 4,
                "name": "Account Manager",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "publisher",
                "report_field": "account_manager_for_publisher",
                "last_modified": "2010-09-14 22:12:51"
            },
            {
                "id": 5,
                "name": "Region",
                "member_id": null,
                "is_user_associated": false,
                "is_reporting_enabled": true,
                "object_type": "advertiser",
                "report_field": "region_for_advertiser",
                "last_modified": "2011-01-21 19:39:37"
            },
            {
                "id": 7,
                "name": "Trafficker",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "line_item",
                "report_field": "trafficker_for_line_item",
                "last_modified": "2011-05-31 16:11:21"
            },
            {
                "id": 8,
                "name": "Sales Rep",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "line_item",
                "report_field": "salesrep_for_line_item",
                "last_modified": "2011-05-31 16:11:29"
            },
            {
                "id": 9,
                "name": "Test/Control",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "campaign",
                "report_field": "user_group_for_campaign",
                "last_modified": "2011-12-06 18:07:44"
            },
            ...  
        ],
        "count": 10,
        "start_element": 0,
        "num_elements": 100
    }
}
```

### View the labels that are applied to your advertisers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/label?show_values=true&object_type=advertiser'
{
    "response": {
        "status": "OK",
        "labels": [
            {
                "id": 1,
                "name": "Salesperson",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "advertiser",
                "report_field": "salesperson_for_advertiser",
                "values": [
                    {
                        "object_id": "7669",
                        "value": "Phillip Turner"
                    },
                    {
                        "object_id": "7670",
                        "value": "Ami Kraft"
                    },
                    {
                        "object_id": "7713",
                        "value": "Michelle Jacobs"
                    },
                    {
                        "object_id": "7719",
                        "value": "Michelle Jacobs"
                    },
                    {
                        "object_id": "7759",
                        "value": "Phillip Turner"
                    },
                    {
                        "object_id": "7760",
                        "value": "Phillip Turner"
                    },
                    {
                        "object_id": "7761",
                        "value": "Ami Kraft"
                    }
                ],
                "last_modified": "2011-12-18 20:13:32"
            },
            {
                "id": 3,
                "name": "Account Manager",
                "member_id": null,
                "is_user_associated": true,
                "is_reporting_enabled": true,
                "object_type": "advertiser",
                "report_field": "account_manager_for_advertiser",
                "values": [
                    {
                        "object_id": "7669",
                        "value": "Tina Rivera"
                    },
                    {
                        "object_id": "7670",
                        "value": "Richard Seiken"
                    },
                    {
                        "object_id": "7713",
                        "value": "Richard Seiken"
                    },
                    {
                        "object_id": "7719",
                        "value": "Norman Fischer"
                    },
                    {
                        "object_id": "7759",
                        "value": "Norman Fischer"
                    },
                    {
                        "object_id": "7760",
                        "value": "Tina Revera"
                    },
                    {
                        "object_id": "7761",
                        "value": "Norman Fisher"
                    }
                ],
                "last_modified": "2010-09-28 20:13:32"
            }
        ],
        "count": 2,
        "start_element": null,
        "num_elements": null
    }
}
```
