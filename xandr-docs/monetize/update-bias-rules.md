---
title: Update Bias Rules
description: This page provides an overview to update Bias Rules. Learn how to view, create, duplicate and delete bias rule details from the Bias Rule Manager screen.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Update bias rules

> [!NOTE]
> This feature is not available by default. If you are interested in gaining access or discussing potential use cases that may apply to your business, reach out to your Microsoft Advertising representative.

The **Bias Rule Manager** screen lists all bias rules for the publisher, allows you to view and edit rule details, and offers bulk editing options.

## Getting to the bias Rule Manager Screen

To reach this screen, select **Publishers** \> **Bias Rules** from the navigation menu, and then select a publisher when you are prompted.

## Viewing bias rule details

To view details about a bias rule, select the rule by clicking anywhere in the row except the checkbox. The **Bias Settings** section then shows you the following:

- **Bias Direction**: The type of bias applied to a buyer or buyer group; positive (bid preference), negative (bid deterrent), or neutral (no bias applied).
- **Applied To**: The number of buyers or buyer groups that the bias direction has been applied to.

The **Rule Details** section then shows you the following:

- **Name**: The name that you provided for the rule.
- **ID**: The rule's ID.
- **Priority**: The rule's priority. Rules are checked against the impression in priority order.

For conditional bias rules, the **Rule Details** section will also display the following (not shown in screen shot):

- **Audience Targeting**: An overview of the rule's audience targeting settings.
- **Supply Targeting**: An overview of the rule's supply targeting settings.

## Filtering by Name/ID

You can find all bias rules whose names or IDs include a specific string of characters or numbers. Click **Filter** and then enter the characters in the **Name/ID** field.

## Creating bias rules

> [!TIP]
> For step-by-step instructions on creating a bias rule, see [Create a Bias Rule](create-a-bias-rule.md).

## Editing bias rule settings

To edit a rule's bias settings, select the rule's row and then click the **Edit** button in the **Buyers** or **Buyer Groups** table.

To edit a rule's details or targeting settings, select the rule's row and then click the **Full edit** button in the **Rule Details** section.

> [!TIP]
> For step-by-step instructions on editing bias rules, see [Create a Bias Rule](create-a-bias-rule.md).

## Duplicating bias rules

You can duplicate one or more bias rules directly from the **Bias Rule Manager** screen. Check the checkbox for each rule that you want to duplicate and click **More Actions** \> **Duplicate**.

## Deleting bias rules

You can delete bias rules directly from the **Bias Rule Manager** screen. Check the checkbox for each rule that you want to delete and click **More Actions** \> **Delete**.

A confirmation dialog lists the rule(s) to be deleted. Click **Confirm** to complete the action.

> [!WARNING]
> Be careful when deleting bias rules. As soon as a rule is deleted it **immediately** stops applying to transactions; this may have significant revenue repercussions.

## Related topics

- [Create a Bias Rule](create-a-bias-rule.md)
- [Understanding Yield Management](understanding-yield-management.md)
- [Working with Yield Management](working-with-yield-management.md)
- [Create a Floor Rule](create-a-floor-rule.md)
- [Update Floor Rules](update-floor-rules.md)