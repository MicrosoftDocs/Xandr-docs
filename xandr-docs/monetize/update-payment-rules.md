---
title: Update Payment Rules
description: This page provides an overview to update Payment Rules. Learn to view, filter, create, edit, delete and duplicate conditional payment rules in this page.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Update payment rules

The **Payment Rules** screen shows you the existing payment rules that have been established for a publisher. These are created primarily to allow publishers to have separate and distinct payment conditions with members. You can create payment rules, edit existing payment rules, and view details about them.

## Getting to the payment rules screen

To reach this screen, select **Publishers** \> **Payment Rules** in the menu bar.

## Viewing payment rules information

The information on the **Payment Rules** screen show the dollars that have been earned by different categories (publisher, network, etc.):

- **ID**: The unique identification number of the payment rule.
- **Rule**: The name of the payment rule.
- **Type**: The type of payment rule. This can be **Base** or **Conditional**.
- **Priority**: The order in which rules are considered when determining which payment rule to apply. Priorities can be from **1** to **10**, with **1** being the lowest priority and **10** being the highest priority.
- **Revenue (USD)**: Indicates the total dollars earned through this payment rule.
- **Publisher Revenue (USD)**: Indicates the total dollars earned by the publisher through this payment rule.
- **Network RPM (USD)**: Indicates the dollars earned per 1,000 impressions by the network through this payment rule.
- **Publisher RPM (USD)**: Indicates the dollars earned per 1,000 impressions by the publisher through this payment rule.

Additionally, you can change the time frame of the information with the date dropdown.

You can select one of the following time frames:

- **Today**
- **Yesterday**
- **Last 7 Days**
- **Lifetime**

## Filtering payment rules

You can apply filters to limit the number of payment rules visible on this screen. To do so, select the **Filter** button. The **Name/ID** field appears. Enter the name
or unique identification number of the rule(s) you wish to see and select **Apply Filter**. The list will show only those rules that match the filter criteria.

## Creating new base and conditional payment rules

You can create new base and conditional rules on this page. Click the **Create New** option to expose the dropdown list, and choose **Base** or **Conditional**. For the detailed steps required to create a payment rule, see [Create Payment Rules](create-payment-rules.md).

## Editing a conditional payment rule

To make changes to a conditional payment rule, select the line of the payment rule you wish to edit (this is different than checking the checkbox). The **Payment Rules Details** section appears at the bottom of the screen. To change any settings for that publisher, select the **Full Edit** button.

For details on the specific settings, see [Create Payment Rules](create-payment-rules.md).

## Deleting conditional payment rules

To delete one or more payment rules, check the checkbox of each payment rule you want to delete. Once at least one payment rule has been checked, theoptions in the **More Actions** dropdown become active. Select the **Delete** option. A confirmation dialog appears.

> [!IMPORTANT]
> You cannot delete Base payment rules.

Once you confirm the deletion, the selected payment rules are removed from the list.

## Duplicating conditional payment rules

To copy one or more payment rules, check the checkbox of each payment rule you want to duplicate. Once at least one payment rule has been checked, the options in the **More Actions** dropdown become active. Select the **Duplicate** option. A confirmation dialog appears.

> [!IMPORTANT]
> You cannot duplicate Base payment rules.

Once you confirm the duplication, the rule or rules that you duplicated appear in the list preceeded by the word **Copy**. If desired, you can edit this field to change the name (using up to 100 characters).

## Related topics

- [Working with Payment Rules](working-with-payment-rules.md)
- [Create Payment Rules](create-payment-rules.md)
- [Base and Conditional Rules](base-and-conditional-rules.md)
