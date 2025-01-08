---
title: Digital Platform API - Seller Fill and Delivery Publisher Report
description: Sellers can use the Seller Fill and Delivery Publisher report to troubleshoot impressions and diagnose delivery issues.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Seller Fill and Delivery Publisher report

The Seller Fill and Delivery Report was designed as a troubleshooting tool to provide sellers granular information regarding all impressions sent to Xandr for auction and to help diagnose delivery issues all the way down to the tag and domain level. Using the new descriptive fields, it is possible to see an approximation of overall fill rate on Xandr using the “Total Ad Responses" and "Total Ad Requests” metrics.

The data contained in this report will help pinpoint issues contributing to untransacted impressions stemming from:

- Improper default/passback tag setup
- Inventory blocklisting related to IP or domain blocking
- Video player errors, etc.

> [!NOTE]
> **For video sellers only**
>
> As a result of video caching by video players, the Xandr data pipeline allows a six-hour window to register a response from a video player after the auction is complete and the creative VAST XML has been sent to the page, before considering a video impression ‘non-responsive’ (Bid Sent No Response). Xandr will update some counts, for video tags only, six hours after the time of the auction. Therefore, to receive the most accurate view of video counts across dimensions, schedule your reports to run **after** the six-hour window for a given hour of data.

:::image type="content" source="media/seller-fill-and-delivery-publisher-report-fig-a.png" alt-text="Diagram that shows the process involved in generating the total ad responses.":::

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- last_48_hours
- today
- yesterday
- last_7_days
- last_24_hours
- last_14_days
- last_2_days
- month_to_date
- quarter_to_date
- last_month
- last_available_day
- last_7_available_days
- last_14_available_days

The `time_granularity` of the data is `hourly`. For instructions on retrieving a report, see the [Report Service](./report-service.md) or the [Example](#example) below.

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 99 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | No | `"2010-02"` | The month of the auction. |
| `day` | date | No | `"2010-02-01"` | The day of the auction. |
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `seller_member_id` | int | Yes | `2718` | The seller's Xandr member ID. |
| `seller_member_name` | string | No | `"MegaSeller"` | The seller's name. |
| `seller_member` | string | No | `"MegaSeller (2718)"` | **Deprecated** (as of October 17, 2016). |
| `placement_id` | int | Yes | `737099` | The ID of the placement where the impression occurred. |
| `placement_name` | string | No | `"Webmail.com ROS 728x90"` | The name of the placement where the impression occurred. |
| `placement` | string | yes | `"300x250 Business (546)"` | **Deprecated** (as of October 17, 2016). |
| `publisher_id` | int | Yes | `44389` | The ID associated with the publisher on whose site the impression occurred. |
| `publisher_name` | string | No | `"LOL - US"` | The name of the publisher on whose site the impression occurred. |
| `publisher` | string | Yes | `"LOL - US (44389)"` | **Deprecated** (as of October 17, 2016). |
| `geo_country` | string | Yes | `"US"` | The code of the geographical country/region. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographical country/region. |
| `site_id` | int | Yes | `223936` | The ID of the site containing this placement. |
| `site_name` | string | No | `"Total-Web Email"` | The name of the [site](./site-service.md) where the impression occurred. |
| `site` | string | No | `"Total-Web Email (223936)"` | **Deprecated** (as of October 17, 2016). |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated** (as of October 17, 2016). |
| `mobile_application_id` | string | No | `'343200656' (iOS) or 'com.rovio.angrybirds' (Android)` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `site_domain` | string | No | `"gwar-rules-forever.org"` | The domain where the impression occurred. There is one additional value that may appear in place of a domain:<br>`"---"`: This means that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| `supply_type` | string | Yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `'web'`<br> - `'mobile_app'`<br> - `'mobile_web'` |
| `call_type` | string | Yes | `"/ttj"` | The type of handler that was used to send the impression to Xandr (e.g., `ttj`, `ut`, `mob`, `ptv`, `openrtb`) |
| `allowed_media_types` | string | No | `Banner`, `Expandable`, `Native` | The media types that are allowed to participate in the auction. The permitted media types is a combination that is enabled through the ad call and placement settings. |
| `openrtb2_request_subdomain` | string | No | `wrapper-emea` | The subdomain of the URL that the OpenRTB2 ad request was sent to.<br>**Note**: This value is blank for non-OpenRTB2 call types. A blank value in OpenRTB2 indicates no subdomain was used. |

## Metrics

| Column | Type | Formula | Description |
|:---|:---|:---|:---|
| `filtered_requests` | int |  | Ad requests filtered pre-bid by Xandr for inventory quality. |
| `imps_kept` | int |  | An impression where a managed advertiser's creative serves on a managed publisher's site. |
| `imps_resold` | int |  | An impression that is resold to a third-party buyer. |
| `defaults` | int |  | Ad requests where a default creative served because there were no valid bids. |
| `video_player_errors` | int |  | Errors reported from the video player after the VAST XML has been delivered. |
| `video_default_errors` | int |  | Errors reported from the video player when a default creative should have served. |
| `bid_sent_no_responses` | int |  | Ad requests sent from Xandr to external ad servers for a secondary auction that did not result in a win. This metric is most relevant for external sellers where the final auction is outside of Xandr. |
| `default_no_responses` | int |  | Ad requests where a default creative was sent but no response was received from the end ad server. This could be the result of an error or an alternate default tag was chosen by the final ad server. |
| `psas_or_blanks` | int |  | The number of blanks or PSAs served. |
| `total_ad_requests` | int | filtered_requests + imps_kept + imps_resold + defaults + video_player_errors + video_default_errors + bid_sent_no_responses + default_no_responses + psas_or_blanks | The total number of ad requests sent to Xandr for auction. |
| `total_ad_responses` | int | imps_kept + imps_resold + video_player_errors + bid_sent_no_responses | The total number of ad responses counted within Xandr. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"seller_fill_and_delivery_publisher"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat seller_fill_and_delivery_publisher

{"report":
    {
        "format": "csv",
        "report_interval": "yesterday",
        "row_per": ["geo_country"],
        "columns":["placement_id","imps_kept","total_ad_responses","total_ad_requests","geo_country"],
        "report_type": "seller_fill_and_delivery_publisher"
    }
}
```

### `POST` the request to the [Report Service](./report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @seller_fill_and_delivery_publisher "https://api.appnexus.com/report"

{
   "response":{
      "status":"OK",
      "report_id":"c445bca183a3d338dc1c5b85a3d484f5"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=c445bca183a3d338dc1c5b85a3d484f5'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2014-11-19 22:33:31",
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"geo_country\"],\"columns\":[\"placement_id\",\"imps_kept\",\"total_ad_responses\",\"total_ad_requests\",\"geo_country\"],\"report_type\":\"seller_fill_and_delivery_publisher\",\"filters\":[{\"seller_member_id\":\"958\"}]}}",
            "url": "report-download?id=c445bca183a3d338dc1c5b85a3d484f5"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=c445bca183a3d338dc1c5b85a3d484f5' > /tmp/seller_fill_and_delivery_publisher.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
