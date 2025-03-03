---
title: Microsoft Monetize - Data Marketplace Overview
description: In this article, find information about the workflow, filtering, and data usage for the Data Marketplace.
ms.date: 10/28/2023
---

# Microsoft Monetize - Data Marketplace overview

The data marketplace consolidates data offerings from a diverse range of integrated third-party data providers. It facilitates automatic clearing for data purchased on our platform. The available data caters to various use cases and encompasses both cookie-based and non-cookie-based segments.

To get in touch with our data provider partners refer to the non-exhaustive list [Data Marketplace Partners and Contact Information](data-marketplace-partners-and-contact-information.md).

## Workflow

The procedures outlined in this section elucidate the steps to make a data provider's segments accessible to your members via the data marketplace. This results in distinction being made between Media costs and Data costs (e.g., for user segments, etc.)

### Add data providers

To access a particular data provider's segment offering:

1. Navigate to the Segments screen **Network** > **Segments** > **Segment Manager**
1. Click **Manage Data Providers**. If you don't see this option, contact your Account Manager.
1. Select the data providers for whom you want the data cost to be cleared directly by Microsoft. Each activated data provider (whose data cost will be cleared by Microsoft) will appear checked and highlighted.

> [!NOTE]
> If you ever choose to deactivate a data provider, you must first remove all active targeting of their segments. Once you have removed any targeting that is using these segments, log in to the [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) and create a ticket to complete the deactivation.

### Determining if a segment will be cleared within the data marketplace

- If the **Price** column in the **Segment Manager** or **Segment Chooser** lists a value for the segment, that segment will be cleared as part of the Data Marketplace.
- If **--** is displayed in the **Price** column in the **Segment Manager** next to a segment, that segment is not supported by the Data Marketplace. If you opt to utilize these unsupported segments for audience targeting, you will need to agree upon an established billing process with the data provider.

### Setting segment targeting

1. When selecting targeting options on the line item, navigate to the "Data Marketplace" section under "**Audience**"
1. The available segments (along with prices, when available) will then be displayed on the **Segments** screen. It is possible to filter for different data providers in the menu.
1. You can select the various segments that you wish to include in or exclude from your targeting. By selecting a segment, an estimation of the Data Costs is automatically calculated. When selecting more than one segment, it is possible to see the overlap between the segments under "**View Overlap Visualisation**". Especially if Boolean AND targeting is used, overlap between segments is important for campaign delivery. For more information on Data Cost calculation and Boolean logic, please refer to: [Data Cost Calculation Mechanics](data-cost-calculation-mechanics.md).

## Filtering

The data marketplace provides multiple filtering options to simplify the process of locating desired audiences. New data filters have been introduced to quickly identify environment-compatible segments, including ad type, device type, and geography. Additionally, there are new IAB audience taxonomy filters in the Data Marketplace to pinpoint relevant third-party segments.

### Environment filters

| Filter Type | Examples | Description |
|--|--|--|
| `Ad Format` | "Video", "Display" | Segments that have recently participated in auctions for this ad format(s) |
| `Device Type` | "CTV", "Mobile" | Segments that have recently participated in auctions with this device type(s) |
| `Geography` | "Canada", "United States" | Segments that have recently participated in auctions from the region(s) |

## Data usage in reports

We provide reports on the utilization of data in our data marketplace.

> [!NOTE]
> The usage of free segments will not be reflected in data usage reports.

To offer clarification, the following are some of the metrics that appear in the reports below:

- **Total cost** is the sum of your Media cost plus any third-party data costs (e.g., segments purchased from Data Providers).
- **Media cost** is just the cost of buying the actual media (impression).
- **Data costs** are the aggregated costs of all third-party services and data used in purchasing that media (e.g., user segments, etc.).

> [!NOTE]
> The expenses for segments for which the prices were not provided by the data provider, are presently not included in the overall cleared totals. For usage reports and the associated costs of such segments, you must coordinate with the data providers as billing for these segments will be handled separately by the Data Provider.

| Report Type | Description |
|--|--|
| `Data Usage Report (API)` | For details on the API version of this report, see the [Data Usage Report](data-usage-report.md). |
| `Data Usage Report (UI)` | For details on the UI version of this report, see the [Data Usage Report](data-usage-report.md). |
| `Network Analytics Report (API)` | The `data_costs` field in the `network_analytics` report contains the sum of all third-party data costs. For details on these data costs, see [Data Usage Report](data-usage-report.md). In addition, the `revenue` field in the `network_analytics` report includes all third-party data costs in totals when the Line Item's `revenue_type` is set to `cost_plus_cpm` or `cost_plus_margin`. |
| `Network Analytics Report (UI)` | The `data_costs` field in the **Member Analytics** report contains the sum of all third-party data costs. For details on these data costs, see [Data Usage Report](data-usage-report.md). In addition, the `revenue` field in the Network Analytics reports also includes all third-party data costs in totals when the Line Item's Revenue Type is set to `"Cost Plus"` (with either a "Margin" or flat "CPM" value). |

## Data usage in invoices

Your invoices contain the **Cost of Data** row. This row is a sum of all third-party data costs incurred for that month. To verify that these invoice values are accurate, compare them to the data in your [Data Usage Report](data-usage-report.md). For more details on invoices, see [Understanding Your Invoice](understanding-your-invoice.md).

### Setting data costs to display in grid views

To set your Insertion Order or Line Item grid views to display your third-party data costs, click on the column settings button (for each object) and select Third-party Costs on the Configure Columns screen that appears. As a result of selecting this option, the aggregated totals of all third-party data costs will appear within your grid views.

### Data cost metric on the insertion order grid view

- An aggregated total of all third-party data costs incurred as a result of the use of third-party services or data (e.g., data segments, etc.) will be displayed on your insertion orders. This value represents the total of all third-party data costs associated with any line item under the insertion order.
- An aggregated total of all third-party data costs incurred as a result of the use of third-party services or data (e.g., data segments, etc.) will be displayed on your line items. This value represents the total of all third-party data costs.

> [!NOTE]
> The cost of any segments for which the data provider did not provide a price is not currently reflected in the aggregate cleared totals. You will be billed separately by the Data Provider for the cost of those segments.

## Related topics

- [Understanding Your Invoice](understanding-your-invoice.md)
- [Data Marketplace Partners and Contact Information](data-marketplace-partners-and-contact-information.md)
- [Data Cost Calculation Mechanics](data-cost-calculation-mechanics.md)
- [Data Marketplace FAQ(s)](data-marketplace-faq.md)
