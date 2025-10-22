---
title: Digital Platform API - Buyer Engagement Report
description: In this article, learn about the Buyer Engagement report and the dimensions and metrics associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Buyer engagement report

The Buyer Engagement Report gives you insight into the viewable duration of your display and video creatives.

For instructions on retrieving a report, please see [Report Service](report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- yesterday
- last_7_days
- last_14_days
- month_to_yesterday
- last_30_days

### Data retention period

Data in this report has a daily time granularity and is retained for five weeks. This report also displays data under the UTC/GMT time zone.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Description |
|---|---|---|---|
| `buyer_member_id` | int | Yes | The ID of the buying member of the impressions. |
| `seller_member_id` | int | Yes | The ID of the selling member. |
| `size` | string | Yes | The size of the creative that was served. |
| `seller_member_name` | string | No | The name of the selling member. |
| `advertiser_id` | int | Yes | The ID of the advertiser object associated to the served impressions. |
| `advertiser_name` | string | No | The name of the advertiser object associated to the served impressions. |
| `line_item_id` | int | Yes | The ID of the line item under which the impressions were purchased. The buy-side hierarchy is **Line Item** > **Campaign**. |
| `line_item_name` | string | No | The name of the line item under which the impressions were purchased. The buy-side hierarchy is   **Line Item** > **Campaign**. |
| `campaign_id` | int | Yes | The ID of the campaign that purchased the impressions. |
| `campaign_name` | string | No |The name of the campaign that purchased the impressions. |
| `imp_type` | int | Yes | The name of the impression type which was occurred.  |
| `imp_type_id` | int | Yes | TheID for the type of impression that served (associated types in parentheses): <br> - **1** ("Blank"): No creative served <br> - **2** ("PSA"): A public service announcement served because there were no valid bids and no default creative was available <br> - **3** ("Default Error"): A default creative served due to a timeout issue <br> - **4** ("Default"): A default creative served because there were no valid bids <br> - **5** ("Kept"): Your advertiser's creative served on your publisher's site <br> - **6** ("Resold"): Your publisher's impression was sold to a third-party buyer<br> - **7** ("RTB"): Your advertiser's creative served on third-party inventory <br> - **8** ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative <br> - **9** ("External Impression"): An impression from an impression tracker <br> - **10** ("External Click"): A click from a click tracker <br> - **11** ("Insertion"): Your creative served on third-party inventory, where it persists across page-loads and sessions. This impression type is currently only for Facebook News Feed creatives. |
| `insertion_order_id` | int | Yes | The ID of the  insertion order under which the impressions were purchased. The buy-side   hierarchy is **Insertion Order** > **Line Item** > **Campaign**. |
| `insertion_order_name` | string | No | The name of the insertion order under which the impressions were purchased. The buy-side   hierarchy is  **Insertion Order** > **Line Item** > **Campaign**. |
| `publisher_id` | int | Yes | The ID of the publisher object on whose inventory the impressions were occurred. |
| `publisher_name` | string | No | The name of the publisher object on whose inventory the impressions were occurred. |
| `placement_id` | int | Yes | The ID of the placement or the open slot on publisher website where the advertiser's creative with matching specifications was served. |
| `placement_name` | string | No | The name of the placement or the open slot on publisher website where the advertiser's creative with matching specifications was served. |
| `member_id` | int | Yes | The ID of the member for which report is generated. |
| `creative_id` | int | No | The ID of the creative served for the impression. For impressions older than 14 months, creatives will be aggregated   into one row with 0 as the creative ID. <br> **Note**: For external click or impression trackers, creative_id will be "External Clicks" or "External Imps". |
| `creative_name` | string | No | The name of the   creative served for the impression. |
| `mediatype` | string | No | The name of the media type associated with the creative that served on the impression. |
| `mediatype_id` | int | Yes | The ID of the media type associated with the creative that served on the impression. |
| `device_type` | string | Yes | The   type of device on which the impression was served. Possible values: <br> - Desktops & Laptops <br> - Tablets  <br>  - Mobile Phones <br> - TV  <br> - Game Consoles <br> - Set Top Box  <br> - Media Players <br> - Other Devices |
| `day` | date | Yes | The day of the auction. |
| `operating_system_family_id` | int | Yes | The ID of the operating system family associated with the device where the impression was served on. |
| `operating_system_family_name` | string | No | The name of the operating system family associated with the device where the impression was served on. |
| `split_id` | int | Yes | The ID of the split that purchased the impressions in this data set. Splits are   only applicable to augmented line items. For any reports that contain campaigns, the split_id (if included) will be null. |
| `split_name` | string | No | The name of the split that purchased the impressions in this data set. Splits are   only applicable to augmented line items. For any reports that contain campaigns, the split_id (if included) will be null. |
| `domain_id` |   |   | The ID of the domain on which the impression was occurred. |
| `deal_id` |   |   | The ID of the deal with which  the served impression is associated. For more information about deals you have negotiated with sellers, see   Deal Buyer Access Service. |
| `deal_name` |   |   | The name of the deal with which  the served   impression is associated. |
| `supply_type` |   |   | The supply (inventory) type on which the impression occurred: <br> - Web <br> - Mobile Web <br> - Mobile App |
| `media_type_id` | int | Yes | The ID of the `media_type`.  |
| `media_type` | string | No | The general display style of the creative that served:   <br>   - Banner   <br>   - Interstitial <br>  - Video  <br>  - Text <br>  - Expandable <br> - Skin  <br>  - Facebook |

## Metrics

| Column | Type | Formula | Description |
|---|---|---|---|
|`imps` | int | N/A | The total number of impressions. |
| `clicks` | int | N/A | The total number of clicks. |
| `ctr` | double | clicks/imps | The click-through rate – the ratio of clicks to impressions, expressed as a percentage |
| `average_viewable_duration` | double | Total Viewable Duration/Viewable Imps | The average number of seconds for which the creative was in view according to IAB viewability criteria. |
| `total_viewable_duration` | int | N/A | The total number of seconds for which the creative was in view according to IAB viewability criteria. |
| `video_completion_rate` | double | Video Completion Rate = Video Completions/Total Impressions | The ratio of video completions to total impressions, expressed as a percentage. |
| `video_completions` | int | N/A | The total number of video creatives played for their entire duration |
| `view_measurable_imps` | int | N/A | The total number of impressions that were measured for viewability |
| `view_measurable_rate`| double |  View Measurable Imps / Imps | The percentage of impressions measured for viewability out of the total number of impressions. |
| `view_rate` | double | Viewed Imps / View Measurable Imps | The percentage of impressions that were viewable out of the total number of impressions measured for viewability.|
| `viewable_completion_rate`| double |Viewable and Completed Video Impressions/Measurable Video Impressions | The   ratio of in-view video completions to total impressions, expressed as a percentage. |
| `viewdef_view_rate` | double | N/A | The percentage of impressions that were viewable, according to the member-level   custom definition configuration, out of the total number of impressions measured for viewability |
| `viewdef_viewed_imps` | int | N/A | The   number of measured impressions that were viewable, according to the   member-level custom definition configuration (for more details, contact your Xandr account representative) |
| `viewed_imps` | int | N/A | The   total number of impressions that were deemed viewable as defined by the   Interactive Advertising Bureau (IAB): For at least one second, 50% of a creative's pixels (or 30% for a creative with at least 242,500 pixels) must be viewable to a viewer on their screen. |

## Example

### Create the JSON-formatted report request

The JSON file should include the `report_type` `"engagement_report_for_buyers"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (year, month, day), and specify the format in which the data should be returned (csv, excel, or html). For a full explanation of fields that can be included in the JSON file, see [Report Service](report-service.md).

```
$ cat engagement_report_for_buyers
  {
    "report":
    {
        "report_type":"engagement_report_for_buyers",
        "columns":[
            "line_item_id",
            "line_item_name",
            "creative_name",
            "viewable_completion_rate",
            "average_viewable_duration",
            "ctr",
            "clicks",
            "imps"
        ],
        "report_interval":"last_7_days",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @engagement_report_for_buyers 'https://api.appnexus.com/report'
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
         "created_on":"2021-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"engagement_report_for_buyerss\",\"columns\":[\"line_item_id\",
            \"line_item_name\",\"creative_name\",\"viewable_completion_rate\",\"average_viewable_duration\",\"ctr\",\"clicks\",\"imps\"],
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/engagement_report_for_buyers.csv
```
