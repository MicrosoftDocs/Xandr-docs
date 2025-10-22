---
title: Digital Platform API - Nielsen Digital Ad Ratings - Site/Split Report
description: The Nielsen Digital Ad Ratings (DAR) Site/Split report provides insights on publisher domains and audiences for line item impressions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Nielsen Digital Ad Ratings - Site/Split report

The Nielsen Digital Ad Ratings (DAR) - Site/Split Report gives you insight into the publisher domains and audiences connected to your line item's impressions. If your line item's using splits, this report also gives you information on their performance. Audience demographic measuring must be enabled for your line item to utilize this report.

For instructions on retrieving a report, please see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- last_7_days
- last_14_days
- month_to_date
- last_30_days
- quarter_to_date
- last_100_days
- last_365_days
- year_to_date

### Data retention period

Data retention period for this report is 365 days. Data in this report has a daily time granularity and lifetime retention. This report also displays data under the U.S. Eastern time zone.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `insertion_order_id` | int | Yes | `553515` | ID of the insertion order. |
| `split_id` | int | Yes | `261181457` | ID of the line item split. |
| `advertiser_id` | int | Yes | `4919231` | ID of the advertiser. |
| `line_item` | int | Yes | `13731149` | ID of the line item. |
| `line_item.name` | string | Yes | `"My Line Item"` | Name of the line item. |
| `site_domain_unobfuscated` | string | Yes | `"thesaurus.com"` | The web domain where impressions were recorded. |
| `ymd` | date | Yes | `2021-05-02` | The year, month, and day of the last available day for data. |
| `member_id` | int | Yes | `958` | ID of the member. |
| `demographic_group` | string | Yes | `"male 25-29"` | A demographic group sorted by sex and age range. |
| `platform` | string | Yes | `"desktop"`, `"mobile"`, or `"connected device"` | Filter for the type of device used. |
| `nielsen_campaign_ref` | string | No | `"scm1521250"` | The Nielsen campaign reference ID. |
| `start_date` | date | No | `2021-04-26`  | The date on which Nielsen first started collecting data. |
| `country_name` | string | No | `"United States"` | Country/region where impressions were recorded.
| `country_code` | string | Yes | `91` | The code representing a country/region where impressions were recorded. |
| `split_name` | string | No | `"My Split"` | The name of a line item's split. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `population` | int | `11080000` | N/A | Based on census-provided data, the number of people in the country/region included in a given demographic. |
| `total_imps` | int | `89` | N/A | The total number of impressions your line item has made. |
| `on_target_imps` | int | `32` | On Target Impressions = Impressions Seen by Target Demographic ÷ Total Impression Count for your Line Item | The number of impressions served to your desired demographic group that are within your selected reporting dimensions. |
| `imps_share` | double | `0.5128205128205128` | Impressions Share (%) = Demographic Impressions ÷ Total Number of Impressions Across all Demographic Groups × 100 | Based on the line item's total impression count, the percentage that served to your targeted demographic. |
| `imps_index` | double | `21.851728591916128` | Impressions Index = Impression Share (%) ÷ Demographic-Specific Population × 100 | A targeting success score based on how the line item's impressions are divided across all demographics. |
| `on_target_pct` | double | `0.5128205128205128` | On Target Percent (%) = Impressions Seen by Target Demographic ÷ Total Impression Count for your Line Item × 100 | The percentage of impressions served to your selected demography. |
| `population_share` | double | `7.7502` | Population Share (%) = Demographic Population ÷ Population of all Demographics × 100 | Percentage of people within a demographic relative to the total population. |
| `unique_audience` | int | `132297` | N/A | The total of unique individuals in the audience that your line item has reached. |
| `audience_share` | double | `23.64` | Audience Share (%) = Row Level Audience Count ÷ Campaign Total Audience Count × 100 | The percentage share of the total audience a line item has reached within a certain demographic group. This measurement is rounded to two decimal places. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"video_indemo_site_split"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat site_split_report

{
    "report":
    {
        "report_type":"video_indemo_site_split",
        "columns":[
            "nielsen_campaign_ref",
            "line_item",
            "line_item.name",
            "start_date",
            "site_domain_unobfuscated",
            "split_name",
            "demographic_group",
            "total_imps",
            "on_target_imps"
        ],
        "report_interval":"last_7_days",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @site_split_report 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"video_indemo_site_split\",\"columns\":[\"nielsen_campaign_ref\",
            \"line_item\",\"line_item.name\",\"start_date\",\"site_domain_unobfuscated\",\"split_name\",\"demographic_group\",\"total_imps\",\"on_target_imps\"],
            \"report_interval\":\"last_7_days\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_indemo_audience_profile.csv
```
