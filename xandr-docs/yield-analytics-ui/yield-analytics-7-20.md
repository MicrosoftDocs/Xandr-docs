---
title: Yield Analytics 7.20
description: In this page, learn how to build and use the new advanced filter in the Availability screen called Roadblock.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Yield Analytics 7.20

## Feature enhancements

### Roadblock look ups

We have created a new advanced filter on the left hand column of the Availability screen called Roadblock.

:::image type="content" source="media/i.png" alt-text="Screenshot of Roadblock filter in Availablity screen.":::

The options within the roadblock are:

- All
- As Many
- One or More
- Only One

Some ad servers have multiple options, while others have a more restrictive set of options.

> [!TIP]
> For OAS (Open AdStream), you would use the All option to facilitate Strict Companions.
>
> Select the product that you want to use to build your Roadblock. Then select the Advance link on the bottom-right of the screen in the top model. After the options expand, select the Create Product Variants option.

:::image type="content" source="media/j.png" alt-text="Screenshot to select the product to build your Roadblock.":::

- Once you have accessed the Vary this attribute: functionality under the main Product must match all of these criteria: box, then you must select either size or **position** in order to build the additional variables necessary for the Roadblock.

:::image type="content" source="media/k.png" alt-text="Screenshot of Vary this attribute functionality under the main Product must match all of these criteria box.":::

- Select **Check Availability**.
- The results will become available in the **Availability Report** section of the User Interface.

:::image type="content" source="media/l.png" alt-text="Screenshot of Availability Report section of the User Interface.":::

Within the results you will be able to see a break down of each size or position. You will also see an additional column that will be added into the table that will display Roadblock Availability and Roadblock Capacity. These numbers will be for the Roadblock as a whole and will be the same numbers for each row.

## Additional notes

- The export option will deliver the same experience as seen in the User Interface.
- There will be a new API endpoint available.
  - This endpoint will deliver the summary number for the roadblock only.
  - The **Add to Batch** button will be disabled for Roadblock look ups.
  - Should the look up not be performed properly, there will be no results in the Roadblock column.
