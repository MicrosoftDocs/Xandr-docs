---
title: Explore Global Line Items
description: Explore Global Line Item Management, uncover metrics, get alerts on serving, swiftly access details, manage child campaigns, and perform bulk editing/reporting.
ms.date: 10/28/2023
---

# Explore global line items

The **Global Line Item Management** screen shows you essential metrics about all line items across all advertisers within your network, informs you of conditions preventing line items from serving, provides quick access to each line item's details and child campaigns, and offers bulk editing and reporting options.

This feature is currently available only to select Adserver customers.

The Global Line Item Management screen is where you'll go to manage demand from your direct-sold advertisers, including standard and guaranteed delivery line items.

Things you can do on this page include: - Use filters to quickly identify line items with specific criteria, and save those filters for future use - See delivery and performance metrics - See important line item details and make changes quickly.

## Get to the global line item management screen

To get to the line items screen:

- Select **Advertisers** >  **Line Items** from the navigation menu at the top of the screen,

  or

- From the **Advertisers** screen, find the advertiser whose line items you want to see and click the button in the **Line Items** column.
  This will take you to the line items screen with the Advertiser filter applied for the selected advertiser.

  Publisher users can:

- Select **Orders** >  **Line Items** from the navigation menu at the top of the screen

  or

- Click **All Line Items** in the left panel on the Line Items or Orders screens.

## Filter your line items

On the Global Line Item Management screen, you will see all of the line items you're eligible to view, with a stack of filters in a sidebar on the left. Use the filters to get to the exact line item view you need to work with. Your last applied view will be automatically applied the next time you access the Line Items screen.

The available filters are:

- **Advertiser Filter**: Show only the line items associated with the advertisers you select. Up to ten advertisers are displayed at a time. If you have more than ten advertisers, use the arrows or the page box to page through the list of advertisers. Click **Select All** to filter on all advertisers currently displayed in the filter box. This will not select all advertisers; if you have 200 advertisers and 10 are displayed in the **Advertiser Filter** box, clicking **Select All** will select only the 10 advertisers currently displayed in the filter box. If all advertisers on a filter page are selected, you can click **Deselect All** to remove all those advertisers from your filtering.
- **Insertion Order Filter**: Show only the line items that are associated with certain IOs. The **Insertion Order Filter** box contains a Select All button. This button works the same as the **Select All** button for the **Advertiser Filter**.
- **Delivery Filter**: Drag the scrollbar buttons from either end to show only line items with delivery percentages in a given range. The Delivery filter uses pacing percentages from both impressions and revenue when calculating delivery percentage. The percentages are calculated like this:
  - Impression Pacing Percentage = impressions/(expectedPacing \* 100)
  - Revenue Pacing Percentage = revenue/(expectedPacing \* 100)  
    The filter will return all line items with either an impression pacing percentage or a revenue pacing percentage that fall within the selected range.
- **Priority Filter**: Drag the scrollbar buttons from either end to show only line items with priorities in the given range.
- **Status Filter**: Check the box to show only those line items that have the given status. For more information about line item reservation statuses, see [Guaranteed Delivery](guaranteed-delivery.md).
  Possible statuses:
  - Proposal: The line item is inactive, with start and end dates sometime in the future. It's not ready to serve yet.
  - Scheduled: The line item is not serving and is in one of the following states:
    - The line item and at least one campaign are active, with line item start and end dates in the future and campaign dates within the line item dates.
    - The line item and at least one campaign are active. The line item start date is in the past and the end date is in the future, but the campaign has a start date in the future.
    - Note that if the scheduled line item is a guaranteed line item it is reserving inventory.

  - Reserved: The line item is inactive, with start and end dates sometime in the future, and has a reservation.
  - Live: The line item is active, with a start date in the past and an end date in the future. In addition, at least one campaign under the line item is active, with a start date in the past and an end date in the future.
  - Paused: The line item is not serving and is in one of the following states:
    - The line item is inactive, with a start date in the past and an end date in the future
    - The line item is active, with a start date in the past and an end date in the future, but it has no active campaigns.
  - Canceled: The line item is inactive, with a start date in the past and an end date in the future. It had guaranteed delivery goals, but is no longer serving, and no longer has any inventory reserved for it.
  - Complete: The line item has either delivered its budget in full or has met its end date.
  - Ready: This status has been deprecated.
