---
title: Microsoft Monetize - Viewing Your Object Limits
description: Explore efficient line item, creative management with Object Limits Report. Monitor platform usage, ensure compliance, reduce characters.
ms.date: 10/28/2023
---

# Microsoft Monetize - Viewing your object limits

Microsoft Advertising limits the number of object (line items, creatives, etc.) that you can have on the platform. The Object Limits Report allows you to view these limits and proactively monitor your current usage.

Both active and inactive objects are counted against the object limit. For creatives, only non-expired objects are counted against the limit. A creative expires when it has neither served nor been modified in 45 days.

> [!IMPORTANT]
> **Automatic archiving of objects:** Objects that have not served or been edited in more than 180 days and that are not scheduled to serve in the future are automatically archived. If an object is in the "archived" state, it cannot spend or be edited. However, it can still be copied, deleted or used in reports (or exported for use in an external reporting tool). In addition, once an object is archived, any child objects it may own (e.g., Insertion Order \> Line Item) will also be archived and no additional child objects can be created beneath the archived parent object. For details, see [Automatic Archiving of Buy-Side Objects](automatic-archiving-of-buy-side-objects.md).

## Getting to the object limits report

Your object limits report is available under your Network Settings.

## Object limits report

The **Object Limits Report** section lists the types of objects that are limited and provides the following data
for each:

- **Usage/Used** - The current number of active and inactive objects.  For creatives, this does not include expired objects.
- **Limit/Available** - The maximum number of objects that you are allowed.
- **% Limit** -The percent of your limit that you have reached. For creatives, this does not include expired objects.
- **% Active** - Out of the total number of objects in use, the percent that are active.
- **% Served or Modified in the Last 90 Days** - The percent of objects that have had impressions, or have been modified, in the last 90 days. For creatives, since expired creatives are not counted, this will always be 100%. If the percentage is low, the client has many objects that are candidates for deletion.

> [!TIP]
> Line items that have not served or been modified in the last 90 days are good candidates for deletion. For information about finding and deleting line items, see [Update Line Items](update-line-items.md).
>
> Contact your Microsoft Advertising representative if you need assistance in cleaning out old objects or to request that your object limit be increased.

## FAQ's

### How will I know that I am approaching my limit for an object?

We send you an email notification when you reach 85%, 95%, and 100% of your limit for an object. You can change the email addresses that receive notifications via your Network Settings.

### What if I reach my limit for an object?

When you approach or reach your limit for any object other than creatives, you should delete any inactive, unused, or unnecessary instances. These deleted objects will continue to appear in reporting but cannot be undeleted.

When you approach or reach your limit for creatives, you should remove non-expired creatives. Non-expired creatives have the `is_expired` field set to `false`. Note that removing expired creatives will not impact your creative count.

### What if I am already over my limit?

If you need to create additional objects but have already met or exceeded your limit as listed above, please delete unused objects.

### Can my limit be raised?

In exceptional cases, a limit may be temporarily lifted by a small amount at the discretion of our engineering team. Please contact your Microsoft Advertising representative to discuss this option.
