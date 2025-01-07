---
title: Prebid Server Premium Seller Analytics
description: Explore the Prebid Server Premium Seller Analytics report to access performance information on configured Prebid Server Premium (PSP) demand partners.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Prebid Server Premium Seller Analytics

The Prebid Server Premium Seller Analytics Report contains performance information on configured Prebid Server Premium (PSP) demand partners. Using this report, you can:

- Track revenue by heading bidder demand partner, publisher, or geographical region.
- Track lift on inventory you've opened up to header bidding demand.
- Monitor the health and efficiency of your Prebid Server Premium partners and placements.

For information on other reports via API, see [Report Service](report-service.md). For information on accessing data via UI, see [Reporting Guide](../monetize/reporting-guide.md) for Microsoft Monetize and [Prebid Server Premium Seller Analytics Report](../monetize/prebid-server-premium-seller-analytics.md).

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_hour
- last_48_hours
- today
- yesterday
- last_7_days
- month_to_date
- quarter_to_date
- last_month
- lifetime
- month_to_yesterday

The `time_granularity` of the data is hourly. For instructions on retrieving a report, see the [Report Service](report-service.md) or the [Examples](#examples) below.

### Data retention period

Data retention period for this report is 30 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | date | no | `"2018-02-01-09:54"` | The hour of the auction. |
| `month` | date | no | `"2018-02"` | The month of the auction. |
| `day` | date | yes | `"2018-02-01"` | The day of the auction. |
| `seller_member_id` | int | yes | `123` | The ID of the seller member. |
| `seller_member_name` | string | no | `"Cool Seller Inc"` | The name of the seller member. |
| `tag_id` | int | yes | `456` | The ID of the placement tag. |
| `publisher_id` | int | yes | `789` | The ID of the publisher. |
| `publisher_name` | string | no | `"Neat Publisher Ltd"` | The name of the publisher. |
| `publisher` | string | no | `"Neat Publisher Ltd (789)"` | A string consisting of the publisher name and publisher ID. |
| `size` | string | yes | `300x250` | The width and height of the placement associated with the impression. |
| `geo_country` | string | yes | `"US"` | The country/region abbreviation. |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country/region. |
| `site_id` | int | yes | `555` | The ID of the site. For more information, see the [Site Service](site-service.md). |
| `site_name` | string | no | `"My Site"` | The name of the site. For more information, see the [Site Service](site-service.md). |
| `site` | string | no | `"My Site (555)"` | A string containing the name and ID of the site. For more information, see the [Site Service](site-service.md). |
| `tag_name` | string | no | `"My Placement"` | The name of the tag associated with the impression. |
| `header_bidding_demand_partner_id` | int | no | `9645` | The ID of the demand partner associated with the placement. |
| `header_bidding_demand_partner_name` | string | no | `"PubMatic (PSP)"` | The demand partner associated with the placement. |
| `header_bidding_demand_partner` | string | no | `"PubMatic (PSP) (9645)"` | The name and ID of the demand partner associated with the placement. |
| `included_header_bidding_demand` | int | yes | `654` | The included demand from non-Xandr demand partners. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `34534` | imps | The total number of impressions (including defaults). |
| `seller_revenue` | money | `999.99` | total seller revenue | The seller revenue on the deal, represented as a dollar amount. |
| `seller_ecpm` | money | `1.00` | See Description | The seller revenue on the deal, represented in eCPM. |
| `view_measured_imps` | int | `1500` | See Description | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `87.00` | imps_viewed / view_measured_imps | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. |
| `view_measurement_rate` | int | `91.00` | view_measured_imps / imps | The percentage of impressions measured for viewability out of the total number of impressions. |
| `imps_viewed` | int | `1100` | See Description | The number of viewable impressions for the placement. |
| `ad_requests` | int | `1200` | See Description | The number of ad requests associated with the placement. |
| `fill_rate` | double | `85.00` | Kept impressions + resold impressions / total number of impressions | The percentage of ad requests that were filled with demand. (Kept Impressions and Resold Impressions / total number of impressions). |

## Examples

### Create JSON formatted report request

The JSON file should include the `report_type` of `"prebid_server_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat prebid_server_analytics
  {"report": 
    {
        "format": "csv",
        "report_interval": "yesterday",
        "columns": ["hour", "publisher_id","site_id"," "header_bidding_demand_partner", "imps", "seller_revenue", "view_rate"],
        "report_type": "prebid_server_analytics"
    }
}
```

### `POST` the request to the [Report Service](report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @prebid_server_analytics "https://api.appnexus.com/report"
{
   "response":{
      "status":"OK",
      "report_id":"97a181df6d77a8f3cd5a45eff4ea3dab"
   }
}
```

### `GET` the report status from the Report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=97a181df6d77a8f3cd5a45eff4ea3dab'
{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2014-11-19 21:57:00",
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"publisher_id\"],\"columns\":[\"hour\", \"publisher_id\",\"site_id\",\"header_bidding_demand_partner\",\"imps\",\"seller_revenue\", \"view_rate\"],\"report_type\":\"prebid_server_analytics\"
            "url": "report-download?id=97a181df6d77a8f3cd5a45eff4ea3dab"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=97a181df6d77a8f3cd5a45eff4ea3dab' > /tmp/prebid_server_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topics

- [Report Service](report-service.md)
- [Prebid Server Premium Seller Analytics Report (UI)](../monetize/prebid-server-premium-seller-analytics.md)
