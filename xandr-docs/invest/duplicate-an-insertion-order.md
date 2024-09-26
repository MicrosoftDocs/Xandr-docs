---
title: Duplicate an Insertion Order
description: In this article, follow our step-by-step instructions to duplicate an insertion order with all of its child line items and splits in Microsoft Invest.
ms.date: 10/28/2023
---

# Duplicate an insertion order

Insertion Order (IO) Duplication is a feature in Microsoft Invest that allows traders to duplicate an insertion order with all of its child line items and splits. This saves time and reduces manual effort when a similar set up is used repeatedly. It is unnecessary to re-enter all the targeting settings.

This is what you can accomplish with IO Duplication:

- Duplication of a **single** insertion order with up to 100 line items. Each line item can have up to 100 splits. If a duplication job is submitted and any line items have more than 100 splits, the job as a whole will succeed, but the offending line item(s) will fail. The user will receive explicit notification of which lines succeeded and which failed, and the reason for failure.
- You can choose which augmented line item(s) from the insertion order to duplicate (default to all or first 100).
- You can rename the duplicated insertion order.

> [!NOTE]
>
>- IO Duplication only works for one insertion order at a time. If you submit a duplication, you must wait for it to finish to do another duplication.
>- All dates and budget numbers will be cleared out from the new insertion order and child line items. They must be recreated. Everything that is not related to the date or a budget will be duplicated.

## Prerequisites/considerations

There are certain considerations you should keep in mind before duplicating an insertion order:

- You will need to set new billing periods for the insertion order.
- All line items will inherit the new billing periods as flights.
- If a trader needs line item flights to differ from insertion order billing periods, they will need to update the flights **after** duplication.
- Insertion order budgets can be set during duplication.
- Line item budgets will be set to 0 and must be updated after duplication. This can be done via bulk upload, bulk edit, or individual line item edits. You will not be able to make any other edits to these line items until their budgets are updated.

## Insertion order duplication procedure

1. Log in to Microsoft Invest.
1. Access the **Insertion Orders** screen.
1. Select an insertion order from the IO list.
1. Select **Duplicate** in the horizontal bar above the IO list.
1. Enter the new insertion order name.
1. The **Budget Type** is inherited from the parent insertion order. No action is necessary.
1. Enter however many **Billing Periods** are needed for the insertion order, and the associated fields:
    - **Set Dates**: Select this to specify a billing period **Start Date** and **End Date**.
    - **No End Date**: Select this to remove the **End Date** field and all additional billing periods.
    - **Start Date**: Select this to enter the new **Start Date** for the new billing period.
    - **End Date**: Select this to enter the new **End Date** for the new billing period. The **Set Dates** field must be selected for this field to be visible.
    - **Set Budgets**: Select this to specify a **Total Lifetime Budget**.
    - **Unlimited Budget**: Select this to remove the budget fields from all billing periods. **Total Lifetime Budget** will be: Unlimited.
    - **+ Add Another Billing Period**: Select this to add additional billing periods.

1. You have the option to **Duplicate Line Items**. If you choose to exercise this option, the following fields/buttons must be selected:
    - **Associated line items will be duplicated**: If this toggle is on, line items associated with this insertion order will be visible. If this toggle is **off**, all settings underneath this field will not be visible.
    - All line items will inherit the billing periods of the insertion order as flights. These flights can be edited later.
    - Duplicated line items will have **_Copy** appended to their names. You can edit the names later.

      > [!NOTE]
      > All line items are selected by default. If the IO has more than 100 line items, the first 100 are selected, and you may change the selection. If you need to duplicate more than 100 line items, you may bulk upload the rest or contact your Microsoft Advertising Account Manager for help.

1. Once the above information is entered, select **Duplicate** to duplicate the insertion order with the selected criteria. You can select **Cancel** to cancel the insertion order duplication process if required.
1. Once you select **Duplicate**, there is an **Import Processing** option located on the upper right-hand corner of your screen.
1. By selecting this option, you can see the process happening. A **Last Import** window will be visible. It shows the **Date** and **Status** of the current duplication. The **Status** shows the number of objects that are complete, and any errors that occurred during processing.
1. Select **View Results** to access the **Bulk Processor Tool Results**. This shows what was successfully processed, and what was not, by line item.
1. Select **OK** to automatically download a text file entitled **Bulk_Uploader Results (XX).txt**. This file provides details on specific errors that may have occurred for each line item and split.
