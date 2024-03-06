---
title: Microsoft Monetize - Working with Roles
description: Explore defining user access roles in the system at Platform or Feature level. Customize roles to meet business needs.
ms.date: 10/28/2023
---

# Microsoft Monetize - Working with roles

Roles determine what the users can view and perform in the Microsoft Advertising system, and can be applied at the Platform or Feature level. You can also create custom roles depending on the need of the business.

A **role** represents a set of capabilities (also known as permissions) that a user has access to in the system. For example, a user with the Platform role of Network Admin can view, create, update, and edit anything within the system for their network, while a user with a Custom role that includes only the Advertisers/Orders - Read Only permission
won't be able to do anything other than view network advertisers and insertion orders on that network.

There are three types of roles:

- **Platform**: Roles that are built into the Microsoft Advertising system
- **Feature**: Roles that provide access to alpha and beta features.
- **Custom**: Roles that you create. Custom Roles give you fine-grained control over how your users access console.

## Platform roles

Platform roles are created by Microsoft Advertising and cannot be changed. They have a pre-defined set of permissions that relate mostly to administrative and specialized tasks.

Platform roles differ by network, but could include roles such as the following:

- **Network Admin**: Full permission to the network.
- **Network Observer**: Read-only permission to all aspects of the network.
- **Network Advertiser Manager**: Permission to generate reports for the network's advertisers.
- **Network Publisher Manager**: Permission to generate reports for the network's publishers.
- **User Manager**: Permission to create, edit and deactivate all member-level users.
- **Team Manager**: Ability to create and modify teams and team membership.
- **Roles Manager**: Ability to create and modify custom roles.
- **Finance Management**: Ability to view and manage sensitive financial information.

You can assign platform roles to users when you create the user account. You can also assign users to a new platform role by editing the user account.

> [!IMPORTANT]
> If you do NOT have a Team setup, the following applies to the **Network Advertiser Manager** and the **Network Publisher Manager** roles:
>
> - If a user has either one of the above mentioned roles; that is the ONLY role the user can have. Neither of the roles can be assigned in conjunction with any other role.
> - After you have created a user with one of the roles, you will NOT be able to edit the role.

## Feature roles

Like platform roles, feature roles are created by Microsoft Advertising, and the resources granted based on those roles cannot be changed by network administrators. You can, however, update the role to ensure all the appropriate users in your network have permissions to the feature. When a feature role is removed, all users who had access to that product or feature will retain access.

## Custom roles

Depending on the size and needs of your business, you may want to restrict access for some of your users to specific capabilities within Microsoft Monetize. Reasons you might want to do this include:

- You are a publisher that contracts with a sales house to represent a particular region of your inventory, and you need to provide limited booking and reporting access.
- You want to allow salespeople to view your book of business, but you don't want them to create or manage line items themselves.
- A specific user within your organization requires one-off custom access.

With custom roles, you can control how your users access Microsoft Monetize so they only see the parts of
your business that you choose. For more information about the permissions available to custom roles, see [Create a Custom Role](create-a-custom-role.md).

## Related topics

- [Getting Started with Roles](getting-started-with-roles.md)
- [Create a Custom Role](create-a-custom-role.md)