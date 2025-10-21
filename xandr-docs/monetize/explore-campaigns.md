---
title: Explore Campaigns
description: Explore the Campaigns screen, highlight key metrics, detect issues, access campaigns swiftly, and enable bulk editing and reporting.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Explore campaigns

The **Campaigns** screen shows you essential metrics about all campaigns under an advertiser or under a specific line item, informs you of conditions preventing campaigns from serving, provides quick access to each campaign's details, and offers bulk editing and reporting options.

**Automatic archiving of objects:** Campaigns that have not served or been edited in more than 180 days and that are not scheduled to serve in the future are automatically archived. If a campaign is in the "archived" state, it cannot spend or be edited. However, it can still be copied, deleted or used in reports (or exported for use in an external
reporting tool). In addition, once an object is archived, any child objects it may own (e.g., **Insertion Order** >  **Line Item** **> **Campaign**) will also be archived and no additional child objects may be created beneath the archived parent object. For details, see [Automatic Archiving of Buy-Side Objects](automatic-archiving-of-buy-side-objects.md).

## Getting to the campaigns screen

> [!TIP]
> **Lost?**
>
> Did you know that you can verify where you are in Monetize and navigate easily among Monetize pages by using the breadcrumb at the top of all **Advertiser**, **Insertion Order**, **Line Item**, and **Campaign screens**? The rightmost section of the breadcrumb is the page you are on, and all the sections to the left of it are parent object screens. You can click directly on any section to navigate there in one easy step.
>
> The breadcrumb may not function if you are not using the latest version of your browser.

There are two main ways to navigate to the **Campaigns** screen: from the **Advertisers** screen and from the **Line Items** screen. When you navigate from the **Advertisers** screen, you get the complete list of campaigns under the advertiser. When you navigate from the **Line Items** screen, you get the list of campaigns under a specific line item.

## From the advertisers screen

On the **Advertisers** screen, find the advertiser for which you want to view campaigns and click the button in the **Campaigns** column.

This takes you to the **Campaigns** screen. The screen lists all campaigns under the advertiser.

## From the line items screen

On the **Line Items** screen, find the line item for which you want to view campaigns and click the button in the **Campaigns** column.

This takes you to the **Campaigns** screen. The screen lists only the campaigns under the selected line item.

## Viewing and filtering by status

The **Status** column shows you whether your campaigns are eligible or ineligible to serve.

- **Play** - Campaigns with the "play" icon are eligible to serve.
- **Paused** - Campaigns with the "paused" icon are ineligible to serve due to conditions that are likely intentional and user-driven. When a campaign shows this status, hover over the icon to see exactly what conditions are preventing it from serving. The following conditions can provoke this status:
  - State is set to inactive.
  - Flight start is in the future.
  - Flight end is in the past.
  - Lifetime impression budget has been met.
  - Lifetime cost budget has been met.
  - Daily impression budget has been met.
  - Daily cost budget has been met.

  > [!WARNING]
  > Campaigns with the "warning" icon are ineligible to serve due to conditions are are likely unintentional and that should be addressed. When a campaign shows this status, hover over the icon to see exactly what conditions are preventing it from serving. The following conditions can provide this status:
  >
  > - No creatives are associated with this campaign.
  > - All creatives associated to this campaign are either ineligible to serve (inactive, expired, prohibited) or can serve only on direct inventory and on supply partners who trust your network's self-classification (unaudited).

## Searching by name/ID

You can use the search field at the top of the screen to find all campaigns whose names or IDs include a specific string of characters or numbers.

## Finding inactive campaigns

Campaigns with the **Inactive** state are shown with their IDs, names, and stats in italics.

## Viewing stats

The stats on the **Campaigns** screen help you assess the performance and delivery of your campaigns at a glance. These metrics are faster and more readily accessed than via standard reporting; whereas reporting requires you to submit a request and then wait for a response, stats are cached on a regular basis.

Because stats are dependent upon reporting data and are synched after reporting has closed for any given hour, for a small chunk of time each hour, there may be discrepancies between reporting and stats data. For more details, see [Availability of Reporting Data](availability-of-reporting-data.md).

> [!TIP]
> To sort your campaigns by any stat, click on the relevant metric column. For example, to sort yourcampaigns by the amount of money your network has made from advertisers (revenue - media cost), click the **Profit** column.

## Intervals

