---
title: Lookup Builder
description: In this article, learn about lookup builders, their filters, how to build lookups, and how to run them individually or in batches.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Lookup builder

Selecting the **Lookup Builder** tab accesses the **Lookup Builder** screen. This is where you build any of your lookups, regardless of how you are going to run them (batch or individual).

There are filters on the left-hand side of the screen. They are Configuration filters and Advanced filters.

## Configuration filters

In the **Configuration** panel on the left side of the page, select the high-level settings for your lookup:

### Date range

This field determines the timeframe for the availability lookup. By default, the lookup is for the Next Month. Select the icon to the right of the Next Month verbiage to access the **Date Range** screen.

> [!NOTE]
> Availability lookup is always forward-facing. You cannot do lookups in the past. The default is Next Month, but you can change it to anything that you want into the future.

**Standard** - These are typical date range selections. There are two drop-down menus, and a numerical value entry between them. The drop-down menu on the left of the screen allows you to select either **Next** (default) or **Remainder of Current**. This relates to the secondary drop-down window on the right, which allows you to select one of the following:

- Month(s) (default)
- Day(s)
- Week(s)
- Quarter(s)
- Year(s)

Between Next and Month(s) is a window for you to enter a numerical value. This is to designate how many months, days, etc. that you are selecting.

**Custom** – Selecting this accesses the calendar. You can select the "from” and “to” date ranges on the calendar, or enter the dates in the text boxes below the calendar. The selected date range is visible at bottom of **Date Range** screen.

**Cancel** - Selecting this cancels your entries, and allows you to re-enter the information.

**Update** - Selecting this updates your date range information.

### Group By

This field determines how available impressions and capacity are broken down in the lookup. By default, the lookup shows total available impressions and capacity only. Choose a group from the drop-down list (Example: Select **Weekly** to see available impressions and capacity for each week in the selected time period).

These are the options:

- Daily
- Weekly
- Monthly
- Quarterly
- Yearly

Example: If you had a lookup grouped by months, and wanted to group by weeks, you would select **Weekly**. It would then take the lookup and break it down into four different rows on the **Lookup Results** screen. Each row represents a week in that month.

## Advanced filters

### Priority

This field determines the ad server priority for your availability lookup. By default, the lookup calculates availability by subtracting guaranteed consumption from capacity, regardless of priority. In the **Priority** dialog that appears, choose a priority from the drop-down list (e.g., select 4 to see availability at priority 4).

> [!NOTE]
> When you set a priority, all consumption (guaranteed and preemptible) at a worse priority than your selected priority - will be considered available.
>
> If you have multiple ad server integrations, there is another option in the configuration for you to select which ad server you want to focus on. The ad server filter will determine the priority scale.
>
> The options available under **Advanced Filters** have to do with your set up. If you are interested in adding additional filters you do not currently have, speak with your services representative.

### Frequency Cap

This field determines the maximum number of times an ad should appear for a given user for a specified number of minutes, hours, days, weeks, months, or for the lifetime of the ad. Available impressions and capacity are adjusted based on the cap you set. To set a frequency cap, select the current selection. Then in the **Frequency Cap** dialog that appears, type the maximum number of views for the timeframe you want (e.g., for a weekly frequency of 3, set the frequency cap to be 3 views per 1 week).

### Viewable

This setting will allow you to run an availability check that includes additional viewability metrics. These are based on the historical viewable rate for the set of inventory that you are checking.

### Competitive Separation

This field allows for refinements in availability lookups results by considering delivery restrictions due to advertiser and advertiser group restrictions. Competitive Separation will exclude competitors' order lines from showing on the same page.

### Roadblock

This field allows for customization of availability lookup results based on the type of roadblock that you would like to run. When selecting the roadblock type within the advanced option and running an availability lookup that varies by size values, Yield will model the capacity and availability based on how the ad server will deliver the roadblock.

### Displacement

