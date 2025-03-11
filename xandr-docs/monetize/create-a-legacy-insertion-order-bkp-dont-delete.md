---
title: Create a Legacy Insertion Order
description: In this article, find information on how to create and set up a legacy insertion order.
ms.date: 10/28/2023
---

# Create a legacy insertion order

> [!IMPORTANT]
> Legacy insertion orders are required for [Guaranteed Delivery Line Items](create-a-guaranteed-delivery-line-item.md). For all other line items, we recommend the use of the [Insertion Orders](create-an-insertion-order.md).

Insertion orders allow you to easily manage collections of line items that may share a common budget, time span, and business terms. Insertion orders are a standard part of the [Object Hierarchy](object-hierarchy.md). An insertion order can contain one line item or many line items. The instructions in this topic apply to a now-deprecated type of insertion order. The legacy insertion order:

- Is not compatible with augmented line items (ALIs).
- Uses flight dates, not billing periods.

If you currently use legacy insertion orders, you should consider making the transition to standard (formerly seamless) insertion orders and augmented line items soon.

> [!IMPORTANT]
> You can only create insertion orders under advertisers for which insertion orders are enabled. See [Create an Advertiser](create-an-advertiser.md) for more details.

## Select the advertiser

On the **Advertisers** screen (**Advertisers** > **All Advertisers**), click the name of the advertiser under which you want to create an insertion order.

## Create a new insertion order

On the **Advertiser Details** screen of the advertiser under which you want to create an insertion, click **Create New** > **Insertion Order**.

The **Create New Insertion Order** screen is then displayed. Define all relevant details for your insertion order.

> [!TIP]
> You can expand or collapse each section as needed. To expand or collapse all sections at once, click the **Expand All** or **Collapse All** link in the upper right.

## Enter basic details and flight dates

In the **Basic Setup** section, enter the basic details and flight dates for the insertion order.

- **Name** - Enter the name for the insertion order. You will later be able to search for and report on the insertion order using this name.
- **External Code** - If you want to report on the insertion order using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code here. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). No two objects at the same level (e.g., line items or campaigns) can use the same code per advertiser. For example, two line items cannot both use code "XYZ", but a single line item and its child campaign can.
- **Billing Code** - Enter any internal billing code you want to associate with this insertion order. If you receive an invoice per insertion order, the code you enter here will appear on that invoice. For details on invoices, see [Understanding Your Invoice](understanding-your-invoice.md).
- **State** - Set the state of the insertion order. If "**Active**", child line items and campaigns will be eligible to serve. However, it is best practice to set the state to "**Inactive**" until everything related to the buy has been set up and verified. This will avoid spending before you are ready.
- **Currency** - The currency is inherited from the advertiser, but you can set a different currency for the insertion order, if necessary. Note that you cannot change the currency after saving the insertion order.
  
  > [!NOTE]
  > As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience. Read [Currency Support](currency-support.md) for more details.

- **Viewability Standard** - The criteria by which an impression is measured as viewable. Please see [Introduction to Viewability](introduction-to-viewability.md) for more information.
- **Flight Dates** - Enter or select the start and end dates and times for the insertion order. By default, the start date is today, the start time is now, and the insertion order is set to run indefinitely (no end date/time). To set a specific end date and time, deselect **Run indefinitely**. Note that the time format (12-hour or 24-hour) and time zone are inherited from the advertiser.
  
  > [!IMPORTANT]
  > You can set flight dates for each line item and campaign under the insertion order as well, but your insertion order flight dates take precedence. When you reach the insertion order end date, all line items and campaigns under the insertion order will stop buying impressions, whether or not they have reached their own end dates.

## Set the insertion order budget

By default, your insertion order **Budget** is "**Unlimited**". If you prefer, you can define exactly how much the advertiser has allocated for you to spend over the lifetime of the insertion order and/or on any single day. The budget can be in **impressions** or in **revenue** (money).

- **Lifetime** - This is the budget that the advertiser has allocated for you to spend over the entire lifetime of the insertion order.

    There are two options:
  - **Custom** - Select this option to enter a specific amount of impressions or money.
  - **Unlimited** - Select this option to leave your lifetime budget undefined.
- **Daily** - This is the budget that the advertiser has allocated for you to spend on any single day.

    There are three options:
  - **Custom** - Select this option to enter a specific amount of impressions or money.
  - **Pace Lifetime Budget** - Select this option to spread your lifetime budget evenly across your flight dates. As each day passes, the system spreads the remaining impression or revenue budget across the remaining days of the flight.

    The system is not able to pace its spending if it does not have a budget amount, and the system must know the number of days in the insertion order in order to apply the remaining budget amount equally for the remainder of the flight. Therefore, this option requires that you enter a custom lifetime budget and select an end date. For more details, examples, and best practices, see [Lifetime Pacing](lifetime-pacing.md).

  - **Unlimited** - Select this option to leave your daily budget undefined.

> [!IMPORTANT]
> You can set budgets at the line item, campaign, and creative levels as well, but your insertion order budget takes precedence. When your insertion order budget runs out, all line items and campaigns under the insertion order will stop buying impressions, whether or not they have reached their own budgets. For more details about budgeting and best practices, see [Budgeting and Pacing](budgeting-and-pacing.md).

## Enter political advertising information

If necessary, fill out the information required for political advertising.

> [!NOTE]
> This section will only appear if you have already declared that this advertiser conducts political advertising on the [Create an Advertiser](create-an-advertiser.md).

These settings must be filled out if you are using this insertion order for advertising related to an election, ballot initiative, or political candidate in the United States.

### Your details

