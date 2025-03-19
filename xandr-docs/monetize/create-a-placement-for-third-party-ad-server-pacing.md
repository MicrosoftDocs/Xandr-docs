---
title: Create a Placement for Third-Party Ad Server Pacing
description: In this article, find information on how to create and set up a placement that is third-party pacing compliant.
ms.date: 10/28/2023
---

# Create a placement for third-party ad server pacing

When creating a programmatic guaranteed (PG) deal that uses third-party ad server pacing, you must first create a placement that is third-party pacing compliant.

PG deals that use a third-party ad server for pacing require a single, exclusive placement to be made only for that deal. The placement must also be the only placement contained within a single placement group. To create the placement:

1. Click **Publishers** > **Inventory Manager**.

1. Select a publisher.

1. Click **Create New** > **Placement Group**.

1. Enter a name for the placement group.

1. **Optional:** Enter the top level domain name for the placement group.

1. Select **Do not participate** to ensure that your placement group and placement don't participate in real-time bidding.

1. Select the **Allow deal demand for this placement group** checkbox.

    Making this selection and creating a unique placement for your PG deal ensures that your PG line item is the only demand eligible for the placement.

1. Click **Save & Add New Placement**.

    The **Create New Placement** dialog displays.

    You've just created the placement group needed for your PG deal placement. Now, you can create the placement that you'll use for your third-party pacing PG deal.

1. Enter a name for the placement.

1. Set a state for your placement:
    - **Active**
    - **Inactive** - the recommended state for the placement before your PG deal begins. However, you must eventually change the placement's state to **Active** once the PG deal begins.

1. Select a media (creative) type for the placement.

    > [!IMPORTANT]
    > You can currently only use banner creatives in your PG deal without a Microsoft Advertising representative's assistance. If you'd like to use other creative types, please contact your Microsoft Advertising account representative.

1. Select a size for the media type.

    If you choose a banner media type for your placement, you must select **Sizeless**. You can later add banner sizes to the generated placement tag using macros.

1. Click **Save**.

    You've just finished creating your placement. Now, you must retrieve its placement tag.

1. Click **Export Tag** within the placement's **Placement Details** pane.

    For more information on exporting placement tags, see [Export Placement Tags](export-placement-tags.md).

The placement tag is now available to you for trafficking in your third-party ad server. You can now begin creating a PG deal that uses third-party ad server pacing. For more information, see [Create a Programmatic Guaranteed Deal that Uses Third-Party Ad Server Pacing, Tag Integration](create-a-programmatic-guaranteed-selling-line-item-ssp.md).

## Related topic

[Selling Programmatic Guaranteed Deals](programmatic-guaranteed-selling-line-items.md)
