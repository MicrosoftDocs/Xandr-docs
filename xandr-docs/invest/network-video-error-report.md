---
title: Microsoft Invest - Member Video Error Report
description: Use the Member Video Error report to get insight into video errors and their cause.
ms.date: 10/28/2023
---

# Microsoft Invest -  Member Video Error report

The Member Video Error Report gives insight into video errors and their cause.

You can use this report to troubleshoot video settings and eliminate errors relating to buy- and sell-side video advertising. [VAST 3 error codes](https://wiki.iabtechlab.com/index.php?title=VAST_Error_Code_Troubleshooting_Matrix) provide further insight into the source of errors.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports. However, all time ranges are not available for every report.

- Custom
- Current Hour
- Last Available Day
- Last Hour
- Today
- Last 24 Hours
- Last 48 Hours
- Yesterday
- Last 2 Days
- Last 7 Days
- Last 7 Available Days
- Last 14 Days
- Last 14 Available Days
- Last 30 Days
- Last 30 Available Days
- Last Month
- Last 100 Days
- Last 365 Days
- Quarter to Date
- Month to Date
- Month to Yesterday
- Lifetime

### Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

> [!NOTE]
> For impressions older than 100 days, the day will be returned rather than the hour.


### Data retention period

Data in this report has the following retention period:

- Hourly retention: 100 days
- Daily retention: 500 days


## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, select the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.

For all revenue fields, the currency is defined by the **Buying Currency** field.

| Column | Filter? | Description |
|:---|:---|:---|
| Only include results where a Deal is present | N | Determines whether results are limited to deals only. |
| Advertiser | Y | The name of the advertiser associated with the impression. |
| Insertion Order | Y | The name of the insertion order associated with the impression. |
| Line Item | Y | The name of the line item associated with the impression. |
| Campaign | Y | The name of the campaign associated with the impression. (Does not apply to all advertisers.) |
| Deal | Y | The name of the deal associated with the impression. |
| Creative | Y | The name of the creative served. |
| Publisher | Y | The name of the publisher associated with the impression. |
| Placement Group | Y | The name of the placement group associated with the impression. |
| Placement | Y | The name of the placement associated with the impression. |
| Ad Request Call Type | N | The type of handler that was used to send the impression to Microsoft Advertising (e.g., `vmap`, `ut` , `mob` , `ptv` , `openrtb` ). |
| Site Domain | Y | The ID of the user's mobile app. |
| Application ID | N | The ID of the mobile app on the device where the impression occurred. |
| Device Type | Y | The type of device where the impression occurred. |
| Impression Type | Y | The type of impression. An integer value which translates as follows: <br> - `1` = Blank <br> - `2` = PSA <br> - `3` = Default Error <br> - `4` = Default <br> - `5` = Kept <br> - `6` = Resold <br> - `7` = RTB <br> - `8` = PSA Error <br> - `9` = External Impression <br> - `10` = External Click |
| Video Context | Y | When and where the video ad plays – pre-roll, mid-roll, post-roll, or outstream. |
| Video Playback Method | Y | The playback method for the creative, for example ' Autoplay, Sound On'. |
| Video Player Size | Y | The size of the player based on width in pixels, e.g., 'small', 'medium', 'large'. |
| Creative Duration | N | The length of the video creative, in seconds. |
| Bidder Name | N | The name of the bidder associated with the impression. |
| Buyer | N | The name of the buyer associated with the impression. |
| Country | Y | The country in which the impression took place. |
| Seller | N | The name of the seller associated with the impression. |
| Supply Type | Y | The supply type for the impression - Web, Mobile Web, or Mobile App. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|:---|:---|
| Imps | The total number of impressions. Note that for a video, an impression occurs when the first frame of the creative plays. |
| Imps (default) | Impressions where a default creative served because there were no valid bids. |
| Imps (kept) | The number of impressions in which a managed advertiser's creative serves on the managed publisher's site. |
| Imps (resold) | The total number of resold impressions. |
| Imps (RTB) | The total number of RTB impressions. |
| Clicks | The total number of clicks associated with the video ad. |
| CTR | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| Revenue | The total revenue for all video ad completion |
| Revenue per Complete | The revenue per video completion |
| Total RPM | The total reported revenue for the placement. |
| Cost | The total cost of impressions for the buyer. |
| CPM | The cost per mille (CPM) for the impressions. |
| Cost per Complete | The cost to the buyer per video completion. |
| VAST Error Rate | The rate of vast errors for the video player, expressed as a percentage. |
| Ads Served | The total number of creative responses returned in response to a bid request. (Note that for a video, this does not equal an impression, because the first frame may or may not have been played.) |
| Total Error Count | The total number of VAST errors for the video player. |
| VAST 100 Error Count | Indicates XML parsing error on the placement. Possible causes include: <br> - VAST supplied in adm is not a valid XML document. <br> - URL supplied in nurl does not resolve to a valid XML document. <br> - Nurl only: Server did not respond with VAST, or at all when player called the nurl.<br> - Perhaps a CORS issue |
| VAST 101 Error Count | Indicates VAST schema validation error on the placement. This means that the VAST validates as XML, but does not validate per the VAST schema (in other words there are missing mandatory elements or attributes, or combinations of elements/attributes that are not permissible).<br>Some possible reasons for invalidity: <br> - In-line and wrapper both present. <br> - AdTagURI missing in wrapper element. <br> - Duration missing. <br> - Missing ad node or MediaFile node. <br> - Offset attribute on progress event is missing or not a valid value. |
| VAST 102 Error Count | Indicates that the VAST version of response is not supported. Possible causes: <br> - Bidder did not respect the VAST version(s) listed in the bid request.<br> - Exchange is sending wrong VAST version(s) in bid request. <br> - VAST does not contain version (this could also be considered a schema validation issue) |
| VAST 200 Error Count | Indicates a trafficking error. Possible causes: <br> - Layer wanted Skippable Linear, but got back Linear.<br> - Player wanted Linear, but got back Skippable Linear.<br> - For Skippable Linear, skipoffset doesn't meet publisher expectations.<br> - Bidder did not respect the skippability/skipoffset in the bid request. <br> - Exchange is sending wrong skippability/skipoffset in the bid request. <br> - Potentially any of the reasons in 201-203 |
| VAST 201 Error Count | The number of errors caused by the video player expecting different linearity. For more information see IAB's [VAST documentation](https://www.iab.com/wp-content/uploads/2016/04/VAST4.0_Updated_April_2016.pdf). |
| VAST 202 Error Count | The number of errors caused because the video player was requires a different video duration. For example, if a player is set up to play only 15-second video creatives and receives a 30-second creative from the buyer, the creative won't serve. In addition, creatives that are too short to fill the video duration may not serve unless the player allows ad podding and the total duration of videos in the ad pod fits the required duration. |
| VAST 203 Error Count | The number of errors that occurred because the video player was expecting a different size. |
| VAST 300 Error Count | The number of errors caused by a general wrapper error. |
| VAST 301 Error Count | The number of errors caused due to the timeout of the VAST URI provided in the wrapper element, or of VAST URI provided in a subsequent wrapper element. This includes request errors such as invalid URI, unreachable or request timeout for URI, and security or other exceptions related to requesting a VAST URI. |
| VAST 302 Error Count | The number of errors caused because the wrapper limit was reached, as defined by the video player. Too many Wrapper responses have been received with no in-line response. |
| VAST 303 Error Count | The number of errors caused due to no VAST response after one or more wrappers. Also includes the number of empty VAST responses from fallback (waterfall handling). |
| VAST 400 Error Count | The number of general linear errors, generally because the video player is unable to display the linear ad. |
| VAST 401 Error Count | The number of errors caused because the file was not found when the player was unable to find Linear/MediaFile in the URI. |
| VAST 402 Error Count | The number of errors due MediaFile URI timeouts. |
| VAST 403 Error Count | The number of errors caused because the video player can't find a media file whose attributes it supports. |
| VAST 405 Error Count | The number of errors caused due to a problem displaying the media file. |
| VAST 500 Error Count | The number of general NonLinearAds errors. |
| VAST 501 Error Count | The number of errors caused due to creative dimensions that do not align with creative display area (i.e., creative dimension too large). |
| VAST 502 Error Count | The number of errors caused because the player could not fetch the NonLinearAds/NonLinear resource. |
| VAST 503 Error Count | The number of errors caused because the player could not find NonLinearresource with the supported type. |
| VAST 600 Error Count | The number of general companionAds errors. |
| VAST 601 Error Count | The number of errors caused because because the creative dimensions do not fit within the companion ad display area (i.e., no available space). |
| VAST 602 Error Count | The number of errors caused because the required companion could not be displayed. |
| VAST 603 Error Count | The number of errors caused because the player was unable to fetch companionAds/companion resource. |
| VAST 604 Error Count | The number of errors caused because the player could not find companion resource with supported type. |
| VAST 900 Error Count | The number of undefined errors. |
| VAST 901 Error Count | The number of general VPAID errors. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   <br>Or<br>
   From the Publishers top menu, select **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**.

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.
   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](./dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).

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

1. Select **Run report** to send your report request.
