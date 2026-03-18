---
title: Update a Placement
description: This page provides an overview to update a placement. Learn to edit, delete, duplicate, and move placements in this page. 
ms.date: 3/18/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Update a placement

You can update placements to modify placement settings, move placements between placement groups, duplicate placements, or delete placements that are no longer needed.

Placements are managed from **Inventory Manager**, where you can view placement groups and their associated placements.

---

# Edit a placement

You can edit a placement using the **Placement Details** pane.

To edit a placement:

1. Navigate to **Publishers > Inventory Manager**.
2. Use the **Select Publisher** dropdown to search for the publisher you want to work with.
3. Switch to **Tree view** using the top-right table header to see **Placement Groups** and their associated **Placements**.
4. Expand the placement group that contains the placement you want to edit.
5. Click the placement row to select and highlight it.

The **Placement Details** pane appears.

You can edit a placement by clicking the placement row to select and highlight it, then clicking either the **Edit** or **Edit Inline** button in the **Placement Details** pane that appears.

* **Edit** opens the full placement editor where you can modify all placement settings.
* **Edit Inline** allows you to update selected placement fields directly in the Placement Details pane.

After making changes, select **Save**.

---

# Move placements

You can move placements from one placement group to another placement group.

To move placements:

1. Navigate to **Publishers > Inventory Manager**.
2. Use the **Select Publisher** dropdown to search for the publisher you want to work with.
3. Switch to **Tree view** using the top-right table header to see **Placement Groups** and their associated **Placements**.
4. Expand the placement group that contains the placements you want to move.
5. Check the boxes for all the placements you want to move.
6. Select **Move** in the table header.
7. In the dialog that appears, select the placement group you want to move the placements to.
8. Select **Move** to confirm.

The placements are moved to the selected placement group.

---

# Duplicate placements

You can duplicate a placement to create a new placement with the same configuration.

This can be useful when you want to create multiple placements with similar settings.

To duplicate a placement:

1. Navigate to **Publishers > Inventory Manager**.
2. Use the **Select Publisher** dropdown to search for the publisher you want to work with.
3. Switch to **Tree view** using the top-right table header to see **Placement Groups** and their associated **Placements**.
4. Expand the placement group that contains the placement you want to duplicate.
5. Check the box for the placement you want to duplicate.
6. Select **Duplicate** in the table header.

A new placement is created using the same configuration as the original placement.

After duplicating the placement, you can update the placement name, reserve price, or other settings as needed.

## Set reserve price for duplicated placements

You can set a reserve price for the duplicated placement to define the minimum CPM buyers must meet to serve an ad on the placement.

To set or update the reserve price:

1. Select the duplicated placement.
2. In the **Placement Details** pane, select **Edit**.
3. Locate the **Reserve Price** field.
4. Enter the desired CPM value.
5. Select **Save**.

The updated reserve price applies to all demand sources bidding on the placement.


---

# Delete placements

You can delete placements that are no longer needed.

Deleting a placement permanently removes it from Inventory Manager.

## Step 1. Select placements

1. Navigate to **Publishers > Inventory Manager**.
2. Use the **Select Publisher** dropdown to search for the publisher you want to work with.
3. Switch to **Tree view** using the top-right table header to see **Placement Groups** and their associated **Placements**.
4. Expand the placement group containing the placements you want to delete.
5. Check the boxes for the placement or placements you want to delete.

## Step 2. Confirm deletion

1. Select **Delete** in the table header.
2. Confirm the deletion when prompted.

The selected placements are removed from Inventory Manager.



<!-- 
# Update a placement

There are many actions you can perform on placements. This page explains how to edit, delete, duplicate, and move placements.

## Edit a placement

You can edit a placement by clicking the placement row to select and highlight it, then clicking either the **Full Edit** or **Edit Inline** button in the **Placement Details** pane that appears. See [Create a Placement](create-a-placement.md) for descriptions of the fields you can edit.

## Delete a placement

You can delete placements from the Microsoft Advertising system in just two steps.

> [!WARNING]
> Before you proceed, please note that deleting placements is permanent and cannot be reversed.

## Step 1. Get started with placements

