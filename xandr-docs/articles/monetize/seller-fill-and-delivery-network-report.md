---
title: Microsoft Monetize - Seller Fill and Delivery Network Report
description: Learn what is a Seller Fill and Delivery Network Report and how it is useful to sellers.
ms.date: 10/28/2023
---


# Microsoft Monetize - Seller fill and delivery network report

The Seller Fill and Delivery Report was designed as a troubleshooting
tool to provide sellers granular information regarding all impressions
sent to Xandr and to help diagnose delivery
issues all the way down to the tag and domain level. Using the new
descriptive fields, it is possible to see an approximation of overall
fill rate on Xandr using the "Total Ad
Responses" and "Total Ad Requests" metrics. This report provides
guidance on areas to troubleshoot but should not be used as a source of
truth for billing or transacted impressions.

> [!NOTE]
> This report only provides directional guidance on potential areas to troubleshoot. Figures in this report might see slight discrepancies with other standard reports, including the Network Analytics Report and the Video Analytics Report. 
>
> We recommend viewing each report independently and not comparing the directional figures from the Seller Fill and Delivery Report with other Xandr reporting, to avoid unnecessary confusion.

The data contained in this report will help pinpoint issues contributing
to untransacted impressions stemming from:

- Improper default/passback tag setup
- Inventory blocklists related to IP or domain blocking
- Video player errors
- Miscellaneous causes

> [!NOTE]
> **For video sellers only :** As a result of video caching by video players, the Xandr data pipeline allows a six-hour window to register a response from a video player after the auction is complete and the creative VAST XML has been sent to the page, before considering a video impression 'non-responsive' (Bid Sent No Response). 
>
> Xandr will update some counts, for video tags only, six hours after the time of the auction. Therefore, to receive the most accurate view of video counts across dimensions, schedule your reports to run after the six-hour window for a given hour of data.

The diagram below is a representation of how metrics are grouped and
counted for this report: 

:::image type="content" source="media/create-seller-filler-and-delivery-explanatory-graphic.png" alt-text="Screenshot of Create Seller and Delivery Explanatory Graphic .":::

## Time frame

All dates and times are given in UTC.

**Time ranges**

Time ranges define the time period of the data extracted for the report.
The following is a complete list of time ranges available for reports.

However, all time ranges are not available for every report.

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

**Intervals**

Intervals determine how your data is grouped together into rows in the
report response. The following is a complete list of intervals available
for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the
  entire selected time range.

This report's data is retained for 403 days. The time granularity of the
data is hourly.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report. 

| Column | Description |
|---|---|
| Bid Sent No Reponses | Bid responses returned by Xandr where ultimately the creative does not render.<br>The most common scenario in which this occurs is when Xandr receives an ad request from an external system - such as a publisher ad server utilizing prebid or a traditional waterfall - and returns a response, but the external system selects a different bid.<br>Other examples of reasons this can occur include:<br> - The end user leaves the page before the impression tracker fires.<br> - An ad is requested but never loads due to lazy loading.<br> - A video player requests an ad but never plays the ad. |
| Default No Reponses | Ad requests where a default creative was sent but no response was received from the end ad server. This could be the result of an error or an alternate default tag was chosen by the final ad server. |
| Defaults | Ad requests where a default creative served because there were no valid bids. |
| eCPM | For definition of eCPM, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). In this report, eCPM is seller revenue earned per 1000 impression resold to a third-party buyer. [1000 * Seller Revenue / Imps (resold)] |
| Fill Rate | The rate of total number of resold and kept impressions to the total number of ad requests sent to Xandr for auction. [Imps (resold + kept) / Total Ad Requests] |
| Filtered Request Rate | The rate of filtered requests to the total number of ad requests sent to Xandr for auction. (Filtered Requests / Total Ad Requests) |
| Filtered Requests | Ad requests filtered pre-bid by Xandr for inventory quality. |
| Imps (kept) | An impression where a managed advertiser's creative serves on a managed publisher's site. |
| Imps (resold) | An impression that is resold to a third-party buyer. |
| PSAs or Blanks | The number of blanks or PSAs served. It can also include ad requests where no bids were submitted by Xandr, such as unfilled header bidding requests. |
| Response Rate | The rate of total number of ad responses counted within Xandr to the number of ad requests that are not filtered pre-bid by Xandr. [Total Ad Responses / (Total Ad Requests - Filtered Requests)] |
| RPM | For definition of rpm, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). In this report, RPM is seller revenue earned per 1000 ad requests sent to Xandr for auction. (1000 * Seller Revenue / Total Ad Requests) |
| Seller Revenue | Revenue earned by the Seller. |
| Total Ad Requests | The total number of ad requests sent to Xandr. (Filtered Requests + Imps (kept) + Imps (resold) + Defaults + Video Player Errors + Video Default Errors + Bid Sent No Responses + Default No Responses + PSAs or Blanks) |
| Total Ad Responses | The total number of ad responses counted within Xandr. (Imps (kept) + Imps (resold) + Video Player Errors + Bid Sent No Responses) |
| Video Default Errors | Errors reported from the video player when a default creative should have served. |
| Video Player Errors | Errors reported from the video player after the VAST XML has been delivered. |
| Win Rate | The rate of total number of managed and kept impressions to the total number of ad responses counted within Xandr. [Imps (kept + resold) / Total Ad Responses] |

