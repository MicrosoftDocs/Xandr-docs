---
title: Work With User Groups
description: Learn how by having administrative permissions you can add, edit, duplicate, search, and delete a User Group.  
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Work with user groups

Permissions within Yield Analytics are configured through user groups. Each Yield Analytics user account can belong to multiple groups. However, the group with the broadest permissions overrides the more restrictive groups (Example: If a user belongs to the Admin group and the AdOps group, the permissions for the Admin group win).

If you have administrative permissions, you can add, edit, duplicate, and delete user groups.

## Add a user group

If you have administrative permissions, you can add user groups to determine permissions for a set of users.

1. On the **Admin Tools** menu, select **Permissions**. The Permissions page appears. This displays the Groups panel with a table of all existing user groups.
1. Above the list of groups, select **Add Group**. The **Group: New Group** panel appears.
1. In **Group Summary** section, in the **Name** field, type a name to identify the group (e.g., `AdOps`), and optionally, in the **Description** field, type an explanation for the group (i.e., `Permissions for the Ad Operations team`).
1. In the **Users in This Group** section, select the usernames you want to add to the group, or select **Select All** to add all available users. As you select users on the left, they're added to the list of users on the right.
1. In the **Features Available In This Group** section, clear the check boxes for the features this group shouldn't be able to access. Select the check boxes for the features this group should be able to access.

    The features are broken up into the following sets: Capacity, Availability, Products, Orders, Proposals, Pricing, Reports, Scenario, Admin Tools, and Other. All features are selected by default.
1. Select **Save**.

## Edit a user group

If you have administrative permissions, you can edit user groups to add and remove users in the group. You can also change the permissions for the group.

1. On the **Admin Tools** menu, select **Permissions**. The Permissions page appears, displaying the Groups panel with a table of all existing user groups.
1. Select the user group you want to edit. The Group: \[Group Name\] panel appears. \[Group Name\] is the name of the group you selected.
1. Update the name and/or description of the group in the **Group Summary** section as needed.
1. Add and remove users in the **Users in This Group** section as follows:
    - To add users to the group, in the list of usernames on the left, select each username you want to add (or select **Select All** to add all users). As you select users, they are highlighted in the list on the left, and added to the list on the right.
    - To remove users from the group, in the list of usernames on the right, select the X for each username you want to remove (or select **Clear All** to remove all users). As you select to remove users, they are deleted from the list on the right and un-highlighted in the list on the left.
1. Change the permissions for the group as needed in the **Features Available In This Group** section. Select the check boxes for the features the group should be able to access. Clear the check boxes for the features the group shouldn't be able to access. The features are broken up into the following sets: Capacity, Availability, Products, Orders, Proposals, Pricing, Reports, Scenario, Admin Tools, and Other.
1. Select **Save**.

## Duplicate a user group

If you have administrative permissions, you can duplicate a user group to quickly set up a new group with similar permissions.

1. On the **Admin Tools** menu, select **Permissions**. The Permissions page appears, displaying the Groups panel with a table of all existing user groups.
1. Select the user group you want to duplicate. The Group: \[Group Name\] panel appears, where \[Group Name\] is the name of the group you selected.
1. At the bottom of the page, select **Duplicate**.
1. In the **Group Summary** section, type a name and description for the duplicate group.
1. Add and remove users in the **Users in This Group** section as follows:
    - To add users to the group, in the list of usernames on the left, select each username you want to add (or select **Select All** to add all users). As you select users, they are highlighted in the list on the left and added to the list on the right.
    - To remove users from the group, in the list of usernames on the right, select the X for each username you want to remove (or select **Clear All** to remove all users). As you select to remove users, they are deleted from the list on the right and un-highlighted in the list on the left.
1. Change the permissions for the duplicate group as needed in the **Features Available In This Group** section. Select the check boxes for the features the group should be able to access. Clear the check boxes for the features the group shouldn't be able to access. The features are broken up into the following sets: Capacity, Availability, Products, Orders, Proposals, Pricing, Reports, Scenario, Admin Tools, and Other.
1. Select **Save**.

## Search user groups

If you have administrative permissions, you can quickly search for user groups by group name, username, or permission. For example, you may want to find all user groups to which a certain username belongs, or you may want to find all groups that have permissions for a particular feature.

1. On the **Admin Tools** menu, select **Permissions**. The **Permissions** page appears, displaying the **Groups** panel with a table of all existing user groups.
1. In the **Search** panel on the left side of the page, type your criteria for the groups you want to find as follows:
    - To search for groups by name, type a value in the **Group Name** field.
    - To search for groups that contain a specific username, type a value in the **User Name** field.
    - To search for groups with access to a specific feature, type a value in the **Permission (Feature Name):** field.
    - To search for multiple values in a single field, separate the values with a semicolon (e.g., to search for all groups that contain "ad" or "ops," type `ad;ops`).
1. Select **Search**. The **Groups** panel is redisplayed to show only the groups that meet your search criteria.

## Delete a user group

If you have administrative permissions, you can delete a user group.

1. On the **Admin Tools** menu, select **Permissions**. The **Permissions** page appears, displaying the Groups panel with a table of all existing user groups.
1. Select the user group you want to delete. The Group: **[Group Name]** panel appears. **[Group Name]** is the name of the group you selected.
1. At the bottom of the page, select **Delete**. On the dialog that appears, select **OK**.
