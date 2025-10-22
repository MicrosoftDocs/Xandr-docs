---
title: Digital Platform API - Saved Report Service
description: Explore the Saved Report service to generate and store reports that can be accessed whenever needed.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Saved Report service

The Saved Report service can be used to create new reports which are saved and can be retrieved at any time. They are useful for reports which are executed frequently. The Saved Report Service acts as a wrapper around the [Report Service](report-service.md).

> [!NOTE]
> There is a limit of 100K rows per report.

A few facts to keep in mind about saved reports:

- Saved reports expire after 6 months. You must create a new saved report after 6 months.
- Saved reports cannot have a **Lifetime** or **Custom** date range.
- Saved reports are run in the order in which they were originally created. For example, if you create two daily reports, the daily report created first will run first each day.
- Daily reports are run and sent each day at varying times throughout the day.
- Weekly reports are run and sent on the Monday of each week for the previous 7 days.
- Monthly reports are run and sent on the first day of each month.

## REST API

> [!NOTE]
> Reports saved by other users within your network (member) will not be returned in these calls. Only those reports saved by your user account will be returned.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/saved-report?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/saved-report?advertiser_id=ADVERTISER_ID) | To view all saved reports for an advertiser. |
| `GET` | [https://api.appnexus.com/saved-report?publisher_id=PUBLISHER_ID](https://api.appnexus.com/saved-report?publisher_id=PUBLISHER_ID) | To view all saved reports for a publisher. |
| `GET` | [https://api.appnexus.com/saved-report?id=SAVED_REPORT_ID](https://api.appnexus.com/saved-report?id=SAVED_REPORT_ID) | To view a specific saved report. |
| `POST` | [https://api.appnexus.com/saved-report?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/saved-report?advertiser_id=ADVERTISER_ID) | To add a new saved report for an advertiser. |
| `POST` | [https://api.appnexus.com/saved-report?publisher_id=PUBLISHER_ID](https://api.appnexus.com/saved-report?publisher_id=PUBLISHER_ID) | To add a new saved report for an publisher. |
| `PUT` | [https://api.appnexus.com/saved-report?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/saved-report?advertiser_id=ADVERTISER_ID) | To modify an existing saved report for an advertiser. |
| `PUT` | [https://api.appnexus.com/saved-report?publisher_id=PUBLISHER_ID](https://api.appnexus.com/saved-report?publisher_id=PUBLISHER_ID) | To modify an existing saved report for publisher. |
| `DELETE` | [https://api.appnexus.com/saved-report?id=SAVED_REPORT_ID](https://api.appnexus.com/saved-report?id=SAVED_REPORT_ID) | To delete an existing saved report. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `category` | string | The category of the report. |
| `created_on` | string | The date and time on which the saved report was created. |
| `emails` | array | The list of emails to send the report. The array should be in the format `["email_address1@domain.com", "email_address2@domain.com", ...]` |
| `entity_id` | int | The entity ID of the user creating the report. This sets the scope of the report. |
| `expires_on` | string | The date and time on which a saved report expires. This is currently limited to one year in the future. The date/time should be specified in the format `"YYYY-MM-DD HH:MM:SS"` where the time is specified in 24-hour format.<br>**Required On:** `POST` and `PUT`. |
| `format` | enum | The format in which the report results will be saved. Possible values: `"excel"` or `"csv"`. |
| `id` | int | The internal ID associated with the saved report.<br>**Required On:** `PUT` |
| `last_modified` | string | The date and time on which the saved report was last modified. |
| `name` | string | The name of the report which is display in the UI. The maximum length is 100 characters. |
| `report` | object | Report defined in the same format as used in the [Reporting Service](report-service.md). |
| `scheduling` | enum | The frequency with which the report is executed. Possible values: `"daily"`, `"weekly"`, or `"monthly"`. |

## Examples

### Add a new saved report for a publisher

1. Construct a report JSON (as described in [Report Service - Step 1](./report-service.md#step-1-create-a-json-formatted-report-request)).
1. `POST` the JSON to the saved-report service.
1. Store the ID that is returned.

```
$ cat saved-report

{
   "saved-report":{
      "name":"Publisher Report Last 48 Hours",
      "report":{
         "report_type":"publisher_analytics",
         "columns":[
            "publisher_revenue",
            "imps_total",
            "imps_sold",
            "imps_default",
            "clicks",
            "ctr",
            "month",
            "day",
            "hour",
            "geo_country",
            "size",
            "placement",
            "total_convs",
            "convs_rate",
            "publisher_rpm"
         ],
         "row_per":[
            "month",
            "day",
            "hour",
            "geo_country",
            "size",
            "placement_id"
         ],
         "timezone":"EST",
         "report_interval":"last_48_hours"
      },
      "scheduling":"daily",
      "format":"excel",
      "emails":[
         "reporting@publisher.com",
         "noreply@publisher.com"
      ],
      "expires_on":"2010-10-31 0:00:00"
   }
}

$ curl -b cookies -c cookies -X post --data-binary @saved-report 'https://api.appnexus.com/saved-report?publisher_id=35'

{
   "response":{
      "status":"OK",
      "id":39
   }
}
```

### Execute and retrieve a saved report

> [!NOTE]
> You must perform this step every time you wish to retrieve an updated report.

1. `POST` to the report service with the id from above, and store the returned `report_id`.
1. Check the report's status with a `GET` to the report service with the `report_id` (as described in [Report Service - Step 3](./report-service.md#step-3-get-the-report-status-from-the-report-service)).
1. `GET` the report from the `report-download` service (as described in [Report Service - Step 4](./report-service.md#step-4-get-the-report-data-from-the-report-download-service)).

```
$ curl -b cookies -c cookies -X post "https://api.appnexus.com/report?saved_report_id=39&publisher_id=35"

{
   "response":{
      "status":"OK",
      "report_id":"fa16873114e1d5697091069e45bccec0"
   }
}

$ curl -b cookies -c cookies "https://api.appnexus.com/report?id=fa16873114e1d5697091069e45bccec0"

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-06-10 15:53:07",
         "json_request":"{\"report\":{\"report_type\":\"publisher_analytics\",\"columns\":[\"publisher_revenue\",\"imps_total\",
             \"imps_sold\",\"imps_default\",\"clicks\",\"ctr\",\"month\",\"day\",\"hour\",\"geo_country\",\"size\",\"placement\",
             \"total_convs\",\"convs_rate\",\"publisher_rpm\"],\"row_per\":[\"month\",\"day\",\"hour\",\"geo_country\",\"size\",
             \"placement_id\"],\"timezone\":\"EST\",\"report_interval\":\"last_48_hours\",\"filters\":[{\"publisher_id\":\"4642\"},
             {\"publisher_id\":\"4642\"}]}}",
         "data":"publisher_revenue,imps_total,imps_sold,imps_default,clicks,ctr,month,day,hour,geo_country,size,placement,total_convs,convs_rate,publisher_rpm\r\n"
      },
      "execution_status":"ready"
   }
}

 
$ curl -i -b cookies -c cookies 'https://api.appnexus.com/report-download?id=fa16873114e1d5697091069e45bccec0' > /tmp/publisher_analytics.csv
```
