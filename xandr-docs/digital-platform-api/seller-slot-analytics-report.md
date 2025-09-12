---
title: Seller Slot Analytics Report
description: Use the Seller Slot Analytics report to view metrics for impressions within groups of ads delivered sequentially in between segments of non-commercial video programming.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Seller Slot Analytics report

> [!NOTE]
> This functionality currently is in **Alpha**. It is still under development and may be subject to change without notice. Contact your Xandr Account Representative to get it enabled.

The **Seller Slot Analytics report** shows metrics for impressions (slots) within groups of ads (pods) delivered sequentially in between segments of non-commercial video programming.

You can use this report to gain insight in answering the following questions:

- On average how many seconds per impression are being served for mid-roll slot positions 1, 2 and 3?
- How does the CPM of the first slot within a pre-roll compare to the first slot within a mid-roll?
- How many seconds has a brand served in pre-rolls compared to mid-rolls?
- Which slot positions is a line item delivering in?
- What is the percentage of slots by position being consumed by my house line item?
- Which cities did a line item deliver to?
- How does the completion rate by video context and slot position compare?

## Time frame

The `report_interva`l field in the JSON request can be set to one of the following:

- custom
- today
- yesterday
- last_7_days (not including today)
- month_to_date
- last_month
- quarter_to_date

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data in this report has the following retention period:
- Hourly retention: 100 days
- Daily retention: 500 days

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `application_id` | string | yes | `"platform.app"` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `advertiser_id` | int | yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| `advertiser_name` | string | no | `My Advertiser` | The name of the advertiser whose creative was served. |
| `advertiser` | string | no |`My Advertiser (789)` | The name of the advertiser followed by the ID (AppNexus format). |
| `ad_slot_position` | string | yes | `"Outro Bumper"` | The chronological order of an ad within its ad pod (placement set). |
| `advertiser_default_currency` | string | yes | `Member's default currency` | The default currency to be used for the advertiser. This will be a three-letter code that you can retrieve from the read-only [Currency Service](./currency-service.md). See [Currency Support](../monetize/currency-support.md) in the UI documentation for details about the concept.<br><br>As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience. |
| `advertiser_default_exchange_rate` | double | yes |  | The exchange rate on day of event. Rate is updated daily at 4 PM GMT. |
| `buyer_seat` | string | Yes | `My Buyer Seat (DSP Name)` | The display name for the buyer seat code. |
| `browser` | string | no | `webOS Browser (33)` | The name of the browser. |
| `billing_exchange_rate` | double | yes |  | Sourced **once daily** from [Refinitiv](https://www.lseg.com/en/fx) at approximately **3:00 a.m. UTC**. All Xandr applications (bidder, budgeting, billing, etc.) use the [API Currency Service](./currency-service.md) (also available to clients) to access the latest rates. |
| `bidder_id` | int | yes |  | The ID of the bidder. |
| `bidder_name` | string | no | `My Bidder and formatting` | The name of the bidder. |
| `buyer_member_id` | int | yes | `123` | The ID of the member who can buy the deal. A deal will either be set up with a buyer member ID or a buyer seat code. This is your Xandr member ID. |
| `buyer_member_name` | string | no | `"My Network"` | Display name of the buyer member. |
| `buyer_member` | string | no | `"My Network (123)"` | The name of the buying member followed by the ID (AppNexus format). |
| `brand_name` | string | no | `"The Best Wedding Music"` | Brand name associated with the creative. |
| `billing_currency` | string | yes | `"USD"` | The transaction currency that the buyer used to purchase this impression. This dimension is available only when Currency 2.0 is disabled. |
| `billing_exchange_rate` | double | yes |  | Sourced **once daily** from [Refinitiv](https://www.lseg.com/en/fx) at approximately **3:00 a.m. UTC**. All Xandr applications (bidder, budgeting, billing, etc.) use the [API Currency Service](./currency-service.md) (also available to clients) to access the latest rates. |
| `browser_id` | int | Yes | `8` | The ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service. |
| `brand` | int | yes | `1234` | The ID of the brand associated with a creative. |
| `buyer_seat_id` | double | yes |  | The ID of the buyer seat. |
| `buyer_seat_name` | string | yes | `My Buyer Seat (DSP Name)` | The display name for the buyer seat code. |
| `bidder` | string |  | `My DSP` | The name and ID of the bidder. |
| `creative_size` | string | yes | `1x1` | The width x height of the creative. |
| `country` | string | yes | `"France"` | The country of the user's location. |
| `content_category_name` | string | no | `"Games"` | The name of the content category. |
| `content_category` | string | no | `"Games (45)"` | The name of the content category followed by the ID (AppNexus format). |
| `creative_name` | string | no | `"Q1 2010 728x90"` | The name of the creative that served. |
| `creative` | string | no | `My Creative (123)` | The creative name and id. |
| `creative_duration` | int | no | `"10"` | The length of the ad in seconds. |
| `call_type` | string | yes | `ttj, ut, mob, ptv, openrtb` | The type of handler that was used to send the impression to Xandr. |
| `city_name` | string | no | `"Abenberg"` | The name of the city. |
| `content_network_id` | int | yes |  | The network delivering the video content. |
| `content_language_id` | int | yes |  | The language in which the content is being streamed. |
| `content_genre_id` | int | yes | `771` | The ID of the main genre of the program on which the ad will be played. For example, `Game-Show`, `History`, `Music`. |
| `content_program_type_id` | int | yes | `987` | The ID of higher level categorization of the program on which the ad will be played. For example, `Movie`, `Series`, `Special`, `Show`, `Event`, `Clip`. |
| `content_rating_id` | int | yes | `322` | The ID of type of rating of the content. For example, `All`, `Children (7+)` , `Teens (13+)`, `Young Adults (14+)`, `Adults (18+)`. |
| `content_delivery_type_id` | int | yes | `889` | The ID for the type of streaming content delivery. For example, `Live`, `Video On Demand (VOD)`. |
| `creative_width` | int | yes |  | The width of the creative. |
| `creative_height` | int | yes |  | The height of the creative. |
| `content_category_id` | int | yes |  | Users can optionally specify a primary [content category](./content-category-service.md) for a placement. This category can be used for targeting and will appear in reports. Content categories can be set either at the Site level or the Placement level, but not both. |
| `city` | int | yes |  | The read-only City Service allows you to see information about the cities registered in the Xandr system, including the region, designated market area, and country to which each city belongs. |
| `creative_id` | int | yes |  | **Owner Phase**: The ID of the creative to use as the new default creative for the impression.<br>**Non-owner phase**: The ID of the creative that is submitted as part of the member's bid for the impression. |
| `creative_size` | string | no |  | The creative sizes included in the package. For more details, see [Sizes] in [Package Buyer Access Service](../bidders/package-buyer-access-service.md). |
| `deal_id` | int | yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | no | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | no | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated**. |
| `day` | string | yes | `"2010-02-01"` | The day on which the impression occurred. |
| `device_type` | string | yes | `"set top box"` | The type of device on which the impression was served. Possible values are:<br>`0` = Other Devices<br>`1` = Desktops and Laptops<br>`2` = Mobile Phones<br>`3` = Tablets<br>`4` = TV<br>`5` = Game Console<br>`6` = Media Players<br>`7` = Set Top Box |
| `external_deal_code` | string | yes | `"This is a deal code"` | The deal code for a deal, if included in the request. To retrieve deal codes, use the [Deal Service](./deal-service.md). |
| `geo_region` | string | yes | `L6` | The region or state code code (Federal Information Processing Standard) of the user's location. For example CA for California and L6 for Shropshire. |
| `geo_country` | string | yes | `"US"` | The code of the geographical country associated with the impression. |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country associated with the impression. |
| `hour` | int | yes | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>For impressions older than 100 days, the day will be returned rather than the hour. |
| `inventory_url_id` | int | yes | `99999` | The ID of the URL of the domain or app on which the request originated. |
| `insertion_order` | string | yes | `"Insertion Order (321)"` | The name of the Insertion Order. |
| `impression_type` | string | yes | `Resold (6)` | The ID for the type of impression. Possible values (associated types in parentheses):<br> `1`("Blank"): No creative served.<br>`2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>`3` ("Default Error"): A default creative served due to a timeout issue.<br>`4` ("Default"): A default creative served because there were no valid bids.<br>`5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>`6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>`7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>`8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>`9` ("External Impression"): An impression from an impression tracker.<br>`10` ("External Click"): A click from a click tracker. |
| `inventory_url` | string | no |  | The URL of the inventory or application package. |
| `insertion_order_id` | int | yes | `1234` | The ID of the Insertion Order |
| `insertion_order_name` | string | no | `"Insertion Order Name"` | The name of the insertion order. |
| `insertion_order` | string | no | `"Insertion Order Name (654)"` | **Deprecated**. |
| `imp_type` | string | yes | `"Blank"` | The type of impression. For possible values, see `imp_type_id` . |
| `inventory_url_name` | string | no |  | The URL of the inventory or application package. |
| `inventory_url` | string | no |  | URL of the app or domain once it has been validated. |
| `line_item_name` | string | no | `"LineItemDEF"` | The name of the line item that served the impression. |
| `line_item` | string | no | `"Default Line Item (111)"` | The name of the line item followed by the ID (AppNexus format). |
| `language` | string | yes |`German (6)` | The language of the creative. |
| `language_id` | int | yes |  | The ID of the language. You can use the [Language Service](./language-service.md) to retrieve language IDs. |
| `month` | string | yes | `"2010-02"` | The month in which the impression occurred. |
| `member_currency` | string | yes |  | The currency associated with the curator member's seat. |
| `member_exchange_rate` | double | yes |  |  |
| `max_vast_version` | string | yes |  | Filter only. Sets the maximum publisher player VAST version for inventory to be included in the report. |
| `max_number_ads` | int | yes |  | The maximum number of ads that are allowed to be played on the placement. If `maximum_number_ads` is > 1, then the placement can be an ad pod (a linear grouping of more than one ad designed to fill a single placement). |
| `max_duration` | int | yes |  | The maximum duration of a video ad that is allowed to be played on the placement.<br> - If `maximum_number_ads` is > 1, then the max duration applies to the entire length of an ad pod (a linear grouping of more than one ad designed to fill a single placement).<br> - This field must be set in order to enable ad pods. |
| `operating_system` | string | no | `"Android 2.3.5 Gingerbread"` | The name and ID of an operating system under an operating system family on which devices run. For example, Android 8.1, Oreo 9.0 Popsickle under Android Operating System Family, iOS 8.1, 9.0 under Apple iOS family, etc. |
| `operating_system_name` | string | no | `"Android 2.3.5 Gingerbread"` | The name of the operating system. |
| `operating_system_family_name` | string | no | `"Android"` | The name of the operating system family associated with the device the impression was served on.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_id` | int | yes | `24` | The ID of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_id` | int | yes | `2` | The ID of the operating system family associated with the device the impression was served on.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family` | string | no | `Android, Apple Mac, Apple iOS, Microsoft Windows` | The name and ID of the supported operating system family on which the devices run. |
| `player_size` | string | no | `1920x1080` | The size of the video player. |
| `placement_group` | string | yes | `My Placement Group` | The placement group name. |
| `placement_set_id` | int | yes | `1234` | The ID of the placement set. |
| `publisher_currency` | string | yes | `"EUR"` | The default currency of the publisher in this impression. This dimension is available only when Currency 2.0 is disabled. |
| `placement_id` | int | yes | `456` | The ID of the placement.<br><br>For RTB impressions older than 30 days, and for non-RTB impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | no | `"Photos 728x90"` | Display name of the placement.<br><br>For impressions older than 100 days, placements are aggregated into one row with a generic `placement_name`. |
| `placement` | string | no | `"Ivillage 160x600 (456)"` | The name of the placement followed by the ID (AppNexus format). |
| `publisher_id` | int | yes | `374967` | The ID of the publisher that owns the inventory. |
| `publisher_name` | string | no | `"Publisher XYZ"` | The name of the publisher that owns the inventory. |
| `publisher` | string | no | `"Facebook (321)"` | The name of the publisher followed by the ID (AppNexus format). |
| `playback_method` | string | yes |`"auto-play, sound on"` | The playback method for the creative, e.g, `'auto-start, sound on'`. |
| `publisher_exchange_rate` | double | yes |  | The exchange rate (publisher currency: USD) on the day of the transaction. |
| `player_width` | int | yes |  | The default width of the player. This field is mandatory. If the width is zero, the `autoInitialSize` option will not automatically set the width of the player on the page. |
| `player_height` | int | yes |  | Parameter recommended to ensure video bidders receive height on bid requests. |
| `placement_set_id` | int | yes |  | The placements that are associated with the placement set. |
| `slot_type` | string | yes | `Standard Slot, 1` | The ID of the type of position (ad or bumper) within an ad pod.<br> `0` - normal slot <br> `1` - intro bumper <br>`2` - outro bumper |
| `slot_position` | int | yes | `3` | The position of the ad in the sequence of the pod. |
| `support_vpaid` | string | yes | `Boolean` |  |
| `site_name` | string | no | `"Site Name"` | The name of the site on which the placement is used. |
| `site` | string | no | `"Site Name (194)"` | The name of the site followed by the ID (AppNexus format). |
| `site_id` | int | yes | `555` | The ID of the site. For more information, see the [Site Service](./site-service.md). |
| `seller_member_id` | int | yes | `567` | The internal ID of the selling member. |
| `supply_type` | string | yes | `mobile_web` | The type of supply. Possible values:<br>`0` = WEB<br>`1` = MOBILE_WEB<br>`2` = MOBILE_APP<br>`5` = TOOLBAR |
| `video_context` | string | yes |`Pre-Roll, "3"` | The type of the video creative. See `video_context` below for possible values. |
| `video_content_rating` | string | no | `"teens"` | The publisher-identified audience group for which the content is rated, for example, `All`, `Children (7+)`, `Teens (13+)`, `Young Adults (14+)`, or `Adults (18+)`. |
| `video_content_delivery_type` | string | no | `"vod"` | The type of streaming content delivery: `Video on Demand (VOD)` or `Live`. |
| `video_content_program_type` | string | no | `"vod"` | The format of the video program, for example, `Movie`, `Series`, `Special`, `Show`, `Event`, or `Clip`. |
| `video_delivery_type` | string | no | `"vod"` | The type of streaming content delivery. For example, `Video On Demand (VOD)` and `Live`. |
| `video_content_genre` | string | no | `"action"` | The main genre of the program in which the ad will be played. For example, `Action`, `Adventure`, `Biography`, `Business`, `Comedy`, etc. |
| `video_program_type` | string | no | `"series"` | The higher level categorization of the video program's format on which the ad will be played. For example, `Movie`, `Series`, `Special`, `Show`, `Event`, `Clip`, etc. |
| `video_content_network` | string | no | `"AMC"` | The network delivering the video content. For example, `9 Story`, `CBC`, `Disney`, `AMC`, `Fox`, etc. |
| `video_content_language` | string | no | `"Spanish"` | The language of the video program in which ad will be played. For example, `Spanish`. |
| `video_content_duration` | int | yes | `100` | The length of the video content in seconds. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `ad_requests` | int |  |  | The total number of ad requests sent to Xandr. (Filtered Requests + Imps (kept) + Imps (resold) + Defaults + Video Player Errors + Video Default Errors + Bid Sent No Responses + Default No Responses + PSAs or Blanks). |
| `ad_responses` | int |  |  | The total number of ad responses counted within Xandr. (Imps (kept) + Imps (resold) + Video Player Errors + Bid Sent No Responses). |
| `booked_revenue_dollars` | money | `16.3519` | booked_revenue_dollars | The total revenue booked through direct advertisers (line item). |
| `click_through_rate` | double |  | Click-Through Rate = The Number of Clicks to Date ÷ The Number of Impressions Delivered to Date | The rate or frequency at which users click on a digital creative and arrive at its landing page. |
| `clicks` | int | `576` | clicks | The total number of clicks across all impressions. For Microsoft Invest, clicks from all media types are supported. For external DSPs, only clicks from Native and Video media types are supported. |
| `cpm` | money | `30.5` | total_revenue / imps * 1000 | The total revenue (booked revenue +reseller revenue) divided by the number of imps multiplied by 1000. |
| `completion_rate` | double | `0.85` | video_completions / impressions | The ratio of video ad completions to impressions, expressed as a percentage. |
| `completions` | int | `12` |  | The total number of times the video creatives played for the entire duration. |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. |
| `error_rate` | double | `0.01` | errors / impressions | The rate of errors per impression. |
| `errors` | int | `2` |  | The total number of times a video error occurred. |
| `first_quartile_rate` | double | `9101` | first_quartiles | The number of times the video player reported a 25% complete event. |
| `first_quartiles` | int | `9101` | first_quartiles | The number of times the video player reported a 25% complete event. |
| `impression_seconds` | int | `6976` | creative_duration * imps | The total number of seconds served on impressions. If you are using a house line item to report unsold opportunities then you may wish to filter or add impression type as a dimension to separate sold and unsold impression seconds. |
| `imps` | int | `2340` | imps | The total number of impressions. For video ads, the video player would normally count an impression when the first frame of the video is loaded. |
| `reseller_revenue_dollars` | money | `23.9442` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `revenue_per_complete` | money | `5.43` | (booked_revenue + reseller_revenue) / completions | The revenue divided by the number of completions. |
| `revenue_per_minute_sold` | money | `3.55` | sum(reseller_revenue_dollars + booked_revenue_dollars) * 60 / sum(creative_duration * imps) | The revenue the ad delivered per minute. |
| `revenue_per_second_sold` | money | `0.23` | total_revenue / impression_seconds | The total revenue per second sold. |
| `revenue_per_click` | money | `0.20` | total_revenue / clicks | The revenue generated per click event recorded. |
| `responses_seconds` | int | `63424` | creative_duration * responses | The total seconds of demand Xandr received for the auctions it holds for demand. |
| `revenue_per_minute_sold` | money | `3.55` | sum(reseller_revenue_dollars + booked_revenue_dollars) * 60 / sum(creative_duration * imps) | The revenue the ad delivered per minute. |
| `seconds_per_imp` | double | `15.78` | sum(creative_duration * imps) / sum(imps) | The total creative duration. |
| `seconds_per_impression` | double | `15.78` | sum (creative_duration * imps) / sum (imps)  | The total creative duration. |
| `starts` | int | `9236` | starts | The total number of times the first segment of the video creative was downloaded and started. |
| `second_quartiles` | int | `8912` | second_quartiles | The number of times the video player reported a 50% complete event. |
| `start_rate` | double | `0.98` | starts / impressions | The percentage of times the first segment of the video creative was downloaded and started. |
| `skip_rate` | double | `0.01` | skips / impressions | The number of skips divided by the number of impressions recorded. |
| `second_quartile_rate` | double | `0.90` | second_quartiles / video_starts | The number of second quartiles fired by the video player divided by the number of start events. |
| `started_video_completion_rate` | double | `0.98` | video_completions / video_starts | The number of video starts that resulted in a completion. |
| `skips` | int | `10` | skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `slot_cpm` | money |  |  |  |
| `second_quartile_rate` | double | `8912` | second_quartiles | The number of times the video player reported a 50% complete event. |
| `total_revenue` | money | `25.78435` | booked_revenue + reseller_revenue | The total resold and booked revenue. |
| `third_quartiles` | int | `8646` | third_quartiles | The number of times the video player reported a 75% complete event. |
| `third_quartile_rate` | double | `0.87` | third_quartiles / video_starts | The number of third quartiles fired by the video player divided by the number of start events. |
| `the_total_revenue` | money | `450.00` | booked_revenue | The total revenue. |
| `25_pcts` | int | `10` |  | The total number of times the video creatives completed 25% of the entire duration. |
| `50_pcts` | int | `10` |  | The total number of times the video creatives completed 50% of the entire duration. |
| `75_pcts` | int | `10` |  | The total number of times the video creatives completed 75% of the entire duration. |
| `Average View Time` | int | `28` | sum (creative_duration * ((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions)) / sum (starts)) | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| `Average View Time Percent` | percentage | `89%` | sum (((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions))∕starts) | The average view time expressed as a percentage of the total possible view time. |

## Example

The JSON file should include the `report_type` of `"seller_slot_video_report_network"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

### Create a JSON report request

```
$ cat seller_slot_video_report_network
 
{"report":
    {
        "report_type":"seller_slot_video_report_network",
        "columns":[
            "Buyer_Member",
            "video_content_network",
            "Video_Context",
            "placement_name",
            "Billing_Currency",
            "ad_responses",
            "click_through_rate",
            "responses_seconds",
            "seconds_per_imp",
            "started_video_completion_rate",
            "revenue_per_complete",     
        ],
        "report_interval":"last_7_days",
        "format":"csv"
    }
}
```

### `POST` the JSON request to get back a report ID

```
$ curl -b cookies -X post -d @seller_slot_video_report_network "https://api.appnexus.com/report?seller_member_id=123"
 
{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

### Retrieve the status of the report

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'
 
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2023-02-03 20:09",
         "json_request": "{\"report\":{\"report_type\":\"seller_slot_video_report_network\",
             \"columns\":[\"day\",\"seller_member_id\",
             \"call_type\",\"url\",\"ad_requests_gdpr_country\",\"ad_requests_gdpr_applied_valid_consent_string\",\"ad_requests_gdpr_applied_blank_consent_string\",
             \"ad_requests_gdpr_applied_valid_consent_string_tcf_version_2\",\"pct_ad_requests_gdpr_country_gdpr_applied\",
             \"pct_ad_requests_gdpr_applied_valid_consent_string\",\"pct_ad_requests_gdpr_applied_blank_consent_string\",
             \"pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_2\"],
             \"report_interval\":\"last_7_days\",\"format\":\"csv\",\"filters\":[{\"seller_member_id\":\"123\"}]}}",
             "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### Download the report

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/seller_slot_video_report_network.csv
```

> [!NOTE]
>
> - If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.
> - There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