This setting will allow you to see displaced availability in addition to the standard Availability metric. Displacement Availability is a metric that will show the impressions available if we were to remove consumption from a particular set of inventory that could reasonably be displaced (or moved) elsewhere.

## Lookup builder work screen

### Button descriptions and functionality

| Button/Field | Description |
|:---|:---|
| Open | Selecting this accesses Lookup Templates that you have previously saved. A Lookup Template is a way to save and reuse a particular lookup configuration. This is distinct from a saved batch, which allows you to reuse the resulting target expressions rather than the configuration itself. |
| Save | Selecting this accesses the **Save Lookup Template** screen. This screen has these fields:<br> - Save as New (radio button)<br> - Replace Existing (radio button)<br> - Name (text box)<br> - Category (pull-down menu)<br> - Description (text box)<br> - Permissions (table)<br><br>After making selections, select **Save** to save this template. Now when you select the **Open** button, you will see this template. |
| Attribute and Product View/Product Group View | There are two different views that are accessibile from a drop-down menu: <br>The **Attribute and Product View** (default) and the **Product Group** View. The latter is specific to product groups.  |
| Target Expression Editor | Selecting the small icon to the right of the Attribute and Product View verbiage allows you to view the target expression on a user-friendly screen. Target expressions are often very lengthy, and could be hundreds of lines long. The target expression is editable from this screen. You can make changes and select **Update**. The **Lookup Builder** screen is displayed, and the values are updated accordingly. |
| Vary By | This allows you to vary base targeting criteria by selected variant targeting criteria. It builds multiple targeting strings by combining each variant with the base targeting. |
| Undo | This clears the last action that you entered. |
| Clear All | This clears all of your entries, and allows you to start over. |
| Select Attributes or Product | Lookups are either built from an existing product(s), or the particular attributes must be specified. Selecting **Select Attributes** accesses the **Select Attributes** screen. From this screen, you are able to choose attributes. Likewise, selecting **Product accesses** the **Select Product** screen, where you can choose products.<br>Selecting the information icon to the right of the Select Attribute or Product verbiage provides very basic general information about the workflow. |

## Copy/delete attributes and values across segments

You can copy and delete attributes/values across different segments with an availability lookup.

If you have a multi-segment lookup then you will have access to the following options by selecting the sprocket icon shown below:

> [!NOTE]
> If the sprocket icon showed below is grayed-out, this means the lookup is not a multi-segment lookup. You will not be able to access any options.

Here’s the explanation for what the options do:

### Duplicate attribute across segments

- This will copy the attribute along with its value to all segments in the lookup. If the duplicated attribute exists in the other segments, the values will get replaced.
- If you have size = 300x250 in segment 1 and size = 728x90 in segment 2; if you select the **Duplicate Attribute** across Segments for size = 300x250, you will see this attribute and its value appear in both segments 1 & 2 and will no longer see size = 728x90.
- This is a replace function when the attribute exists within other segments.

### Add attribute values across segments

- This will copy the attribute and its value to all segments in the lookup.
- If the attribute does not exist, it will be added to the segment.
- If the attribute does exist, it will have the values from the selected attribute added to its own values.
- If you have size = 300x250 in segment 1 and size = 728x90 in segment 2; if you select the **Add Attribute Values** across Segments for size = 300x250, it will update segment 2 to include size = 728x90, 300x250.
- This is an additive function when the attribute exists within other segments.

### Delete attribute across segments

- This will remove the attribute and all values from all segments in the lookup.
- If you have size = 300x250 in segment 1 and size = 728x90 in segment 2; if you select the **Delete Attribute** across Segments for size = 300x250 you will no longer see size in ANY segment.

### Delete attribute values across segments

- This will remove the attributes and the specific values from all segments in the lookup.
- If you have size = 300x250 in segment 1 and size = 728x90 in segment 2; if you select the **Delete Attribute Values** across Segments for size = 300x250 you will no longer see size in segment 1, but size = 728x90 will still exist in segment 2.
- If you have size = 300x250 in segment 1 and size = 728x90, 300x250 in segment 2; if you select the **Delete Attribute** across Segments for size = 300x250 you will no longer see size in segment 1 while segment 2 shows size = 728x90 (size = 300x250 was removed).

