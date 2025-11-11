---
title: Deals screen in Microsoft Monetize
description: In this article, find information on Deals acreen in Microsoft Monetize and its features along with technical details.
ms.date: 11/11/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# Deals screen in Microsoft Monetize

The Deals screen in Microsoft Monetize is your central workspace for managing all types of deals. From a single view, you can create, edit, monitor, and troubleshoot deals across your account.

You can use the unified list to see every deal in one place, or switch to the dedicated tabs to focus on a specific deal type. The interface offers flexible sorting and filtering options and highlights real-time health and performance insights, helping you track and optimize deals efficiently.

## Key benefits

- **Unified management**: Work with all deal types in one place using a consistent, intuitive interface.
- **Flexible grid layout**: Customize columns, adjust size, and apply multilevel sorting to organize data your way.
- **Powerful discovery**: Quickly find deals using search and advanced filters, including multi-ID lookups.
- **Efficient editing**: Use the side pane to make quick updates, review deal health and performance, check eligibility, and troubleshoot issues.
- **Repeatable workflows**: Save and share views with URL bookmarking for fast access to commonly used setups.
- **Bulk updates**: Apply changes to multiple deals at once to manage operations at scale.

## Access the Deals screen

1. Sign in to Microsoft Monetize with your account credentials.

1. In the navigation bar, select **Deals**.

1. The **All deals** view opens by default. To focus on a specific deal type, use the tabs at the top to switch views.

## The grid: Customize your view

The grid is your main workspace for managing deals. It’s flexible and adapts to your workflow, allowing you to view and interact with deal data efficiently.

### Time range

The current time range appears in the upper-right corner of the grid.

1. Select the time range to open the list of available options, such as **Last 24 hours**, **Last 7 days**, or **Lifetime**.

1. Choose a range to update the grid with data for that period.

> [!NOTE]
> Some metrics might not be available for longer time ranges, such as Lifetime. The grid automatically updates based on your selection. If a metric isn’t available for the chosen range, it displays Not applicable.

### Columns 

Use the column header or the Edit columns option to adjust what you see in the grid. Columns are highly configurable, allowing you to organize deal data in the way that best fits your workflow.

**Quick adjustments**

- Select a **column header** to open a menu.

- From the menu, you can:
  
    - Hide or show the column.
    - Sort the data.
    - Apply filters specific to that column’s values.

You can also resize columns by dragging their borders to adjust the width for better visibility.

**Advanced configuration**

For more control over your grid layout:

1. Select **Edit columns**.

1. In the panel that opens, you can:

    - View which columns are currently selected.

    - Browse available columns, organized by logical groups.

    - Add or remove columns as needed.

    - Drag and drop to reorder columns.

1. When finished, select **Apply** to update the grid.

> [!TIP]
> Use a compact column set for daily operations, and expand your view when you need deeper performance insights.

To restore the original setup, select **Reset to default** at any time from Edit columns.

### Sorting

By default, the grid is sorted by **Deal ID** (descending) so that the newest deals appear at the top.

**Quick sorting**

- Select any **column header** (for example, Revenue) to sort the grid by that column.

- This action overrides any existing sort order.

**Advanced sorting**

For more control, use Edit sorts to create multilevel sorting rules—for example, sort first by **Revenue**, then by **Priority**.

1. Select **Edit sorts**.

1. In the panel that opens, you can:

    - View which sorts are currently applied.

    - Browse available sorts, organized by logical groups listed in alphabetical order.

    - Add or remove sorts.

    - Set each level to ascending or descending.

    - Drag and drop to reorder levels.

1. When finished, select **Apply** to update the grid.

The **Edit sorts** button displays a badge showing the number of active sort rules. The corresponding column headers in the grid also indicate which sorts are active.

To restore the original setup, select **Reset to default** at any time from Edit sorts.

> [!NOTE]
> Any edits, sorts, and filters you apply affect all tabs, not just the current one.

## Filtering and Search

### Filters

By default, only **active deals** are shown to keep the view focused on in-progress activity.

**Apply filters**

1. Select **Filters** to open the filter panel.

1. Browse the available filters, listed alphabetically for easier discovery.

1. Add one or more filters as needed, then select **Apply**.

    - The grid updates to display only the deals that match the selected filters.

**Remove filters**

- To remove a filter, select the **x** on its tag.

- The grid refreshes to show a broader view of deals.

> [!NOTE]
> **Archived deals** are hidden by default. To view them, select **Filters → Archived → Only show archived deals → Apply**.
> Archived and non-archived deals are never shown together in the grid to avoid confusion.

**Search**

Use the search box to quickly find specific deals in the grid. You can search by:

- Deal name

- Deal ID

- Line item ID

- Deal code

To search for multiple deals at once, enter a comma-separated list of **Deal ID**s. The grid updates to show only the matching deals.

## Saveable Views (URL Bookmarking)


Your current grid configuration—including **columns**, **sorts**, **filters**, and **time range**—is automatically encoded in the page URL.

- **Bookmark the URL** to return to the same view later.

- **Share the URL** with teammates to use a consistent setup across your team.

