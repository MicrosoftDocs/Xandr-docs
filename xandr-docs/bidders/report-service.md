---
title: Bidders - Report Service
description: In this article, find information about the Report Service, the fields associated with it, and the process for retrieving reports.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Report service

The Report Service offers reporting data of interest to both buyers and sellers. It's used to answer questions such as:

- How much money was spent?
- How many impressions were seen?
- How many impressions were sold?
- How much revenue was earned?

This is a **read-only** service. Although you will `POST` a JSON-formatted report request, this will not alter any data in the Imp Bus cache. You must be authenticated as a `"bidder"` user type to run reports. Each report type provides its own metrics, filtering, and grouping options.

> [!TIP]
> Need more than 90 days of data?
>
> The `platform_buyer` and `platform_seller` report types pull from tables that store the last 90 days worth of data. For older data, please use the `bidder_pricing_report` and `seller_invoice_report` report types.
>
> The Report Service runs reports asynchronously, which means it can run several processes in parallel. When you make a report request, you will either receive the report, an error message, or a pending message. For more information, see [How to Retrieve a Report](#how-to-retrieve-a-report) below.
>
> There is also a graphical user interface (UI) to view this reporting data at [Bidder](https://bidder.xandr.com/). If you do not have access to this UI, contact your Xandr representative.
> [!NOTE]
> The Bidder UI does not expose all functionality that is available via the API. It only exposes the `platform_buyer` analytics report. If you need a different report, you must use the API.

## Report types

The primary report types are:

- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Platform Seller Report](platform-seller-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Seller Platform Billing Report](seller-platform-billing-report.md)
- [Completed Creative Audits Report](completed-creative-audits-report.md)
- [Bidder Bid Error Report API](bidder-bid-error-report-api.md)

## REST API for viewing metadata

There are two layers of data in the Report Service - metadata and actual data. Metadata is a list of available reporting parameters.

To run a custom report you will need a JSON-formatted request. You can request data by a filter, group, or column. A filter will filter out results. A request having a filter such as `day`, will filter based on aggregated data. You can also search by individual parameters, such as `imps_sold`.

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/report?meta=buyer_platform_billing` | Return metadata for `bidder_pricing_report` type. |
| GET | `https://api.adnxs.com/report/meta/platform_buyer` | Return metadata for `platform_buyer` type. |
| GET | `https://api.adnxs.com/report/meta/platform_seller` | Return metadata for `platform_seller` type. |
| GET | `https://api.adnxs.com/report/meta/seller_platform_billing` | Return metadata for `seller_invoice_report` type. |

> [!NOTE]
> You can also use a more standard query format to return metadata:
>
> ```
> report?meta=report_type
> ```
>
> For example:
>
> ```
> GET https://api.adnxs.com/report?meta=platform_buyer
> ```
>

Metadata comes in the following format:

```
{"column":"day","type":"time"}
{"column":"month","type":"time"}
{"column":"geo_country","type":"string"}
```

## Metadata example

```
$ curl "https://api.adnxs.com/report/meta/platform_buyer"
  "response": {
    "status": "OK",
 "meta": {
      "columns": [
        {
          "column": "month",
          "type": "time"
        },
        {
          "column": "day",
          "type": "date"
        },
        {
          "column": "hour",
          "type": "date"
        },
      ...
      ],
      "filters": [
        {
          "column": "hour",
          "type": "date"
        },
        {
          "column": "day",
          "type": "date"
        },
        {
          "column": "year",
          "type": "date"
        },
        ...
      ],
      "havings": [
        {
          "column": "clicks"
        },
        {
          "column": "buyer_spend"
        },
        {
          "column": "imps_bought"
        },
        {
          "column": "buyer_ecpm"
        },
        {
          "column": "click_rate_sold"
        }
      ],
      "time_intervals": [
        "current_hour",
        "last_hour",
        "last_48_hours",
        "today",
        "yesterday",
        "last_7_days",
        "month_to_date",
        "quarter_to_date",
        "last_month",
        "lifetime",
        "mtd"
      ]
    }
}
```

## REST API for data retrieval

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/report/REPORT_ID` | Request the status of a report. |
| GET | `https://api.adnxs.com/report-download/REPORT_ID` | Retrieve report data. |
| POST | `https://api.adnxs.com/report?member_id=MEMBER_ID` <br> (report JSON) | Request a report. |

## JSON fields

| Field | Required | Type | Description |
|---|---|---|---|
| `columns` | yes (at least one) | array | List of columns to include in the report. See the documentation for each individual report to learn which columns are available. For a simple example, see [How to Retrieve a Report](#how-to-retrieve-a-report) below. |
| `end_date` | no | string | The ending date for the report. <br> - For report types that offer hourly data, this must be formatted as `"YYYY-MM-DD HH:MM:SS"`. However, `MM:SS` must be `00:00`, as data is not available for minutes and seconds. <br> - For report types that do not offer hourly data, this must be formatted as `"YYYY-MM-DD"`. <br><br> **Note**: The `end_date` is non-inclusive. For example, if you start a monthly report on "`2012-07-01"` and end the report on `"2012-07-31"`, your report will not include data from the last day of the month. The correct way to retrieve this data would be to end the report on `"2012-08-01"`. |
| `escape_fields` | no | boolean | When `true`, it adds quotes around each field in the report output to allow for safer import into Excel. This only applies to CSV and tab-delimited reports. |
| `filters` | no | array | List of filters to apply to the report. See the documentation for each individual report to see which fields can be filtered on. For a simple example, see [How to Retrieve a Report](#how-to-retrieve-a-report) below. <br><br> **Note**: The `is_delivered` filter value is only `true` if the impression was served successfully. Otherwise, it's `false`. |
| `report_interval` | no | enum | The time range for the report. Not all reports accept all intervals; see each report's documentation and metadata for details. Possible values: <br> - `current_hour` <br> - `last_hour` <br> - `today` <br> - `yesterday` <br> - `last_48_hours` <br> - `last_7_days` <br> - `lifetime` <br> - `month_to_date` <br> - `mtd` <br> - `last_month` |
| `report_type` | yes | enum | Must be one of: <br> - "`platform_buyer`" <br> - "`platform_seller`" <br> - "`bidder_pricing_report`" <br> - "`seller_invoice_report`" <br> - "`completed_creative_audits`" <br> - "`bidder_bid_error_report`" <br> This determines which information will be returned. |
| `row_per` | no | array | List of groupings to include in the report. See the documentation for each individual report to learn which columns can be used to group by. For a simple example, see [How to Retrieve a Report](#how-to-retrieve-a-report) below. |
| `start_date` | no | string | The ending date for the report. <br> - For report types that offer hourly data, this must be formatted as `"YYYY-MM-DD HH:MM:SS"`. However, `MM:SS` must be `00:00`, as data is not available for minutes and seconds. <br> - For report types that do not offer hourly data, this must be formatted as `"YYYY-MM-DD"`. |
| `timezone` | no | string | The timezone in which the data will be reported. For a list of possible timezone values, see [Reporting Timezones](reporting-timezones.md). |

## How to retrieve a report

- [Step 1. Create a JSON-formatted report request](#step-1-create-a-json-formatted-report-request)
- [Step 2. POST the request to the Report Service](#step-2-post-the-request-to-the-report-service)
- [Step 3. GET the report status from the Report Service](#step-3-get-the-report-status-from-the-report-service)
- [Step 4. GET the report data from the Report Download Service](#step-4-get-the-report-data-from-the-report-download-service)

### Step 1. Create a JSON-formatted report request

The JSON file should include the specific `report_type` that you want to run, as well as the `columns` (dimensions and metrics) and `report_interval` (`"today"`, `"yesterday"`, `"month_to_date"`, etc.) that you want to retrieve. You can also include `filters` for dimensions and define granularity (year, month, day) and specify the `format` in which the data should be returned. The `format` options are:

- `"csv"` - Comma-separated file
- `"xls"` - Tab-separated M.S. Excel file
- `"xlsx"` - Native M.S. Excel format

> [!NOTE]
> To filter a dimension by more than one value, use an array. For example:
>
> Correct:
>
> ```
> "filters": [{"bid_type": ["learn","optimized"]}, {"geo_country":"US"}]
> ```
>
> Incorrect:
>
> ```
> "filters": [{"bid_type":"learn"}, {"bid_type":"optimized"}, {"geo_country":"US"}]
> ```
>

See [JSON Fields](#json-fields) above for more details about the fields that can be included in the request. For a full list of available dimensions and metrics, see the documentation for the specific report type that you want to run, or pull that report's metadata as described in [REST API for Viewing Metadata](#rest-api-for-viewing-metadata).

```
$ cat report_request
{
    "report": {
        "report_type": "platform_buyer",
        "report_interval": "last_48_hours",
        "columns": ["day","imps_bought"],
        "filters": [{"geo_country":"US"}],
        "orders": [{"order_by":"day", "direction":"ASC"}],
        "format": "csv"
    }
}
```

### Step 2. `POST` the request to the report service

You `POST` the JSON request and get back a report ID.

```
$ curl -b cookies -c cookies -X POST -d @report_request 'https://api.adnxs.com/report?member_id=255'
{
    "response": {
        "status": "OK",
        "report_id": "ca9955709eade9a0e89f5cda5345c12r",
        "dbg_info": {
            ...
        }
    }
}
```

### Step 3. `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `"execution_status"` is `"ready"`. Then use the `report-download` service to save the reporting data to a file. (This is described in the next step.)

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/report/ca9955709eade9a0e89f5cda5345c12r'
{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2012-03-13 18:15:48",
            "cache_hit": false,
            "fact_cache_hit": false,
            "json_request": "{\"report\":{\"report_type\":\"network_analytics\",\"report_interval\":
                \"last_48_hours\",\"columns\":[\"day\",\"imps\",\"clicks\"],\"filters\":[{\"geo_country\":
                \"US\"},{\"entity_member_id\":\"514\"},{\"entity_member_id\":null}],\"orders\":
                [{\"order_by\":\"day\",\"direction\":\"ASC\"},{\"order_by\":\"imps\",\"direction\":
                \"DESC\"}]}}",
            "header_info": "Report type:,network_analytics\r\n,\r\nRun at:,2012-03-13 18:15:48\r\nStart date:,
                \r\nEnd date:,\r\nTimezone:,\r\nUser:,John Smith (9385)\r\n",
            "report_size": "10",
            "row_count": "35",
            "url": "report-download?id=ca9955709eade9a0e89f5cda5345c12r"
        },
        "execution_status": "ready",
        "dbg_info": {
            ...
        }
    }
}
```

### Step 4. `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the url field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTPS error code and message. Use `-i` or `-v` in your request to expose the response header.
>
> ```
> $ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=<download_id>
> ```
>

You can then open the file.

:::image type="content" source="media/network-analytics.png" alt-text="A screenshot of the downloaded file with the report data.":::

## Schedule recurring reports

You can automate the reporting process by creating saved versions of the reports you care about and having our system email the data to you at specified intervals. For more information about how to set up these automated reports, see the [Saved Report Service](saved-report-service.md).

## Related topics

- [Saved Report Service](saved-report-service.md)
- [Completed Creative Audits Report](completed-creative-audits-report.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Platform Seller Report](platform-seller-report.md)
- [Seller Platform Billing Report](seller-platform-billing-report.md)
- [Bidder Bid Error Report API](bidder-bid-error-report-api.md)
- [Inventory Availability Reporting](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
