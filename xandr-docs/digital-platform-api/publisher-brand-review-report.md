---
title: Publisher Brand Review Report
description: Explore the publisher brand review report to view brand performance across a specific publisher's inventory.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Publisher brand review report

This report provides a view of brand performance across a specific publisher's inventory. This report is available to both network and publisher users. You can:

- Review what creative has served on your inventory under a specific publisher and how it performed.
- Review creative performance by audit status.

This report requires that a publisher ID be specified as part of the URL as follows:

```
https://api.appnexus.com/report?publisher_id=PUBLISHER_ID
```

The `time_granularity` of the data is `daily`. For instructions on retrieving a report, see the [Report Service](report-service.md) or the [example](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- yesterday
- last_7_days
- last_30_days
- month_to_date
- last_month

### Data retention period

Data retention period for this report is 428 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | time | no | `"2010-02"` | The month of the auction. |
| `day` | time | no | `"2010-02-01"` | The day of the auction. |
| `placement_id` | int | yes | `546` | The ID of the placement. |
| `placement_name` | string | no | `"300x250 Business"` | The name of the placement. |
| `placement` | string | no | `"300x250 Business (546)"` | **Deprecated** (as of October 17, 2016). |
| `geo_country` | string | yes | `"US"` |  |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country/region. |
| `imp_type` | string | yes | `"Kept"` | The type of impressions. For possible values see `imp_type_id`. |
| `imp_type_id` | int | yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br>- `1` ("Blank"): No creative served.<br>- `2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>- `3` ("Default Error"): A default creative served due to a timeout issue.<br>- `4` ("Default"): A default creative served because there were no valid bids.<br>- `5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>- `6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>- `7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>- `8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>- `9` ("External Impression"): An impression from an impression tracker.<br>- `10` ("External Click"): A click from a click tracker. |
| `creative_id` | int | yes | `654` | The ID of the creative. |
| `site_id` | int | yes | `555` | The ID of the site. For more information, see the [Site Service](site-service.md). |
| `site_name` | string | no | `"My Site"` | The name of the site. For more information, see the [Site Service](site-service.md). |
| `brand_id` | int | yes | `3` | The ID of the brand associated with a creative served on the publisher's inventory. |
| `brand_name` | string | no | `"Ace Hardware"` | The name of the brand associated with a creative served on the publisher's inventory. |
| `brand` | string | no | `"Ace Hardware (3)"` | **Deprecated** (as of October 17, 2016). |
| `width` | int | yes | `250` | The width of the creative. |
| `height` | int | yes | `300` | The height of the creative. |
| `site` | string | no | `"My Site (555)"` | **Deprecated** (as of October 17, 2016). |
| `site_code` | string | no | `"Site Name Code"` | The custom code for the site. |
| `placement_code` | string | no | `"Photos Code"` | The custom code for the placement. |
| `media_type` | string | yes | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"` | The general display style of a creative served on the publisher's inventory. You can use the [Media Type Service](media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | yes | `444` | The ID of the media type associated with the creative that was served. For more information, see the [Media Type Service](media-type-service.md). |
| `deal_id` | int | yes | `2345` | The ID of the deal. For more information about deals you have negotiated with buyers, see [Deal Service](deal-service.md). |
| `deal_name` | string | no | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | no | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated** (as of October 17, 2016). |
| `deal_code` | string | no | `"Custom code"` | The custom code for the deal. |
| `brand_offer_category_id` | int | yes | `1256` | The ID of the brand offer category associated with the impression. See `category_id` in the [Brand Service](brand-service.md) page. |
| `brand_offer_category_name` | string | no | `"Luxury Cars"` | The name of the brand offer category associated with the impression. See `category_id` in the [Brand Service](brand-service.md) page. |
| `creative_audit_status_id` | int | yes | `0` | The ID of the audit status of the creative associated with the impression:<br>- `0` = unaudited<br>- `1` = seller audited only<br>- `2` = appnexus audited |
| `creative_audit_status` | string | no | `"Unaudited"` | The audit status of the creative associated with the impression:<br>- `"Unaudited"`<br>- `"Self Audit Only"`<br>- `"AppNexus Audited"` |
| `size` | string | yes | `"728x90"` | The width and height of the creative associated with the impression. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `34534` | imps | The total number of impressions (including defaults). |
| `clicks` | int | `345` | clicks | The total number of clicks across all impressions. |
| `total_convs` | int | `205` | total_convs | The total number of post view and post click conversions. |
| `convs_rate` | double | `0.000856` | total_convs / imps | The rate of conversions to impressions. |
| `ctr` | double | `0.002327` | clicks / imps | The rate of clicks to impressions. |
| `publisher_revenue` | money | `400.05` | publisher_revenue | The revenue paid out to the publisher (based on revshare or CPM). |
| `publisher_rpm` | money | `1.71` | (publisher_revenue / imps) x 1000 | The publisher revenue per 1000 impressions. |
| `convs_per_mm` | double | `221.877080097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |

## Examples

### Create the JSON report request

The JSON file should include the `report_type` of `"publisher_brand_review"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat publisher_brand_review

{"report": 
    {
        "format": "csv",
        "report_interval": "yesterday",
        "row_per": ["placement_id"],
        "columns": ["placement_id","imp_type","creative_id","brand_id"],
        "report_type": "publisher_brand_review"
    }
}
```

### `POST` the request to the [Report service](report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @publisher_brand_review "https://api.appnexus.com/report?publisher_id=384186"

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
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"placement_id\"],\"columns\":[\"placement_id\",\"imp_type\",\"creative_id\",\"brand_id\"],\"report_type\":\"publisher_brand_review\",\"filters\":[{\"seller_member_id\":\"958\"},{\"publisher_id\":\"384186\"}]}}",
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
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=97a181df6d77a8f3cd5a45eff4ea3dab' > /tmp/publisher_brand_review.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
