---
title: Check Availability
description: The article explains how to check for available attributes, evaluating impressions, setting criteria, and examining results in the Availability Report panel.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Check availability

The following article explains how to check for available attributes, evaluating impressions, setting criteria, and examining results in the **Availability Report** panel.

## Check available impressions

To check for available impressions, specify your lookup criteria and then view the results in the **Availability Report** panel.

1. On the **Availability Dashboard** page, in the **Availability Tasks** panel, select **Check Availability**. The **Availability Lookup** page appears.
1. In the **Configuration** panel on the left side of the page, select the high-level settings for your lookup, as follows.
    - **Time Period** – This field determines the timeframe for the availability lookup. By default, the lookup is for the next month. Click the link for the current selection (e.g., Next Month). Then in the Time Period dialog that appears, set the timeframe for which you want to check availability.
    - **Group By** – This field determines how available impressions and capacity are broken down in the lookup. By default, the lookup shows total available impressions and capacity only. Click the link for the current selection (e.g., None). Then choose a group from the drop-down list (e.g., select **Weekly** to see available impressions and capacity for each week in the selected time period).
    - **Priority** – This field determines the ad server priority for your availability lookup. By default, the lookup calculates availability by subtracting guaranteed consumption from capacity, regardless of priority. To set a priority, select the link for the current selection (e.g., None). Then in the Priority (DFP) dialog that appears, choose a priority from the drop-down list (e.g., select **4** to see availability for products with a priority of 4 and higher). Note that if you set a priority, availability will be calculated by subtracting all consumption (guaranteed as well as preemptible) from capacity below that priority level.  
    - **Frequency Cap** – This field determines the maximum number of times an ad should appear for a given user for a given number of minutes, hours, days, weeks, months, or for the lifetime of the ad. Available impressions and capacity are adjusted based on the cap you set. To set a frequency cap, select the current selection (e.g., None), Then in the Frequency Cap dialog that appears, type the maximum number of views for the timeframe you want (e.g., for a weekly frequency of 3, set the frequency cap to be 3 views per 1 week).
1. In the **Lookup Criteria** panel, select the product attributes you want to use for your lookup.
    - To start with the attributes of an existing product, select it from the Products list. To start with the attributes across a product group, select **Group**, and select a product group from the list that appears.
    - To specify additional attributes, select them from the Attributes list. You can search for products/product groups by typing in the filter field at the top of each list. As you type, the list of products/product groups is narrowed accordingly.
1. In the **Lookup Request** panel, review the product criteria you selected and specify the values for the attributes you chose.
    - To specify attribute values, select the **click to add attribute values** link. Add the values you want to look up, and then select **Update**. You can type the values you want to look up or you can choose them from a comprehensive list by selecting **Select** and adding/removing values in the Attribute Values dialog.
    - By default, the lookup criteria you selected in step 3 appear in the Products must match all of these criteria box. Products that match all criteria in this box are returned in the lookup results. To have your lookup exclude results with certain attributes, select **Include**. Then select **Exclude** from the drop-down list that appears.
    - To have your lookup also match any of a set of criteria, select the **And any of these criteria** box. Select attributes from the **Lookup Criteria** panel. Then specify the values for the attributes you chose.
1. (Optional) Add an advanced lookup option.
    - You can set up an OR lookup by selecting **Advanced**. Then select **Create Complex** Product. The lookup returns all products that match either set of criteria you define.
    - You can run a lookup for several values at the same time by selecting **Advanced**. Then select **Create Product** Variants. The lookup returns products that match all of the values in the main criteria, and each of the values in the Vary these attributes box.
1. Click **Check Availability**. The **Availability Report** panel displays the available inventory based on your lookup criteria.

After you check availability the structure of your query is retained, so you can use the previous lookup as a template for a new one.

## Save an availability lookup

You can save a lookup for available inventory to run again later.

1. On the **Availability Lookup** page, set up a new lookup for availability based on a combination of targeting attributes or open an existing saved lookup, and then select **Save**. The **Availability Lookup** dialog appears.
1. To save as a new lookup, select the **Save as New option** (default). To replace an existing saved lookup, select the **Replace Existing** option (enabled only if you have already saved at least one lookup).
1. In the **Name** field, type a name to summarize the lookup or select from the list of existing lookups (available only if you selected to replace an existing lookup). In the **Description** field, type a detailed description for the lookup, and then select **OK**.

## Open a saved availability lookup

You can open a saved availability lookup to rerun it or edit the details of the lookup.

