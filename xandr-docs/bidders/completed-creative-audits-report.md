---
title: Bidders - Completed Creative Audits Report
description: Completed Creative Audits Report gives you insight into how your creatives are moving through the audit process. Learn the advantages of using this report in this page and steps to retrieve the report.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Completed creative audits report

The **Completed Creative Audits Report** is designed to give you insight into how your creatives are moving through the audit process. Using this report, you can find out:

- How many of your creatives have been audited over a given time frame
- Which of your creatives have completed audit
- How much your creative audit fees will be

See the [Example](#example) below for instructions on retrieving this report.

> [!TIP]
> For more information about how reporting works, see the [Report Service](report-service.md).

This report's data is retained for 90 days.

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- `yesterday`
- `last_7_days`
- `month_to_date`
- `last_month`
- `last_30_days`
- `last_14_days`

## Dimensions

| Column | Type | Filter? | Description |
|--|--|--|--|
| `audit_completion_date` | date | Yes | The day on which the audits were completed. |
| `audit_reason` | string | Yes | The type of audit. This will be either "Initial" or "Reaudit". |
| `audit_reason_id` | int | Yes | The integer code for the type of audit. There are two allowed values: <br> - `1`: Initial audit <br> - `2`: Reaudit |
| `audit_type` | string | Yes | The priority of the audit. Allowed values: <br> - `"standard"` <br> - `"priority"` |
| `audit_type_id` | int | Yes | The integer code for the priority of the audit. Allowed values: <br> - `1`: Standard <br> - `2`: Priority |
| `creative_id` | int | Yes | ID of the creative that was audited. |
| `creative_name` | string | Yes | Name of the creative that was audited. |
| `day` | date | Yes | Day on which audits were completed (alias for `audit_completion_date`). |
| `member_id` | int | Yes | ID of the member whose creative was audited. |
| `member_name` | string | Yes | The name of the member whose creative was audited. |

## Metrics

| Column | Type | Description |
|--|--|--|
| `num_audits_completed` | int | The number of audits completed in the grouping specified. |
| `total_audit_fee` | double | The total fees for audits in the grouping specified. |

## Example

### Create the JSON report request

``` 
$ cat completed-creative-audits.json
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

### `POST` the request data to the Reporting Service

``` 
$ curl -b cookies -X POST -d @completed-creative-audits.json https://api.adnxs.com/report
{
    "response": {
        "existing": false,
        "status": "OK",
        "report_id": "3883b9d919e9361f47aa92e707849058",
        "dbg": {
            ...
        }
    }
}
```

### `GET` the report data

``` 
$ curl -b cookies https://api.adnxs.com/report/c2c682185b62ec9afd019536a8d947cc
{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2014-08-14 16:06:14",
            "header_info": "Report ID:,3883b9d919e9361f47aa92e707849058
Run at:,2014-08-14 16:06:14
Start date:,2014-08-13 00:00:00
End date:,2014-08-14 00:00:00
Timezone:,
User:,Rick Land (14311)
",
            "row_count": "0",
            "report_size": "149",
            "user_id": "14311",
            "entity_id": "0",
            "started_on": "2014-08-14 16:06:16",
            "finished_on": "2014-08-14 16:06:18",
            "query_time": "1",
            "data": "day,creative_id,creative_name,member_id,audit_completion_date,audit_type,num_audits_completed,total_audit_fee,audit_completion_date
",
            "url": "report-download?id=3883b9d919e9361f47aa92e707849058"
        },
        "execution_status": "ready",
        "dbg": {
            ...
        }
    }
    }
```

## Related topics

- [Report Service](report-service.md)
- [Saved Report Service](saved-report-service.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Platform Seller Report](platform-seller-report.md)
- [Seller platform billing report](seller-platform-billing-report.md)
- [Inventory Availability Reporting](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
