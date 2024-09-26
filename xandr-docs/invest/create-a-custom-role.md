---
title: Microsoft Invest - Create a Custom Role
description: Learn how to control what a user sees in Microsoft Invest page by creating a custom role. 
ms.date: 10/28/2023
---

# Microsoft Invest - Create a custom role

If you need more fine-grained control over how your users access Microsoft Invest, you can create a custom role. Custom roles allow you to control what a user sees in Microsoft Invest so they only see the parts of your business that you choose.

Custom roles control the actions a user is allowed to take, such as the ability to view information or full permissions to modify that same information. For example, you may want an external sales house to have limited booking and reporting access. This page shows you how to create a custom role. For more information about roles, see [Working with Roles](working-with-roles.md).

## Locate the Roles screen

- Select **Network \> User Management \> Roles** from the navigation menu.
- Select **Roles** from the top right corner under the member (Select member name to get the dialog).
  
## Create Role

- From the **Roles** management screen, in the **Custom Roles** section, select **+New**.
- The **Create Role** screen will appear, where you can choose which permissions this custom role will have along with other details as mentioned below.

## Basic setup

- In **Role Name** field, enter a name that will help you to identify this role.The name must be unique within your Member.
- In **Role Description** field, enter a detailed description of the purpose of this role. This field is optional.
- In **Feature Roles** field, select **Edit Role Links**.

    A new dialog **Feature Roles** opens to specify feature roles to associate with this custom role.

- Select the feature role(s) to associate with this custom role. This field is applicable only if your Member has Feature Roles and you want to link this custom role to that.
- In **Users** field, select **Edit Associated Users**.
  
    A new dialog **Users** opens to specify the users for the role.

- Select the user(s) to link to the custom role who will have the permissions specified by the capabilities you assign in this role.

   Alternatively, you can select on **Roles** under **Network \> User Management** to go to **Roles** screen. There, you can select the **pencil** icon to open the **Edit Role** dialog and assign users. You can also assign an existing role when you create a new user. See [Create a User](create-a-user.md) for more information on user settings. After you assign a role to a user, it could take up to 10 minutes for the new permissions to take effect.

## Capabilities

Check the box next to each capability you want users who are assigned to this new role to have permission to access. For more information, see [Role Capabilities](role-capabilities.md).

## Landing page

Select a landing page from the dropdown list for the custom role. The capabilities for this role will determine where a user can begin their session in the application when they first log on. All users assigned to this custom role will log in directly to the selected landing page. This field is mandatory.