- **Create multiple bookmarks** to quickly switch between different workflows.

> [!NOTE]
> Your preferences are stored locally in your browser. You don’t need to reconfigure the grid each time you sign in—unless you clear your cookies.


## Export (download)

Use **Download** to export your deals—including all associated metrics—to a file for offline analysis or sharing.

> [!TIP]
> Choose the file format that best fits your workflow. Exports are useful for detailed reporting, troubleshooting, or sharing data with other teams.

## Create deals

You can create a new deal from scratch, from a template, or by duplicating an existing one.

### Create a deal from scratch

1. At the top of the grid, select **Create**.

1. Choose the type of deal you want to create:

    - [Standard deal](create-a-simplified-deal-line-item.md)

    - [Guaranteed deal](create-a-simplified-programmatic-guaranteed-deal.md)

    - [Code-mapped deal](create-a-code-mapped-deal.md)

1. Complete all required fields.

1. Select **Save**.

The new deal appears in the grid. If the default **Deal ID** (descending) sort is active, it will display at the top.

If the deal doesn’t appear immediately, select **Refresh** in the upper-right corner.

### Create a deal from a template

1. In the grid, select an existing deal to use as a template.

1. Select **Use templates**.

1. A new form opens, prepopulated with the source deal’s details.

1. Make any necessary edits and select **Save**.
   
### Save and duplicate

After saving a deal, select ** Save and duplicate** to create another deal prepopulated with the current deal’s details.
Repeat as needed to streamline bulk deal creation.

## Edit Deals and Side Pane

## Quick edit

To make a fast update, select the **edit icon** (pencil) in the **Name** column of the grid.
The icon appears when you hover your pointer over the column.

## Side pane (row click)

Select any row to open the **side pane**, which provides additional context and tools for managing the deal. You can resize or collapse the pane to fit your screen and workflow.

The side pane includes multiple tabs, each offering detailed information about the selected deal:

- **Settings**: Review and update the deal configuration.

- **Analytics** (*Guaranteed deals only*): View pacing and delivery details for the deal’s flight.

- **Deal health**: Get a quick view of key health indicators.

- **Performance**: View recent performance metrics for Last 10 minutes, Last hour, or Last 24 hours.

- **Eligibility**: Review Ineligible reasons with corresponding error counts and percentages for the selected time frame.

- **Troubleshooting**:

    - View a snapshot of the impression funnel.

    - Run a bid error report.

    - Use the request sampler to inspect bid requests sent to external DSPs.

        > [!NOTE]
        > Sensitive information is stripped from sampled requests to ensure privacy compliance.

- **History**: View a full change log for the deal.
  
### Bulk actions

Select multiple deals in the grid to access bulk actions from the top toolbar. These actions help you manage several deals at once:

- **Activate**: Turn on selected deals so they begin serving.

- **Deactivate**: Pause selected deals without deleting them.

- **Archive**: Move deals out of the active view for record-keeping.

- **Delete**: Permanently remove selected deals.

- **Run report**: Generate a performance report for the selected deals.

## Tips and best practices

- Use templates and duplication for efficiency: Create multiple deals quickly with templates or the Save and duplicate option to streamline bulk setup.

- Verify the time range before analyzing metrics: Some fields and performance metrics may be unavailable for extended time ranges such as Lifetime.

- Standardize views with URL bookmarks: Share bookmarked URLs with your team to maintain consistent configurations and reduce time to insight.

## Troubleshooting and FAQs

**Q: Why don’t I see a new deal I just created?**
**A**: Make sure the grid is refreshed. If the default Deal ID (descending) sort is active, new deals should appear at the top.
Check your current filters (for example, State: Active) to confirm the new deal meets the filter criteria.

**Q: Why are some metrics blank when I select “Lifetime”?**
**A**: Longer time ranges may not support all metrics.
Switch to Last 7 days or Last 24 hours to view more real-time fields.

**Q: How can I view archived deals?**
**A**: Go to **Filters → Archived → Only show archived deals → Apply**.
Archived and non-archived deals are not shown together to prevent confusion.

**Q: Can I save a specific view?**
**A**: Yes. The page URL encodes your columns, sorts, filters, and time range.
Bookmark or share the URL to replicate the same view later.

**Q: How do I run a report on multiple deals?**
**A**: Select the desired deals in the grid, then choose Run report from the bulk actions menu.

**Q: Where can I view pacing for Programmatic Guaranteed deals?**
**A**: Open the deal’s side pane and go to the Analytics tab (available only for Programmatic Guaranteed deals).

**Q: How do I add a column to the grid?**
**A**: Select Edit columns in the upper-right corner.
From the panel, browse available columns and select the ones you want to add.

**Q: How do I reorder columns in the grid?**
**A**: Select Edit columns in the upper-right corner.
Drag and drop from the list of selected columns to set the display order in the grid.

## Related topics

- [Microsoft Monetize – Impression funnel](impression-funnel.md)  
- [Troubleshooting reports](troubleshooting-reports.md)  
- [Microsoft Monetize – Sample bid requests](sample-bid-requests.md)
- [Deal Archival](automated-deal-archival.md) 