- **Trafficker Filter**: Enter the name of a trafficker to see only their line items. Note that the trafficker's name must be listed in the **Trafficker** label on the line item in order to match.
- **Salespeople Filter**: Enter the name of a salesperson to see only their line items. Note that the salesperson's name must be listed in the **Salesperson** label on the line item in order to match.
- **Flight Date Filter**: Enter ranges of start and end dates to show only the line items that start and end within that date range.
- **Unlikely to Deliver Filter**: Check the box to show only line items that our forecasting engine has determined are unlikely to meet their delivery goals.
- **Creative Filter**: There are two creative filters, **Missing Creatives** and **Has Creatives**. These filters return opposite data sets, which means that if you select both these filters no line items will be displayed.
  - **Missing Creatives**: Check this box to show only line items that are missing a creative. This is important because line items without creatives can't serve. This filter has the opposite functionality from the Has Creatives filter.
  - **Has Creatives**: Selecting this filter will show line items that meet either of the following criteria:
    - The line item has at least one creative associated with it.
    - All of the line item's associated campaigns have creatives.
      This filter has the opposite functionality from the Missing Ceatives filter.

      Once you choose a filter, a **Filters** panel appears at the top of the page displaying all filters in each group that you have selected. Note that the filters aren't applied dynamically as you select them, they're simply added to the **Filters** list. You must click **Apply All** to apply the selected filters. You can quickly remove a filter by clicking the X next to the filter name, or remove all filters by clicking **Remove All**.

      :::image type="content" source="media/gdali-filter.png" alt-text="Screenshot that explains the status of the filters as reserved and scheduled.":::

## Save views

Filtering provides you with a specific view of your line items. You can save individual views for future use. At the top of the **Filters** sidebar, above the filtering selections, are three options:

- **All Advertisers**. Click this option to return to the Advertisers screen.
- **All Orders**. Click this option to retrieve insertion orders. Your last view of Insertion Orders will be reapplied, even if you didn't save it.
- **All Line Items**. Click this option to retrieve line items. Your last view of Line Items will be reapplied, even if you didn't save it.

When you select filters (as described in the previous section), the **Filters** panel will be displayed above the line items (or insertion orders) showing all the currently selected filters along with an **Apply** button and dropdown menu. The menu contains the following options:

- **Apply**  
  Apply the selected filters to the current display. The filters are not saved.

- **Apply & Save**  
  Apply the selected filters to the current display and save those filters to the currently selected view.

- **Save**  
  Save changes to the currently-selected view. All filters showing in the Filters panel will be saved, even those that have not been applied.

- **Apply & Save As**  
  Apply the selected filters to the current display and save the view with a new name. The name can have a maximum of 99 characters, including spaces.

- **Save As**  
  Save the selected filters and assign a name to that view. The name can have a maximum of 99 characters, including spaces. This option saves all filters currently selected, even if they haven't been applied.

  When you save a view, the name will be displayed in the **Filters** sidebar under the **All Line Items** option (or **All Orders** if you're viewing Insertion Orders). Views are user-specific, so the views you create will be available only to you. This allows each user to create the set of views that is most useful to them.

  You can save up to 10 views for Line Items. (You can save up to 10 more for Insertion Orders.) You can have as many filters within a view as you need.

  To display filtered content using a saved view, click the view name in the **Filters** sidebar.

  To delete a view, click the X to the right of the name in the Filters sidebar.

## Search by name/ID

You can use the search field at the top of the screen to find all line items whose names or IDs include a specific string of characters or numbers.

## Find inactive line items

Line items with the **Inactive** state are shown in italics.

## View/edit line item details

In the line item list, you can see a full, detailed summary along with a graphical view of delivery and performance by clicking the graph icon that appears when you hover over the line item. This will take you to a new screen with detailed information about the line item.

To view a summary of details about a line item, find the line item in the list and click that line item's name. This will open a pane below the list of line items that displays summary information about the selected line item. You can edit some of this information directly from this details pane. Information in any details pane section with a pencil
icon next to the heading can be edited.

:::image type="content" source="media/settings-quick-edit.png" alt-text="Screenshot that explains the basic settings.":::

To edit information in the given section, click the pencil icon in the section heading. This will open a dialog box where you can quickly update and save the information related to the settings in that section.

:::image type="content" source="media/li-basic-settings-quick-edit.png" alt-text="Screenshot that explains the basic settings where you can update and save the information related to the settings in the section.":::

For more information about line item details, see [View Line Item Details](view-line-item-details.md). For complete information on updating all areas of the line item, see [Update Line Items](update-line-items.md).

## View metrics

The metrics on the **Line Items** screen help you quickly assess the performance and delivery of your line items. These metrics are faster and more readily accessible than standard reporting data. This data is cached on a regular basis and shown whenever you open the Line Items screen.

Note that the metrics shown here may not exactly match the data from standard reporting. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).

