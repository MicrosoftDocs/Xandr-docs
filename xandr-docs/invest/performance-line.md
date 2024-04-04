---
title: Performance Line
description: Learn about the Performance Line feature in Microsoft Invest UI that utilizes automated bidding. This new workflow seeks to enhance the efficiency and effectiveness of ad buying for advertisers.
ms.date: 04/04/2024
---

# Performance line

> [!NOTE]
> This feature is currently in Alpha and may undergo changes without notice. Contact your Microsoft Advertising Account Representative to enable it.

This document outlines how to serve performance campaigns from Microsoft Invest users using the MSAN Bidder. The goal is to potentially improve Return on Ad Spend (ROAS). It not only accessing Microsoft's advertising inventory but also utilizes bidding strategies available within the MSAN (Microsoft Audience Network) to optimize performance.

Advertisers set up two main objects in the Microsoft Invest DSP:

- Performance Insertion Orders (PIO): Maps 1:1 with MSAN campaigns.
- Performance Line Items (PLI): Maps 1:1 with MSAN Ad Group.

## Performance lifecycle overview

When a user creates a performance line item in Microsoft Invest, it undergoes processing through various services:

1. Microsoft Invest Buy-side setup UI.
1. Microsoft Invest Buy-side API.
1. MSAN API (translates objects from Microsoft Invest API to MSAN Data Model).
1. MSAN Bidder.

The PIO and PLI have specific features for budgeting, configurations, and targeting. Once a user sets up these objects in the Microsoft Invest UI, they are sent to an object translation layer that maps the Xandr data model to fields within the MSAN data model. These objects are then saved and synchronized to both the Console and Azure production databases, ensuring that all relevant systems are synchronized and up-to-date with the latest data. Once saved on the MSAN side, the MSAN bidder utilizes automated bidding for the advertiser’s campaigns.

## Create a Performance Insertion Order

The Performance Insertion Order maps 1:1 with the MSAN campaign and allows clients to configure basic settings (name, state, currency), campaign budgeting parameters, and labels/comments.

1. On the Insertion Order **Create** or **Edit** page, a new insertion order type is available. Select **Microsoft Enhanced Performance** from the type selector.
1. Fill out the **Basic Settings**, which include information such as name, budget, and billing details. For more information on these settings, see [Basic Settings](#basic-settings).
1. Optionally, assign reporting labels. The labels (**Trafficker**, **Sales Rep**, and **Insertion Order Type**) then appear in the [Member Analytics Report](network-analytics-report.md). For more information, see [Reporting Labels](reporting-labels.md).
1. Optionally, add comments to the insertion order.
1. Click **Save** to save the insertion order. Alternatively, click the arrow next to **Save** and select **Save and Create Line Item** to go directly to creating a line item associated with this insertion order. Updates are now sent to the Buyside API, which handles the translation from the Xandr data model to the MSAN data model.

### Basic Settings

| Field  | Description  |
|:---------|:---------|
| **Name** | The name of the insertion order. You can later search for and report on the insertion order using this name. |
| **External Code** (optional) | An external code used for reporting. (Microsoft Advertising also assigns an internal code automatically.) The code may only contain alphanumeric characters, periods, underscores, or dashes. It's not case-sensitive (upper- and lower-case characters are treated the same). |
| **Billing Code** (optional) | An internal billing code you want to appear on invoices for this insertion order if you receive insertion-order-specific invoices. For details on invoices, see [Understanding Your Invoice](understanding-your-invoice.md). |
| **State** | The state of the insertion order. If set to **Active**, child line items and campaigns are eligible to serve. |
| **Billing Periods** |  Billing periods allow you to allocate portions of your marketing budget to discrete periods of time. You can associate an external code with a billing period for reporting and invoicing. Any line item flight dates must occur within the dates of the parent insertion order's billing periods.<br><br> You may set both a start and an end date (**Set Dates**) or set a start date without an end date (**No Dates**). If you select **No End Date**, you can only create a single billing period on the insertion order, but you may still specify multiple flights with end dates on the line item. If you select **Set Dates**, you can create up to 52 billing periods. |
| **Budget** | Determines how quickly budget is spent over the lifetime of the insertion order. Set a custom daily budget to define your own pacing. Budgeting components are limited to one budget interval; MSAN campaigns don't support multiple intervals. Both a start date and a budget must be set.<br><br>**Important:**<br>You can set budgets at the line item level, but your insertion order budget takes precedence. When your insertion order budget runs out, all objects under the insertion order will stop buying impressions, whether or not they have reached their own budget limits. |
| **Bid Strategy** | Determines how much advertisers want to spend on ad placements. The field is set to enhanced CPC by default and cannot be changed.<br>**Read-only.**|

## Create a Performance Line Item

The Performance Line Item maps 1:1 with MSAN Ad Group and allows clients to configure basic settings, creatives, and targeting parameters.

You can create a new performance line item from the **Create New Line Item** screen.

1. Select **Line Items** > **Create New** or click **+New** from the Line Items screen. The **Create New Line Item** screen displays.
1. Select the **Microsoft Enhanced Performance** option under **Line Item Type**.
1. Search and select an advertiser from the **Advertiser** text field.
1. Search and select the Microsoft Enhanced Performance insertion order from the **Insertion Order** text field.
1. Click **Next**.
1. Fill out the **Basic Settings**, which include information such as the name and state. The **Insertion Order** field has the pre-selected performance insertion order. The **Ad type** is a read-only field set to **Native** by default.
1. In the **Budgeting & Scheduling** section, set the **Daypart** details for the line item. **Budget** and **Flight** details are inherited from the currently selected parent PIO. For more information, see [Set up Line Item Budgeting and Scheduling](./set-up-line-item-budgeting-and-scheduling.md).
1. In the **Targeting** section, set the geography, age, gender, and device type targeting for a line item.
     1. **Geography:** Target users by country, region, state, city, metro code, postal code, and political districts.
     1. **Age:** Narrow your targeting to only specific preset age ranges, or you can define custom age ranges.
     1. **Gender:** Narrow your targeting to one gender or the other.
     > [!TIP]
     > If you target specific ages or a specific gender, you should consider selecting **Unknown Age** or **Unknown Gender** as well to avoid severely restricting reach.
     1. **Audience segments:** Target curated lists of users determined to be in the market and ready to buy within a particular category. When you use Microsoft Audience segments, you can only associate hosted creatives with this line item, limiting the use of third-party pixels and measurements. For more information, see [Microsoft In-Market Audiences](./microsoft-in-market-audiences.md).
     1. **Device Type:** Select the checkboxes for each device type that you plan to target. For more information on device types, see [Device Type Targeting](./device-type-targeting-ali.md).
     > [!TIP]
     > **Predictive targeting**
     > This feature in the MSAN side helps find more audiences that are similar to the current selection under the campaign, widening the target audience for impressions.
1. In the **Creatives** section, associate the appropriate creatives with your line item.
1. In the **Reporting Labels & Comments** section, you can optionally assign custom reporting labels (**Trafficker**, **Sales Rep**, **Line Item Type**, and **OMS ID**) to a line item, as well as add comments to a line item for your reference.
1. Click **Save** to save the line item.
