---
title: Working with Roles using the API
description: In this article, learn about the two types of roles using the API.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Working with roles using the API

A Role represents a set of capabilities (also known as permissions) that a user may have access to in the system. For example, a user may have a `"Salesperson"` role that needs to have read-only access to buy-side information using the **Advertisers/Orders - Read Only** permission. Since the user's access is read-only, they can view those parts of the system, but they can't make any changes.

There are two types of roles:

- **Platform**: Roles that are built into our system, such as Network Admin. Platform roles have a pre-defined set of permissions that cannot be changed.
- **Custom**: Roles that you create. Custom Roles give you fine-grained control over user access.

## About custom roles

Depending on the size and needs of your business, you may want to restrict access for some of your users to specific capabilities. Reasons you might want to do this include:

- You're a publisher that contracts with a sales house to represent a particular region of your inventory, and you need to provide limited booking and reporting access.
- You want to allow salespeople to view your book of business, but you don't want them to create or manage line items themselves.
- A specific user within your organization requires one-off custom access.

With custom roles, you can control user access so they only see the parts of your business that you choose.

For instructions on creating a custom role using the API, see [Create a Custom Role using the API](create-a-custom-role-using-the-api.md).

## The role object hierarchy

The relationship of users, roles, and resources is shown in the diagram below:

- A **User** can fill one or more **Roles**
- A **Role** can have access to one or more **Resources**
- A **Resource** may depend on other **Resources**

:::image type="content" source="media/role-object-hierarchy.png" alt-text="Diagram that illustrates a role object hierarchy.":::

## Related topics

- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [Add a User to a Role using the API](add-a-user-to-a-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
