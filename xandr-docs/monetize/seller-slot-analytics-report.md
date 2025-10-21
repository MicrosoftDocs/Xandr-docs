---
title: Seller Slot Analytics
description: The Seller Slot Analytics report shows metrics for impressions within groups of ads delivered sequentially in between segments of non-commercial video programming. Learn how to run this report in this page.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Seller slot analytics

> [!NOTE]
> This functionality currently is in **Alpha**. It is still under development and might change without notice. Contact your Microsoft Advertising Account Representative to get enabled.

The Seller Slot Analytics report shows metrics for impressions (slots) within groups of ads (pods) delivered sequentially in between segments of non-commercial video programming. You can use this report to gain insight in answering the following questions:

- On average how many seconds per impression are being served for mid-roll slot positions 1, 2 and 3?
- How does the CPM of the first slot within a pre-roll compare to the first slot within a mid-roll?
- How many seconds has a brand served in pre-rolls compared to mid-rolls?
- Which slot positions is a line item delivering in?
- What is the percentage of slots by position being consumed by my house line item?
- Which cities did a line item deliver to?
- How does the completion rate by video context and slot position compare?

## Navigation

1. Go to **Reporting** > **Report Center** and click **Create New**
2. In **Search for a Report** search box, type the report name
3. The relevant report widget will be shown under its category such as **Analytics**, **Troubleshooting** or **Reach**.
4. Click on **Create new report** button to create the new report.

## Time frame

The report_interval field in the JSON request can be set to one of the following:

- `custom`
- `today`
- `yesterday`
- `last 7 days(not including today)`
- `month to date`
- `last month`
- `quarter to date`

To run a report for a custom time frame, set the `Start Date` and `End Date`fields in your report request. For more details about these fields, see [Report Service](../bidders/report-service.md).

**Data Retention**