> [!NOTE]
> If you are adding a new attribute across segments (and it doesn’t exist in any segment), it does not matter if you use the **Duplicate Attribute** or **Add Attribute Values** option. They will result in the same targeting.

## Build a lookup/target expression with attributes

There are a few methods of building a lookup/target expression:

### Method 1

This method is recommended if you know exactly what you are looking for, and your target expression is small.

Select **Type Attribute**. This allows you to type directy into the window. Start typing, and a list of the available attributes appears. Scroll down the list and select the attributes you desire. Select **Enter**, and it automatically goes to the next one.

### Method 2

This method is recommended if you do not know specifically what you are looking for. You can start by doing a high-level search, and drill down further until you get the results you are looking for.

- Select **Select Attributes**. This accesses the **Select Attributes** screen. There are three main windows and three search windows.
- The list in the left-hand window is every attribute that you have available to you.
- There is extensive search capaibility. The **Contains and Search** window at the top of the screen allow you to drill down into the search.
- The four options in the search criteria are: Contains, Starts with, Ends with, Equals.
- Once the attribute has been identified and selected, the values for that attribute are displayed in the middle column of the screen. Then you can further drill-down into your search by applying the same search functionality to those results.
- If you want to select multiple attributes at once, you can do so by holding down the shift key while making your selection.
- There is also a **Select All** button, if you would like to select all the attributes listed in that window.
- The result of the search is displayed in the right-hand window.
- The right-hand window also has include/exclude functionality. You can exclude attributes from your final selection.
- When you are satisfied with your selection, select **Update**. You will now see the attributes listed on the **Lookup Builder** screen.
- If you would like to delete an attribute, mouse-over the attribute and select **x** in the upper right-hand corner.
- If you want to add other attributes, select **Attributes** again, and the entire list is displayed again. The previous selections will still be displayed in the right-hand column.

### Method 3

- Select **Add Attribute** to add an attribute directly from the **Lookup Builder** screen.
- This accesses a text window, where you can add the attribute’s name. Start typing and it will display a list of what is available to you.

## Build a lookup/target expression for products

- You can select a product as base targeting and then add additional targeting as described in one of the three attribute methods above.
- If you have existing products in the system that you want to look up, then select **Select Product**. This accesses the **Select Product** screen, which displays a list of products.
- You can start your search by **Name** or **Product ID**.
- The additional four options in the search criteria are: Contains, Starts with, Ends with, Equals.
- There are five checkboxes at the top of the screen: Rate Card, Reporting, Seasonal, Custom, Inactive. By default, Rate Card and Reporting are selected. These filters are used to narrow down your search, especially if you have a lot of products.
- If you wanted to start with a product, and then add additional attributes and attribute values, you can do that from the **Lookup Builder** screen. Select an attribute from the middle column, and select **Update**. The new attribute value will now be shown in the **Lookup Builder** screen.

### Run/add to batch

Once you have built your lookup(s), you can either Run it directly or you can Add to Batch.

- Run - This is for individual lookups. When you select **Run**, a message appears at the top of the screen that says **Currently running 1 lookup item(s)**. Supertext is also displayed on the **Lookup Results** tab that says (1 item). Proceed to **Lookup Results** for next steps.
- Add to Batch - This is used when you are building numerous target expressions that are grouped together. It allows you to run them, and continue to work on other tasks. It runs in a different thread in the background.

## Related topics

- [Availability Lookup](availability-lookup.md)
- [Availability Lookup - Quick Start Guide](availability-lookup-quick-start-guide.md)
- [Lookup Results](lookup-results.md)
- [Batch Builder](batch-builder.md)
- [Batch Queue](batch-queue.md)
