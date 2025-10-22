---
title: Bidders - Saved Report Service
description: In this article, find information about the Saved Report Service and the fields associated with it along with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Saved report service

The Saved Report service can be used to create new reports which are saved and can be retrieved at any time. They are useful for reports which are executed frequently. The Saved Report Service acts as a wrapper around the [Report Service](../digital-platform-api/report-service.md).

> [!NOTE]
> There is a limit of 100K rows per report.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| DELETE | `https://api.adnxs.com/saved-report/ID`  | Delete an existing saved report. |
| GET | `https://api.adnxs.com/saved-report`  | View all saved reports for your member. |
| GET | `https://api.adnxs.com/saved-report/ID`  | View a specific saved report. |
| POST | `https://api.adnxs.com/saved-report` | Add a new saved report. |
| PUT | `https://api.adnxs.com/saved-report/ID` | Modify an existing saved report. |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `category` | string | The category of the report. |
| `created_on` | string | The date and time on which the saved report was created. |
| `emails` | array | The list of emails to send the report. The array should be in the format [`"email_address1@domain.com"`, `"email_address2@domain.com"`, ...] |
| `entity_id` | int | The entity ID of the user creating the report. This sets the scope of the report. |
| `expires_on` | string | The date and time on which a saved report expires. This is currently limited to one year in the future. The date/time should be specified in the format "YYYY-MM-DD HH:MM:SS" where the time is specified in 24-hour format. <br> **Required On**: POST |
| `format` | enum | The format in which the report results will be saved. <br> Possible values: "excel" or "csv". |
| `id` | int | The internal ID associated with the saved report. <br> **Required On**: PUT |
| `last_activity` | string | The date and time on which the saved report was last modified. |
| `name` | string | The name of the report which is display in . The maximum length is 100 characters. |
| `report` | object | Report defined in the same format as used in the [Report Service](../digital-platform-api/report-service.md). |
| `scheduling` | enum | The frequency with which the report is executed. Possible values: "daily", "weekly", or "monthly". |

## Examples

### Adding a new saved report for a publisher

```
    {
    "saved-report": {
        "name": "Seller Platform Billing Report 48 Hours JMS",
        "report": {
            "report_type": "seller_platform_billing",
            "columns": [
                "day",
                "imps",
                "seller_revenue"
            ],
            "timezone": "EST",
            "report_interval": "last_48_hours"
        },
        "scheduling": "daily",
        "format": "excel",
        "emails": [
            "ejones@xandr.com",
            "bsmith@xandr.com"
        ],
        "expires_on": "2014-08-05 11:22:33"
    }
}
 
$ curl -b cookies -c cookies -X POST -d @saved-report.json 'https://api.adnxs.com/saved-report' | json-pp
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null,
        "saved_reports":[
            {
                "id":826,
                "name":"Seller Platform Billing Report 48 Hours JMS",
                "report":{
                    "report_type":"seller_platform_billing",
                    "columns":[
                        "day",
                        "imps",
                        "seller_revenue"
                    ],
                    "timezone":"EST",
                    "report_interval":"last_48_hours",
                    "filters":[
                        {
                            "seller_member_id":"7"
                        }
                    ]
                },
                "scheduling":"daily",
                "format":"excel",
                "emails":[
                    "jschneider@xandr.com",
                    "bsmith@xandr.com"
                ],
                "created_on":"2014-04-16 20:55:59",
                "expires_on":"2014-08-05 11:22:33",
                "category":null,
                "entity_id":null,
                "last_activity":"2014-04-16 20:55:59"
            }
        ]
        }
}
```

### Executing and retrieving a saved report

```
$ curl -b cookies -c cookies -X POST 'https://api.adnxs.com/report?saved_report_id=826' 
{
    "response":{
        "existing":false,
        "status":"OK",
        "report_id":"5f45fcccc5c4b4ba6fb9747bf6fc33b9"
        }
}
$ curl -b cookies -c cookies "https://api.adnxs.com/report?id=fa16873114e1d5697091069e45bccec0"
{
    "response":{
        "status":"OK",
        "report":{
            "name":null,
            "created_on":"2014-04-16 21:15:04",
            "json_request":
                                "{\"report\":
                                        {\"report_type\":\"seller_platform_billing\",
                    \"columns\":[
                        \"day\",
                        \"imps\",
                        \"seller_revenue\"
                    ],
                    \"timezone\":\"EST\",
                    \"report_interval\":\"last_48_hours\",
                    \"filters\":[
                        {
                            \"seller_member_id\":\"7\"
                        },
                        {
                            \"seller_member_id\":\"7\"
                        }
                    ]
                }
            }
            "data":"day,imps,seller_revenue\r\n",
        },
        "execution_status":"ready",
   }
}
 
$ curl -b cookies -c cookies -s "https://api.adnxs.com/report-download?id=fa16873114e1d5697091069e45bccec0" > report.csv
```

### Updating an existing report

```
$ cat add-columns-saved-report.json
{
    "saved_report": {
            "report":{
                "report_type":"seller_platform_billing",
                "columns":[
                    "day",
                    "imps",
                    "seller_revenue",
                    "bidder_id"       
                ],
                "timezone":"EST",
                "report_interval":"last_48_hours",
                "filters":[
                    {
                        "seller_member_id":"7"
                    }
                ]
            }
    }
}
 
$ curl -b cookies -c cookies -X PUT -d @add-column-saved-report.json 'https://api.adnxs.com/saved-report?id=826'
{
 "response": {
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null,
        "id":"826",
        "saved_report":{
            "id":826,
            "name":"Seller Platform Billing Report 48 Hours JMS",
            "report":{
                "report_type":"seller_platform_billing",
                "columns":[
                    "day",
                    "imps",
                    "seller_revenue",
                    "bidder_id"
                ],
                "timezone":"EST",
                "report_interval":"last_48_hours",
                "filters":[
                    {
                        "seller_member_id":"7"
                    }
                ]
            },
            "scheduling":"daily",
            "format":"excel",
            "emails":[
                "jschneider@xandr.com",
                "bsmith@xandr.com"
            ],
            "created_on":"2014-04-16 20:55:59",
            "expires_on":"2014-08-05 11:22:33",
            "category":null,
            "entity_id":null,
            "last_activity":"2014-04-17 16:00:27"
        },
        "dbg":{
            ...
        }
    }
}
```

## Related topics

- [Report Service](../digital-platform-api/report-service.md)
- [Completed Creative Audits Report](completed-creative-audits-report.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Platform Seller Report](platform-seller-report.md)
- [Seller Platform Billing Report](seller-platform-billing-report.md)
- [Inventory Availability Reporting](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
