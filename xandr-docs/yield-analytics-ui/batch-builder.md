---
title: Batch Builder
description: Leverage simultaneous multiple lookups for efficiency in handling large datasets or reusing lookup sets in scheduled or ad hoc tasks.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Batch builder

The **Batch Builder** allows you to collect multiple lookups that you can then run as a batch. This is particularly useful if you want to run a large number of lookups, or if you want to save and reuse a set of lookups either on a scheduled or ad hoc basis.

## Save a batch

- Open a batch that is already saved. Make any desired changes to it.
- When you are finished, select **Save**.
- Selecting this accesses the **Save Batch** screen. This screen has these fields:
  - Save as New (radio button)
  - Replace Existing (radio button)
  - Name (text box)
  - Category (pull-down menu)
  - Description (text box)
  - Permissions (table)

- After making selections, select **Save** to save this batch. Now when you select the **Open** button, you will see this batch.

## Open/send a batch

- Select **Open**. Your saved batches are displayed.
- Select **Send**. This accesses the **Send a Lookup Report** screen. This screen has these fields:
  - Recurrence (drop-down menu)
  - One-Time (radio button)
    - Immediately
    - Date
  - Send To (text box)
  - Message (text box)
  - Attachment (drop down menu)
- Make your selections to schedule and send your batch.

## Run a batch

- Selecting **Run** accesses the **Batch Queue**.
- It clears the batch off the **Batch Builder** screen. It now appears in superscript on the **Batch Queue** tab. (1 item)
- The batch runs in a queue in the background. You can continue to do other work.

> [!TIP]
> You can run up to 10,000 lookups (default). If you need the ability to run more, please contact your client services representative.

## Related topics

- [Availability Lookup](availability-lookup.md)
- [Availability Lookup - Quick Start Guide](availability-lookup-quick-start-guide.md)
- [Lookup Builder](lookup-builder.md)
- [Lookup Results](lookup-results.md)
- [Batch Queue](batch-queue.md)
