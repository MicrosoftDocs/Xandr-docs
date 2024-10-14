---
title: Batch Queue
description: Monitor and manage daily batches using Batch Queue tab, including instructions for retrieving or canceling.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Batch queue

Selecting the **Batch Queue** tab accesses any batches that are running or have completed during the current day.

## Retrieve a batch

- Selecting **Run** on the **Batch Builder** screen moves that batch to the Batch Queue.
- There are the following columns displayed: Name, Created By, Progress.
- The **Name** column indicates the number of lookups in the batch, to the right of the batch name.
- Progress is a percentage bar. Hover over the Progress result for additional batch run information. (Example: XX out of XX lookups completed).
- Select the **sprocket** icon to the left of the batch to access these options:
  - Edit in Batch Builder - This will open the batch lookups in the Batch Builder screen so you can make changes and rerun the batch.
  - Export to Excel
  - Export to CSV
  - Custom Export
- If you just want to view the results that were run against these lookups, select the batch Name result itself, (it is hyperlinked). This accesses the Lookup Results page, where you can see availability and capacity data.
- If the batch was configured to be emailed either on a scheduled or ad hoc basis, an envelope icon within the **Progress** field will indicate the batch was sent successfully.

## Cancel a batch

Batches that are not yet complete may be canceled. If you have the proper permission you may use the **Cancel All** button on the top right-hand side of the screen to cancel all incomplete batches at once. Alternatively, you can cancel an individual batch by rolling over the sprocket icon and selecting **Cancel**, if you have the permission to do so for the given batch.

> [!TIP]
>
> - Any batches created that day stay within the batch queue table for the day.
> - The Batch Queue is viewable to everybody. If you have proper permissions, you will be able to view all the batches that are being run by all users.

## Related topic

[Availability Lookup](availability-lookup.md)
