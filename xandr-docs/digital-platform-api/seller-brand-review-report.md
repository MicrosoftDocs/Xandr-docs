---
title: Digital Platform API - Seller Brand Review Report
description: Use the Seller Brand Review report to analyze brand and creative performance across all inventory, including audit status and client brand category performance.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Seller Brand Review report

This report provides a view of brand performance across all of your inventory. You can:

- review what creative has served on your inventory and how it performed.
- review creative performance by audit status.
- review client brand category performance across all of your inventory.

The `time_granularity` of the data is `daily`. For instructions on retrieving a report, see the [Report Service](./report-service.md) or the [Example](#example) below.

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- yesterday
- last_7_days
- last_30_days
- month_to_date
- last_month

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 428 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | time | no | `"2010-02"` | The month of the auction. |
| `day` | time | no | `"2010-02-01"` | The day of the auction. |
| `buyer_member_id` | int | yes | `643` | The ID of the member that won the auction. |
| `buyer_seat_name` | string | no | `"My Custom Seat"` | The display name for the buyer seat code. |
| `buyer_seat_id` | int | yes | `123` | The ID of the buyer seat. |
| `buyer_seat_code` | string | no | `"Custom Seat"` | The Custom Buyer Seat ID (submitted by DSP) which was used to bid on the impression. |
| `bidder` | int | no |  | **Deprecated**. |
| `bidder_name` | int | no | `"Microsoft Invest"` | The name of the bidder. |
| `bidder_id` | int | no | `2` | The bidder ID of the member. |
| `curator_member_id` | int | yes | `10652` | The ID of the curator member. |
| `placement_id` | int | yes | `546` | The ID of the placement. |
| `placement_name` | string | no | `"300x250 Business"` | The name of the placement. |
| `placement` | string | no | `"300x250 Business (546)"` | **Deprecated**. |
| `publisher_id` | int | yes | `6787` | The ID of the publisher. |
| `geo_country` | string | yes | `"US"` | The code of the geographical country/region. |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country/region. |
| `imp_type` | string | yes | `"Kept"` | **Deprecated**. |
| `imp_type_id` | int | yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br>`1` ("Blank"): No creative served.<br>`2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>`3` ("Default Error"): A default creative served due to a timeout issue.<br>`4` ("Default"): A default creative served because there were no valid bids.<br>`5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>`6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>`7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>`8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>`9` ("External Impression"): An impression from an impression tracker.<br>`10` ("External Click"): A click from a click tracker. |
| `creative_id` | int | yes | `654` | The ID of the creative. |
| `site_id` | int | yes | `555` | The ID of the site. For more information, see the [Site Service](./site-service.md). |
| `site_name` | string | no | `"My Site"` | The name of the site. For more information, see the [Site Service](./site-service.md). |
| `brand_id` | int | yes | `3` | The ID of the brand associated with a creative served on the publisher's inventory. |
| `brand_name` | string | no | `"Ace Hardware"` | The name of the brand associated with a creative served on the publisher's inventory. |
| `brand` | string | no | `"Ace Hardware (3)"` | **Deprecated**. |
| `payment_type` | string | yes | `"cpm"` | The type of payment to the broker. |
| `revenue_type` | string | no | `"cpm"` | The way the advertiser has agreed to pay you. |
| `revenue_type_id` | int | yes | `4` | The ID of the revenue type. Possible values:<br>`-1` = No Payment<br>`0` = Flat CPM<br>`1` = Cost Plus CPM,<br>`2` = Cost Plus Margin<br>`3` = CPC<br>`4` = CPA<br>`5` = Revshare<br>`6` = Flat Fee<br>`7` = Variable CPM<br>`8` = Estimated CPM |
| `width` | int | yes | `250` | The width of the creative. |
| `height` | int | yes | `300` | The height of the creative. |
| `site` | string | no | `"My Site (555)"` | **Deprecated**. |
| `publisher_code` | string | no | `"My Publisher Code"` | The custom code for the publisher. |
| `site_code` | string | no | `"Site Name Code"` | The custom code for the site. |
| `placement_code` | string | no | `"Photos Code"` | The custom code for the placement. |
| `buyer_member_name` | string | no | `"Network"` | The name of the buying member. |
| `buyer_member` | string | no | `"Network (567)"` | **Deprecated**. |
| `media_type` | string | yes | `"Banner", "Pop", "Interstitial", "Video", "Text"` | The general display style of a creative served on the publisher's inventory. You can use the [Media Type Service](./media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | yes | `444` | The ID of the media type associated with the creative that was served. For more information, see the [Media Type Service](./media-type-service.md). |
| `publisher_name` | string | no | `"LOL - US"` | The name of the publisher on whose site the impression occurred. |
| `publisher` | string | yes | `"LOL - US (44389)"` | **Deprecated**. |
| `deal_id` | int | yes | `2345` | The ID of the deal. For more information about deals you have negotiated with buyers, see [Deal Service](./deal-service.md). |
| `deal_name` | string | no | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal_type` | string | yes | `1` | The ID representing the type of deal. Possible values:<br>`1` = Open Auction<br>`2` = Private Auction<br>`4` = Programmatic Guaranteed<br>`5` = Curated Auction |
| `deal` | string | no | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated**. |
| `deal_code` | string | no | `"Custom code"` | The custom code for the deal. |
| `brand_offer_category_id` | int | yes | `1256` | The ID of the brand offer category associated with the impression. See `category_id` in the [Brand Service](./brand-service.md) page. |
| `brand_offer_category_name` | string | no | `"Luxury Cars"` | The name of the brand offer category associated with the impression. See `category_id` in the [Brand Service](./brand-service.md) page. |
| `creative_audit_status_id` | int | yes | `0` | The ID of the audit status of the creative associated with the impression:<br>`0` = unaudited<br>`1` = seller audited only<br>`2` = appnexus audited |
| `creative_audit_status` | string | no | `"Unaudited"` | The audit status of the creative associated with the impression:<br> - `"Unaudited`"<br> - `"Self Audit Only"`<br> - `"AppNexus Audited"` |
| `size` | string | yes | `"728x90"` | The width and height of the creative associated with the impression. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `34534` | imps | The total number of impressions (including defaults). |
| `clicks` | int | `345` | clicks | The total number of clicks across all impressions. |
| `cost` | money |`16.833378` | cost | The total amount of media cost for direct publisher and purchased real-time inventory. |
| `revenue` | money | `25.767257` | booked_revenue + reseller_revenue | The sum of booked revenue and reseller revenue. |
| `booked_revenue` | money | `25.767257` | booked_revenue | The total revenue booked through direct advertisers (line item). |
| `reseller_revenue` | money | `0` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `profit` | money | `970.40` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `cpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `total_convs` | int | `5` | total_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `ctr` | double | `0.002327` | clicks / imps | The rate of clicks to impressions. |
| `rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `ppm` | money | `0.944966292134831` | (profit / imps) x 1000 | **To be deprecated**. The profit per 1000 impressions. |
| `convs_per_mm` | double | `221.877080097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `network_profit` | money | `123.45` | (booked_revenue + reseller_revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost. |
| `network_profit_ecpm` | money | `123.45` | (network_profit/imps) * 1,000 | Network profit per 1,000 imps. |
| `network_profit_ecpc` | money | `123.45` | network_profit/clicks | Network profit per click. |
| `network_profit_ecpa` | money | `123.45` | network_profit/conversions | Network profit per conversion. |
| `network_profit_margin` | money | `123.45`| network_profit/(booked_revenue + reseller_revenue) | Network profit margin. |
| `profit_ecpm` | money | `123.45` | ((booked_revenue - total_cost)/imps) * 1,000 | Profit per 1,000 imps. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |

## Example

### Create a JSON report request

The JSON file should include the `report_type` of `"seller_brand_review"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat seller_brand_review
{"report":
    {
        "format": "csv",
        "report_interval": "yesterday",
        "row_per": ["geo_country"],
        "columns": ["placement_id","imp_type_id","creative_id","brand_id","geo_country"],
        "report_type": "seller_brand_review"
    }
}
```

### `POST` the request to the [Report Service](./report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @seller_brand_review "https://api.appnexus.com/report"
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
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"geo_country\"],\"columns\":[\"placement_id\",\"imp_type_id\",\"creative_id\",\"brand_id\",\"geo_country\"],\"report_type\":\"seller_brand_review\",\"filters\":[{\"seller_member_id\":\"958\"}]}}",
            "url": "report-download?id=c445bca183a3d338dc1c5b85a3d484f5"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=c445bca183a3d338dc1c5b85a3d484f5' > /tmp/seller_brand_review.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