Use the interval drop-down near the top right of the screen to choose the interval for stats:

- **Today** Current calendar day up to the last hour.
- **Yesterday** Full 24-hour period of the previous calendar day.
- **Last 7 Days** Full 7 days previous to the current calendar day, excluding today.
- **Month to Date** Start of the current calendar month to the current calendar day, including today.
- **Last 365 Days** Full 365 days previous to the current calendar day, excluding today.
- **Lifetime** Entire lifetime of each campaign, including the current calendar day.

## Columns

The following stats are shown for each campaign. Columns that show an arrow in the header when you hover over them are sortable. Note that the data always reflects the currently selected stats interval:

- **Imps** Number of impressions for the campaign.

> [!TIP]
> For campaigns with specific lifetime impression budgets, you can select the **Pacing** toggle to visualize how well the campaigns are pacing for the selected stats interval. For more details, see **Showing/Hiding Pacing Bars**.
>
> - **Clicks** Number of clicks for the campaigns.
>
> - **Convs** Number of times conversion pixels under the parent line item have loaded. Note that a conversion pixel load does not necessarily mean that a conversion was attributed to the campaign. To get information about attributed conversions, rather than just conversion pixel loads, see [Reporting on Conversions](reporting-on-conversions.md).
>
> - **CTR** (Click-Through-Rate) Number of clicks divided by total impressions served for the campaign.
>
> - **Viewable Imps** The number of measured impressions that were viewable, per the IAB Viewability definition, which states that 50% of the pixels of a creative are in-view during 1 consecutive second.
>
> - **View-Measured Imps** The total number of impressions that were measured for viewability.
>
> - **Viewability Rate** The percentage of impressions that were viewable out of the total number of impressions measured for viewability (Viewed Imps / View Measured Imps).
>
> - **Viewability Measurement Rate** The percentage of impressions measured for viewability out of the total number of impressions (View Measured Imps/Imps).
>
> - **Rev** Money the advertiser has paid or will pay your network as a result of the campaign. Using the currency toggle, you can choose whether to show **Rev** in USD or in the currency set at the line item.
>
> - **Media Cost (USD)** Money your network has spent buying media for the campaign. Media Cost always appears in USD, as that is the currency in
>   which Microsoft Advertising transacts. For campaigns with specific lifetime media cost budgets, you can select the **Pacing** toggle to visualize how well the campaigns are pacing for the selected stats
>   interval. For more details, see **Showing/Hiding Pacing Bars**.
>
> - **Profit (USD)** Money your network has made from the advertiser as a result of the campaign. This is revenue - media cost. Profit always appears in USD.
>
> - **Rev eCPM** Money the advertiser has paid or will pay your network per 1000 impressions. Using the currency toggle, you can choose whether to show **Rev eCPM** in USD or in the currency set at the line item.
>
> - **Cost eCPM (USD)** Money your network has spent buying media per 1000 impressions. Cost eCPM always appears in USD, as that is the currency in which Microsoft Advertising transacts.
>
> - **Cost eCPA (USD)** Money your network has spent buying media per conversion. Cost eCPA always appears in USD, as that is the currency in which Microsoft Advertising transacts.

## Showing/Hiding pacing bars

For campaigns that meet certain **Requirements for Pacing Bars**, Microsoft Monetize helps you visualize how well the campaigns are pacing to their budgets for the selected stats interval. When you turn the **Pacing** toggle on, the **Imps** or **Media Cost** quickstat, depending on the type of budget set for the campaign, is transformed into a pacing bar.

It is important to note that pacing bars, like all other stats, reflect the currently selected stats interval, and for each stats interval, there are specific requirements for pacing to be calculated. See **Requirements for Pacing Bars** below for more details.

### Understanding pacing bars

Each pacing bar tells you the following. Note that for a campaign with a media cost budget, the pacing bar will show media cost rather than impressions.

Please keep these points in mind:

