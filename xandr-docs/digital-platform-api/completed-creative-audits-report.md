---
title: Digital Platform API - Completed Creative Audits Report
description: Learn about the Digital Platform API's Completed Creative Audits report, their time frame, data retention period, dimensions, and metrics with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Completed Creative Audits report

The **Completed Creative Audits Report** is designed to give you insight into how your creatives are moving through the audit process. Using this report, you can find out:

- How many of your creatives have been audited over a given time frame?
- Which of your creatives have completed audit?
- How much your creative audit fees will be?

For instructions on retrieving this report, see the [examples](#examples) below.

> [!NOTE]
> For more information about how reporting works, see the [Report Service](report-service.md).

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- yesterday
- last_7_days
- month_to_date
- last_month
- last_30_days
- last_14_days

### Data retention period

Data retention period for this report is 365 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Description |
|:---|:---|:---|:---|
| `day` | date | Yes | Day on which audits were completed (alias for `audit_completion_date`). |
| `creative_id` | int | Yes | ID of the creative that was audited. |
| `creative_name` | string | Yes | Name of the creative that was audited. |
| `advertiser_id` | int | Yes | The ID of the advertiser associated with the creative that was audited. |
| `advertiser_name` | string | Yes | The name of the advertiser associated with the audited creative. |
| `member_id` | int | Yes | ID of the member whose creative was audited. |
| `audit_reason_id` | int | Yes | The integer code for the type of audit. There are two allowed values:<br> - `1`: Initial audit<br> - `2`: Reaudit |
| `audit_reason` | string | Yes | The type of audit. This will be either `"Initial"` or `"Reaudit"`. |
| `audit_type_id` | int | Yes | The integer code for the priority of the audit. Allowed values:<br> - `1`: Standard<br> - `2`: Priority |
| `audit_type` | string | Yes | The priority of the audit. Allowed values:<br> - `"standard"`<br> - `"priority"` |
| `member_name` | string | Yes | The name of the member whose creative was audited. |
| `audit_completion_date` | date | Yes | The day on which the audits were completed. |

## Metrics

| Column | Type | Description |
|:---|:---|:---|
| `num_audits_completed` | int | The number of audits completed in the grouping specified. |
| `total_audit_fee` | double | The total fees for audits in the grouping specified. |

## Examples

### Create the JSON report request

```
$ cat completed_creative_audits.json

{
    "report": {
        "format": "csv",
        "report_interval": "yesterday",
        "filters": [
            {
                "member_id": 88
            }
        ],
        "columns": [
            "day",
            "creative_id",
            "creative_name",
            "advertiser_name",
            "member_id",
            "audit_completion_date",
            "audit_type",
            "num_audits_completed",
            "total_audit_fee",
            "audit_completion_date"
        ],
        "report_type": "completed_creative_audits"
    }
}
```

### `POST` the request data to the Report Service

```
$ curl -b cookies -X POST -d @completed-creative-audits.json https://api.appnexus.com/report

{
    "response":{
        
         "existing":true,
         "report_id":"c2c682185b62ec9afd019536a8d947cc",
         "status":"OK"
    }
}
```

### `GET` the report status

```
$ curl -b cookies https://api.appnexus.com/report?id=c2c682185b62ec9afd019536a8d947cc


{
    "response":{
         "execution_status":"ready",
         "status":"OK"
    }
}
```

### `GET` the report data

```
curl -b cookies https://api.appnexus.com/report-download?id=c2c682185b62ec9afd019536a8d947cc > /tmp/completed_creative_audits.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topics

- [Report Service](report-service.md)
- [Saved Report Service](saved-report-service.md)
