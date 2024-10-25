---
title: Microsoft Monetize - Create an Insertion Order
description: In this article, find step-by-step instructions on how to create and set up an insertion order.
ms.date: 10/28/2023
---

# Microsoft Monetize - Create an insertion order

Insertion orders enable you to better organize, track, and allocate budget to your line items. Associating your line items with insertion orders allows you to preserve historical pacing and performance data across line items under a single insertion order, and to streamline your setup for long-standing advertiser relationships.

For an overview of all buy-side objects, see the [Object Hierarchy](object-hierarchy.md).

## Create a new insertion order

1. On the **Insertion Orders** screen, click on the **New** button.
1. Select the **Advertiser** you want your new insertion order to be associated to.

    > [!NOTE]
    > You can only create insertion orders under advertisers for which insertion orders are enabled. See [Create an Advertiser](create-an-advertiser.md) for more details.

1. Fill out the basic setup, which includes information such as name and budget and billing details. For more information on these settings, see [Basic Setup](#basic-setup).

    > [!NOTE]
    > The **Budget Type** setting in insertion orders may restrict associated guaranteed delivery augmented line items (GDALI) and programmatic guaranteed line items (PGLI) that have conflicting settings. We recommend using an insertion order with **Budget Type** set to **Flexible** for GDALIs and PGLIs so you can associate both impression-based and revenue-based line items to the same insertion order.

    - Enter a name for the insertion order and optionally enter an external code and/or a billing code.
    - Select a state.

       > [!NOTE]
       > To avoid spending before you're ready, set the state to "**Inactive**" until everything related to the buy has been set up and verified.

    - Optionally, set a currency. If not set, the insertion order will inherit the advertiser's currency. You cannot change the currency after saving the insertion order.

       > [!TIP]
       > As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience. See [Currency Support](currency-support.md).
    - Select a viewability standard.
    - Select a budget type.
    - Optionally, set up billing periods and pacing. For more information, see [Billing Periods](#billing-periods) and [Pacing](#pacing).
    - Optionally, enable political advertising on this insertion order and identify whether this advertising takes place on the federal or state or local level, or both. For more information, see [Political Advertising](#political-advertising).

      > [!NOTE]
      > This option will only appear if you have already declared that this advertiser conducts political advertising on the [advertiser](create-an-advertiser.md).

1. Set the supply strategy, determining the inventory type and inventory lists for targeting. These settings can be further refined on the line item. For more information, see [Inventory Lists (ALI)](inventory-lists-ali-only.md).
    - Select the inventory type:
  
       - **App & Web** (the default),
       - **App Only** (mobile inventory), or
       - **Web Only** (standard websites and websites optimized for browsers on mobile devices).

    - Select an allowlist, or create one directly from the insertion order. This determines the inventory that may be targeted by any line items belonging to this insertion order.

       Allowlists include the Microsoft Advertising Inventory List, a collection of inventory that Microsoft Advertising has selected based on demonstrated demand interest within our marketplace and vetted via additional quality controls (as well as platform inventory quality filtering).

    - Select a blocklist, or create one directly from the insertion order. This determines which inventory will be excluded from targeting by line items belonging to this insertion order. The Microsoft Advertising blocklist is applied by default.

1. If this insertion order contains line items for political advertising, fill out the [Political Advertising](#political-advertising) section.

1. Optionally, set caps for frequency (how many times a user may see ads for this insertion order) and recency (how much time must elapse before a user may see another ad for this insertion order). For more information, see [Frequency and Recency Caps](frequency-and-recency-caps.md).

    > [!IMPORTANT]
    > Frequency caps can also be set at the advertiser, line item, and creative levels. The most restrictive setting always takes precedence.

1. Optionally, assign reporting labels. The labels (**Trafficker**, **Sales Rep**, and **Insertion Order Type**) will then appear in the [Network Analytics Report](network-analytics-report.md). For more information, see [Reporting Labels](reporting-labels.md).

1. Optionally, associate existing augmented line items with the insertion order.

    > [!NOTE]
    > Any budget or impressions that occurred before the line item was associated to the insertion order do not count towards the lifetime budget of the insertion order.

1. Optionally, add comments to the insertion order.
1. Click **Save** to save the insertion order. Alternatively, click the arrow next to **Save** and select **Save and Create Line Item** to go directly to creating a line item associated with this insertion order.

## Basic setup

In the **Basic Setup** section, you enter basic information about the insertion order, such as its name and its budget and billing details. Settings are:

### Name

The name for the insertion order. You will later be able to search for and report on the insertion order using this name.

### External code (optional)

An external code used for reporting. (Microsoft Advertising also assigns an internal code automatically.) The code may only contain alphanumeric characters, periods, underscores or dashes. It is not case-sensitive (upper- and lower-case characters are treated the same).

No two objects at the same level (like line items or campaigns) can use the same code. For example, two lines items cannot both use code "XYZ", but a single line item and its child campaign can.

### Billing code (optional)

An internal billing code you want to appear on invoices for this insertion order, if you receive insertion-order-specific invoices. For details on invoices, see [Understanding Your Invoice](understanding-your-invoice.md).

### State

The state of the insertion order. If "**Active**", child line items and campaigns will be eligible to serve.

> [!TIP]
> To avoid spending before you're ready, set the state to "**Inactive**" until everything related to the buy has been set up and verified.

### Currency

If not set, the insertion order will inherit the advertiser's currency. You cannot change the currency after saving the insertion order.

> [!TIP]
> As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience. See [Currency Support](currency-support.md).

### Viewability standard

The viewability standard used for this insertion order. Defaults to **IAB** (Internal Advertising Bureau). For more information, see [Introduction to Viewability](introduction-to-viewability.md).

### Budget type

Determines whether the budget will be allocated by revenue (money) or by impression. All billing periods must have the same budget type.

Select a budget type:

- **Revenue** - use to associate only revenue-based line items to this insertion order.
- **Impression** - use to associate only impression-based line items to this insertion order.
- **Flexible** - use to associate both impression-based and revenue-based line items to this insertion order. All budgets must be set on the line item object when using the **Flexible** budget type.

> [!WARNING]
> You cannot change the **Budget Type** once you save the insertion order.

### Billing periods

Billing periods allow you to allocate portions of your marketing budget to discrete periods of time. You can associate an external code with a billing period for reporting and invoicing.

You can also set billing periods (or flight dates) on augmented line items, or copy the periods you have set on the insertion order to augmented line items already associated with the insertion order. Any line item flight dates must occur within the dates of the parent insertion order's billing periods.

- **Dates**

     You may set both a start and an end date (**Set Dates**) or set a start date without an end date (**No Dates**). If you select **No End Date**, you can only create a single billing period on the insertion order, but you may still specify multiple flights with end dates on the line item. If you select **Set Dates**, you can create up to 52 billing periods.

- **Budgets**

    You may set a budget for each billing period (**Set Budgets**) or not specify a budget (**Unlimited Budget**). If you do not specify a budget at the insertion order level, you can still specify budgets on the line item.

> [!IMPORTANT]
>
> - You cannot set a start date in the past.
>   - Once you have saved an insertion order with **Set Dates** or **No End Date**, or **Set Budget** or **Unlimited Budget**, these settings cannot be changed.

### Pacing

Pacing determines how quickly budget is spent over the lifetime of the insertion order.

Options are:

- **Base daily allocation on average of remaining billing period budget** - Automatically divide your remaining budget evenly across the remaining days in the billing period. Use the slider to adjust the percentage of the daily average allocation as necessary. This option is only available if the insertion order has both a billing period end date and a budget.

- **Set pacing on the line item**

  > [!WARNING]
  > If you select this option, be sure to set your budget pacing on the line item or campaign level. Otherwise, severe overspend can occur.

- **Use Daily Budget** - Set a custom daily budget to define your own pacing.

  > [!IMPORTANT]
  > You can set budgets at the line item or campaign level, but your insertion order budget takes precedence. When your insertion order budget runs out, all objects under the insertion order will stop buying impressions, whether or not they have reached their own budget limits. For more details about budgeting and best practices, see [Budgeting and Pacing](budgeting-and-pacing.md).

## Political advertising

> [!NOTE]
> This section will only appear if you have already declared that this insertion order will conduct political advertising in its **Basic Setup** section.

### Political organization details

This section contains the details of the person or organization that is purchasing ads on Microsoft Advertising. For example, a candidate, an agency, or a political consultant.

The required fields must be filled out for any state or local political advertising that will or could serve in California, Illinois, Maryland, Nevada, New Jersey, New York, Virginia, or Washington, or for political advertising at the federal level that will or could serve in Washington State. If your political ad will not be served in any of those states, you may enter "N/A”. For more information on political advertising, see [Political Advertising](political-advertising.md).

We reserve the right to implement additional screening at any time.

| Field Name | Description |
|---|---|
| **Address** | Address of the person, group, organization, or business that is advertising. |
| **City** | City of the person, group, organization, or business that is advertising. |
| **Country** | Country of the person, group, organization, or business that is advertising. |
| **Independent Expenditure Committee** | Select this if any ads are being paid for by an independent expenditure committee: a political committee that makes only independent expenditures; that is, it spends money on political communications that expressly advocate the election or defeat of a clearly identified candidate and does not coordinate with a candidate, a candidate’s authorized committee, or an agent of the candidate. |
| **Organization Name** | Name of the person, group, organization, or business that is paying you to advertise on Microsoft Advertising. |
| **Payment Method** | How the political organization pays you. Options are: <br> - **Bank account (direct deposit)** <br> - **Check** <br> - **Credit or debit card** <br> - **Other** - If this is selected, you must specify details. |
| **Phone** | Phone number of the person, group, organization, or business that is advertising. |
| **State Registration Form** | New York and New Jersey require copies of state registration forms from independent expenditure committees making purchases. Creatives won't serve in those states until the form is uploaded. |
| **State, Province, or Region** | State, province, or region of the person, group, organization, or business that is advertising. |
| **Subject of the Ads** | The candidate or ballot initiative that is supported or opposed. |
| **Treasurer Name** | Treasurer for the committee purchasing the ads, or the person whose role mostly closely resembles a treasurer. |
| **U.S. FEC ID** | Optional. ID number assigned by the [U.S. Federal Election Committee](https://www.fec.gov/). |
| **ZIP or Postal Code** | ZIP or postal code of the person, group, organization, or business that is advertising. |

You must check **I certify that all information provided herein is accurate and up to date, and acknowledge and agree that Microsoft Advertising is relying on the accuracy of this information.** before you can save the insertion order.

## Related topics

- [View Insertion Order Details](view-insertion-order-details.md)
- [Create an Advertiser](create-an-advertiser.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Augmented Line Items (ALI)](augmented-line-items-ali.md)
- [Buy-Side Targeting](buy-side-targeting.md)
- [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md)
- [Political Advertising](political-advertising.md)
