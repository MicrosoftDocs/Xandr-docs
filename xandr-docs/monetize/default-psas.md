---
title: Default PSAs
description: Learn how Microsoft Advertising serves Default public service announcement creatives (PSAs or PSA creatives) to prevent serving blanks. Also, this page covers some example PSAs. 
ms.date: 10/28/2023
---


# Default PSAs

Default public service announcement creatives (PSAs or PSA creatives) are actual PSAs that Microsoft Advertising serves in order to prevent serving blanks under certain circumstances.

> [!TIP]
> To prevent a PSA from serving, it is best practice to set up a default creative or House Line Item for each placement. For more information, see [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md) or [House Line Item](ad-campaign-house-line-items.md).

> [!NOTE]
> **About Flagged Impressions**
>
> In the past, filtered impressions on inventory flagged as violating platform standards would serve blanks. Now, these impressions follow seller preferences for impressions with no demand. As with all impressions that follow this workflow, sellers will be charged the applicable fee.
>
> Default PSAs are ads intended for general audiences that Microsoft Advertising serves for various causes and nonprofit organizations at no cost in order to prevent serving a blank when there is no other creative to serve.

## Example PSAs

Below are a few examples of default PSAs served for managed inventory.

:::image type="content" source="media/default-psas.png" alt-text="Screenshot of Default PSAs.":::

A PSA creative provided by Microsoft Advertising will be served for your managed inventory in the following circumstances:

- The impression is not purchased through a line item

- No bid meets your reserve price

- No default creative is available

  We have PSAs for all standard placement sizes. If the placement tag is an unusual size for which we don't have a PSA, a blank will be served.

## Report on PSAs

In network reporting, PSAs will show up as a buyer in a report grouped by buyer. The buyer member associated with Microsoft Advertising default PSAs is ID 229, Public Service Announcements, but the report will show a row for Buyer: PSA, and will not include Buyer 229.

## Avoid showing PSAs

To avoid showing PSAs, you can do the following:

- Make sure that your inventory is being targeted successfully by one or more line items. You may wish to review frequency caps, budget, and category/placement group/placement targeting to make sure they are not limiting the purchase of your direct inventory.
- [Add a default creative to the placement](assign-a-default-creative-to-a-placement.md). This will serve in case the impression is not purchased.

## Related topics

- [Working with Placements](working-with-placements.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)