All data is in Eastern Time (EST).

> [!TIP]
> To sort your line items by any given metric, click on the column name, e.g., **Profit**.

## Intervals

Use the drop-down at the top right of the screen to choose the interval for quickstats. Available intervals include:

- **Today**  
  Current calendar day up to the last hour.
- **Yesterday**  
  Full 24-hour period of the previous calendar day.
- **Last 7 Days**  
  Full 7 days previous to the current calendar day, i.e., excluding
  today.
- **Lifetime**  
  Entire lifetime of each line item, including the current calendar day.

## Export to CSV

Click the **Export to CSV** file to export your data to a comma-separated values (CSV) file. All of your current filters will be applied to the data that is exported. (All rows returned will be exported, not only the rows currently showing on the screen).

## Currency display

You can toggle between displaying currency for each line item in USD (U.S. dollars) or local currency by clicking the $ (USD) and € (local currency) toggle buttons. Local currency is determined by the currency settings for each advertiser. Current exchange rates will be applied. Exchange rates are updated hourly. See [Currency Support](currency-support.md) for more information on currencies.

The following fields will be displayed in local currency when the local currency toggle is selected:

- Rev eCPM
- Rev eCPC
- Rev eCPA
- Rev
- Media Cost
- Profit
- Cost eCPM
- Cost eCPA
- Cost eCPC

  When you sort on any of the columns in the above list, the line items will be sorted according to the USD value. This means that if you've chosen to display in local currency, the values might look out of order because of the exchange rates.

  Any value that was added to the system prior to July 7, 2016 cannot be converted to local currency. In these cases, when you select to display line items with local currency values, no value will be retrieved and you'll see two dashes (--) in that field.

## Columns

The following data is available for each line item. Note that the data always reflects the currently selected interval. (You may not see all columns by default. See "Show/Hide Columns" below for more information on viewing columns.)

