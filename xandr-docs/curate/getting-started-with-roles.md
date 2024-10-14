---
title: Microsoft Curate - Get Started with Roles
description: Learn what are roles and how it defines the actions a user is allowed to take depending upon the permissions granted to the user. 
ms.date: 11/14/2023

---

# Microsoft Curate - Get started with roles

As a company doing business with Microsoft Advertising, it's possible that you have more than one user responsible for your company's interaction with the system, whether that interaction is through the UI or the API. You may have several users who are responsible for different advertisers and publishers, and for different aspects of working with those advertisers and publishers. In creating and managing your interactions, you want to ensure that you have the right users responsible for the right parts of the system. User access control with roles gives you the ability to restrict user permissions based on the user's specific business needs.

## Roles

A role defines the actions a user is allowed to take. For example, a user may have permission to view, modify, or delete a component in the system (such as an advertiser, publisher, or insertion order).

Access control involves assigning a user to a role.

## Remove components

A user's ability to view, create, edit, and delete components depends on the combination of roles and permissions. As mentioned previously, sometimes these combinations can lead to some confusion. Here is a possible scenario having to do with removing components, and what the results will be.

User1 has the following permissions:

- Custom Role: Advertisers Create/Edit and Advertisers/Orders - Delete
- Team: SalesTeamUS with access to insertion orders 1, 2, and 5 under AdvertiserA

This gives User1 permissions to create new insertion orders under AdvertiserA (and add those insertion orders to team SalesTeamUS). This also gives User1 permission to view, edit, and delete insertion orders 1, 2, and 5, but not the full AdvertiserA information or insertion orders 3 and 4. So what happens if User1 deletes insertion orders 1, 2, and 5 before creating more insertion orders?

In that case, even though everything User1 had been able to view under AdvertiserA is gone, User1 will still be able to create new insertion orders under AdvertiserA and add those insertion orders to SalesTeamUS.
