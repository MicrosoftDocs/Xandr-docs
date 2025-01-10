---
title: Microsoft Monetize - Seller CMP Analytics Report
description: Learn how the Seller CMP analytics report helps sellers get information on how many ad requests contained TCF strings encoded, how many ad requests contained TCF strings that were not encoded properly and information on CMP.   
ms.date: 10/28/2023
---


# Microsoft Monetize - Seller CMP analytics report

The Seller CMP Analytics Report provides insight into the number, validity, and content of the IAB Transparency & Consent Framework (IAB TCF) strings on seller ad requests to Microsoft Advertising endpoints. This report enables sellers to answer questions like:

- How many ad requests contained TCF strings encoded according to the TCF v1 or v2 specifications?
- How many ad requests contained TCF strings that were not encoded properly and therefore invalid or malformed?
- Is my CMP (Consent Management Platform) correctly passing permission information to Microsoft Advertising?

This report does not prove or disprove compliance with any laws or regulations. The language "GDPR applied" for this report means, Microsoft Advertising applied TCF logic. Microsoft Advertising supports the IAB TCF and this report enables sellers using the TCF to confirm that TCF signals are communicated properly.

For ad requests where TCF logic is applied the classification is summarized in this diagram:

:::image type="content" source="media/seller-cmp-analytics.png" alt-text="Screenshot of ad requests where TCF logic is applied.":::

Sellers wishing to have all of their ad requests treated according to the IAB TCF standards and policies can force application of Microsoft Advertising TCF logic by passing 'gdpr=1' according to the IAB OpenRTB Spec. If the GDPR parameter is omitted but the request includes a TCF string via URL params, Microsoft Advertising will apply TCF logic (unless the impression is received via OpenRTB). For impressions received via OpenRTB, the **Regs.ext.gdpr** field must be set to **1** in order for Microsoft Advertising to apply TCF logic.

A high number of present but malformed strings for a given publisher usually means that the publisher's CMP is not creating or encoding the strings according to TCF specifications, and therefore are unreadable to Microsoft Advertising and other vendors. Unreadable strings, because they do not provide clear signals to vendors, are treated as no permission for any vendor, and should be avoided.

For more information about the IAB TCF, please refer to the following resources:

- [IAB Techlab TCF v1 and v2 Technical Spec](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework)
- [IAB Techlab TCF RTB Spec](https://iabtechlab.com/wp-content/uploads/2018/02/OpenRTB_Advisory_GDPR_2018-02.pdf)

## Time frame

All dates and times are given in UTC.

**Time ranges**

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports.

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

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

Data for this report is grouped into rows by the day.

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Ad Request Call Type | N | The path where Microsoft Advertising received the ad request. This generally corresponds to the seller integration. For example: /openrtb2, /ut/v3, /ut/v3/prebid, /ptv, /ttj. |
| Publisher | Y | The name and ID of the publisher associated with the impression. For example, New York Times (723968) |
| Publisher Name | N | The publisher associated with the impression. |
| URL | N | The URL of the incoming impression. |
| YMD | N | The year, month, and day of the impression, expressed using the format yyyy-mm-dd, for example: 2019-09-15. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Ad Requests GDPR Applied | The number of incoming ad requests for which Microsoft Advertising applied TCF logic. Microsoft Advertising applies TCF logic if the IAB OpenRTB Specified flag gdpr is set to 1 or if the gdpr flag is omitted but the request includes a gdpr_consent field. If your digital properties intend to use TCF for all GDPR-covered inventory, this number should be close to Ad Requests GDPR Country. |
| Ad Requests GDPR Country | The number of incoming ad requests for which the impression originated from a GDPR-implementing country/region, or the impression contained a consent string. |
| Blank Consent Strings | The number of ad requests where Microsoft Advertising applied TCF logic ("GDPR applied"), but the string was either blank or the field gdpr_consent was omitted. This number should ideally be zero. |
| Invalid CMP Impressions | Number of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is NOT registered with the IAB, as seen at [https://iabeurope.eu/cmp-list/](https://iabeurope.eu/cmp-list/). |
| Malformed Consent Strings | The number of ad requests where Microsoft Advertising applied TCF logic ("GDPR applied"), but the string received could not be decoded. This number should ideally be zero. |
| Percent Ad Requests GDPR Applied | The percentage of incoming ad requests from GDPR-implementing countries for which GDPR is applied. |
| Percent Bad Consent Strings | The percentage of incoming ad requests for which GDPR is applied and the consent string is non-blank and malformed. |
| Percent Blank Consent Strings | The percentage of incoming ad requests for which GDPR is applied and the consent string is blank. |
| Percent TCF Version 1 Impressions | The percentage of incoming ad requests for which GDPR is applied and the consent string is valid and encoded according to TCF v1. |
| Percent TCF Version 2 Impressions | The percentage of incoming ad requests for which GDPR is applied and the consent string is valid and encoded according to TCF v2. |
| Percent Valid CMP Impressions | The percentage of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is registered with the IAB, as shown at [https://iabeurope.eu/cmp-list/](https://iabeurope.eu/cmp-list/). |
| Percent Valid Consent Strings | The percentage of incoming ad requests for which GDPR is applied and the consent string is non-null and valid. |
| Percent Microsoft Advertising Consented | The percentage of incoming ad requests for which GDPR is applied and the vendor bit (#32) for Microsoft Advertising is a 1 for TCF v1 encoded strings |
| Percentage Invalid CMP Impressions | The percentage of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is NOT registered with the IAB, as shown at [https://iabeurope.eu/cmp-list/](https://iabeurope.eu/cmp-list/). |
| Seller Revenue Invalid Consent Strings | TThe total estimated seller revenue associated with invalid (un-decodable) strings. If a string is unreadable but present, an impression is served without personal data such as cookies. This number should ideally be zero, indicating that all ad requests had a decodable string. |
| TCF Version 1 Impressions | The number of ad requests where Microsoft Advertising applied TCF logic ("GDPR applied"), the string was parseable, and the decoded value of cookie_version was 1, indicating that this TC string was created according to the TCF v1.0 specification. The specification can be found here: [https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework). |
| TCF Version 2 Impressions | The number of ad requests where Microsoft Advertising applied TCF logic ("GDPR applied"), the string was parseable, and the decoded value of cookie_version was 2, indicating that this TC string was created according to the TCF v2.0 specification. The specification can be found here: [https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework). |
| Valid CMP Impressions | The number of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is registered with the IAB, as seen at [https://iabeurope.eu/cmp-list/](https://iabeurope.eu/cmp-list/). |
| Valid Consent Strings | The number of ad requests where Microsoft Advertising applied TCF logic ("GDPR applied") and the request contained a string that was parseable. This number should ideally equal the number of ad requests where Microsoft Advertising applied TCF logic. |
| Microsoft Advertising Consented Impressions | For TCF v1-encoded strings, the number of incoming ad requests for which GDPR is applied, and Microsoft Advertising's vendor bit (#32) is a 1 in the string.<br>For TCF v2 encoded strings, the number of incoming ad requests for which GDPR is applied, Microsoft Advertising's vendor bit (#32) is a 1 in the string, and we have established legal basis to process personal data (i.e. consent for purpose 1 **and** either consent or legitimate interest for purposes 2, 7 and 10 is signalled in the consent string). |

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
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under
      **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topic

[Seller CMP Analytics Report API](../digital-platform-api/seller-cmp-analytics-report.md)