| Status | The current status of the line item. See descriptions of each status under Filter Your Line Items above. |
|---|---|
| **Advertiser** | The name of the advertiser. |
| **Order** | The name of the insertion order in which the current line item is contained. |
| **Priority** | The priority contains either the priority of a guaranteed delivery line item or the highest priority of all the campaigns under a standard line item. Campaigns can have a priority between 1 and 10, with 5 being the default. Guaranteed delivery line items typically have priorities ranging from 11 - 20 depending on delivery type (14 is the default). See [Guaranteed Delivery](guaranteed-delivery.md) for more on line item priorities. See [Bidding Priority](bidding-priority.md) for more on campaign priorities. |
| **Start Date** | The date the line item starts. All campaigns within this line item must have date that fall within the line item start and end dates. |
| **End Date** | The date the line item ends. All campaigns within the line item must end by this date. |
| **Expected Delivery** | Impression total that this line item is expected to deliver, based on actual historical delivery and forecasted remaining delivery<br>If the projected delivery is greater than the Lifetime Budget impressions for the line item, this value will be the number of lifetime budgeted impressions.<br>If projected delivery is less than or equal to the Lifetime Budget impressions, **Likely to Underdeliver** will be displayed in parentheses under the number of impressions.<br>**Note** - This number will refer to the number of viewable impressions if the line item has the vCPM revenue type. |
| **Issues** | This field presents you with a graphical representation of possible delivery issues with the line item. Issues represented in this column will be related to the **State** of the line item, the **Flight** dates, issues with a **Creative**, or issues related to **Targeting**. Hover over the issues to see a detailed listing.<br><br>:::image type="content" source="media/issues.png" alt-text="Screenshot that explains the issues when you Hover over the issues to see a detailed listing.":::.<br><br>The issues are color-coded according to the type of issue (State, Flight, Creative, or Targeting). One issue will be described below the color bar, along with the number of additional issues that exist. All issues will be outlined in the **Issues** box when you hover over the field. See [Issue Types](explore-global-line-items.md#issue-types) below for a list of possible issues that can be displayed and further description. |
|**Pulse** | This field aggregates impression, clicks, and revenue in real time to help determine pacing of ad spend. This value is updated approximately every minute. The data is reset at midnight in the line item's time zone. |
| **Imps** | Number of impressions for the line item (and any campaigns under the line item) during the selected time period. |
| Pace to Date | This column displays current delivery pacing and expected delivery for the line item. See "Understanding Pacing Bars" below for details on the pacing information in this column. |
| **Revenue Type** | Based on the revenue type and value chosen when the line item was created. Here is a list of possible values and their corresponding revenue types:<br> - **cpm**: CPM and a revenue value specified<br> - **est_cpm**: CPM and no revenue value or margin specified<br> - **cpc**: CPC<br> - **cpa**: CPA<br> - **cost_plus_cp**m: Cost Plus with a CPM revenue value<br> - **cost_plus_margin**: Cost Plus with a Margin revenue value<br> - **flat_fee**: Fixed Fee<br> - **vcpm**: Viewable CPM<br> - **none**: Do not track Revenue |
| **Revenue Value** | The revenue value specified under the revenue type when the line item was created. |
| **Rev eCPM** | Money the advertiser has paid or will pay your network per 1000 impressions. |
| **Lifetime Budget** | The Lifetime Budget specified when the line item was created. This is the budget that the advertiser has allocated for you to spend over the entire lifetime of the line item. This value will be:<br> - The monetary amount allocated<br> - The number of impressions to buy<br> - Unlimited |
|**Daily Budget** | If a custom Lifetime Budget was specified, the Daily Budget will contain value specified when the line item was created. This is the budget that the advertiser has allocated for you to spend on any single day. This column will contain one of the following for either impressons or revenue:<br> - The amount to spend per day for this line item<br> - The pacing lifetime budget along with the estimated spend per day<br> - Unlimited |
| **Clicks** | Number of clicks for all campaigns under the line item. |
| **CTR** | The overall click-through rate on this line item's creatives. |
| **Conversions** | Number of times conversion pixels under the line item have loaded. Note that a conversion pixel load does not necessarily mean that a conversion was attributed to one of the advertiser's campaigns. |
| **Media Cost** | Money your network has spent buying media for campaigns under the line item. |
| **Remaining Days** | The number of days between today and the end date for the line item.<br><br>The progress bar provides a visual representation of how far into the flight the line item is.<br>:::image type="content" source="media/remaining-days.png" alt-text="Screenshot that explains the number of days between today and the end date for the line item."::: <br><br> - The numbers inside the progress bar indicate: Number of days since the flight started / Total number of days in the flight<br> - Below the progress bar will be one of the following:<br>&nbsp;&nbsp; - Number of days remaining in the flight<br>&nbsp;&nbsp; - The start date of the flight if that date is in the future<br>&nbsp;&nbsp; - The end date of the flight if that date is in the past<br>If no end date has been set, you'll see a message saying "End date not set" rather than a progress bar. |
| **Profit** | Money your network has made from the advertiser as a result of campaigns under the line item. This is revenue minus media cost. |
| **Cost eCPM** | Money your network has spent buying media per 1000 impressions. |
| **Rev eCPC** | Money the advertiser has paid or will pay your network per 1000 click-throughs. |
| **Cost eCPC** | Money your network has spent buying media per 1000 click-throughs. |
| **Rev eCPA** | Money the advertiser has paid or will pay your network per 1000 attributed conversions. |
| **Campaigns** | This column contains a button displaying the number of campaigns associated with this line item. Click the button to navigate to the **Campaigns** screen. |
| **Creatives** | If creatives are associated with this line item (or no creatives have been assigned) this column contains a button showing the number of creatives assigned. Clicking the button will open the **Associated Creatives** dialog. If creatives were assigned at the campaign level, this column will display **Campaign Level**. |
| **Rev** | Money the advertiser has paid or will pay your network as a result of campaigns under the line item. |
| **Cost eCPA** | Money your network has spent buying media per 1000 attributed conversions. |
| **Viewable Imps** | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| **View-Measured Imps** | The total number of impressions that were measured for viewability. |
| **Viewability Rate** | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| **View Measurement Rate** | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |

To get information about attributed conversions, rather than just conversion pixel loads as shown in the **Conversions** column, see [Reporting on Conversions](reporting-on-conversions.md).

## Issue types

| Issue Type | Message | Description |
|--|--|--|
| **State** | IO is inactive | The insertion order is set to inactive and isn't serving. See [Update Insertion Orders](update-insertion-orders.md) to activate your IO. |
| **State**  | LI is inactive | The line item is set to inactive and isn't serving. See [Update Line Items](update-line-items.md) to activate your LI. |
| **State** | ADV is inactive | The advertiser is set to inactive and isn't serving. See [Explore and Manage Advertisers](explore-and-manage-advertisers.md) to activate your advertiser. |
|**State**  | ADV requires IOs; this LI doesn’t have any | The advertiser uses insertion orders, but this line item is not associated with an IO. |
| **Flight** | IO flight date expired | The current date is past the end date for the flight on this insertion order. |
|**Flight**  | IO is pre-flight | This insertion order has not yet reached its scheduled start date. |
|**Flight**  | LI flight date expired | The current date is past the end date for the flight on this line item . |
|**Flight**  | LI is pre-flight | This line item has not yet reached its scheduled start date. |
|**Flight**  | IO requires billing periods on the LI | The insertion order contains billing periods, but there are no billing periods on the line item. |
|**Flight**  | LI is between billing periods | The line item isn't serving because the previous billing period has ended but the next billing period hasn't started yet. |
|**Flight**  | LI billing periods not yet started | The start date for the billing period for the line item is in the future. |
|**Flight**  | LI billing periods have expired | The end date for the billing period for the line item has passed. |
| **Creative** | No eligible creatives; associate an active creative to see delivery | The line item has been defined to manage creatives at the line item level, but there are no creatives associated with the line item. See [Create a Standard Line Item](create-a-standard-line-item.md) for more information. |
|**Creative**  | Creatives 1, 2, 3 require landing page URLs | The creative has been defined to use a landing page URL for non-3rd party image and flash creatives that is set at the line item level, but there is no URL defined at the line item. See [Dynamic Landing Pages](dynamic-landing-pages.md) for more information. |
|**Creative**  | Creatives 1, 2, 3 are malicious | The creative has been flagged as containing malware or loading domains placed on blocklists. The creative will not serve. |
|**Creative**  | Creatives 1, 2, 3 size not approved for Outlook | The line item (in the line item, insertion order, or advertiser profile) is targeting outlook.com inventory. Outlook.com requires creatives to be either 100x72 or 160x600, but there are no creatives of that size associated with this line item. |
|**Creative**| SSL audit is required to serve on Outlook | The line item (in the line item, insertion order, or advertiser profile) is targeting outlook.com inventory. This line item has not passed the SSL audit required by outlook.com. |
|**Creative** | Creatives 1, 2, 3 target gambling in [country] | Your network must be specifically placed in an allowlist to serve gambling ads in certain countries. If you're not placed in an allowlist, the specified creatives will not serve. Contact [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) to inquire about being placed in an allowlist. |
|**Creative**  | Creatives 1, 2, 3 failed audit | The line item inventory type has been defined as either "real-time" or "both" and the creative has failed the audit. |
|**Creative**  | Creatives 1, 2, 3 not audited, limiting inventory | The line item inventory type has been defined as either "real-time" or "both" and the creative has not been audited. (Audit could still be pending.) |
|**Creative**  | Creatives 1, 2, 3 are expandable; verify targeted inventory | The specified creatives are expandable. To ensure that these creatives will be able to serve, verify that you're targeting placements that support expandable creatives. |
|**Creative**  | Creative(s) 1, 2, 3 failed AdX audit | The line item inventory type has been defined as either "real-time" or "both" and the specified creatives are targeting Google Ad Manager inventory but have failed the Google Ad Manager audit. See [Google Ad Manager Creative Audit Process](adx-creative-audit-process.md) for more information. |
|**Creative**| LI needs a goal pixel | You must define a goal pixel (conversion pixel) for line items with a revenue type of CPA. |
|**Creative**  | Pixel IDs 1, 2, 3 have no recorded conversions | The line item has a revenue type of CPA but the specified conversion pixels have no recorded conversions. |
| **Targeting**<br><br><br><br><br> | Demographic targeting is limiting delivery | The line item is targeting a specific age range or gender, and does not allow for users where no age or gender is specified. This could limit your delivery to target customers because their age or gender is unknown. See [Demography Targeting](demography-targeting.md) for more information. |
|**Targeting**  | Position targeting is limiting delivery | The line item is targeting a specific position (above or below the fold), and does not allow for impressions where no position is specified. This could limit your delivery because some positions are unknown. See [Page Properties Targeting](page-properties-targeting.md) for more information. |
|**Targeting**  | Targeting only reviewed inventory, but not allowing any sensitive attributes | The line item is set to target only reviewed inventory, but is not allowing any sensitive attributes. This can greatly limit delivery. |
|**Targeting**  | [action1, action2, etc.], are set to include, but do not contain any items | The specified action (for example, browser, carrier, domain, etc.) is set as targeted, but no targets have been specified. See [Create a Domain List or App List](create-a-domain-list-or-app-list.md) for more information. |
|**Targeting**  | A top-level domain is in a blocklist; this could severely limit delivery | Target is excluding a top-level domain (such as .com or .org). This will prevent inventory from serving on any domain ending with that extension. See [Create a Domain List or App List](create-a-domain-list-or-app-list.md) for more information. |
|**Targeting**  | [example-1.com, example-2.com] are in allowlists and blocklists; you will not serve on the domains | The specified domains are both allowed and blocked. The blocklist will take precedence and the line item will not serve on on those domains. See [Create a Domain List or App List](create-a-domain-list-or-app-list.md) for more information. |
|**Targeting**  | Domain targeting on ADV and LI don't intersect | Different domains are targeted on the advertiser and the line item. For example, the advertiser is targeting `example1.com` and the line item is targeting `domain1.com`. This will prevent the line item from serving. |

> [!NOTE]
> No issues will be shown if **Status** is **Complete**.

## Understanding pacing bars

Each pacing bar tells you the following.

:::image type="content" source="media/pacing-bar.png" alt-text="Screenshot that explains the pacing bars.":::

For line items:

- pacing against an impression-based lifetime budget, the pacing bar uses actual vs. expected imps.
- pacing against a revenue-based lifetime budget, the pacing bar uses actual vs. expected booked revenue.
- pacing against a viewable impression-based lifetime budget, the pacing bar uses actual vs. expected viewable imps.

## Requirements for pacing bars

The exact requirements for calculating pacing depend on the quickstats interval selected, the type of budget set, and whether or not there's a
flight end date. For each quickstats interval, the requirements are as follows:

| Quickstats Interval | Requirements |
|--|--|
| Lifetime | Lifetime Budget and Flight End Date |

## Show/hide columns

You can choose the columns that are displayed by clicking the **Configure Columns** button on the upper right.

This opens the **Configure Columns** dialog. From there you can use the checkboxes to select or deselect the columns you want to display.

## Report on line items

You can initiate a report for one or more line items directly from this screen. Check the box for each line item that you want to report on and
click **Actions >  Run Report**. This takes you to the [Advertiser Analytics Report](advertiser-analytics-report.md), where the line items you selected are set as
filters. For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md).

## Create a new line item

To create a new line item, click the **+New** button on the upper left-hand side of the grid.

For instructions on creating a guaranteed delivery line item, see [Create a Guaranteed Delivery Line Item](create-a-guaranteed-delivery-line-item.md).

## Activate/deactivate line items

You can activate or deactivate one or more line items directly from the **Line Items** screen. Check the box next to each line item that you want to activate or deactivate and click **Actions** >  **Activate** or **Actions** >  **Deactivate**.

When you deactivate a line item, the line item will typically stop serving within 10 - 15 seconds, with a maximum wait time of approximately 60 seconds.

## Related topics

- [Working with Line Items](working-with-line-items.md)
- [View Line Item Details](view-line-item-details.md)
- [Update Line Items](update-line-items.md)
- [Create a Guaranteed Delivery Line Item](create-a-guaranteed-delivery-line-item.md)
- [Using Multiple Campaigns with a Guaranteed Line Item](using-multiple-campaigns-with-a-guaranteed-line-item.md)
- [Guaranteed Delivery Pacing](guaranteed-delivery-pacing.md)
