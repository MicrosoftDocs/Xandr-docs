---
title: Digital Platform API - Report Service
description: Use the Report service to access different types of reports.
ms.date: 07/14/2025
ms.custom: digital-platform-api
---

# Digital Platform API - Report service

The Report Service is used to provide access to many different types of reports. It also ensures that each user types can only access the reports that are appropriate for that type. For example, network users have access to all report types, while advertiser and publisher users only have access to a few.

The available metrics vary depending on the report type, but can include how much money was spent on inventory, the number of impressions seen and/or sold, revenue earned, and more. This document describes how to request and download data from the Report Service. It also describes how to get more information about each of the supported report types, as well as providing links to further documentation about each report type.

> [!NOTE]
>
> - For more information about how to sync Xandr data to your reporting database, see [Bulk Reporting Feeds](bulk-reporting-feeds.md).
> - This is a read-only service; you will `POST` a JSON-formatted report request, but this will not alter any of the data stored on our servers.

## Report types

| Report Type | User Type | Description | Data Retention |
|:---|:---|:---|:---|
| [Network Analytics](./network-analytics.md)<br>`network_analytics` | Network | General overview of what is happening. What's serving, what's doing well, on both buy and sell side. | Lifetime - some data at reduced granularity after 100 days. |
| [Network Billing](./network-billing.md)<br>`network_billing` | Network | What you might need to bill advertisers, what you might be billed by publishers or Xandr. | Lifetime - some data at reduced granularity after 100 days. |
| [Buying Billing Report](./buying-billing-report.md)<br>`buyer_invoice_report` | Network | Reporting for financial reconciliation with buying related charges. | 1095 days |
| [Selling Billing Report](./selling-billing-report.md)<br>`seller_invoice_report` | Network | Reporting for financial reconciliation with selling related charges. | 1095 days |
| [Network Advertiser Analytics](./network-advertiser-analytics.md)<br>`network_advertiser_analytics` | Network | Network reporting on advertisers. | Lifetime - some data at reduced granularity after 100 days. |
| [Network Publisher Analytics](./network-publisher-analytics.md)<br>`network_publisher_analytics` | Network | Network reporting on publishers. | Lifetime - some data at reduced granularity after 100 days. |
| [Publisher Analytics](./publisher-analytics.md)<br>`publisher_analytics` | Network, Publisher | Reporting for what a publisher should see. | Lifetime - some data at reduced granularity after 100 days. |
| [Advertiser Analytics](./advertiser-analytics.md)<br>`advertiser_analytics` | Network, Advertiser | Reporting for what an advertiser should see. | Lifetime - some data at reduced granularity after 100 days. |
| [Network Video Analytics](./network-video-analytics.md)<br>`video_analytics_network` | Network | Video event reporting across advertisers and publishers. | 420 days |
| [Network Advertiser Video Analytics](./network-advertiser-video-analytics.md)<br>`video_analytics_network_advertiser` | Network | Video event reporting for a single advertiser. | 420 days |
| [Network Publisher Video Analytics](./network-publisher-video-analytics.md)<br>`video_analytics_network_publisher` | Network | Video event reporting for a single publisher. | 420 days |
| [Buyer Segment Performance Report](./buyer-segment-performance-report.md)<br>`buyer_segment_performance` | Network | Reporting on segment performance across campaigns and multiple advertisers. | 45 days |
| [Seller Brand Review Report](./seller-brand-review-report.md)<br>`seller_brand_review` | Network | Reporting on brand performance across all of network's inventory. | 428 days |
| [Publisher Brand Review Report](./publisher-brand-review-report.md)<br>`publisher_brand_review` | Publisher | Reporting on brand performance across all of publisher's inventory. | 428 days |
| [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md)<br>`network_advertiser_frequency_recency` | Network | Network reporting on creative frequency and recency for a single advertiser. | 120 days |
| [Advertiser Creative Frequency & Recency](./advertiser-creative-frequency-and-recency.md)<br>`advertiser_frequency_recency` | Network, Advertiser | Reporting for what an advertiser should see about its creative frequency and recency. | 120 days |
| [Network Site Domain Performance](./network-site-domain-performance.md)<br>`network_site_domain_performance` | Network | Network reporting on domain performance across advertisers. | 45 days |
| [Site Domain Performance Report](./site-domain-performance-report.md)<br>`site_domain_performance` | Network, Advertiser | Reporting on domain performance for a single advertiser. | 45 days |
| [Seller Site Domain](./seller-site-domain-report.md)<br>`seller_site_domain` | Network | Reporting on what inventory is coming through a publisher. | 60 days |
| [Segment Loads Report](./segment-loads-report.md)<br>`segment_load` | Network | Network reporting on segments. | 30 days |
| [Advertiser Attributed Conversions](./advertiser-attributed-conversions.md)<br>`attributed_conversions` | Network | Network reporting on advertisers' attributed conversions. | 90 days |
| [Geo Analytics Report](./geo-analytics-report.md)<br>`geo_analytics` | Network | Break down campaign delivery and performance by geographic area. | 45 days |
| [Network Carrier Analytics](./network-carrier-analytics.md)<br>`network_carrier_analytics` | Network | Report on buy-side and sell-side performance data based on mobile device carriers. | 46 days |
| [Network Device Analytics](./network-device-analytics.md)<br>`network_device_analytics` | Network | Report on buy-side and sell-side performance data based on devices where impressions were served. | 428 days |
| [Conversion Pixel Last Fire](./conversion-pixel-last-fire.md)<br>`pixel_fired` | Network | Network reporting on the last fire date and time of advertisers' conversion pixels. | Lifetime |
| [Completed Creative Audits Report](./completed-creative-audits-report.md)<br>`completed_creative_audits` | Network | Network report designed to give you insight into how your creatives are moving through the audit process | 365 days |
| [Bulk Reporting Feeds](./bulk-reporting-feeds.md)<br>`network_analytics_feed`<br>`clicktrackers` | Network | The ability to sync our aggregated reports to your reporting database. | 30 days |
| [Data Usage Report](./data-usage-report.md)<br>`buyer_data_usage_analytics` | Network | Network report that gives details on your usage of data provided by third parties (e.g., user segment providers), the costs of that data usage and line items/campaigns in which that data was used to target users. | 60 days |
| [Vendor Usage Report](./vendor-usage-report.md)<br>`buyer_vendor_usage_analytics` | Network | Network report that provides the details on your usage of data or platform powered by third party vendors (e.g., user segment providers), the costs of that data or feature usage , and the line items/campaigns where vendor costs were applicable. | 60 days |
| [Buyer Engagement Report](./buyer-engagement-report.md) <br>`buyer_engagement_report` | Advertiser | Provides insight into the viewable duration of your display and video creatives. | Last five weeks |
| [Buyer Deal Metrics](./buyer-deal-metrics.md)<br>`buyer_deal_metrics` | Advertiser, Network | Key information about deal metrics, performance, and rejection reasons that is relevant to buyers. | 30 days |
| [Seller Deal Metrics](./seller-deal-metrics-report.md)<br>`seller_deal_metrics` | Publisher, Network | Key information about deal metrics, performance, and rejection reasons that is relevant to sellers. | 30 days |
| [Multi-Buyer Seller Deal Metrics](./multi-buyer-seller-deal-metrics.md)<br> `multi_buyer_seller_deal_metrics`  | Publisher, Network | Key information about deal metrics, performance, and rejection reasons that is relevant to seller. | 30 days |
| [Key Value Analytics](./key-value-analytics-report.md)<br>`key_value_analytics` | Network | Network reporting on information associated with your network's defined targeting keys and values. Impressions with key/value targeting will serve and be reported only for those impressions that were logged by a placement tag containing the kw_ prefix on the key name. | 428 days |
| [Curator Analytics Report](./curator-analytics-report.md)<br>`curator_analytics` | Curator | Provides curators insight into how money is flowing from demand to supply within their curated marketplace. | 14 months |
| [Curator Segment Performance Report](./curator-segment-performance-report.md)<br>`curator_segment_performance` | Curator | Provides curators insights into how their targeted segments are contributing to the overall performance of their curated deals. | 14 months |
| [Buyer Reach And Frequency Report](./buyer-reach-and-frequency-report.md)<br>`buyer_approximate_unique_users_hourly` | Network | Provides the information associated with "reach" which is the number of unique devices or persons exposed to ads and "frequency" which is the average number of times each unique device or person was exposed to advertisements. | 90 days |
| [Offline Attribution Report](./offline-attribution-report.md)<br>`offline_attribution` | Advertiser | Provides insight into your line item's performance in influencing in-store purchases among your target audiences. The Offline Attribution report is only accessible to clients who have Offline Sales Attribution enabled for their line items. | 120 days |
| [Seller CMP Analytics Report](./seller-cmp-analytics-report.md)<br>`cmp_analytics` | Network | Provides insight into the number, validity, and content of the IAB Transparency & Consent Framework (IAB TCF) strings on seller ad requests to our endpoints. | 30 days |
| [Prebid Server Premium Health Analytics Report](./prebid-server-premium-health-analytics.md)<br>`psp_health_analytics` | Network | Data related to [Prebid Server Premium](../monetize/prebid-server-premium.md) bid requests and transactions. Useful for troubleshooting and optimization. Report is based on **sample data multiplied to estimate the full volume of PSP activity**. The [Monetize historical report](../monetize/monetize-historical-reporting.md) or other [Monetize reports](../monetize/reporting-guide.md) should be used for those purposes. | 99 days |
| [Inventory Availability Report](./inventory-availability-report.md)<br>`platform_inventory_availability` | Advertiser, Publisher | Inventory availability reports offer insight into the types of inventory available on the platform. | 30 days |