1. On the Availability Lookup page, select **Open**. The Availability Lookup dialog appears.
1. Select an existing lookup from the list. You can search for an existing lookup by typing in the field at the top of the dialog. The list of lookups is narrowed as you type.

## Create an availability batch lookup

You can run multiple availability lookups as part of a single availability report, by creating a batch lookup.

1. Set up a new lookup for availability based on a combination of targeting attributes or open an existing saved lookup. Then select **Add to Batch**. The **Availability Report** panel displays the available inventory based on your lookup criteria, excluding CPM, impressions, and capacity.
1. Modify the lookup criteria to set up a different set of targeting, and select **Add to Batch**. The **Availability Report** panel is updated with the available inventory based on your original lookup criteria and the new lookup criteria.
1. Repeat step 2 as needed. Then select **Run Batch**.
1. On the confirmation dialog that appears, note the batch lookup name, and then select **OK**.

> [!TIP]
> The lookup query that you set up on this screen will be broken out into multiple result rows that will appear in the **Availability Report** panel at the bottom of the screen once you select **Add to Batch**. The maximum number of rows is capped at 10,000 by default. That figure represents a reasonable limit, which is configurable at your request. Please contact your Client Services Manager if you feel that a higher ceiling is necessary.

## View availability batch lookups

You can check the status of your batch availability lookups and view the resulting Availability reports.

1. On the **Availability Dashboard** page, in the **Availability Tasks** panel, select **View Batch Lookups**. The **View Batch Lookups** page appears.
1. (Optional) In the **Filters** panel on the left side of the page, look for batch lookups by name or by the user who created the batch.
1. In the **Availability reports** panel on the right, select a link in the **Name** column to view the results of the batch in the **Availability Reports** panel on the **Availability Lookup** page. You can also export the results of the batch to an Excel file or a comma-separated values file by selecting **XLS** or **CSV** in the **Export** column.

## View availability in a calendar

You can view daily availability in a calendar for a given month, to find openings for new deals. This is especially useful for sponsorships.

To view the calendar:

1. On the **Availability Dashboard** page, in the **Availability Tasks** panel, select **View Calendar**. The **View Calendar** page appears.
1. In the **Filter** panel on the left side of the page, in the **Configuration** section, select how you want availability to be displayed:
    1. In the **Show Availability As** list, choose to see availability as a percentage of available impressions or as the number of available impressions.
    1. In the **Availability Based On** list, choose whether you want to see availability based on all order lines, or only order lines in sponsorship/exclusive campaigns.
    1. In the **Consumption Type** list, choose whether you want to see availability based on consumption type (Contained, Direct, and Indirect).
    1. On the **Colors** slider, determine the percentages you want to use to determine whether a date is available for booking. The calendar shows you at a glance the dates that meet these percentages as follows: Dates displayed in green are available for booking. Dates displayed in yellow have some inventory available for booking. Dates displayed in red are unavailable for booking.
1. In the **Filter** panel on the left side of the page, in the **Lookup Criteria** section, select the product groups, products, and targeting you want to use for lookup. For example, you may want to choose a product group for sponsorships only and targeting for a particular demographic. As soon as you choose a product, the calendar view is populated accordingly and is refreshed automatically as you change your criteria (e.g., if you add targeting). By default, availability is displayed for the current month. You can change this using the month filter on the calendar toolbar. Mouse over a date to see a summary of availability. This includes capacity, availability, and sell-through information, as well as the number of booked, pending, and proposed order lines.
1. To see the full details for a particular date, select that date on the calendar. The page is redisplayed in a table (also referred to as the list view) with the date you selected expanded by default.

## Switch between the calendar and list views

The **View Calendar** page can be displayed in two views:

- A calendar view that shows a graphical high-level overview of each day on the selected month's calendar.
- A list view that shows the month in a table where each row can be expanded to drill down for detailed information for a given day.

To switch from the calendar view (default) to the list view, on the calendar toolbar, select.

To switch from the list view to the calendar view, on the calendar toolbar, select.

## Related topics

- [Anatomy of the Availability Lookup Page](anatomy-of-the-availability-lookup-page.md)
- [Create an Availability Batch Lookup](create-an-availability-batch-lookup.md)
- [View Availability Batch Lookups](view-availability-batch-lookups.md)
- [Availability Overview (Old Workflow)](availability-overview-old-workflow.md)
- [Save an Availability Lookup](save-an-availability-lookup.md)
- [Open a Saved Availability Lookup](open-a-saved-availability-lookup.md)
