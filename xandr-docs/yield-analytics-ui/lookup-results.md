---
title: Lookup Results
description: In this article, explore a detailed understanding of how to interpret lookup results.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Lookup results

Selecting the **Lookup Results** tab accesses the **Lookup Results** screen.

## Column descriptions

- There are five columns on the main screen: Name, Availability, Capacity, Range, and Target Expression.
- The Name is either hyperlinked or not hyperlinked. If the name is hyperlinked, that means it is an existing product in the system. Selecting the hyperlink will access the Product metadata screen. This displays information about that product.
- If it is is not hyperlinked, it is not a current product in our system. It is called a dynamic lookup. The system assembles attributes and determines availability accordingly.
- The **Availability** column displays how much you have available to sell.
- The **Capacity** column displays the total capacity.
- The **Range** column displays what date range you are running this against.
- The **Target Expression** column displays the target expression. In some instances, the target expression is hyperlinked. Target Expressions are often very lengthy, and could be hundreds of lines long. Selecting this allows you to view the target expression on a user-friendly screen. The target expression is not editable from this screen.
- You can filter results in any column further by selecting the down-arrow icon next to the column name.

## Change advanced filters/date range

If **Advanced Filters** were assigned, they would also be columns. They are Priority, Frequency Cap, Viewable, Competitive Separation, and Roadblock.

In the **Lookup Results** screen, you can change any configuration or filter on the left and then re-run any lookup against the new configuration by selecting the sprocket icon and selecting **Run Lookup**. The original version of the lookup will be retained, allowing you to compare lookups with the same targeting but different configurations side by side.

## Button functionality

### Sprocket icon

Selecting the sprocket icon to the left of the **Name** column gives you the following options: Create Product, Edit Lookup, Run Lookup, View Contention, and Remove Lookup.

- If the product is already a product in the system, the Create Product option will not be displayed.
- If it is a dynamic lookup, it allows you to create a product within the system. select **Create Product**.
  
    The following message is displayed on the top of the screen: Product created with Yield ID XXXXXX. The newly-created product name is now a hyperlink. Selecting this link accesses a product metadata screen, which displays information about the product. Products created in this manner will become temporary analysis products that will automatically deactivate after fourteen days. To avoid deactivation, you will need to go to **Products \> Find Products**, locate the product and edit it, setting the Product Type to Reporting.
- Selecting **Edit Lookup** accesses the **Lookup Builder** screen, and allows you to edit and run the lookup again.
- Selecting **Run Lookup** will re-run the lookup.
- Selecting **View Contention** will open a quick view into the demand that will be competing on the inventory utilized within the lookup.
- Selecting **Remove Lookup** removes the lookup from the list of reported lookups.

### Export drop-down menu

There are three export options:

- XLSX - Excel
- CSV - Comma-separated values
- Custom XLSX - This accesses a sub-screen that gives you additional options:
  - Attribute-Value Breakdown - This will break out the attributes by column, as opposed to putting them all in the same column.
  - Show Start and End dates as separate columns.

**Clear All** - This clears the data in the **Lookup Results** screen.

**Add to Batch** - This is used when you are building numerous target expressions that are grouped together. It allows you to run them, and continue to work on other tasks. It runs in a different thread in the background. It will add these lookups to the **Batch Builder** screen.

## Related topics

- [Availability Lookup](availability-lookup.md)
- [Availability Lookup - Quick Start Guide](availability-lookup-quick-start-guide.md)
- [Lookup Builder](lookup-builder.md)
- [Batch Builder](batch-builder.md)
- [Batch Queue](batch-queue.md)
