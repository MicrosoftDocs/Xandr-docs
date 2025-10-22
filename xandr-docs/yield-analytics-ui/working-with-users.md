---
title: Working With Users
description: Learn how with administrative permissions you can add, import, disable, delete and reset password of a User. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Work with users

During implementation, Yield Analytics sets up an initial set of usernames, passwords, and user permissions.

After this initial setup, you can add, edit, disable, and delete user accounts for your organization. (This is assuming you have administrative permissions).

You can then grant permissions to these users by adding them to the appropriate user groups.

## Add a new user

If you have administrative permissions, you can add a new user account.

1. On the **Admin Tools** menu, select **Users**. The Users page appears, displaying a list of all user accounts.
1. At the bottom left of the list, select **Add User**. The New User page appears.
1. In the **Username** field, type the ID the user will use to log in to Yield Analytics.
1. In the **Password** field, type a password for the new ID. Retype it in the **Confirm Password** field, and then select **Save**.

## Import users

If you have administrative permissions, you can quickly add multiple users to Yield Analytics by importing a CSV (comma-separated values) file that contains a set of usernames and passwords.

1. On the **Admin Tools** menu, select **Users**. The Users page appears, displaying a list of all user accounts.
1. At the bottom of the list, in the **CSV File** field, select **Choose File**.
1. In the dialog that appears, select the CSV file you want to import.
1. Select **Import Users**. The new accounts are added to the list, and the system displays a count of the users that were successfully created.

## Reset a user's password

If you have administrative permissions, you can reset a user's password.

1. On the **Admin Tools** menu, select **Users**. The **Users** page appears, displaying a list of all user accounts.
1. In the **Username** column, select the username for the user you want to update. The **Edit User** page appears.
1. In the **Password** field, type the new password. Retype it in the **Confirm Password** field, and then select **Save**.

## Disable a user

If you have administrative permissions, you can disable user accounts to prevent previously active users from logging in to Yield Analytics.

1. On the **Admin Tools** menu, select **Users**. The **Users** page appears, displaying a list of all user accounts.
1. In the **Username** column, select the username for the user you want to disable. The **Edit User** page appears.
1. Clear the Enabled check box.
1. Select **Save**.

## Delete a user

If you have administrative permissions, you can delete user accounts.

> [!WARNING]
> You should only delete users who have not logged in to Yield Analytics. To prevent a previously active user from logging in, disable the user account instead.

1. On the Admin Tools menu, select **Users**. The **Users** page appears, displaying a list of all user accounts.
1. In the far right column for the user you want to remove, select **Delete**.
1. Select **OK**.

## Related topic

[Working With User Groups](working-with-user-groups.md)
