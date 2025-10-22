---
title: Site Domain Performance Report
description: Use the Site Domain Performance report to view performance and optimization data by domain for a specific advertiser.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Site Domain Performance report

The Site Domain Performance report can be used to view performance and optimization data by domain for a specific advertiser.

> [!TIP]
> To view performance and optimization data by domain for multiple advertisers, use the [Network Site Domain Performance](./network-site-domain-performance.md) report.

For instructions on retrieving a report, please see [Report Service](./report-service.md) or see the [example](#example) below. For an advertiser user, the advertiser ID is detected based on the user's authentication. For a network user, however, this report requires specifying the advertiser ID as part of the URL, for example:

```
https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- yesterday
- last_7_days
- month_to_date
- month_to_yesterday

If you use the `start_date` and `end_date` fields to define the time range, the `start_date` must not be more than 45 days in the past. Since hourly data is not available for this report, `start_date` and `end_date` cannot be identical and must be formatted as `"YYYY-MM-DD"` rather than `"YYYY-MM-DD HH:MM:SS"`. Report data can be returned only for the UTC timezone.

### Data retention period

Data retention period for this report is 45 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | yes | `11/1/11` | The month and year (with the first day of the month). |
| `day` | date | yes | `11/16/11` | The day, month, and year. |
| `site_domain` | string | no | `bestsiteever.com - or - itunes.apple.com/app/app-name/id1234567` | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store.<br>There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| `campaign` | string | no | `ExampleCampaign (123456)` | The name of the campaign followed by the ID (Xandr format). |
| `campaign_id` | int | yes | `123456` | The ID of the campaign. |
| `campaign_code` | string | no | `CampaignCode` | The custom code for the campaign. |
| `campaign_name` | string | no | `ExampleCampaign` | The name of the campaign. |
| `campaign_priority` | int | no | `5` | The bidding priority of a campaign that targets direct inventory. For more information, see [Bidding Priority](../monetize/bidding-priority.md) in the UI documentation.<br>Possible values: `1` - `10`, where `10` is the highest priority. |
| `line_item` | string | no | `ExampleLineItem (323)` | The name of the line item followed by the ID (Xandr format). |
| `line_item_id` | int | yes | `323` | The ID of the line item. |
| `line_item_name` | string | no | `ExampleLineItem` | The name of the line item. |
| `campaign_group` | string | no | `ExampleCampaign(123)` | The name of the campaign group followed by the ID (Xandr format).<br><br>**Note**: `campaign_group` is a synonymous with `line_item`. |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null` . |
| `split_name` | string | yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `top_level_category_id` | int | yes | `19821` | The ID of the top content category assigned to the domain. This field may be `0` if the domain's `second_level_category` has no parent category. |
| `top_level_category_name` | string | yes | `"Shopping"` | The name of the top content category assigned to the domain. This field may be blank if the domain's `second_level_category` has no parent category. |
| `top_level_category` | string | yes | `"Shopping (19821)"` | The name and ID of the top content category assigned to the domain. This field may be blank if the domain's `second_level_category` has no parent category. |
| `second_level_category_id` | int | yes | `20129` | The ID of the second-level content category assigned to the domain.<br><br>**Note**: If the domain is an a top-level category, you should not request this dimension. |
| `second_level_category_name` | string | yes | `"Shoes"` | The name of the second-level content category assigned to the domain.<br><br>**Note**: If the domain is an a top-level category, you should not request this dimension. |
| `second_level_category` | string | yes | `"Shoes (20129)"` | The ID and name of the second-level content category assigned to the domain.<br><br>**Note**: If the domain is an a top-level category, you should not request this dimension. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about deals you have negotiated with sellers, see [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | The name of the deal followed by the ID (Xandr format). |
| `deal_code` | string | No | `"External seller deal code"` | The custom code for the deal. For deals with external supply partners, this is generally the string that you use to identify the deal. |
| `advertiser` | string | no | `ExampleAdvertiser (123)` | The name of the advertiser followed by the ID (Xandr format). |
| `campaign_group_name` | string | no | `ExampleGroupName` | The name of the campaign group |
| `advertiser_id` | int | yes | `123` | The ID of the advertiser. |
| `campaign_group_id` | int | no | `123` | The unique identification number of the campaign group |
| `advertiser_code` | string | no | `AdvertiserCode` | The custom code for the advertiser. |
| `advertiser_name` | string | no | `ExampleAdvertiser` | The name of the advertiser. |
| `buyer_member` | string | no | `MyNetwork (4567)` | The name of the buying member followed by the ID (Xandr format). |
| `buyer_member_id` | int | yes | `4567` | The ID of the buying member. |
| `buyer_member_name` | string | no | `MyNetwork` | The name of the buying member. |
| `supply_type` | string | Yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `'web'` <br> - `'mobile_app'` <br> - `'mobile_web'` |
| `mobile_application_id` | string | Yes | `‘343200656’ (iOS) or ‘com.rovio.angrybirds’ (Android)` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `mobile_application_name` | string | Yes | `Angry Birds` | The name of the mobile application as it appears in the Apple App and Google Play Stores. |
| `mobile_application` | string | No | `Angry Birds (com.rovio.angrybirds)` | The name of the mobile application followed by the ID (Xandr format). |
| `fold_position_id` | int | Yes | `0` | The ID of the fold position, i.e. where on the page the placement is located.<br>Possible values for impressions:<br>`0` = "unknown"<br>`1` = "above"<br>`2` = "below" |
| `fold_position` | string | Yes | `"Unknown"` | The fold position, i.e. where on the page the placement is located. For allowed values, see `fold_position_id`. |
| `age_bucket` | string | Yes | `"25-34"` | The bucket for the age of the user. See [Age Buckets](#age-buckets) below for possible values.<br><br>**Note**: For impressions older than 100 days, the `age_bucket` will be `"unknown"`. |
| `age_bucket_id` | string | No | `"3"` | The ID of the age bucket. See [Age Buckets](#age-buckets) below for possible values.<br><br>**Note**: For impressions older than than 100 days, the `age_bucket_id` will be `0`. |
| `gender` | string | Yes | `"m"`, `"f"`, `"u"` | The gender of the user.<br><br>**Note**: For impressions older than 100 days, `gender` will be `"u"`. |
| `is_remarketing` | int | Yes | `0`, `1` | If `1`, the campaign is remarketing. If `0`, the campaign is not remarketing.<br><br>**Note**: For impressions older than 100 days, `is_remarketing` will be `-1`. |
| `pixel_id` | int | yes | `1942` | The unique identification number of the conversion pixel.<br><br>**Note**: This dimension will return a maximum of 10 conversion pixels. Also, you can filter by no more than 10 conversion pixels. Although `pixel_id` is groupable, we do not recommend that you group by this dimension since doing so will cause conversion events to then be shown in separate rows from impression and click events. We generally assume you want to view all of these events in a single row so as to be able to retrieve accurate and aggregated values for conversion rate and cost-per-conversion calculations. As a result, we instead recommend that you filter by `pixel_id` so you can retrieve conversion counts and related metrics for your most relevant pixel IDs. |
| `operating_system_id` | int | Yes | `24` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_name` | string | Yes | `"Android 2.3.5 Gingerbread"` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_id` | int | Yes | `2` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_name` | string | Yes | `"Android"` | The ID of the operating system of the device.<br> - Use the [Operating System Family Service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended Service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
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
| `profit_ecpm` | money | `0.7778` | ((booked_revenue - media_cost) / imps) * 1000 | Profit (defined as booked revenue minus total cost) per 1,000 impressions. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue  | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |

## Age buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `0` | `"unknown"` |
| `1` | `"13-17"8` |
| `2` | `"18-24"` |
| `3` | `"25-34"` |
| `4` | `"35-44"` |
| `5` | `"45-54"` |
| `6` | `"55-64"` |
| `7` | `"65+"` |

## Example

### Create a JSON formatted report request

```
$ cat domain_performance

{
    "report":
    {
        "report_type": "site_domain_performance",
        "columns": [
            "day",
            "campaign",
            "booked_revenue",
            "imps",
            "clicks",
            "click_thru_pct",
            "site_domain"
        ]
        "report_interval": "last_7_days",
        "emails": ["js@mynetwork.com"],
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

In this example, we request execution of the report for advertiser `660`.

```
$ curl -b cookies -c cookies -X POST -d @domain_performance 'https://api.appnexus.com/report?advertiser_id=660'

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
            "created_on": "2011-11-16 23:51:14",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "fact-cache is off for report site_domain_performance",
            "json_request": "{\"report\":{\"report_type\":\"site_domain_performance\",\"columns\":[\"day\",\"campaign",
             "booked_revenue\",\"imps\",\"clicks\",\"click_thru_pct\",\"site_domain\"],\"report_interval\":\"last_7_days\",
             \"emails\":[\"js@mynetwork.com\"],\"filters\":[{\"buyer_member_id\":\"329\"},{\"advertiser_id\":\"660\"}]}}",
            "header_info": "Report type:,site_domain_performance\u000d\u000a,\u000d\u000aRun at:,2011-11-16 23:51:14\u000d\
             u000aStart date:,2011-11-09 00:00:00\u000d\u000aEnd date:,2011-11-16 00:00:00\u000d\u000aTimezone:,\u000d\
             u000aUser:,John Smith (9685)\u000d\u000a",
            "data": "day,campaign,booked_revenue,imps,clicks,click_thru_pct,site_domain\u000d\u000a2011-11-12,ExampleCampaign - 1
             (123456),.000000,24,0,.000000000000000000%,aaaa.com\u000d\u000a2011-11-13,ExampleCampaign - 2 (789012),.000000,9,0,
             .000000000000000000%,bbbb.net\u000d\u000a2011-11-12,ExampleCampaign - 3 (345678),.000000,2,0,.000000000000000000%,
             ccc.com\u000d\u000a2011-11-13,ExampleCampaign - 3 (345678),.000000,2,0,.000000000000000000%,cccc.de\u000du000a
             2011-11-14,ExampleCampaign - 3 (345678),.000000,10,0,.000000000000000000%,dddd.com\u000d\u000a2011-11-13,
             ExampleCampaign - 4 (901234), 2.574900,22,3,13.636363636363636364%,aaaa.com\u000d\u000a2011-11-15,ExampleCampaign - 3
             (345678),8.583000,2431,10,.411353352529823118%,abab.com\
             ...
            "url": "report-download?id=495d03a7667bac467bb488043ae336e9"
        },
        "execution_status": "ready"
    }
}
```

### Use the download URL to save the report data to a file

You use the `"url"` field in the response to save the report data to a file. Simply make another `GET` call and identify the location and file that you want to save to. Be sure to use the file the extension of the `"format"` that you specified in your initial `POST` request.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=495d03a7667bac467bb488043ae336e9' > /tmp/site_domain.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
