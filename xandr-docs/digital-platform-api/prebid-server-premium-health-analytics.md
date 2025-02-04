---
title: Prebid Server Premium Health Analytics
description: Explore the Prebid Server Premium (PSP) Health Analytics report, enabling users to analyze bid requests and transactions with their configured Demand Partners.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Prebid Server Premium Health Analytics

The Prebid Server Premium (PSP) Health Analytics Report allows users to analyze data related to bid requests and transactions with their configured Demand Partners. This is most useful in troubleshooting known issues and proactively identifying optimization opportunities.

> [!NOTE]
> The dashboard is based on **sample data multiplied to estimate the full volume of PSP activity**. It is not intended to be used for delivery and revenue reporting. The [Prebid Server Premium Seller Analytics Report](../monetize/prebid-server-premium-seller-analytics.md) and other [Microsoft Monetize reports](../monetize/reporting-guide.md) should be used for those purposes.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_hour
- last_24_hours
- last_48_hours
- today
- yesterday
- last_2_days
- last_7_days
- last_14_days
- last_30_days
- month_to_date
- last_month
- month_to_yesterday
- quarter_to_date
- lifetime

The `time_granularity` of the data is hourly. For instructions on retrieving a report, see the [Report Service](report-service.md) or the [examples](#examples) below.

### Data retention period

Data retention period for this report is 99 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `ad_size` | string | yes | `300x250` | The dimensions of the ad slot. |
| `allowed_media_types_bitmap_name` | string | no | `"Banner"` | The category of creative enabled by the publisher on the Monetize placement. For example: banner, video, native. |
| `application_id` | string | yes | `"vizio.pluto"` | The specific application used on the device. |
| `bid_error_type` | int | yes | `21` | The ID of the category of error related to the bid response. For more detail, see the [Bid request error types](#bid-request-error-types) table below. |
| `bid_error_type_name` | string | no | `"NO_BID_PRICE"` | The category of error related to the bid response. For more detail, see the [Bid request error types](#bid-request-error-types) table below. |
| `bid_reject_error_code` | string | yes | `"31"` | The specific error generated from the demand partner's bid response. See [bid error codes](../bidders/bid-error-codes.md) for descriptions and potential resolution for each value.|
| `bidder_id` | int | yes | `443` | The ID of the bidder (443). |
| `bidder_name` | string | no | `Prebid Server` | The name of the bidder (Prebid Server). |
| `browser_code_id` | int | yes | `5414` | The ID of the specific version of the browser. |
| `browser_code_name` | string | no | `"da-chrome-107.0"` | The name of the specific version of the browser. |
| `call_type` | string | yes | `/ut/v3/prebid` |The [type of handler](../monetize/prebid-server-premium-supported-formats-and-integration-paths.md) used to send the bid request to Monetize "(e.g., `/ut/v3/prebid`, `openrtb2/prebid`)".|
| `cookies_present` | boolean | yes | yes |Indicates whether or not a cookie was present in the bid request.|
| `datacenter_id` | string | yes | `"ams3"` | The ID of the data center used to route the request to demand partners. |
| `day` | date | yes | `"2018-02-01"` | The day of the auction. |
| `demand_partner` | string | no | `"PubMatic (PSP) (9645)"` | A string consisting of the demand partner name and ID. |
| `demand_partner_id` | int | yes | `9645` | The ID of the partner to which the request was sent and from which the response (if any) was received. |
| `demand_partner_name` | string | no | `"PubMatic (PSP)"` | The name of the partner to which the request was sent and from which the response (if any) was received. |
| `device_browser_id` | int | yes | `8` | The ID of the browser used on the device. For example, Chrome, Safari, etc. |
| `device_browser_name` | string | no | `"Chrome (all versions)"` | The name of the browser used on the device. For example, Chrome, Safari, etc. |
| `device_os_extended_id` | int | yes | `137` | The ID of the specific version of the operating system. For example, iOS 16.0.0. |
| `device_os_extended_name` | string | no | `"Windows 10"` | The name of the specific version of the operating system. For example, iOS 16.0.0. |
| `device_os_family` | string | no | `"Android (2)"` | A string consisting of the device OS family name and ID. |
| `device_os_family_id` | int | yes | `2` | The ID of the operating system of the device. For example, Microsoft Windows, Apple iOS, etc. |
| `device_os_family_name` | string | no | `"Android"` | The name of the operating system of the device. For example, Microsoft Windows, Apple iOS, etc. |
| `device_type_id` | int | yes | `1` | The category of device: <br>- `0` = Unknown<br>- `1` = desktops & laptops<br>- `2` = mobile phones<br>- `3` = Tablet<br>- `4` = tv<br>- `5` = game consoles<br>- `6` = media players<br>- `7` = set top box |
| `device_type_name` | string | yes | `"mobile phones"` | The name of the category of device (desktops & laptops, mobile phones, etc.). |
| `external_creative_id` | string | yes | `987654` | The external ID associated with the creative served. |
| `geo_country` | string | yes | `"US"` | The code of the country/region in which the impression served. For example, US. |
| `geo_country_name` | string | No | `"United States"` | The name of the country/region in which the impression served. For example, United States. |
| `hour` | date | no | `"2018-02-01-09:54"` | The hour of the auction. |
| `inventory_url` | string | no | `"myurl.com/(1234)"` | The mapped URL from the detected domain on the ad call and the ID in parentheses. |
| `inventory_url_id` | string | yes | `1234` | The mapped URL ID from the detected domain on the ad call. |
| `inventory_url_name` | string | yes | `1234` | The mapped URL from the detected domain on the ad call. |
| `media_type` | string | no | `"Banner"` | The category of creative on transacted impressions. For example: `banner`, `video`, `native`. Unknown media type refers to bid requests that did not result in impressions. The media type is logged only when a creative is served. |
| `media_type_id` | int | yes | `1` | The ID of the category of creative on transacted impressions. |
| `month` | date | no | `"2018-02"` | The month of the auction. |
| `placement_id` | int | yes | `456` | The ID of the placement through which the request originated. |
| `placement_name` | string | no | `"My Placement"` | The name of the placement through which the request originated. |
| `psp_config_id` | int | yes | `10000` |  Unique identifier for the PSP configuration via the [config service](../digital-platform-api/config-service.md). Currently only reportable on `bid_responses_received`, `valid_bid_on_imps`, and `imps_delivered`. Will be updated to cover other metrics in the future. |
| `publisher_id` | int | yes | `789` | The ID of the publisher on whose inventory the request originated. |
| `publisher_name` | string | no | `"Neat Publisher Ltd"` | The name of the publisher on whose inventory the request originated. |
| `sdk_version` | string | yes | `"pbjs-5.20.3"` | The version of the software development kit present in the app. |
| `seller_member_id` | int | yes | `123` | The ID of the seller member. |
| `seller_member_name` | string | no | `"Cool Seller Inc"` | The name of the seller member. |
| `site_id` | int | yes | `555` | The ID of the site on which the the request originated. |
| `site_name` | string | no | `"My Site"` | The name of the site on which the request originated. |
| `supply_type` | string | yes | `"web"` | The category of inventory (web, mobile web, or app). App includes CTV and mobile. |
| `uap_response_error_type_id` | string | yes | `TIMEOUT` | The specific error generated from the bid request. See Bid request [Bid request error types](#bid-request-error-types) table below for a description and potential resolution for each value.|

## Metrics

| Column | Type | Formula | Example | Description |
|:---|:---|:---|:---|:---|
| `average_clear_price` | double | See Description. | `1.00` | The sum of bid price for delivered impressions divided by the number of bid requests sent. |
| `average_response_time` | double | bid_responses_received / bid_requests_sent. | `0.08` | The number of bid responses received from demand partners divided by the number of bid requests sent. |
| `bid_errors` | int | See Description. | `149908040` | The number of errors in bid responses from Demand Partners. |
| `bid_errors_rate` | double | bid_errors / bid_requests_sent | `0.04` | The number of bid errors divided by the number of bid requests sent to Demand Partners. |
| `bid_request_error_rate` | double | bid_request_errors / bid_requests_sent | `0.05`| The number of bid request errors divided by the number of bid requests sent to Demand Partners.|
| `bid_request_errors` | int | See Description. | `200` |The number of specific errors generated from bid requests. See [Bid request error types](#bid-request-error-types) table below for a description and potential resolution for each value. |
| `bid_requests_sent` | int | See Description. | `3990674680` | The number of requests sent from Prebid Server Premium to Demand Partners. |
| `bid_rejection_error_rate` | int | bid_rejection_errors / bid_responses_received | `0.06` | The number of bid rejection errors divided by the number of bid responses received from demand partners.|
| `bid_rejection_errors` | int | See Description. | `300` | The number of specific errors from the demand partner's bid response. See [bid error codes](../bidders/bid-error-codes.md) for a description and potential resolution for each value.|
| `bid_rate` | int |  bid_responses_received / bid_requests_sent | `0.08` | The number of bid responses received from demand partners divided by the number of bid requests sent.|
| `bid_responses_received` | int | See Description. | `381809500` | The number of specific errors from the demand partner's bid response. See [bid error codes](../bidders/bid-error-codes.md) for a description and potential resolution for each value. |
| `bids_submitted_to_ad_server` | int | See Description. | `54021580` | The number of ad requests that had a valid Prebid bid that was not subject to any additional Microsoft rejections returned to the ad server. This number is counted after the Microsoft auction process that evaluates bids received from all sources. The reduced volume between `valid_bid_on_imps` and this metric could be due to creative requirements not being met, being outbid by other bidders, or due to the option to [send only the top bid back to the ad server](../monetize/integrate-web-mobile-web-with-psp.md). |
| `bidder_user_matched_requests` | int | See Description. | `1849169240` | The number of requests where a user identifier was present.<br><br>**Note:** This metric currently only includes cookies for web and mobile web. |
| `imps_delivered` | int | See Description. | `4804540` | The number of impressions successfully delivered and ads rendered.<br><br>**Note:** This report is based on sample log data multiplied to estimate the full volume of PSP activity and does not represent final delivery. |
| `media_type` | string | See Description. | `banner`, `video`, and `native` | Unknown media type refers to bid requests that did not result in impressions. The media type is logged only when a creative is served. |
| `no_bid_rate` | double | no_bids / bid_requests_sent | `0.87` | The number of times Demand Partners did not bid divided by the number of bid requests sent to Demand Partners. |
| `no_bids` | int | See Description. | `3461831640` | The number of times Demand Partners did not bid on a request. This does not include bid errors. |
| `total_bid_price` | int | See Description. | `171869242` | The sum of the bid values received from Demand Partners. |
| `total_buyer_spend` | double | See Description. | `11234.88` | The media cost to buyers of impressions delivered.<br><br>**Note:** This report is based on sample log data multiplied to estimate the full volume of PSP activity and does not represent final delivery. |
| `user_matched_requests_rate` | double | bidder_user_matched_requests / bid_requests_sent | `0.46` | The number of user matched requests divided by the number of bid requests sent to Demand Partners. |
| `valid_bid_on_imps` | int | See Description. | `378935000` | The number of bids received from PSP Demand Partners that do not trigger errors, have a creative ID, and have a bid above $0. There may be multiple bids counted for each auction when multiple PSP Demand Partners return bids. |
| `valid_bids_on_imp_rate` | double | valid_bid_on_imps / bid_responses_received | `0.09` | The number of valid bids divided by the number of bid requests sent to Demand Partners. |
| `win_rate` | double | imps_delivered / bid_responses_received | `0.01` | This metric should only be used with the demand partner dimension applied. It represents the percentage of impressions delivered by a demand partner relative to the total bid responses received. The calculation involves dividing the number of impressions delivered by the demand partner by the total number of bid responses received.|

## Bid request error types

| Code | Error | Description | Remedy |
|:---|:---|:---|:---|
| 0 | `NONE` | No error. | None needed. |
| 1 | `INTERNAL` | There is a server-side error from the Demand Partner, such as a 400 status code. | The Seller should work with Microsoft to collect a specific example code to share with the Demand Partner for investigation. |
| 2 | `TIMEOUT` | The Demand Partner did not respond within the timeout limit. | Either increase timeout settings to allow for a longer response time or contact the Demand Partner to inform them of the restriction. For more information on timeouts, see [Add or Edit PSP Global Settings](../monetize/add-or-edit-psp-global-settings.md). |
| 3 | `CLIENT` | The Demand Partner's Prebid Server adapter generated an error. | For significant quantities of this error type, the Seller should contact Microsoft support to diagnose issues by looking at the internal Microsoft logs. An example of this error could be that video supply has been sent to an adapter that does not support it. |
| 4 | `PARSE` | The Demand Partner has formatted the bid response incorrectly. | The Seller should work with Microsoft and the Demand Partner to determine and resolve the specific formatting issue. |

> [!NOTE]
> For bid response error types, see [Bid Error Codes](../bidders/bid-error-codes.md).

## Examples

### Create JSON formatted report request

The JSON file should include the `report_type` of `"psp_health_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat psp_health_analytics
   {"report": 
    {
        "format": "csv",
        "report_interval": "yesterday",
        "columns": ["hour", "publisher_id","site_id","header_bidding_demand_partner", "imps", "seller_revenue", "view_rate"],
        "report_type": "psp_health_analytics"
    }
}
```

### `POST` the request to the [Report service](report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @psp_health_analytics "https://api.appnexus.com/report"
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
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"publisher_id\"],\"columns\":[\"hour\", \"publisher_id\",\"site_id\",\"header_bidding_demand_partner\",\"imps\",\"seller_revenue\", \"view_rate\"],\"report_type\":\"psp_health_analytics\"
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
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=97a181df6d77a8f3cd5a45eff4ea3dab' > /tmp/psp_health_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topics

- [Prebid Server Premium Seller Analytics Report (UI)](../monetize/prebid-server-premium-seller-analytics.md)
- [Prebid Server Premium Health Analytics Report (UI)](../monetize/prebid-server-premium-health-analytics-report.md)
- [Prebid Server Premium Seller Analytics (API)](prebid-server-premium-seller-analytics.md)
- [Reporting Guide](../monetize/reporting-guide.md)
- [Report Service API](report-service.md)
- [Bid Error Codes](../bidders/bid-error-codes.md)