## REST API for viewing metadata

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/report?meta](https://api.appnexus.com/report?meta) | Return meta data for all reports. |
| `GET` | [https://api.appnexus.com/report?meta=REPORT_TYPE](https://api.appnexus.com/report?meta=REPORT_TYPE) | Return meta data for a particular report type. |

## JSON fields for viewing metadata

The meta array includes the following fields:

| Field | Description |
|:---|:---|
| `time_granularity` | The granularity of time for which the report can provide data. <br>Possible values: <br>- `"hourly"` <br>- `"daily"` <br>- `"monthly"` <br>- `"yearly"` <br>- `"lifetime"`<br><br>If `"hourly"` or `"lifetime"`, data is available for year, month, day, and hour. <br>If `"daily"`, `"monthly"`, or `"yearly"`, data is available for only year, month, and day. |
| `columns` | The columns that can be requested. For each column, the name and type are listed in the JSON response. |
| `filters` | The columns that can be used as filters. For each column, the name and type are listed in the JSON response. |
| `time_intervals` | The time ranges for which the report can be run. |

> [!NOTE]
> Some report types will allow you to run a report for a custom time frame. This can be done by setting the `start_date` and `end_date` fields in your report request.

### Meta data response example (using the `network_analytics` report)

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?meta=network_analytics'

{
    "response": {
        "status": "OK",
        "meta": {
            "time_granularity": "hourly",
            "columns": [
                {
                    "column": "month",
                    "type": "date"
                },
                {
                    "column": "day",
                    "type": "date"
                },
                {
                    "column": "hour",
                    "type": "date"
                },
                {
                    "column": "buyer_member_id",
                    "type": "int"
                },
                {
                    "column": "seller_member_id",
                    "type": "int"
                },
                {
                    "column": "seller_member_name",
                    "type": "string"
                },
                {
                    "column": "seller_member",
                    "type": "string"
                },
                {
                    "column": "advertiser_id",
                    "type": "int"
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
                    "column": "month",
                    "type": "date"
                },
                {
                    "column": "buyer_member_id",
                    "type": "int"
                },
                {
                    "column": "seller_member_id",
                    "type": "int"
                },
                ...
            ],
            "havings": [
                {
                    "column": "imps"
                },
                {
                    "column": "clicks"
                },
                {
                    "column": "cost"
                },
                {
                    "column": "revenue"
                },
                {
                    "column": "booked_revenue"
                },
                {
                    "column": "reseller_revenue"
                },
                {
                    "column": "profit"
                },
                ...
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
}
```

## REST API for data retrieval

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/report](https://api.appnexus.com/report)<br>(report JSON) | Request a report. |
| `GET` | [https://api.appnexus.com/report?id=REPORT_ID](https://api.appnexus.com/report?id=REPORT_ID) | Request the status of a report. |
| `GET` | [https://api.appnexus.com/report-download?id=REPORT_ID](https://api.appnexus.com/report-download?id=REPORT_ID) | Retrieve report data. |

> [!NOTE]
> Network users can run advertiser and publisher-level reports by appending `advertiser_id=ADVERTISER_ID` or `publisher_id=PUBLISHER_ID` to the query string.

## JSON fields for data retrieval

| Field | Required on `POST` | Type | Description |
|:---|:---|:---|:---|
| `report_type` | yes | enum | This determines which information will be returned.<br>Possible values:<br>- `"network_analytics"`<br>- `"network_billing"`<br>- `"buyer_invoice_report"`<br>- `"seller_invoice_report"`<br>- `"network_advertiser_analytics"`<br>- `"network_publisher_analytics"`<br>- `"network_site_domain_performance"`<br>- `"advertiser_analytics"`<br>- `"video_analytics_network"`<br>- `"video_analytics_network_advertiser"`<br>- `"video_analytics_network_publisher"`<br>- `"buyer_segment_performance"`<br>- `"seller_brand_review"`<br>- `"publisher_brand_review"`<br>- `"publisher_analytics"`<br>- `"network_creative_search"`<br>- `"publisher_creative_search"`<br>- `"network_advertiser_frequency_recency"`<br>- `"advertiser_frequency_recency"`<br>- `"site_domain_performance"`<br>- `"seller_site_domain"`<br>- `"inventory_domain_analytics"`<br>- `"inventory_source_analytics"`<br>- `"inventory_daily_uniques"`<br>- `"segment_load"`<br>- `"attributed_conversions"`<br>- `"pixel_fired"`<br>- `"network_analytics_feed"`<br>- `"clicktrackers"`<br>- `"key_value_analytics"`<br>- `"prebid_server_analytics"`<br>- `"psp_health_analytics"` |
| `timezone` | No | string (50) | This determines which timezone the data will be reported in. For a list of possible timezone values, see [API Timezones](./api-timezones.md).<br><br>**Note:** For the `network_billing`, `network_analytics`, `network_advertiser_analytics`, `network_publisher_analytics`, `advertiser_analytics`, and `publisher_analytics` report types, data older than 100 days will be reported in UTC. Also, report types that do not offer hourly data, such as `network_site_domain_performance`, `site_domain_performance`, and `seller_site_domain` will be reported in UTC. |
| `filters` | No | array | The list of filter objects to apply to the report. See [step 1](#step-1-create-a-json-formatted-report-request) of [How to run a report](#how-to-run-a-report) section below. |
| `group_filters` | No | array of objects | Allows you to specify an operation to perform on one or more filters. For [example](#group_filters-example), if you're selecting total impressions grouped by campaign, you can use this field to filter out campaigns that don't have at least 10,000 impressions. |
| `columns` | yes | array of strings | The list of columns to include in the report. See [Create a JSON-formatted report request](#step-1-create-a-json-formatted-report-request) below. At least one column must be specified. |
| `row_per` OR `groups` | No | array | **Note:** **Deprecated.** By default, reporting results are automatically grouped by the dimensions in `columns`. Passing these fields has no effect.<br><br>For most reports, selected dimensions are grouped automatically. For example, if you include the columns `"advertiser_id"`, `"campaign_id"`, `"creative_id"`, and `"imps"`, each row of report data would show the impressions per advertiser, campaign, and creative combination. |
| `start_date` | No | string | The start date for the report.<br>- For report types that offer hourly data, this must be formatted as `"YYYY-MM-DD HH:MM:SS"`.<br><br>**Note:** `MM:SS` must be `00:00`, as data is not available for minutes and seconds.<br><br>- For report types that do not offer hourly data, this must be formatted as `"YYYY-MM-DD"`. |
| `end_date` | No | string | The end date for the report.<br><br>**Note:** The `end_date` is non-inclusive. For example, if you start a report at `"2017-07-01 00:00:00"` and end the report at `"2017-07-01 23:00:00"`, your report will not include data from the last hour of the day. The correct way to retrieve this data would be to end the report at `"2017-07-02 00:00:00"`.<br><br>- For report types that offer hourly data, this must be formatted as `"YYYY-MM-DD HH:MM:SS"`. However, `MM:SS` must be `00:00`, as data is not available for minutes and seconds. For example, `"2017-07-01 00:00:00"` to `"2017-07-02 00:00:00"` would retrieve an entire day's data.<br>- For reports aggregated across intervals longer than hourly (e.g., daily, weekly, etc.), the format must be `"YYYY-MM-DD"`. For example, `"2017-07-01"` to `"2017-07-02"` would retrieve an entire day's data. |
| `report_interval` | No | enum | The time range for the report. Not all reports accept all intervals. See each report's documentation and metadata for details. <br>Possible values:<br>- `current_hour`<br>- `last_hour`<br>- `today`<br>- `yesterday`<br>- `last_48_hours`<br>- `last_2_days`<br>- `last_7_days`<br>- `last_14_days`<br>- `month_to_yesterday`<br>- `month_to_date`<br>- `quarter_to_date`<br>- `last_month`<br>- `lifetime`<br>- `30_days` |
| `orders` | No | array of objects | The list of columns to sort by. See [How to run a report](#how-to-run-a-report) below. |
| `format` | No | enum | The format in which the report data will be returned. If this field is not specified, it will default to `"csv"`.<br>Possible values:<br>- `"csv"`: Comma-separated values<br>- `"excel"`: Tab-separated values<br>- `"html"` |
| `reporting_decimal_type` | No | enum | The decimal mark used in the report. <br>Possible values:<br>- `"comma"`<br>- `"decimal"` (period)<br>If this field is passed, it overrides any reporting decimal preferences set at the user and member levels. |
| `emails` | No | array | The list of email addresses to which the reporting data will be sent. The reporting data is sent as an attachment, and the body of the email contains the information below.<br>- Report type<br>- Member, Advertiser, or Publisher name and ID<br>- Run date<br>- Start date<br>- End date<br>- Timezone<br>- User who generated the report.<br><br>**Note:** Report results larger than 15 MB will not be emailed. For ways to prevent results from being too large, see [Reporting Best Practices](./report-service.md#reporting-best-practices). |
| `escape_fields` | no | boolean | When `true`, it adds quotes around each field in the report output to allow for safer import into Excel. This only applies to CSV and tab-delimited reports. |

### `group_filters` example

```
{
"group_filters": [
{
"imps": {
"value": 10000,
"operator": ">="
}
}
]
}
```

## How to run a report?

- [Step 1. Create a JSON-formatted report request](#step-1-create-a-json-formatted-report-request)
- [Step 2. `POST` the request to the Report Service](#step-2-post-the-request-to-the-report-service)
- [Step 3. `GET` the report status from the Report Service](#step-3-get-the-report-status-from-the-report-service)
- [Step 4. `GET` the report data from the Report Download Service](#step-4-get-the-report-data-from-the-report-download-service)

### Step 1: Create a JSON-formatted report request

The JSON file should include the specific `report_type` that you want to run, as well as the `columns` (dimensions and metrics) and `report_interval` (`"today"`, `"yesterday"`, `"month_to_date"`, etc.) that you want to retrieve. You can also include `filters` for dimensions, define granularity (`year`, `month`, `day`), and specify the `format` in which the data should be returned. The `format` options are:

- `"csv"` - Comma-separated file
- `"excel"` - Tab-separated file
- `"xlsx"` - Modern XML-compatible Excel format (zipped)

> [!NOTE]
> To filter a dimension by more than one value, use an array. For example:
>
> **Correct:**
>
> `"filters": [{"bid_type": ["learn","optimized"]},`
> `{"geo_country":"US"}]`
>
> **Incorrect:**
>
> `"filters": [{"bid_type":"learn"},`
> `{"bid_type":"optimized"},`` {"geo_country":"US"}]`

For more details about the fields that can be included in the request, see [JSON fields](#json-fields-for-data-retrieval) above. For a full list of available dimensions and metrics, see the documentation for the specific report type that you want to run, or pull that report's metadata as described in [REST API for Viewing Metadata](#rest-api-for-viewing-metadata).

```
$ cat report_request

{
    "report": {
        "report_type": "network_analytics",
        "report_interval": "last_48_hours",
        "columns": ["day","imps","clicks"],
        "filters": [{"geo_country":"US"}],
        "orders": [{"order_by":"day", "direction":"ASC"},{"order_by":"imps", "direction":"DESC"}],
        "format": "csv"
    }
}
```

### Step 2: `POST` the request to the Report service

You `POST` the JSON request and get back a report ID.

```
$ curl -b cookies -c cookies -X POST -d @report_request 'https://api.appnexus.com/report'

{
    "response": {
        "status": "OK",
        "report_id": "ca9955709eade9a0e89f5cda5345c12r"
    }
}
```

Alternatively, you can get a Report ID via a `POST` request using a saved report ID. For more information, see the [Saved Report Service](saved-report-service.md):

```
curl -c cookies -b cookies -X POST 'https://api.appnexus.com/report?saved_report_id=30'
```

### Step 3: `GET` the report status from the Report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the `report-download` service to save the reporting data to a file. (This is described in the next step.)

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=ca9955709eade9a0e89f5cda5345c12r'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2017-03-13 18:15:48",
            "cache_hit": false,
            "fact_cache_hit": false,
            "json_request": "{\"report\":{\"report_type\":\"network_analytics\",\"report_interval\":
                \"last_48_hours\",\"columns\":[\"day\",\"imps\",\"clicks\"],\"filters\":[{\"geo_country\":
                \"US\"},{\"entity_member_id\":\"514\"},{\"entity_member_id\":null}],\"orders\":
                [{\"order_by\":\"day\",\"direction\":\"ASC\"},{\"order_by\":\"imps\",\"direction\":
                \"DESC\"}]}}",
            "header_info": "Report type:,network_analytics\r\n,\r\nRun at:,2017-03-13 18:15:48\r\nStart date:,
                \r\nEnd date:,\r\nTimezone:,\r\nUser:,John Smith (9385)\r\n",
            "report_size": "10",
            "row_count": "35",
            "url": "report-download?id=ca9955709eade9a0e89f5cda5345c12r"
        },
        "execution_status": "ready"
    }
}
```

### Step 4: `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the url field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your request to expose the response header.
>
> ```
> curl -i -b cookies -c cookies 'https://api.appnexus.com/report-download?id=ca9955709eade9a0e89f5cda5345c12r' > /tmp/network_analytics.csv
> ```

You can then open the csv file using Microsoft Excel or similar software.

## Report data size limitations

Report results larger than 15 MB will not be emailed to recipients specified in the JSON request.

Reports that take longer than 15 minutes to process will timeout and return with an error status. This amount of processing time roughly corresponds to 1MM rows of data. If your reports routinely timeout, consider one of the following options:

- Verify that you really need all that data. If you don't, update your report requests with a shorter time interval or fewer dimensions. For tips on preventing reports from being unnecessarily large or taking too long to process, see [Reporting Best Practices](#reporting-best-practices) below.
- If you really do need all of that data, follow the instructions in [Report Pagination](report-pagination.md).

## Report throttling

In order to ensure that our systems operate as smoothly as possible for all users, the [Report Service](report-service.md) throttles report requests at both the member level and the user level. This page describes how the limits are determined, and how we handle requests that exceed the limits defined for each member and each user.

## User limits

When a report is submitted by User A, a check is performed to see if User A has submitted 5 report requests in the past 15 minutes that are in pending status or currently being processed. If so, an error is signaled.

## Member limits

A given member is limited to *n* report requests being processed at the same time, where *n* is determined by the member's contract (This is specified internally by the `max_concurrent_reports_processing` field on the api.member table.) Any report requests submitted after the limit has been reached are placed in a queue. No warnings or alerts are given.

## Example

User- and member-level throttling interact with each other as shown in the following example. Assume that User A and User B are associated with the same member; this member has a limit of 5 concurrent report requests. We assume for this example that the following report requests are all submitted within a 15 minute time span:

| Report Request | User | Outcome |
|:---|:---|:---|
| 1 | User A | Processing |
| 2 | User A | Processing |
| 3 | User B | Processing |
| 4 | User B | Processing |
| 5 | User B | Processing |
| 6 | User A | Enqueued |
| 7 | User A | Enqueued |
| 8 | User A | Enqueued |
| 9 | User A | Error |

Report request \# 6 is placed in the queue, since there are already 5 report requests being processed for this member. For the same reason, requests \# 6-8 are also placed in the queue. Finally, we can see that request \# 9 causes an error to be signaled, since User A has submitted their 6th report request within a 15 minute time span.

## Conversion data

Conversions (and related data) in reports are processed asynchronously. As a result, reports are available more quickly, while some conversion-related data is still being processed in the background. For more information, see "Asynchronous Conversion Attribution" on the [Availability of Reporting Data](../invest/availability-of-reporting-data.md) page.

## Reporting best practices

Here are some tips for preventing your reports from being unnecessarily large or taking a long time to process:

- Shorten the `report_interval` (e.g., from `"lifetime"` to `"last_48_hours"`).
- Add more higher-level filters (e.g., for a specific publisher, advertiser, campaign, etc.).
- Avoid combining granular buy-side and sell-side dimensions (e.g., creative and placement), as this increases the number of rows exponentially. If you need to report on such combinations, consider using [Bulk Reporting Feeds](bulk-reporting-feeds.md) or the [Log-Level Data (LLD) Feeds](../log-level-data/log-level-data-feeds.md).

If you must pull large reports that take a long time to process, follow the instructions in [Report Pagination](report-pagination.md).

To determine when a report was last updated, use the [Report Status Service](report-status-service.md).