This report's data is retained for 420 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|--|--|--|--|--|
| Advertiser | string | yes | `"Verizon Wireless (789)"` | The name of the advertiser. |
| Advertiser Default Currency | string | no | `EUR` | The default currency of the advertiser in this impression. This dimension is available only when Currency 2.0 is disabled. |
| Application | string | no |  | The application name. |
| Application ID | string | yes | `"platform.app"` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| Bidder | string | no | `My DSP` | The name of the bidder. This is normally the external DSP or Prebid Server. |
| Billing Currency | string | yes | `USD` | The transaction currency that the buyer used to purchase this impression. This dimension is available only when Currency 2.0 is disabled. |
| Billing Exchange Rate (removed from report) | double | yes |  |  |
| Brand | string | yes | `My Brand Name` | The brand name. |
| Browser | string | no | `webOS Browser (33)` | The name of the browser. |
| Buyer Member | string | yes | `My Buyer` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: 229 = PSA, 0 = Blank, or 319 = Default. |
| Buyer Seat | string | yes | `My Buyer Seat (DSP Name)` | The display name for the buyer seat code. |
| Call Type | string | no | `ttj`, `ut`, `mob`, `ptv`, `openrtb` | The type of handler that was used to send the impression to Microsoft Advertising (e.g., ttj, ut, mob, ptv, openrtb). |
| City | string | yes | `Vienna` | The city in which the user is located. |
| Country | string | yes | `"France"` | The country/region of the user's location, both name and code, in the format "France". The string "250" can appear in cases where we don't know the country/region or if the country/region doesn't map correctly to a location in our database. |
| Creative | string | yes | `My Creative` | The creative name. |
| Creative Size | Int |  | `1x1` | The height of the creative. |
| Deal | string | yes | `My Deal` | The deal name for deals set up in Microsoft Advertising. |
| Device Type | string | yes | `"set top box"` | The type of device on which the impression was served. Possible values are:<br> - "desktops & laptops"<br> - "tablets"<br> - "mobile phones"<br> - "tv"<br> - "game consoles"<br> - "set top box"<br> - "media players"<br> - "other devices" |
| External Deal Code | string | no | `A857249` | The deal code from the external SSP for imps sold via prebid server. |
| Geo Region | string | yes | `L6` | The region or state code code (Federal Information Processing Standard) of the user's location. For example CA for California and L6 for Shropshire. |
| Impression Type | string | yes | `Resold (6)` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - 1 ("Blank"): No creative served.<br> - 2 ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br> - 3 ("Default Error"): A default creative served due to a timeout issue.<br> - 4 ("Default"): A default creative served because there were no valid bids.<br> - 5 ("Kept"): Your advertiser's creative served on your publisher's site.<br> - 6 ("Resold"): Your publisher's impression was sold to a third-party buyer.<br> - 7 ("RTB"): Your advertiser's creative served on third-party inventory.<br> - 8 ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br> - 9 ("External Impression"): An impression from an impression tracker.<br> - 10 ("External Click"): A click from a click tracker. |
| Insertion Order | string | yes | `"Insertion Order (321)"` | The name of the Insertion Order. |
| Inventory URL | string | No |  | The URL of the inventory or application package. |
| Language | string | yes | `German (6)` | The language of the creative. |
| Line Item | string | yes | `"Default Line Item (111)"` | Line Item Name. |
| Max Duration | int | no |  | Max duration of the pod the slot served in. |
| Max Number Ads | int | no |  | The maximum number of ads for the pod the slot served in. |
| Max VAST Version | int | no |  | The max VAST version supported for the slot. |
| Member Currency | string | no |  | The currency of the member. |
| Operating System | string | yes | `"Android 2.3.5 Gingerbread"` | The name of the operating system. |
| Operating System Family | string | yes | `"Android"` | The name of the operating system family. |
| Placement | string | yes | `My Placement` | The placement name. |
| Placement Group | string | yes | `My Placement Group` | The placement group name. |
| Placement Set ID | int | yes | `1234` | The ID of the placement set. |
| Playback Method | string | yes | `auto_play_sound_on` | The playback method for the creative, e.g, 'auto-start, sound on'. |
| Player Size | string | no | `1920x1080` | The size of the video player. |
| Publisher | string | yes | `My Publisher` | The publisher name. |
| Publisher Currency | string | yes | `"EUR"` | The default currency of the publisher in this impression. This dimension is available only when Currency 2.0 is disabled. |
| Slot Position | int | yes | `3` | The position of the ad in the sequence of the pod. |
| Slot Type | yes | string | `Standard Slot` | The type of position (ad or bumper) within an ad pod. |
| Supply Type | string | yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are 'web', 'mobile_app', and 'mobile_web'. |
| Support VPAID |  | Boolean |  |  |
| Video Content Delivery Type | no | string |  | The type of streaming content delivery: Video on Demand (VOD) or Live. |
| Video Content Durations | no | string |  | The length of the video content in seconds. |
| Video Content Genre | no | string |  | The main genre of the program on which the ad will be played. For example, Cooking, Horror, News, or Football. |
| Video Content Language | no | string |  |  |
| Video Content Program Type | no | string |  | The format of the video program, for example, Movie, Series, Special, Show, Event, or Clip. |
| Video Content Rating | no | string |  | The publisher-identified audience group for which the content is rated. For example, All, Children (7+) , Teens (13+), Young Adults (14+), or Adults (18+). |
| Video Context | string | yes | `Pre-Roll` | The type of the video creative. For more possible values, see [Video Context](../digital-platform-api/network-advertiser-video-analytics.md#video-context) |

## Metrics

| Column | Type | Example | Formula | Description |
|--|--|--|--|--|
| Average View Time | int | `28` | sum (creative_duration * ((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions)) / sum (starts)) | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| Average View Time Percent | percentage | `89%` | sum (((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions))∕starts) | The average view time expressed as a percentage of the total possible view time. |
| Booked Revenue Dollars | money | `16.3519` | booked_revenue | The total revenue booked through direct advertisers (line item). |
| Click Through Rate | double | `1.23` | clicks / imps | The rate of clicks to impressions. |
| Clicks | int | `576` | clicks | The total number of clicks across all impressions. For Invest DSP, clicks from all media types are supported. For external DSPs, only clicks from Native and Video media types are supported. |
| Completion Rate | double | `0.85` | video_completions / impressions | The number of impressions that resulted in a completion. |
| Completions | int | `8458` | completions | The number of times the video player reported a completion event. |
| CPM | money | `30.5` | total_revenue / imps * 1000 | The total revenue (booked revenue +reseller revenue) divided by the number of imps multiplied by 1000. |
| Error Rate | double | `0.01` | errors / impressions | The rate of errors per impression. |
| First Quartile Rate | double | `0.94` | first_quartiles / video_starts | The number of first quartiles fired by the video player divided by the number of start events. |
| First Quartiles | int | `9101` | first_quartiles | The number of times the video player reported a 25% complete event. |
| Impression Seconds | int | `6976` | creative_duration * imps | The total number of seconds served on impressions. If you are using a house line item to report unsold opportunities then you may wish to filter or add impression type as a dimension to separate sold and unsold impression seconds. |
| Imps | int | `2340` | imps | The total number of impressions. For video ads, the video player would normally count an impression when the first frame of the video is loaded. |
| Reseller Revenue Dollars | money | `23.9442` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| Revenue Per click | money | `1.56` | total_revenue / clicks | Total revenue per click. |
| Revenue Per Complete | money | `5.43` | (booked_revenue + reseller_revenue) / completions | The revenue divided by the number of completions. |
| Revenue Per Minute Sold | money | `3.55` | sum(reseller_revenue_dollars + booked_revenue_dollars) * 60 / sum(creative_duration * imps) | The revenue the ad delivered per minute. |
| Revenue Per Second Sold | money | `0.23` | total_revenue / impression_seconds | The total revenue per second sold. |
| Second Quartile Rate | double | `0.90` | second_quartiles / video_starts | The number of second quartiles fired by the video player divided by the number of start events. |
| Second Quartiles | int | `8912` | second_quartiles | The number of times the video player reported a 50% complete event. |
| Seconds Per Impression | double | `15.78` | sum(creative_duration * imps) / sum(imps) | The total creative duration. |
| Skip Rate | double | `0.01` | skips / impressions | The number of skips divided by the number of impressions recorded. |
| Skips | int | `85` | skips | The number of times the video player reported a skip event. |
| Start Rate | double | `0.98` | starts / impressions | The number of starts divided by the number of impressions recorded. |
| Started Video Completion Rate | double | `0.98` | video_completions / video_starts | The number of video starts that resulted in a completion. |
| Starts | int | `9236` | starts | The number of times the video player reported a start event. |
| Third Quartile Rate | double | `0.87` | third_quartiles / video_starts | The number of third quartiles fired by the video player divided by the number of start events. |
| Third Quartiles | int | `8646` | third_quartiles | The number of times the video player reported a 75% complete event. |
| Total Revenue | money | `25.78435` | booked_revenue + reseller_revenue | The total resold and booked revenue. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured), or, from the Publishers top menu, click on **Prebid Server Premium** \> **Analytics** \> **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.
