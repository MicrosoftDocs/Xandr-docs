---
title: Explore Global Insertion Orders
description: Explore global insertion orders, showcase metrics for direct-sold advertisers, enable swift access to details, and offer bulk editing/reporting options.
ms.date: 10/28/2023
---

# Explore global insertion orders

The **Insertion Orders** screen shows you essential metrics about all insertion orders under all your direct-sold advertisers, provides quick access to each insertion order's details, and offers bulk editing and reporting options.

> [!NOTE]
> This page provides information about the global Insertion Order screen available to adserver clients. This screen shows all insertion orders for multiple advertisers on one page. See [Explore Insertion Orders](explore-insertion-orders.md) for information about the Insertion Order screen with single advertiser view.

Things you can do on this page include:

- Navigate to insertion orders quickly using filters
- See performance metrics
- Drill down into line items to configure or troubleshoot
- Create and edit insertion orders

## Get to the insertion orders screen

To get to the insertion orders screen, so one of the following:

- Select **Orders** from the navigation menu at the top of the screen. (This may be located under the **Advertiser** menu option.)
- Click **All Orders** in the left panel on the **Insertion Orders** or Line Items screens.
- On the **Advertisers** screen, find the advertiser for which you want to view insertion orders and click the button in the **Ins Orders** column. (This will take you to a filtered view of insertion orders for that advertiser.)

## Filter your insertion orders

### Filtering by status

The selector dropdown at the top of the screen lets you filter for insertion orders based on status. You can choose to view only **Active** advertisers or **Inactive** advertisers, or to view **All** advertisers.

### Filter Sidebar

On the left side of the Insertion Order screen is a list of filters in a sidebar. Use the filters to view only the insertion orders you want to work with.

The available filters are:

- **Advertiser Filter**: Show only the line items associated with the advertisers you select. Up to ten advertisers are displayed at a time.
  If you have more than ten advertisers, use the arrows or the page box to page through the list of advertisers. Click **Select All** to filter on all advertisers currently displayed in the filter box. This will not select all advertisers; if you have 200 advertisers and 10 are displayed in the **Advertiser Filter** box, clicking **Select All** will select only those 10 advertisers. If all advertisers on a filter page are selected, you can click **Deselect All** to remove all those advertisers from your filtering.

- **Trafficker Filter**: Enter the name of a trafficker to see only their insertion orders. Note that the trafficker's name must be listed in the **Trafficker** label on the insertion order in order to match.

- **Salespeople Filter**: Enter the name of a salesperson to see only their insertion orders. Note that the salesperson's name must be listed in the **Salesperson** label on the insertion order in order to match.

- **Flight Date Filter**: Enter ranges of start and end dates to show only the insertion orders that start and end within that date range.
  Once you choose a filter, a **Filters** panel appears at the top of the page displaying all filters in each group that you've selected.
  You can quickly remove a filter by clicking the X next to the filter name, or remove all filters by clicking **Remove All**.

## Saving views

Filtering provides you with a specific view of your insertion orders. You can save individual views for future use. At the top of the **Filters** sidebar, above the filtering selections, are three options:

- **All Advertisers**. Click this option to return to the **Advertisers** screen.

- **All Orders**. Click this option to retrieve insertion orders. Your last view of filters you had applied in the **Insertion Order** view will be reapplied, even if you didn't save it.

- **All Line Items**. Click this option to retrieve line items. Your last view of Line Items will be reapplied, even if you didn't save it.

  When you select filters (as described in the previous section), the **Filters** panel will be displayed above the insertion orders (or line items) showing all the currently selected filters along with a **Save** button and dropdown menu. The menu contains the following options:

- **Save**  
  Save changes to the currently-selected view. All filters showing in the **Filters** panel will be saved.

- **Save As**  
  Save the selected filters and assign a name to that view. The name can have a maximum of 99 characters, including spaces.

  When you save a view, the name will be displayed in the **Filters** sidebar under the **All Orders** option (or **All Line Items** if you're in Line Item view). Views are user-specific, so the views you create will be available only to you. This allows each user to create the set of views that is most useful to them.

  You can save up to 10 views for Insertion Orders. (You can save up to 10 more for Line Items.) You can have as many filters within a view as you need.

  To display filtered content using a saved view, click the view name in the **Filters** sidebar.

  To delete a view, click the X to the right of the name in the **Filters** sidebar.

## View stats

The metrics on the **Insertion Orders** screen help you quickly assess the performance and delivery of your insertion orders. These metrics are faster and more readily accessed
than standard reporting data. They are cached on a regular basis and are khown whenever you open the **Insertion Orders** screen.

> [!NOTE]
> These stats may not match the data from standard reporting exactly for technical reasons. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).
> [!TIP]
> To sort your insertion orders by any given stat, click on that stat's column name (e.g., **Profit**)

## Intervals

Use the dropdown at the top right of the screen to choose the interval for stats:

| Today | Current calendar day up to the last hour. |
|---|---|
| **Yesterday** | Full 24-hour period of the previous calendar day. |
| **Last 7 Days** | Full 7 days previous to the current calendar day, i.e., excluding today. |
| **Lifetime** | Entire lifetime of each insertion order, including the current calendar day. |

## Currency

You can toggle between displaying currency for each line item in USD (U.S. dollars) or local currency by clicking the $ (USD) and € (local currency) toggle buttons. Local currency is determined by the currency settings for each advertiser. Current exchange rates will be applied. Exchange rates are updated hourly. See [Currency Support](currency-support.md) for more information on currencies.

The following fields will be displayed in local currency when the local currency toggle is selected:

- Rev eCPM

- Rev

  When you sort on either of the columns above, the line items will be sorted according to the USD value. This means that if you've chosen to display in local currency, the values might look out of order because of the exchange rates.

  Any value that was added to the system prior to July 7, 2016 cannot be converted to local currency. In these cases, when you select to display line items with local currency values, no value will be retrieved and you'll see two dashes (--) in that field.

### Columns

The following stats are shown for each insertion order. Note that the data always reflects the currently selected stats interval:

| Clicks | Number of clicks for all campaigns under the insertion order. |
|--|--|
| **Convs** | Number of times conversion pixels under the insertion order have loaded. Note that a conversion pixel load does not necessarily mean that a conversion was attributed to one of the advertiser's campaigns. |
| **CTR** | Click-through rate. |
| **Rev** | Money the advertiser has paid or will pay your network as a result of campaigns under the insertion order. This is based on revenue settings at the line item level. |
| **Media Cost** | Money your network has spent buying media for campaigns under the insertion order. |
| **Profit** | Money your network has made from the advertiser as a result of campaigns under the insertion order. This is revenue minus media cost. |
| **Rev eCPM** | Money the advertiser has paid or will pay your network per 1000 impressions. |

To get information about attributed conversions, rather than just conversion pixel loads as shown in the **Convs** column, see [Reporting on Conversions](reporting-on-conversions.md).

### Show/hide columns

You can choose the columns that are displayed by clicking the **Configure Columns** button.
:::image type="content" source="media/configure-columns-button.png" alt-text="Screenshot that displays the Configure Columns button.":::

This opens the **Configure Columns** dialog. From there you can use the checkboxes to select or deselect the columns you want to display.

### View insertion order details

To view advanced details about an insertion order, click the insertion order's name.

See [View Insertion Order Details](view-insertion-order-details.md) for more information.

### Search by name/ID

You can use the search field at the top of the screen to find all insertion orders whose names or IDs include a specific string of characters or numbers.

### Related topics

- [View Insertion Order Details](view-insertion-order-details.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Update Insertion Orders](update-insertion-orders.md)