**Publisher-only clients:** Select **Placements** from the **Inventory** menu in the main navigation menu, then select the publisher you want to work with from the Select a Publisher dialog. This opens the **Inventory Manager**, which shows both the **Placement Group List** and the **Placement List** under each placement group for the publisher.

**All other clients:** Go to **Publishers** \> **Inventory Manager** and select the publisher you want to work with. This will open the **Placement List** for that publisher. Click the box(es) next to the placement or placements you want to delete.

## Step 2. Confirm deletion

Once you have selected the placement or placements to delete, select **More Actions** \> **Delete**. This will open the **Confirm delete** dialog. Verify that you want to delete the placement by clicking **Confirm**.

> [!NOTE]
> If a managed campaign is directly targeting the placement, you will see the warning "Cannot delete placement that is targeted by campaigns. Contact Microsoft Advertising support." In order to delete this placement, you will need to first remove the placement from the campaign targeting. Once this is done, you should be able to delete the placement.

## Move a placement to a different placement group

A placement is an open slot on a publisher website where an advertiser creative with matching specifications can serve. Placement groups provide a way for you to organize and manage placements, apply default inventory categorization, and self-auditing criteria to child placements. This page explains how to move a placement to a new placement group.

## Step 1. Get started with moving placements

**Publisher-only clients:** Select **Inventory** \> **Placements**, then select the publisher you want to work with from the **Select a Publisher** dialog. This opens the **Inventory Manager**, which shows both the **Placement Group List** and the **Placement List** under each placement group for the publisher.

**All other clients:** Go to **Publishers** \> **Inventory Manager** and select the publisher you want to work with. This will open the **Placement List** for that publisher. Click the box(es) next to the placement or placements you want to move.

## Step 2. Move the desired placements to a different placement group

Check the checkbox for the placement under which you want to move to another new placement group, then click **More Actions** \> **Move**. This will open the **Select a destination placement group** dialog. Click **Select** to complete the action. If you want to move more than one placement to the same group, you can move them all at once by checking multiple boxes.

## Step 3. Review the placement list

In the **Placement Group List**, click the placement group under which you moved the placement. You should see the placements you moved show up in the **Placement List** for that placement group.

## Duplicate a placement

When you want to create a number of similar placements, you can save time by duplicating placements and editing the specific features you want to modify.

## Step 1. Get started with duplicating placements

**Publisher-only clients:** Select **Inventory** \> **Placements**, then select the publisher you want to work with from the **Select a Publisher** dialog. This opens the **Inventory Manager**, which shows both the **Placement Group List** and the **Placement List** under each placement group for the publisher.

**All other clients:** Go to **Publishers** \> **Inventory Manager** and select the publisher you want to work with. This will open the **Placement List** for that publisher. Click the box(es) next to the placement or placements you want to duplicate.

## Step 2. Confirm duplicate

Once you have selected the placement or placements to duplicate, go to the **More Actions** dropdown and select **Duplicate**.This will open the **Confirm duplicate** dialog. Type the name of your new placement into the text box and click the **Confirm** button.

## Step 3. Make changes to the new placement

Once you have renamed your placement and confirmed the duplication, your duplicate placement will show up in the Placement List. You can then edit the placement or change its default creatives as you would for any other.

## Set a reserve price

You can set a reserve price, which is the minimum net amount the placement will accept for placing a creative, for the placement from the **Inventory Manager** screen in the **Default Creatives** pane. Under **Reserve Price Settings**, click **Edit**, then complete the selections in the **Reserve Price Settings** dialog that appears as below:

- **Reserved price based on**: Select the criteria of calculating the reserved price from total **Network revenue** or total **Publisher revenue**.
- **Reserved price applies to**: Select whether reserved price is applied to :
  - **All demands**: The rule will apply to bids from your managed advertisers as well as third-party bids.
  - **Third-party and non-preferred direct demand**: The rule will apply to third-party bids as well as bids from your managed advertisers that are not considered a preferred bid.
  - **Third-party demand only**: The rule will apply to third-party bids, and not to bids from your managed advertisers.

  Please note that if you select **All demands**, the reserved price will not apply to learn bids from direct campaigns when your inventory prefers learn bids.

## Related topics

- [Working with Placements](working-with-placements.md)
- [Create a Placement](create-a-placement.md)
