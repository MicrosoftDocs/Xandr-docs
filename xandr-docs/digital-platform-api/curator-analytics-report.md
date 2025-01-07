---
title: Digital Platform API - Curator Analytics Report
description: Use the Curator Analytics report to get curators insight into how money flows from demand to supply within their curated marketplace.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Curator Analytics report

> [!NOTE]
> This report is only available to curators.

The Curator Analytics Report provides curators insight into how money is flowing from demand to supply within their curated marketplace.

For instructions on retrieving a report, see [Report Service](report-service.md) or the [Example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_hour
- today
- yesterday
- month_to_date
- last_month
- lifetime

### Data retention period

Data in this report is retained for 1100 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Time ranges including dates occurring greater than 45 days ago

If you create Curator Analytics reports with the `report_interval` set to `"lifetime"`, your report (regardless of metrics included) will be added to a special queue for "resource-intensive" reports. As a result, the report may take longer than usual to complete. In addition, these resource-intensive reports may, due to the amount of data being requested, fail before being completed. If your report fails to complete, you will receive a notification. If your report request fails or is deleted, you can:

- rerun the report at a later time.
- use a report type other than `curator_analytics`.
- alter the way you structure your reports (if possible) so they do not include dates greater than 45 days ago.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `bidder_id` | int | Yes | `456` | ID of the bidder who bought on the transaction |
| `bidder_name` | string | No |`"That Bidder"` | Name of the bidder who bought on the transaction |
| `billing_currency` | string | Yes | `"USD"` | The currency Xandr bills the curator in |
| `brand_id` | int | Yes | `1234` | Brand ID associated with the creative that served on the curated deal |
| `brand_name` | string | No | `"That Brand"` | Brand name associated with the creative that served on the curated deal |
| `buyer_member` | string | No | `"That Buyer (789)"` | Member name of the buyer who bought on the transaction with their member ID in brackets |
| `buyer_member_id` | int | Yes | `789` | Member ID of the buyer who bought on the transaction |
| `buyer_member_name` | string | No | `"That Buyer"` | Member name of the buyer who bought on the transaction |
| `curated_deal` | string | No | `"My Deal Name (123)"` | Curated deal name with its deal ID in brackets |
| `curated_deal_advertiser_id` | int | Yes | `123` | Advertiser ID of the curator member object that owns the deal line item associated with the curated deal |
| `curated_deal_advertiser_name` | string | No | `"That Advertiser"` | Advertiser name of the curator member object that owns the deal line item associated with the curated deal |
| `curated_deal_id` | int | Yes | `123` | Curated deal ID |
| `curated_deal_insertion_order_id` | int | Yes | `123` | Insertion Order ID of the curator member object that owns the deal line item associated with the curated deal |
| `curated_deal_line_item_id` | int | Yes | `123` | Line Item ID of the curator member object that owns the deal line item associated with the curated deal |
| `curated_deal_insertion_order_name` | string | No | `"IO Name"` | Insertion Order name of the curator member object that owns the deal line item associated with the curated deal |
| `curated_deal_line_item_name` | string | No | `"My Curated LI"` | Line Item name of the curator member object that owns the deal line item associated with the curated deal |
| `curated_deal_name` | string | No | `"My Deal Name"` | Curated deal name |
| `curator_margin_type` | int | No | `"Percent"` | Margin type (if a curator has a margin associated to the line item). Possible values:<br>- `"Unknown"`<br> -  `"Percent"`<br> - `"CPM"` |
| `curator_margin_type_filterable` | int | Yes | `1` | Filterable margin type (if a curator has a margin associated to the line item). Possible values:<br>`0` (Unknown)<br>`1` (Percent)<br>`2` (CPM) |
| `curator_member` | string | No | `"My Account (123)"` | Member name of the curator account with their member ID in brackets |
| `curator_member_id` | int | Yes | `123` | Member ID of the curator account |
| `curator_member_name` | string | No | `"My Account"` | Member name of the curator account |
| `day` | date | Yes | `"2020-02-01"` | The day of the auction |
| `device_type` | string | Yes | `"desktops & laptops"` | Device type on which the impression was served. Possible values are:<br> - `"desktops & laptops"`<br> - `"tablets"`<br> - `"mobile phones"`<br> - `"tv"`<br> - `"game consoles"`<br> - `"set top box"`<br> - `"media players"`<br> - `"other devices"` |
| `geo_country` | string | Yes | `"US"` | The country/region in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. |
| `hour` | date | Yes | `"2020-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `media_type` | string | No | `"banner"` | Media type associated with the creative that served on this impression. Possible values are:<br> - `"banner"`<br> - `"pop"`<br>- `"interstitial"`<br> - `"video"`<br> - `"text"`<br> - `"expandable"`<br> - `"skin"`<br> - `"facebook"`<br> - `"image and text"`<br> - `"high impact"`<br> - `"native"`<br> - `"audio"`<br> - `"Unknown"` |
| `member_currency` | string | Yes | `"USD"` | The currency associated with the curator member's seat |
| `member_id` | int | Yes | `789` | Member ID of the curator account |
| `mobile_application_id` | string | Yes | `"343200656"` (iOS) or<br>`"com.rovio.angrybirds"`<br>(Android) | The mobile application ID associated with the creative that served on this impression |
| `mobile_application_name` | string | No | `"Angry Birds"` | The mobile application name associated with the creative that served on this impression |
| `month` | date | Yes | `"2020-02"` | The month of the auction |
| `placement` | string | No | `"Ivillage 160x600 (456)"` | Placement name of the seller where the curated transaction served with the placement's ID in brackets |
| `placement_group_id` | int | Yes | `4321` | Placement Group ID of the seller where the curated transaction served |
| `placement_group_name` | string | No | `"Placement Group Name"` | Placement Group name of the seller where the curated transaction served |
| `placement_id` | int | Yes | `456` | Placement ID of the seller where the curated transaction served |
| `placement_name` | string | No | `"Ivillage 160x600"` | Placement name of the seller where the curated transaction served |
| `publisher_id` | int | Yes | `321` | Publisher ID of the seller where the curated transaction served |
| `publisher_name` | string | Yes | `"Newscorp"` | Publisher name of the seller where the curated transaction served |
| `seller_deal` | string | No | `"That Seller Deal (6543)"` | The seller deal name being included in a curated deal with the seller deal ID in brackets<br><br>**Note**: If applicable, since not all curated deals will include a seller deal |
| `seller_deal_id` | int | Yes | `6543` | The seller deal ID being included in a curated deal<br>Note: If applicable, since not all curated deals will include a seller deal |
| `seller_deal_name` | string | No | `"That Seller Deal"` | The seller deal name being included in a curated deal<br><br>**Note**: If applicable, since not all curated deals will include a seller deal |
| `seller_deal_type_id` | int | No | `2` | The ID of the type of seller deal being included in a curated deal, if applicable. Possible values are:<br>`1` (Open Auction)<br>`2` (Private Auction) |
| `seller_deal_type_name` | string | Yes | `"Private Marketplace"` | The name of the type of seller deal being included in a curated deal, if applicable. Possible values are:<br>- `"---"` (Open Auction)<br>- `"Private Marketplace`" (Private Auction) |
| `seller_member_id` | int | Yes | `4567` | Member ID of the seller where the curated transaction served |
| `seller_member_name` | string | No | `"That Seller"` | Member name of the seller where the curated transaction served |
| `site_domain` | string | No | `"bestsiteever.com"` | Site Domain / App where the curated transaction served |
| `size` | string | Yes | `"320x50"` | The size of the creative |
| `video_context` | string | Yes | `"pre-roll"` | The type of video format the curated transaction served on. Possible values are:<br> - `"unknown"`<br> - `"pre-roll"`<br> - `"mid-roll"`<br> - `"post-roll"`<br> - `"outstream"` |
| `video_content_duration` | string | Yes | `"Short-Form"` | Length of the content in seconds (two options: short (less than 480s), long (more than 480s)). |
| `content_delivery_type` | string | Yes | `"VOD"` | The type of streaming content delivery. |
| `video_content_genre` | string | Yes | `"Action"` | The main genre of the program on which the ad will be played. |
| `video_program_type` | string | Yes | `"Movie"` | The higher level categorization of the program on which the ad will be played. |
| `video_content_rating` | string | Yes | `"Children(7+)"` | The type of rating of the content. |

## Metrics

> [!NOTE]
> Clicks metrics are available for impressions bought through Microsoft Invest. Video metrics are available for impressions bought through any DSP.

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `curator_margin` | money | `2.57676` | curator_margin | The profit a curator makes on a transaction<br><br>**Note**: When taken as a percentage, Curator Margin is calculated off Curator Revenue. |
| `curator_net_media_cost` | money | `20.6138056` | curator_revenue - curator_margin - curator_tech_fees | The amount of spend a curator sends to exchange sellers, net of curator fees and margins, if applicable. This is the same as gross seller revenue, inclusive of seller fees. |
| `curator_revenue` | money | `25.767257` | curator_revenue | The amount of spend a buyer sends to the curator, net of buyer fees, if applicable. This is the same as buyer media cost, exclusive of buyer fees. |
| `curator_tech_fees` | money | `2.5767257` | curator_tech_fees | The fees Xandr charges to a curator on a transaction |
| `curator_total_cost` | money | `23.1905313` | curator_revenue - curator_margin | The amount of spend a curator sends to the exchange and exchange sellers, net of curator margin but gross of curator fees |
| `imps` | int | `2340` | imps | The number of delivered impressions |
| `viewdef_viewed_imps` | int | `1638` | viewdef_viewed_imps | The number of measured impressions that were viewable, per the buyer's viewability definition |
| `viewdef_view_rate` | double | `0.70` | viewdef_view_rate | The number of measured impressions that were viewable, per the buyer's viewability definition, divided by the number of measured impressions |
| `viewed_imps` | int | `1872` | viewed_imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second |
| `view_measurable_imps` | int | `172` | view_measurable_imps | The total number of impressions that were measured for viewability. |
| `clicks` | int | `7` | clicks | The total number of clicks across all impressions. For Microsoft Invest, clicks from all media types are supported. For external DSPs, only clicks from Native and Video media types are supported. |
| `ctr` | double |`0.3` | clicks / imps | The proportion of Clicks versus Imps. |
| `buyer_cpc` | money | `3.68` | curator_revenue / clicks | Curator Revenue divided by Clicks. |
| `video_errors` | int | `45` | video_errors | The total number of times an error occurred. |
| `video_starts` | int | `2335` | video_starts | The total number of times the first segment of the video creative was downloaded and started. |
| `video_start_rate` | double | `0.99786` | video_starts / imps | The proportion of Video Starts versus Imps. |
| `video_skips` | int | `12` | video_skips | The total number of times a user skipped the video. |
| `video_skip_rate` | double | `0.0051282` | video_skips / imps | The proportion of Video Skips versus Imps. |
| `video_25_pcts` | int | `2100` | video_25_pcts | The total number of times the video completed 25% of the entire duration. |
| `video_50_pcts` | int | `2000` | video_50_pcts | The total number of times the video completed 50% of the entire duration. |
| `video_75_pcts` | int | `1900` | video_75_pcts | The total number of times the video completed 75% of the entire duration. |
| `video_completions` | int | `1800` | video_completions | The total number of times the video played for the entire duration. |
| `video_completion_rate` | double | `0.76923` | video_completions / imps | The proportion of Video Completions versus Imps. |
| `buyer_cost_per_video_complete` | money | `0.014315` | curator_revenue / video_completions | Curator Revenue divided by Video Completions. |
| `buyer_cpm` | money | `11.01164` | curator_revenue / imps * 1000 | Curator Revenue divided by Imps expressed as a CPM. |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` of `"curator_analytics"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat curator_analytics

{
    "report": {
        "columns": [
            "hour",
            "buyer_member_name",
            "curated_deal",
            "imps",
            "curator_revenue",
            "curator_margin"
        ],
        "format": "csv",
        "report_interval": "today",
        "report_type": "curator_analytics"
    }
}
```

### `POST` the request to the report service

```
$ curl -b cookies -X POST -d @curator_analytics 'https://api.appnexus.com/report'

{
   "response":{
      "status":"OK",
      "report_id":"6b177543a9411ffa67b09bdf5e76cac1"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=6b177543a9411ffa67b09bdf5e76cac1'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2020-08-25 13:03:37",
         "json_request":"{\"report\":{\"report_type\":\"curator_analytics\",\"columns\":[\"hour\",\"buyer_member_name\",\"curated_deal\",\"imps\",\"curator_revenue\",\"curator_margin\"],\"report_interval\":\"today\",\"format\":\"csv\",\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"member_id\":\"123456\"}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1598400000,\"start_date\":1598313600,\"user_id\":\"987654\"}",
         "url": "report-download?id=6b177543a9411ffa67b09bdf5e76cac1"
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
$ curl -b cookies 'https://api.appnexus.com/report-download?id=6b177543a9411ffa67b09bdf5e76cac1' > /tmp/curator_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
