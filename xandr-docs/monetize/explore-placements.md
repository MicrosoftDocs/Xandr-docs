---
title: Explore Placements
description: Explore Inventory Manager, discover key metrics, quick access to details, and default creatives for all placements. 
ms.date: 3/18/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Explore placements

The **Inventory Manager** page displays all placements for a selected publisher. It allows you to review placement performance, manage placements, and perform bulk actions.

From this page you can:

* View placement performance metrics
* Filter and organize placements
* Assign default creatives
* Run reports
* Export placement tags

---

# Access the Inventory Manager

You can open Inventory Manager from either of the following navigation paths.

## From the Publishers tab

1. Navigate to **Publishers > Inventory Manager**.
2. Use the **Select Publisher** dropdown to search for the publisher you want to work with.

## From the Inventory tab

1. Navigate to **Partners > Placement**.
2. Use the **Select Publisher** dropdown to search for the publisher you want to work with.

The Inventory Manager grid displays placements associated with the selected publisher.

---

# Customize the data view

You can customize how placement performance data is displayed.

## Time interval

Use the **Interval** dropdown in the top-right corner to select the reporting time range.

Available intervals include:

* **Today** – Data for the current calendar day up to the last completed hour.
* **Yesterday** – Data from the previous calendar day.
* **Last 7 days** – Data from the previous seven full days, excluding today.
* **Lifetime** – Data collected since the placement was created.

---

## Currency

Use the **Currency** dropdown to choose which currency is used for revenue values.

Available options include:

* **USD**
* **Publisher currency**

If the publisher currency is already USD, the currency selector is disabled.

Exchange rates are automatically applied and updated hourly.

---

## Time zone

Use the **Time Zone** dropdown to select the time zone used to calculate reporting intervals.

This affects how data is grouped for intervals such as **Today**, **Yesterday**, and **Last 7 days**.

---

# Manage displayed columns

You can customize which columns appear in the Inventory Manager grid.

To modify the columns:

1. Navigate to **Publishers > Inventory Manager**.
2. Select **Edit columns** in the table header.
3. Select the columns you want to display.
4. Drag columns to reorder them if needed.
5. Save your changes.

The selected columns appear in the grid.

## Available columns

- **ID**: The unique ID number of the placement.
- **Name**: The name of the placement.
- **Impressions**: The number of impressions recorded for the placement.
- **Revenue**: Network revenue booked through direct advertisers and resold to real-time buyers.
- **Placement Group Name**: The parent placement group that the placement belongs to.
- **Self-Audit**: Indicates whether the publisher has enabled **Self-Auditing Creatives** for the placement group inventory.

---

# Placement display modes

Inventory Manager supports two viewing modes.

## Tree view

Tree view displays inventory in a hierarchical structure.

In this view:

* Placement groups appear as top-level items.
* You can expand a placement group to view the placements it contains.
* This helps you understand how placements are organized within placement groups.

To switch to Tree view:

1. Navigate to **Publishers > Inventory Manager**.
2. Select the **Tree view icon** in the table header.

Use this view when managing placements within specific placement groups.

---

## Direct view

Direct view displays placements in a flat list.

In this view:

* All placements for the selected publisher appear in a single list.
* Placements are not grouped by placement group.
* The **Placement Group Name** column identifies which group each placement belongs to.

To switch to Direct view:

1. Navigate to **Publishers > Inventory Manager**.
2. Select the **Direct view icon** in the table header.

Use this view when analyzing performance across all placements.

---

# Filter placements

You can filter placements by name or ID.

To apply a filter:

1. Select **Filters**.
2. Enter a placement **name** or **ID**.
3. Select **Apply filter**.

The grid displays only placements that match the filter criteria.

Select **Reset** to remove the filter and display all placements.

---

# Assign a default creative

You can assign a default creative to a placement.

A default creative serves when no eligible campaign creative is available.

To assign a default creative:

1. Select a placement row in the grid.
2. In the **Default Creatives** panel, select **Add**.
3. Select the creative to assign.

---

# Run reports for placements

You can run reports for one or more placements directly from Inventory Manager.

To run a report:

1. Select the checkboxes for the placements you want to analyze.
2. Select **Run Report** from the table header.

The reporting interface opens with the selected placements applied as filters.

---

# Related topics

- [Create a Placement](create-a-placement.md)
- [Update a placement](update-a-placement.md)
- [Assign a default creative to a placement](assign-a-default-creative-to-a-placement.md)
- [Export placement tags](export-placement-tags.md)

<!-- 
# Explore placements

The **Inventory Manager** screen shows you essential metrics about all placements for a specific publisher, provides quick access to each placement's details and default creatives as well as placement tag exporting, and offers bulk editing and reporting options.

## Getting to the Inventory Manager screen

From the **Publishers** tab: Go to **Publishers >  Inventory Manager**.
From the **Inventory** tab: Go to **Partners >  Placement**.

## Customizing data view

### Intervals

Use the dropdown at the top right of the screen to choose the interval for the data that is displayed for each placement:

- **Today**: Current calendar day up to the last hour.
- **Yesterday**: Full 24-hour period of the previous calendar day.
- **Last 7 Days**: Full 7 days previous to the current calendar day, i.e., excluding today.
- **Lifetime**: Entire lifetime of each line item, including the current calendar day.

### Currency

Click the **Currency** dropdown to select the currency units to display for all monetary values in the grid. You can select either USD (United States Dollars) or the publisher's currency. (If the publisher's currency is USD, this dropdown is disabled.) The default is USD. Current exchange rates will be applied. Exchange rates are updated hourly. (See [Currency Support](currency-support.md) for more information on currencies.)

### Time zone

Click the **Time Zone** dropdown to select a time zone. This will be the time zone that is used to determine the data collected for the specified interval (**Today**, **Yesterday**, or **Last 7 Days**).

### Viewing data

The following information is shown for each placement. Note that the data always reflects the currently selected interval, based on the selected time zone:

- **ID**: ID number of the placement.
- **Name**: Name of the placement.
- **Placement Group**: The parent placement group under which the placement belongs.
- **Self-Audit**: Whether the publisher has opted to [Self-Auditing Creatives](self-auditing-creatives.md) its inventory.
- **Imps**: Number of impressions for the placement.
- **Network Revenue**: Network revenue booked through direct advertisers and resold to real-time buyers.

### Filtering

You can filter your list of placements by name or by ID. Click the **Filter** button and type any part of the name or ID, then click **Apply filter**. The filter will return placements matching the filter only within the selected placement group. It will not return placements from other placement groups.

Click **Reset** to remove the filter and display all placements within the selected placement group.

### Assigning a default creative to the placement

You can assign a default creative to a placement by clicking the placement row to select and highlight it, then clicking the **Add** button in the **Default Creatives** box that appears. For more information, see [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md).

### Reporting on the placement

You can report on one or more placements by checking the boxes for the placements you want to report on, then going to More **Actions** >  **Run Report**. For more information, see [Publisher Reporting](publisher-reporting.md).

### Related topics

- [Working with Placements](working-with-placements.md)
- [Create a Placement](create-a-placement.md) -->