- The pacing bar shows **how much of the campaign budget has been spent.**
- The bold black number that appears across the pacing bar shows **the number of impressions or amount of dollar spend that has actually occurred for the campaign.**
- The gray number below the pacing bar shows the **lifetime budget, in impressions or currency.**
- The blue line represents how much of your budget you should have spent: **Lifetime budget/total number of days in the flight x actual number of days in the flight.**
- The percent shows how closely your campaign is pacing according to even daily pacing: **Actual budget spent/how much of your budget you should have spent.** The color of the main pacing bar tells you how your impression/media cost count compares to your pacing target:
- **Purple** - The current impression/media cost count is over the pacing target (\> 100%) for the selected stats interval.
- **Green** - The current impression/media cost count closely matches the pacing target (95% - 100%) for the selected stats interval.
- **Yellow** - The current impression/media cost count is slightly under the pacing target (85% - 95%) for the selected stats interval.
- **Red** - The current impression/media cost count is significantly under the pacing target (\< 85%) for the selected stats interval.

### Requirements for pacing bars

The exact requirements for calculating pacing depend on the stats interval selected, the type of budget set, and whether or not there's a flight end date. For each stats interval, the requirements are as follows:

| Stats Interval | Requirements |
|--|--|
| Lifetime | Lifetime Budget and Flight End Date |

## Showing/Hiding pulse sparklines

The **Pulse** button provides a visualization of campaign spending in real time. When you click the **Pulse** button, a column containing sparklines that represent campaign delivery appears.

> [!TIP]
> **Pulse Keeps Campaigns Healthy**
>
> You can use Pulse to:
>
> - Confirm campaigns are live seconds after they start spending
> - Diagnose delivery issues quickly with a shorter feedback loop
> - Confidently optimize by seeing changes take effect minutes after you make them

## Showing/hiding columns

You can choose the columns that are displayed by clicking the **Configure Columns** button.

This opens the **Configure Columns** dialog. From there you can select or deselect the columns you want to display using the checkboxes. Click **OK** when you are done making your selections to return to the **Campaigns** screen.

## Viewing settings across multiple campaigns

The **Settings** toggle lets you save time and gain valuable insight by reviewing budgets, buying strategies, and frequency caps across multiple campaigns.

### Budgets

To view the **Lifetime Budget** and **Daily Budget** of multiple campaigns at once, select **Settings >  Budget**.

For campaigns using lifetime pacing, you can see the estimated daily budgets, which are calculated based on the remaining budget divided by the number of days remaining in the flight. For more information, see [Lifetime Pacing](lifetime-pacing.md).

### Buying strategies

To view the direct and third-party buying strategies of multiple campaigns at once, select **Settings >  Buying Strategies**.

- **Direct Buying Strategy** - This column shows you the priority for campaigns that buy your own managed inventory.

- **3rd-Party CPM Bid** - This column shows you how bids are calculated for campaigns that buy third-party inventory on a CPM basis.

- **Other 3rd-Party Bids** - This column shows you how bids are calculated for campaigns that buy third-party inventory on a CPA or CPC basis.

  For more details about buying strategies, see [Create a Campaign](create-a-campaign.md) and [Buying Strategies](buying-strategies.md).

### Frequency caps

To view the how frequently creatives associated to campaigns can be shown to a given user, select **Settings** >  **Frequency Caps**.

- If frequency caps are set in a campaign, they are represented as inclusions (green icon).

- If "Show to users without cookies" is **not** set in a campaign, **Unidentified users** is represented as an exclusion (red icon).

  Frequency caps can be set at the advertiser, line item, and creative levels as well. The most restrictive setting always takes precedence.
  For more details, see [Frequency and Recency Caps](frequency-and-recency-caps.md).

## Inventory targeting

You can view inventory targeting settings in the Campaigns screen. When you select **Inventory Targeting** in the Settings toggle, the direct and 3rd-party segment targeting strategiesfor your campaigns, as well as the associated Boolean logic, will appear as columns.

## Viewing a specific campaign's details

There are two ways to view details for a specific campaign: the **Campaign Summary** pane and the **Campaign Details** pane.

### Campaign summary pane

Clicking the row of the campaign whose details you want to view will open the **Campaign Summary** pane on the **Campaigns** screen. You can use the
slider to resize the pane as desired.

### Campaign details screen

You can also click the graph button in the row of the **campaign** whose details you want to view. This takes you to the [View Campaign Details](view-campaign-details.md).

### Reporting on campaigns

You can initiate an advertiser analytics report for one or more campaigns directly from the Campaigns screen. Check the box for each campaign that you want to report on and
click **Actions >  Run Report**.

This takes you to the Advertiser Analytics report, where the campaigns you selected are pre-set as filters and **Campaigns** is pre-set as a dimension. For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md).
