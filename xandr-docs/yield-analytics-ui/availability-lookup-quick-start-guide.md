---
title: Availability Lookup - Quick Start Guide
description: Optimize with tab-based access in Availability Lookup. Streamline actions in Lookup Builder, Results, Batch Builder, and Queue management.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Availability lookup - Quick start guide

The **Availability Lookup** screen appears in the **Availability** drop-down.

## Basic concepts

There are four tabs within the page which offer the following features:

- [Lookup Builder](lookup-builder.md): Easily create your lookups, no matter if they are simple or very complex.
- [Lookup Results](lookup-results.md): View availability and contention results, change configurations and re-run lookups, and more.
- [Batch Builder](batch-builder.md): Save, schedule, and execute batch lookups.
- [Batch Queue](batch-queue.md): Monitor batch progress and access results for completed batches.

Configuration and Advanced Filters: Select your date range and optionally, how you want dates to be grouped. Use **Advanced Filters** to apply additional constraints, such as a frequency cap.

## Button functionality (lookup builder tab)

- **Open**: This allows you save a frequently used template and share it with other users within your instance. When you select **Open**, a dialogue box is accessed with all of the saved templates.
- **Save**: When you select the **Save** button, you begin the process of saving a lookup template. A dialogue box is accessed that allows you to manage how the template should be saved, and who should have access to it.
- **Views**: The user is able to choose if they would prefer to perform their lookup by building the lookup from an Attribute and Product View (default), or apply a Product Group View, which would enable you to select a Product Group that you would like to filter off of.
- **Vary By**: Allows you to vary your lookup based on additional attributes and values that are selected. This creates one lookup for each different combination of vary by items that are selected.
- **Undo**:  If you make a change, delete or clear all from the lookup, then you can select **Undo** and the previous unaltered lookup will be reinstated.
- **Clear All**:  This button allows you to clear out the entire lookup and start over.

## Build a lookup

There are two ways to define the attribute and attribute value you want to include in the lookup.

- Select the **Select Attribute** hyperlink.
- A screen is accessed which allows you select the attribute and the appropriate attribute value.
- Select the attribute.
- Select the attribute value, as well as the ability to indicate if you would like to include or **exclude** the value within the lookup.

The second way is to type the attribute you are looking for directly in the builder.

- The available list that matches the text will populate, and you can select.
- Follow the same steps to define the attribute value. The available value list that matches the text will populate and you can select. You can add as many attribute values as needed.

After you have selected your attribute and attribute values, there is an option to either and or **or** additional attribute/attribute values to your lookup.

- In order to and an additional attribute value, select on the **Add Attribute** hyperlink.
- In order to or an additional attribute value, select on the Create a **New Segment** hyperlink.
- Within the lookup builder screen you can see where attribute values are grouped by and or **or**.
- While building your lookup, icons on the right allow you to quickly remove all values for a given attribute, or remove the attribute altogether. If you build a targeting segment consisting of multiple attributes and'ed together, an icon in the upper right corner of the segment allows you to easily duplicate the entire segment, creating a new or'ed segment that you can modify as needed.

There is also a feature that allows you to build a target expression instead of using the builder. Select the icon to the right of the Attribute and Product View verbiage. The target editor screen will appear once you select the button above.

When your lookup is defined, select the **Run** button on the bottom right corner of the screen.  When the lookup is running, there will be a blue notification at the top of the screen to confirm the lookup is running.

## Use the lookup results tab

Each lookup in this tab has a gear icon that presents several actions that can be taken for a given lookup:

- Create Product: Create a new product for the lookup's targeting. This option is only displayed if the lookup doesn't correspond to a pre-existing product. Products created in this manner will become temporary analysis products that will automatically deactivate after fourteen days. To avoid deactivation, you will need to go to **Products \> Find Products**. Locate the product and edit it, setting the Product Type to Reporting.
- Edit Lookup:  Modify the lookup in the Lookup Builder tab.
- Run Lookup: Re-run the lookup, typically after you've changed the lookup configuration or advanced options on the left.
- View Contention: Open a quick view into the demand that will be competing on the inventory utilized within the lookup.
- Remove Lookup: Remove the lookup from the list of results.

## Use batches

When a lookup is created in the Lookup Builder tab, there is an option to Add to Batch. Selecting this option moves the lookup to the **Batch Builder** tab. Within Batch Builder you can run many lookups together as a group. You can also save batches for reuse, and schedule saved batches for automatic email delivery. Once you've run a batch, you can monitor progress and access the batch results from the **Batch Queue** tab.

## Related topics

- [Availability Lookup](availability-lookup.md)
- [Lookup Builder](lookup-builder.md)
- [Lookup Results](lookup-results.md)
- [Batch Builder](batch-builder.md)
- [Batch Queue](batch-queue.md)