This section contains the details of the person or organization that is purchasing ads on Microsoft Advertising. The "Buyer Name" will be automatically filled in with the name of the Microsoft Advertising client. You should enter the contact details for the person or team who can best answer any  questions about political advertising on this insertion order.

### Political organization details

This section contains the details of the person, group, organization, or business that is advertising. For example, a candidate, an agency, or a political consultant.

- **U.S. FEC ID**  

    ID number assigned by the U.S. Federal Election Committee.

- **Organization Name**

    Name of the person, group, organization, or business that is paying you to advertise on Microsoft Advertising.

    You can search for a political organization's name by typing in the Organization Name field and selecting the appropriate match. This will automatically fill in the contact details for the organization.

    If the relevant organization is not listed, click **+Add a political organization** to turn the search into a text field, and enter the organization's details.

- **Address**  

    Address of the person, group, organization, or business that is advertising.

- **City**  

    City of the person, group, organization, or business that is advertising.

- **State, Province, or Region**

    State, province, or region of the person, group, organization, or business that is advertising.

- **ZIP or Postal Code**

    ZIP or postal code of the person, group, organization, or business that is advertising.

- **Country**

    Country of the person, group, organization, or business that is advertising.

- **Phone**  

    Phone number of the person, group, organization, or business that is advertising.

- **Independent Expenditure Committee**

    Select this if any ads are being paid for by an independent expenditure committee: a political committee that makes only independent expenditures; that is, it spends money on political communications that expressly advocate the election or defeat of a clearly identified candidate and does not coordinate with a candidate, a candidate’s authorized committee, or an agent of the candidate.

- **Treasurer Name**

    Treasurer for the committee purchasing the ads.

- **Subject of the Ads**

    The candidate or ballot initiative that is supported or opposed.

- **Payment Method**

    How the political organization pays you. Options are:

  - **Bank account (direct deposit)**
  - **Check**
  - **Credit or debit card**
  - **Other** - If this is selected, you must specify details.

- **State Registration Form**

    New York State and New Jersey require copies of state registration forms from independent expenditure committees making purchases. Creatives won’t serve in New York State or New Jersey until the form is uploaded.

- **Acknowledgement**

    You must check **I certify that all information provided herein is accurate and up to date, and acknowledge and agree that is relying on the accuracy of this information.** before you can save the insertion order.

## Enter reporting labels (optional)

In the **Reporting Labels** section, you can associate a **Trafficker**, **Sales Rep**, and/or **Insertion Order Type** to the insertion order. This enables you to report on performance by these labels in [Network Reporting](network-reporting.md).

For example, you might associate a Trafficker with each insertion order and then run a report grouped by Trafficker to find out which ones are responsible for which insertion orders or compare insertion order performance across traffickers. For more details, see [Reporting Labels](reporting-labels.md).

## Add commissions (optional)

If you need to attribute revenue to third parties, you can add fees in the **Commissions** section. Commissions are deducted from the booked revenue (the amount the advertiser pays you) of each line item under the insertion order, and can be defined either as a percentage of booked revenue or a flat CPM.

To add a new commission:

1. Click the **Add Fee** button to display the additional fields.
1. In the **Broker** field, select the relevant broker or create a new broker.
1. In the **Description** field, enter details about the commission.
1. Select the **Fee Type** (**CPM** or **Revenue Share**) and enter the relevant **Fee Value** (dollar amount for **CPM**, percentage for **Revenue Share**).
1. Click **Add**.

> [!NOTE]
>
> - Commissions at the line item level override commissions at the insertion order level.
> - Per broker, you can add no more than one CPM commission and one Revenue Share commission.
> - The commissions here apply to all line items under the insertion order. If you prefer, you can add commissions to specific line items instead. See [Create a Standard Line Item](create-a-standard-line-item.md) for more details.
> - The decimal position support for the broker fees is for 1 place after the decimal. For example, if you set 16.67% as a broker fee in the **Commissions** section, after saving, the value would round off to 16.7%. However, there is no restriction on number of places after the decimal if the [Insertion Order service API](../digital-platform-api/insertion-order-service.md) is used to create the broker fee.

## Associate line items (optional)

In the **Associated Line Items** section, you can associate existing line items to the insertion order. Note that you can do this when creating or editing a line item as well.

> [!IMPORTANT]
> When you associate a line item to an insertion order, any budget or impressions that occurred under the line item before it was associated to the insertion order do not count towards the lifetime budget of the insertion order. For example, if you have Line Item XYZ that spent $100,000 of budget before you associate it to Insertion Order ABC with a lifetime budget of $250,000, the insertion order will not stop serving until the line item reaches $350,000 ($100,000 before being associated to the insertion order, and $250,000 after).

To associate existing line items:

1. Click the **Edit** button.
1. Check the line items that you want to associate to the insertion order.
1. Click **Add**.

## Enter comments (optional)

In the **Comments** section, enter any comments that you would like to record with the insertion order. Comments are for your reference only and will not affect delivery.

## Save the insertion order

To finish adding the insertion order, click the **Save** button. You're then taken to the [View Insertion Order Details](view-insertion-order-details.md) screen.

You can also click the arrow next to the **Save** button and choose to **Save and Create Line Item**. Clicking this option will take you to the **Create New Line Item** page, with the newly-created insertion order already selected.

## Related topics

- [Working with Insertion Orders](working-with-insertion-orders.md)
- [Explore Insertion Orders](explore-insertion-orders.md)
- [Create an Advertiser](create-an-advertiser.md)
- [Create a Standard Line Item](create-a-standard-line-item.md)
- [Political Advertising](political-advertising.md)
