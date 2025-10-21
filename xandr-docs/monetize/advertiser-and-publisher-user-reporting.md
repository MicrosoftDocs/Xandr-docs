---
title: Advertiser and Publisher User Reporting
description: In this article, learn about the Advertiser and publisher user reporting along with the dimensions and metrics associated with them.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Advertiser and publisher user reporting

If you have created separate [user login](managing-user-logins-and-permissions.md) for your advertisers and publishers, they will be able to run reports from their perspective. These advertiser and publisher users have a limited set of metrics, filters, and dimensions available to them. This allows you to give your clients access to reporting while protecting your proprietary business data.

For instructions on how to give advertiser and publisher users access to reporting, see [Create a User](create-a-user.md).

> [!NOTE]
> Conversion-related data in reports is processed asynchronously. As a result, reports are available more quickly, while some conversion-related data is still being processed in the background. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Advertiser user reporting

> [!IMPORTANT]
> The **Metrics** are shown from the advertiser's perspective, so the **Revenue** field displays the advertiser's revenue (not the Network's).

### Metrics

- **Imps** - Total number of impressions served.
- **Clicks** - Total number of clicks across all impressions.
- **CTR** - Click-through rate (Clicks / Imps).
- **Total Conversions** - Total number of post view and post click conversions.
- **Conversion Rate** - Conversions / Imps.
- **CPC** - Clicks / Conversions.
- **Spend** - Booked advertiser revenue.
- **Revenue** - PVRevenue + PCRevenue.
- **PV Convs** - Total number of recorded post view conversions.
- **PV Revenue** - Total amount of recorded post view revenue.
- **PC Convs** - Total number of recorded post click conversions.
- **PC Revenue** - Total amount of recorded post click revenue.
- **CPM** - (Cost / Imps) X 1000.
- **RPM** - (Revenue / Imps) X 1000.
- **PPM** - (Profit / Imps) X 1000.
- **CPC** - (Cost / Clicks).
- **CPA** - (Cost / Conversions).

### Metrics specific to viewability

- **Viewed Imps** - The number of measured impressions that were viewable.
- **View Measured Imps** - The total number of impressions that were measured for viewability.
- **Viewability Rate** - The percentage of impressions that were viewable out of the total number of impressions measured for viewability.
- **Viewability Measurement Rate** - The percentage of impressions measured for viewability out of the total number of impressions.

### Dimensions

- **Insertion Order** - Available if the advertiser uses insertions orders.
- **Line Item**
- **Media Type** - Banner, Interstitial, Video, Text, Expandable, or Skin.
- **Country**
- **Size**
- **Advertiser Currency**
- **Conversion Pixel**

### Filters

- **Insertion Order** - Available if the advertiser uses insertions orders.
- **Line Item**
- **Media Type** - Banner, Interstitial, Video, Text, Expandable, or Skin.
- **Country**
- **Size**
- **Advertiser Currency**
- **Conversion Pixel**
- **Minimum Impressions**

## Publisher user reporting

> [!NOTE]
> The **Metrics** are shown from the publisher's perspective, so the **Revenue** field displays the publisher's revenue (not the Network's)

### Metrics

- **Imps** - Total number of impressions (including defaults).
- **Clicks** - Total number of clicks across all impressions.
- **CTR** - Click-through rate (Clicks / Imps).
- **Total Conversions** - Total number of post view and post click conversions.
- **Conversion Rate** - (Conversions / Imps).
- **Conversions Per Million** - (Conversions X 1,000,000) / Imps.
- **Publisher Revenue** - Revenue paid out to the publisher (based on revshare or cpm).
- **Publisher RPM** - (Publisher_Revenue / Imps) X 1000.

To allow Publisher users to report on the more granular impression and revenue metrics below, click **Edit** on the relevant publisher record, expand the **Advanced** branch and then enable **Report on Defaulted Imps**.

- **Imps Filled** - Total number of blank, PSA, defaulted, kept, resold, and external impressions.
- **Imps Defaulted** - Total number of defaulted impressions.
- **Total Revenue** - Revenue paid out to the publisher for filled and defaulted impressions.
- **Total Revenue eCPM** - Revenue paid out to the publisher per thousand filled and defaulted impressions.
- **Filled Revenue** - Revenue paid out to the publisher for filled impressions.
- **Filled Revenue eCPM** - Revenue paid out to the publisher per thousand filled impressions.
- **Defaulted Revenue** - Revenue paid out to the publisher for defaulted impressions.
- **Defaulted Revenue eCPM** - Revenue paid out to the publisher per thousand defaulted impressions.

### Metrics specific to viewability

- **Viewed Imps** - The number of measured impressions that were viewable.
- **View Measured Imps** - The total number of impressions that were measured for viewability.
- **Viewability Rate** - The percentage of impressions that were viewable out of the total number of impressions measured for viewability.
- **Viewability Measurement Rate** - The percentage of impressions measured for viewability out of the total number of impressions.

### Dimensions

- **Site**
- **Placement** - Note that for impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name.
- **Media Type** - Banner, Interstitial, Video, Text, Expandable, or Skin.
- **Country**
- **Size**
- **Publisher Currency**

### Filters

- **Site**
- **Placement**
- **Media Type** - Banner, Interstitial, Video, Text, Expandable, or Skin.
- **Country**
- **Size**
- **Minimum Impressions**

## Related topics

- [Reporting Guide](reporting-guide.md)
- [Network Reporting](network-reporting.md)
- [Advertiser Reporting](advertiser-reporting.md)
- [Publisher Reporting](publisher-reporting.md)
