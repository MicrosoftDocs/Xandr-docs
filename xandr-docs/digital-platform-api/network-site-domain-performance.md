---
title: Network Site Domain Performance
description: Use the Network Site Domain Performance report to view performance and optimization data by domain for all of a network's advertisers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Network site domain performance

The **Network Site Domain Performance** report can be used to view performance and optimization data by domain for all of a network's advertisers.

> [!NOTE]
> To view performance and optimization data by domain for a specific advertiser, filter this report by `advertiser_id`, or use the [Site Domain Performance Report](./site-domain-performance-report.md) report.
>
> For instructions on retrieving a report, please see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field can be set to one of the following:

- yesterday
- last_7_days
- month_to_yesterday
- month_to_date

If you use the `start_date` and `end_date` fields to define the time range, the `start_date` must not be more than 30 days in the past. Since hourly data is not available for this report, the `start_date` and `end_date` cannot be identical and must be formatted as `"YYYY-MM-DD"` rather than `"YYYY-MM-DD HH:MM:SS"`.

### Data retention period

Data retention period for this report is 45 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | yes | `11/1/11` | The month and year (with the first day of the month). |
| `day` | date | yes | `11/16/11` | The day, month, and year. |
| `site_domain` | string | no | `bestsiteever.com`<br>- or -<br>`itunes.apple.com/app/app-name/id1234567` | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store.<br>There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| `buyer_member` | string | no | `MyNetwork (4567)` | **Deprecated**. |
| `buyer_member_id` | int | yes | `4567` | The ID of the buying member. |
| `buyer_member_name` | string | no | `MyNetwork` | The name of the buying member. |
| `fold_position_id` | int | Yes | `0` | The ID of the fold position, i.e. where on the page the placement is located.<br>Possible values for impressions:<br>`0` = "unknown"<br>`1` = "above"<br>`2` = "below" |
| `fold_position` | string | Yes | `"Unknown"` | The fold position, i.e. where on the page the placement is located. For allowed values, see `fold_position_id`. |
| `campaign` | string | no | `ExampleCampaign (123456)` | **Deprecated**. |
| `campaign_id` | int | yes | `123456` | The ID of the campaign. |
| `campaign_code` | string | no | `CampaignCode` | The custom code for the campaign. |
| `campaign_name` | string | no | `ExampleCampaign` | The name of the campaign. |
| `campaign_priority` | int | no | `5` | The bidding priority of a campaign that targets direct inventory. For more information, see [Bidding Priority](../monetize/bidding-priority.md) in the UI documentation.<br>Possible values: `1`-`10`, where `10` is the highest priority. |
| `line_item` | string | no | `ExampleLineItem (323)` | **Deprecated**. |
| `line_item_id` | int | yes | `323` | The ID of the line item. |
| `line_item_name` | string | no | `ExampleLineItem` | The name of the line item. |
| `campaign_group` | string | no | `ExampleGroupName(123)` | **Deprecated**. |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `top_level_category_id` | int | yes | `19821` | The ID of the top content category assigned to the domain. |
| `top_level_category_name` | string | yes | `"Shopping"` | The name of the top content category assigned to the domain. |
| `top_level_category` | string | yes | `"Shopping (19821)"` | **Deprecated**. |
| `second_level_category_id` | int | yes | `20129` | The ID of the second-level content category assigned to the domain.<br><br>**Note**:<br>If the domain is an a top-level category, you should not request this dimension. |
| `second_level_category_name` | string | yes | `"Shoes"` | The name of the second-level content category assigned to the domain.<br><br>**Note**: If the domain is an a top-level category, you should not request this dimension. |
| `second_level_category` | string | yes | `"Shoes (20129)"` | **Deprecated**. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about deals you have negotiated with sellers, see [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated**. |
| `deal_code` | string | No | `"External seller deal code"` | The custom code for the deal. For deals with external supply partners, this is generally the string that you use to identify the deal. |
| `advertiser` | string | no | `ExampleAdvertiser (123)` | **Deprecated**. |
| `campaign_group_name` | string | no | `ExampleGroupName` | The name of the campaign group. |
| `advertiser_id` | int | yes | `123` | The ID of the advertiser. |
| `campaign_group_id` | int | yes | `123` | The unique identification number of the campaign group. |
| `advertiser_code` | string | no | `AdvertiserCode` | The custom code for the advertiser. |
| `advertiser_name` | string | no | `ExampleAdvertiser` | The name of the advertiser. |
| `supply_type` | string | Yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `"web"` <br> - `"mobile_app"` <br> - `"mobile_web"`. |
| `mobile_application_id` | string | Yes | `'343200656' (iOS)` or<br>`'com.rovio.angrybirds' (Android)` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `mobile_application_name` | string | Yes | `Angry Birds` | The name of the mobile application as it appears in the Apple App and Google Play Stores. |
| `mobile_application` | string | No | Angry Birds (com.rovio.angrybirds) | **Deprecated**. |
| `age_bucket` | string | Yes | `"25-34"` | The bucket for the age of the user. See [Age Buckets](#age-buckets) below for possible values.<br><br>**Note**: For impressions older than 100 days, the `age_bucket` will be `"unknown"`. |
| `age_bucket_id` | string | No | `"3"` | The ID of the age bucket. See [Age Buckets](#age-buckets) below for possible values.<br><br>**Note**: For impressions older than than 100 days, the `age_bucket_id` will be `0`. |
| `gender` | string | Yes | `"m"`, `"f"`, `"u"` | The gender of the user.<br><br>**Note**: For impressions older than 100 days, gender will be `"u"`. |
| `is_remarketing` | int | Yes | `0`, `1` | If `1`, the campaign is remarketing. If `0`, the campaign is not remarketing.<br><br>**Note**: For impressions older than 100 days, `is_remarketing` will be `-1`. |
| `pixel_id` | int | yes | `1942` | The unique identification number of the conversion pixel.<br><br>**Note**: This dimension will return a maximum of 10 conversion pixels. Also, you can filter by no more than 10 conversion pixels. Although `pixel_id` is groupable, we do not recommend that you group by this dimension since doing so will cause conversion events to then be shown in separate rows from impression and click events. We generally assume you want to view all of these events in a single row so as to be able to retrieve accurate and aggregated values for conversion rate and cost-per-conversion calculations. As a result, we instead recommend that you filter by `pixel_id` so you can retrieve conversion counts and related metrics for your most relevant pixel IDs. |
| `operating_system_id` | int | Yes | `24` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_name` | string | Yes | `"Android 2.3.5 Gingerbread"` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_id` | int | Yes | `2` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_name` | string | Yes | `"Android"` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `insertion_order_id` | int | Yes | `451` | ID of the insertion order. |
| `insertion_order_name` | string | No | `"Q1-2016"` | Display name for the insertion order. |
| `seller_member_id` | int | Yes | `12345` | The ID of the seller member associated with the site domain. |
| `seller_member_name` | string | No | `"BestSellerEver"` | The name of the seller member associated with the site domain. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `booked_revenue` | money | `450.00` | booked_revenue | The revenue received from the advertiser. For more information, see [Network Revenue and Billing Your Clients](../monetize/network-revenue-and-billing-your-clients.md) in the UI documentation. |
| `clicks` | int | `2067` | clicks | The total number of clicks. |
| `click_thru_pct` | double | `2.756%` | (clicks / imps) * 100 | The rate of clicks to impressions as a percentage. |
| `convs_per_mm` | double | `384.4` | (post_click_convs + post_view_convs / imps) * 1,000,000 | The number of conversions per million impressions. |
| `convs_rate` | double | `0.0003844` | (post_click_convs + post_view_convs) / imps | The rate of conversions to impressions. |
| `cost_ecpa` | money | `1.1111` | media_cost / (post_click_convs + post_view_convs) | The cost per acquisition/conversion. |
| `cost_ecpc` | money | `0.1834` | media_cost / clicks | The cost per click. |
| `cpm` | money | `5.00` | media_cost / imps * 1000 | The cost per thousand impressions. |
| `ctr` | double | `0.22756` | clicks / imps | The rate of clicks to impressions. |
| `imps` | int | `75000` | imps | The total number of impressions served. |
| `media_cost` | money | `100.00` | media_cost | The expense for the buying member. For more information, see [Network Revenue and Billing Your Clients](../monetize/network-revenue-and-billing-your-clients.md) in the UI documentation. |
| `post_click_convs` | int | `15` | post_click_convs | The total number of recorded post-click conversions. |
| `post_click_convs_rate` | double | `0.0002` | post_click_convs / imps | The rate of post-click conversions to impressions. |
| `post_view_convs` | int | `10` | post_view_convs | The total number of recorded post-view conversions. |
| `post_view_convs_rate` | double | `0.00013` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `profit` | money | `0.084102` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `profit_ecpm` | money | `0.7778` | (profit / imps) * 1000 | The profit (defined as booked revenue minus total cost) per 1,000 imps. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |
| `media_cost_buying_currency` | money | `100.0` | media_cost_buying_currency | The cost to the buying member for the media in the currency which the buyer has set (i.e. the buying currency). |
| `profit_buying_currency` | money | `0.084102` | booked_revenue - total_cost | The booked revenue minus total cost in the buying currency. |
| `revenue_ecpa_buying_currency` | money | `123.45` | booked_revenue/conversions | The revenue per conversion in the buying currency. |
| `revenue_ecpc_buying_currency` | money | `123.45` | booked_revenue /clicks | The revenue per click in the buying currency. |
| `revenue_ecpm_buying_currency` | money | `123.45` | (booked_revenue/imps) * 1,000 | The booked revenue per 1,000 impressions in the buying currency. |
| `revenue_ecpa` | money | `123.45` | booked_revenue/conversions | The revenue per conversion in currency set as per Currency 2.0 parameter. |
| `revenue_ecpc` | money | `123.45` | booked_revenue /clicks | The revenue per conversion in currency set as per Currency 2.0 parameter. |
| `revenue_ecpm` | money | `123.45` | (booked_revenue/imps) * 1,000 | The booked revenue per 1,000 imps in currency set as per Currency 2.0 parameter. |

> [!NOTE]
> **Currency 2.0** - As per Currency 2.0 parameter, currency is an input variable to the reports. Users can use a currency dropdown in the UI and report processor take the currency input and return all monetary fields of the report in the applicable currency. Users can select from the below options to select a currency :
>
> - **Member Currency**: This is the currency defined at the member level which is at the top. Though advertisers and other objects can be set in different currencies under a member, reports can be generated in this currency.
> - **Advertiser Currency**: This is the currency in which the advertiser operates in. While creating the advertiser, the operating currency of it is set and reports can be generated in that currency.
> - **Publisher Currency**: This is the currency in which the publisher sells their inventory in. All child objects such as placement groups/placements under the publisher inherit this currency.
> - **Line Item Currency**: This is the currency in which the budget is set in at the line item level.
> - **Billing Currency**: This is the currency in which billing parameters is set at the insertion order level.

### Age buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `0` | `"unknown"` |
| `1` | `"13-17"` |
| `2` | `"18-24"` |
| `3` | `"25-34"` |
| `4` | `"35-44"` |
| `5` | `"45-54"` |
| `6` | `"'55-64"` |
| `7` | `"65+"` |

## Custom viewable definition metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `viewdef_viewed_imps` | int | `4399` | viewdef_viewed_imps | The number of measured impressions that were viewable, per the member-level custom definition configuration (for more details, contact your Xandr account representative). |
| `viewdef_viewed_rate` | double | `96%` | viewdef_viewed_imps / view_measured_imps | The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability. |

## Example

### Create a JSON formatted report request

```
$ cat network_site_domain_performance
  {
 "report":
    {
    "report_type" : "network_site_domain_performance",
    "columns":[
       "day",
       "advertiser_id",
       "site_domain",
       "campaign_id",
       "line_item_id",
       "booked_revenue",
       "imps",
       "clicks",
       "click_thru_pct",
       "post_click_convs",
       "post_view_convs"],
    "report_interval": "last_7_days",
    "emails": ["js@mynetwork.com"],
    "format": "csv"
  }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @network_site_domain_performance 'https://api.appnexus.com/report'

{
    "response":{
        "status":"OK",
        "report_id":"07af1282c9485adcef49c95fa5d7496b"
    }
}
```

### Use the report ID to retrieve the report data

The standard response includes the report data and a Download URL that you can use to save the data to a file. If you want to get just the Download URL without the report data, pass `"without_data"` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=07af1282c9485adcef49c95fa5d7496b'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2011-12-06 23:24:34",
            "cache_hit": false,
            "fact_cache_hit": false,
            "json_request": "{\"report\":{\"report_type\":\"network_site_domain_performance\",\"columns\":[\"day\",\"advertiser_id\",
             \"site_domain\",\"campaign_id\",\"line_item_id\",\"booked_revenue\",\"imps\",\"clicks\",\"click_thru_pct\",\"post_click_convs\",
             \"post_view_convs\"],\"report_interval\":\"last_7_days\",\"emails\":[\"js@mynetwork.com\"],\"filters\":
             [{\"buyer_member_id\":\"882\"}]}}",
            "header_info": "Report type:,member_site_domain_performance\u000d\u000a,\u000d\u000aRun at:,2011-12-06 23:24:34\u000d
             \u000aStart date:,2011-11-29 00:00:00\u000d\u000aEnd date:,2011-12-06 00:00:00\u000d\u000aTimezone:,\u000d\u000aUser:,
             John Smith (10055)\u000d\u000a",
            "data": "day,advertiser_id,site_domain,campaign,line_item,booked_revenue,imps,clicks,click_thru_pct,post_click_convs,
             post_view_convs\u000d\u000a2011-12-05,33347,site1.com,Fall 2011 C2 - targeted inv (145034),Fall 2011 Revenue CPM (61047),
             .003000,1,0,.000000000000000000%,0,0\u000d\u000a2011-12-05,33347,site2.com,Fall 2011 C2 - targeted inv (145034),
             Fall 2011 Revenue CPM (61047),.006000,2,0,.000000000000000000%,0,0\u000d\u000a2011-12-05,55672,site1.com,
             Fall 2011 C2 - targeted inv (145034),Fall 2011 Revenue CPM (61047),.003000,1,0,.000000000000000000%,0,0\u000d\u000a2011-12-05,
             55672,site2.com,Fall 2011 C2 - targeted inv (145034),Fall 2011 Revenue CPM (61047),1.251000,417,0,.000000000000000000%,0,0\
             u000d\u000a2011-12-05,55672,site3.com,Fall 2011 C2 - targeted inv (145034),Fall 2011 Revenue CPM (61047),.003000,1,0,
             .000000000000000000%,0,0\u000d\u000a" ...,
            "url": "report-download?id=c52347fdcaabbb669b18f55c05698422"
        },
        "execution_status": "ready"
    }
}
```

### Use the download URL to save the report data to a file

You use the `"url"` field in the response to save the report data to a file. Simply make another `GET` call and identify the location and file that you want to save to. Be sure to use the file the extension of the `"format"` that you specified in your initial `POST` request.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=c52347fdcaabbb669b18f55c05698422' > /tmp/network_site_domain_performance.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