You also have the option to display monetary values in USD and the
Advertiser/Buying Currency.

## Filters

| Name | Description |
|---|---|
| Country | The country in which the impression occured. |
| Deal | The deal associated with the transaction for the impression. |
| Placement | The placement on which the impression occurred. |
| Placement Group | The placement group where the impression occurred. |
| Publisher | The publisher on whose site the impression occurred. |
| Supply Type | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values:<br> - `"web"`<br> - `"mobile_app"`<br> - `"mobile_web"` |

## Dimensions

Grouping by dimension allows you to display certain fields of reporting
data in a particular order.

| Name | Description |
|---|---|
| Ad Request Call Type | The type of handler that was used to send the impression to Xandr (e.g., ttj, ut, mob, ptv, openrtb) |
| Allowed Media Types | The media types that are allowed to participate in the auction. The permitted media types is a combination that is enabled through the ad call and placement settings. Possible values are `Banner`, `Expandable` and `Native`. |
| Country | The country in which the impression occurred. |
| Deal | The deal associated with the transaction for the impression. |
| Mobile Application | For mobile app impressions, the Apple App Store or Google Play name and ID of the mobile application where the impression occurred, for example, `"Angry Birds (343200656)"` or `"Angry Birds (com.rovio.angrybirds)"`.<br> - `"---"`: This means that we didn't receive a valid mobile app name as the referrer or the app has received too few impressions to be included in reporting. |
| Placement | The name and ID of the placement on which the impression occurred.<br>Note that a placement ID of `0` may appear for 3rd-party impression trackers. For more information about impression trackers, see [Working with Impression and Click Trackers](working-with-impression-and-click-trackers.md). |
| Placement Group | The name and ID of the placement group where the impression occurred. |
| Publisher | The name and ID of the publisher on whose site the impression occurred. |
| Seller Currency | The seller currency associated with the impressions and/or activity. |
| Site Domain | For web or mobile web impressions, the domain where the impression occurred. There is one additional value that may appear in place of a domain:<br> - `"---"`: This means that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| Supply Type | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are `"web"`, `"mobile_app"`, and `"mobile_web"`. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the
    appropriate top menu (depending on how your account has been
    configured).
    1. Or, from the Publishers top menu, click on **Prebid Server Premium** \> **Analytics** \> **Prebid Server Analytics**.
1. Select the relevant report from the list. The
    Report screen shows the available
    filters, dimensions, and delivery options for the report. The
    selections you make here will determine what report data is
    delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of
    how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the
    information you want. For example, rather than running a report that
    shows impressions for all inventory sources, you may want to list
    results for just a select few. When you select a filter (by clicking
    **Edit**), a selection panel appears.
    Select items in the **Available** list (left), then click
    **Add** to include them in the
    **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in
    the order you prefer.

    > [!WARNING]
    > Dangerous certain consequences of an action<b>Warning:</b> The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and
    grouped by your chosen dimensions, you need to choose a delivery
    method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data,
      you may want to view the report as soon as possible in your
      browser. You can download the report in XLSX, CSV, Excel/TSV and
      JSON format. However, there is a limit of 100,000 rows per report
      when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A
      popup notification will let you know when the report is ready to
      view or download.

      > [!TIP]
    > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to
      one or more email addresses.
    - **Save as report template**: Save your selected report settings so
      that you can run this report again in the future. You can name
      this template using the text entry field under
      **Name this report** (its checkbox
      is auto-selected when you choose this option). A saved report can
      be rerun from the **Your Reports**
      screen.
    - **Add to scheduled reports**: Run this report automatically at
      specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a
      name for future reference.
1. Click **Run report**to send your report request.
