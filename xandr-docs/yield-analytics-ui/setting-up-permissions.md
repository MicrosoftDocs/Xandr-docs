---
title: Set Up Permissions
description: This article provides instructions to set up user group permissions. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Set up permissions

> [!TIP]
> There is no correlation between feature permissions and product permissions. If you belong to multiple groups, and one group has a set of feature permissions and a set of product permissions, then there is no correlation between those two. You will never have feature permissions somehow tied to those product permissions. If you belong to multiple groups, your feature permissions will collapse, and your product permissions will collapse. Both still run independently.

1. Under the **Admin Tools** section, select **Permissions**. From this screen, you can add a new group or edit an existing group.
1. To add a new group, select the **Add Group** button.
1. To edit an existing group, select  the **group(s)** that you would like to edit.

## Product Permissions tab

1. select the **Product Permissions** tab to access options for the product that you want to give that user permissions to.
1. The products that are shown default to Rate Card and Reporting products. You can also select Custom products to be shown as well.
1. Select the products you want to give the user access to. These will be the only products that they will see throughout the system.
1. Select **Save**.

> [!TIP]
> This implicitly includes products that are child products. The system will run in the background and look for any child products that belong to that parent product.

## Product search

Select **Products** > **Find Products** to search for products. You will see greatly narrowed search results for this User Group.

This is also true for the **Analyzer** page. Your search results will be greatly reduced from what the results previously were.

Here are some points to remember:

- When logged in with permissions, only the products and product groups that were selected for the specified User Group will be seen.
- If you search for a Product Group, the results will be Product Groups that include products you have access to that belong to that specific Product Group.
- You may not have access to an entire Product Group, but you have data from a product within that Product Group. These are the products you have access to.
- You will have access to parent products as well.
- There is no constriction on attributes. You can select any targeting attribute that is run.

> [!TIP]
> If there is no data on products you have access to, the data will not return. Therefore, if you select an attribute that belongs to products that you do have access to – you will not receive any data back.

## Order Visibility screen

In the **Order Visibility** screen, you see all the order lines that are consuming against your products for those orders.

Order Lines are decided based on how it is consuming against the products you have access to. If an Order Line is indirectly consuming against your product, you have the right to view the data that pertains to it. However, it is not something you have direct access to. You cannot modify it, but you can see that it is consuming some impressions on your product.

## Order Line Visibility screen

In the **Order Line Visibility** screen, you see the order lines that are competing against the products you have access to.

> [!TIP]
>
> - You will only be shown revenue data to products you have access to.
> - The logic described in the **Order Visibility** screen and **Order Line Visibility** sections is the same logic that follows through all the tabs.

## Consumption tab

From the **Consumption** Tab, you can see what products are consuming against from the order line. These are all the products you have access to.

> [!TIP]
> The display will default to whatever your most expansive privilege is. Your greatest asset to the data will determine what your experience is as a user. You may log-in and see something very different than what you are used to. This is especially true for people who are running dashboards at a lower level. The data will not match the data from someone a higher level, with more access.

### Example

I belong to one User Group today, and then I get added to a separate User Group tomorrow. Everything could change: My data viewpoint, reports, everything I have saved.

Here are some other points to remember:

- The Overlap Type is going to tell you how you have access to it: Parent, Self, or Twin.
- Each User Group has certain system privileges on certain data. What you can do with the data in one User Group may not necessarily match what you can do with data from another User Group.

## Additional information

### Organize products

When you are organizing products, here are some points to remember:

- Your ability to remove products from a product group will be limited to the products you have access to. Even though it may say remove, these are not hyperlinked.
- You can add your products to product groups. You can remove your products from product groups. You cannot alter any other products within that product group.

### Scenario Manager

- You will not be able to add orders to Scenario Manager that you do not have access to.
- You shouldn’t see order lines that you do not have access to. You will see orders.
