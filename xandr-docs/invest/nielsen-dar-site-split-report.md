---
title: Microsoft Invest - Nielsen Digital Ad Ratings - Site/Split Report
description: Learn how to use Nielsen Digital Ad Ratings (DAR) - Site/Split Report to get an insight on publisher domains and audiences connected to your line item's impressions.  
ms.date: 10/28/2023
---

# Microsoft Invest - Nielsen Digital Ad Ratings (Site/Split report)

The **Nielsen Digital Ad Ratings (DAR) - Site/Split Report** gives you insight into the publisher domains and audiences connected to your line item's impressions. If your line item's using splits, this report also gives you information on their performance.

## Time frame

Available time ranges include:

- Custom
- Last 7 Days
- Last 14 Days
- Month To Date
- Last 30 Days
- Quarter To Date
- Last 100 Days
- Last 365 Days
- Year To Date

Intervals determine how your data is grouped together into rows in the report response. Only one interval option is available for a Nielsen DAR - Site/Split report:

- **Cumulative**: Data is grouped together in one figure, covering the entire selected time range.

## Metrics

| Reporting Metric | Description |
|:-|:-|
| Total Impressions | The total number of impressions your line item has made |
| Audience Share (%) | The percentage share of the total audience a line item has reached within a certain demographic group. This measurement is rounded to two decimal places.<br> - Audience Share (%) = Row Level Audience Count ÷ Campaign Total Audience Count × 100 |
| On Target Percent (%) | The percentage of impressions served to your targeted demographic<br>- On Target Percent (%) = Impressions Seen by Target Demographic ÷ Total Impression Count for your Line Item × 100 |
| Unique Audience | The number of unique individuals in the audience that your line item reached |
| On Target Impressions | The number of impressions served to your desired demographic group that are within your selected reporting dimensions |
| Population Share (%) | Percentage of people within a demographic relative to the total population<br> - Population Share (%) = Demographic Population ÷ Population of all Demographics × 100 |
| Impressions Share (%) | Based on the line item's total impression count, the percentage that served to your targeted demographic<br> - Impressions Share (%) = Demographic Impressions ÷ Total number of Impressions Across all Demographic Groups × 100 |
| Population | Based on census-provided data, the number of people in the country included in a given demographic<br>- Example: F18-24 = 14.9 million |
| Impressions Index | A targeting success score based on how the line item's impressions are divided across all demographics<br> - Impressions Index = Impression Share (%) ÷ Demographic-Specific Population × 100 |

## Filters

| Filter | Description |
|:-|:-|
| Site | Filter for website URLs and mobile applications. |
| Platform | Filter for the type of device used: **Computer**, **Mobile**, and/or **Connected Device** |
| Line Item | Filter for the name and ID of an line item. For more information about line items, see [Working with Line Items](working-with-line-items.md). |
| Insertion Order | Filter for the name and ID of an insertion order. For more information about insertion orders, see [Working with Insertion Orders](working-with-insertion-orders.md). |
| Split | Filter for the name and ID of a line item split. Splits are only applicable to augmented line items. |
| Demographic Group | Filter for demographic groups sorted by sex and age range. |
| Country | Filter for countries where Nielsen data is available. |

## Dimensions

| Dimension | Description |
|:-|:-|
| Platform Type | The type of platform an impression occurred on: **"D" (Desktop)**, **"M" (Mobile)**, or **"O" (Connected Device)**. |
| Nielsen Campaign Ref | The Nielsen Campaign reference. **Example**: `cmp3406123` |
| Split | The name and (optional) ID of a split. |
| Site | The domain where impressions occurred. For mobile applications, this can be the URL of the app's location in the app store.<br>**Note**: Two additional values display in place of a domain: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| Last Available Date | The date for when reporting data was last gathered |
| Metrics Start Date | The date for when data for Nielsen report metrics began |
| Country Code | The corresponding code for a country where impressions for your line item occurred |
| Line Item | **Required.** The ID and (optional) name of a line item. For more information about line items, see [Working with Line Items](working-with-line-items.md). |
| Demographic Group | **Required.** Filter for demographic groups sorted by sex and age range. |

## Run your report

Follow these steps to run the report:

1. Select **Reporting \> Advertiser Reports** from the dropdown menu (depending on how your account has been configured).
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. Theselections you make here will determine what report data is delivered to you, and how.
  
   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).
  
1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

   > [!WARNING]
   > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser.
    - **Run in background, notify me when results are ready to view**: A pop-up notification will let you know when the report is ready to view or download.
    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Select **Run report** to send your report request.

## Related topics

- [Nielsen Digital Ad Ratings - Audience Profile Report](nielsen-dar-audience-profile-report.md)
- [Measuring Demographic Targeting Success with Nielsen Digital Ad Ratings](nielsen-digital-ad-ratings.md)
- [Activate Nielsen Digital Ad Ratings for a Line Item](activate-nielsen-digital-ad-ratings-for-a-line-item.md)
- [Metrics for Nielsen Digital Ad Ratings](nielsen-dar-metrics.md)
