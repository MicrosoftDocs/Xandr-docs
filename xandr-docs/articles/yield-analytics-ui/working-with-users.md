---
title : Working With Users
description : Learn how yield analytics can be used to set usernames, passwords, permissions, add, edit, disable and delete user accounts.
ms.date : 10/28/2023
ms.custom : yield-analytics-ui

---


# Working with users

During implementation, yield analytics sets up an initial set of
usernames, passwords, and user permissions.

After this initial setup, you can add, edit, disable, and delete user
accounts for your organization. (This is assuming you have
administrative permissions). 

You can then grant permissions to these users by adding them to the
appropriate user groups.

## Add a new user

If you have administrative permissions, you can add a new user account.

1. On the **Admin Tools** menu, click **Users**. The Users page appears, displaying a list of all user accounts.
1. At the bottom left of the list, click **Add User**. The New User page appears.
1. In the **Username** field, type the ID the user will use to log in to yield analytics.
1. In the **Password** field, type a password for the new ID. Retype it in the **Confirm Password** field, and then click **Save**.

## Import users

If you have administrative permissions, you can quickly add multiple users to yield analytics by importing a CSV (comma-separated values) file that contains a set of usernames and passwords.

1. On the **Admin Tools** menu, click **Users**. The Users page appears, displaying a list of all user accounts.
1. At the bottom of the list, in the **CSV File** field, click **Choose File**.
1. In the dialog that appears, select the CSV file you want to import.
1. Click **Import Users**. The new accounts are added to the list, and the system displays a count of the users that were successfully created.


## Reset a user's password

If you have administrative permissions, you can reset a user's password.

1. On the **Admin Tools** menu, click **Users**. The **Users** page appears, displaying a list of all user accounts.
1. In the **Username** column, click the username for the user you want to update. The **Edit User** page appears.
1. In the **Password** field, type the new password. Retype it in the **Confirm Password** field, and then click **Save**.

## Disable a user
If you have administrative permissions, you can disable user accounts to prevent previously active users from logging in to yield analytics.

1. On the **Admin Tools** menu, click **Users**. The **Users** page appears, displaying a list of all user accounts.
1. In the **Username** column, click the username for the user you want to disable. The **Edit User** page appears.
1. Clear the Enabled check box.
1. Click **Save**.

## Delete a user

If you have administrative permissions, you can delete user accounts.

> [!WARNING]
> You should only delete users who have not logged in to yield analytics. To prevent a previously active user from logging in, disable the user account instead.

1. On the Admin Tools menu, click **Users**. The **Users** page appears, displaying a list of all user accounts.
1. In the far right column for the user you want to remove, click **Delete**.
1. Click **OK**.



## Related topics

- [Working With User Groups](working-with-user-groups.md)
