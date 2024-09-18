---
title: Best Practices - Product group
description: The article highlights using product groups to organize accounts, emphasizing efficiency and expediting work processes.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Best practices - product group

Product groups are helpful to organize your account, allowing you to work faster and more efficiently.

You can use groups as:

- Report filters
- Shortcuts for searching and running availability requests
- Easing the learning curve for new users of the platform

Example: If you select a product group instead of a specific product, Yield Analytics will automatically pull in all products assigned to that group and add them to an availability lookup. If you apply a product group filter in reporting, you can quickly breakout or limit the data in that report - to the products in that group.

## Best practices and recommendations for managing product groups

- Assign every product in your system to at least one group, or reconsider why you need the product in the first place.
- Use a naming convention: A naming convention should be applied to your product groups as well as your products. In many cases, you can simply repurpose your product naming convention. If you name things as **Site_Section_Platform_Adsize**, it is suggested to name a site group as **Site_All Products** and a section group as **Site_Section_All Products**, etc.
- Use groups as a way to categorize horizontally and vertically: An easy way to start using groups is to think about assigning products based on their hierarchy. Example: You have a network that contains multiple sites, and each site has multiple site sections. You would create a group for each individual site, so that you can quickly identify **site A**’s products vs. **site B**’s products. Similarly, if you have multiple sites that contain a **recipes** section, you might create a group that identifies all the recipes products across every site. Consider how you typically need to pull inventory, or generate reports. You can most-likely identify a number of groups that would be useful to your business. You’ll be using groups as a shortcut to filter data, so align your groups to your common search needs.
- Use groups to identify master reporting products - Create some broad reporting products in your account that you can use as a way to filter data. If you need to create regular reports that track aggregate revenue or delivery stats by site across your network, having a single product group that contains all those master products is useful. You then do not need to search for each individual product when constructing a report. You will just add that one product group.
- Use groups specific to system users - It is suggested to create product groups that reflect what those stakeholders want.
Example: Create a few groups for your finance team that help them pull site level reports, section level reports, or audience level reports. When the finance team is building reports, they know they just have to filter to one of those groups and it will have the data they need. This solution is preferred rather than making them learn your naming convention across all products, or showing them how to do wildcard product searching in Analyzer.
- Use groups in the context of your business - This is typically for publishers that package their inventory differently by sales channel. It can be helpful to have product groups that are aligned to each channel. Example: You have a local, national, and a video sales team. Products and inventory are packaged differently for each team. It is advantageous to create groups that help you distinguish, so you can quickly respond to availability requests or reporting needs that are specific to a certain group.
- Use groups to keep track of temporary or experimental products - You may want to create a new product in Yield Analytics to start tracking a pool of inventory. Perhaps you want to combine two audience values, or see how volatile the inventory to a specific combination of zip codes is that a client has requested to buy. These non-standard products typically fill a temporary need. Unless you make them accessible so you can archive them, they simply accumulate. As a best practice, assign every product to at least one group.

## Product group FAQs

### How do I create a product group?

1. Navigate to the **Products** tab.
2. Select **Organize Products**.
3. In the **Filter** window, select **New**.
4. Name and save your new group.

### How do I remove a product group?

1. Navigate to the **Products** tab.
2. Select **Organize Products**.
3. Select the relevant group. This accesses the **Edit Product** screen.
4. Change status to **Inactive**. This removes it from the product group search results in the system, including in Analyzer and Availability.
5. You can re-activate a group at any time.

### How do I assign a product to a group?

1. Navigate to the **Products** tab.
1. Select **Organize Products**.
1. Select the group you would like to assign a product to. This accesses the **Edit Product** screen.
1. Select **Add**. This accesses a screen where you can search and add the products. It is recommended to add or remove products from the group screen rather than product by product.

An alternative way to assign a product to a group is from the **Product Visibility** screen:

1. Select **Edit Product** under the Product Details section.
1. Select **Select** under the **Associated Product Groups** on the **Product Details** screen.
1. A screen where you can add a new group, or remove the product from a group is accessed.

### How do I remove a product from a group?

1. Navigate to the **Products** tab.
1. Select **Organize Products**.
1. Select the group you would like to remove a product from. This accesses the **Edit Product** screen.
1. Select **Remove**. This accesses a screen where you can search and remove the products. It is recommended to add or remove products from the group screen rather than product by product. An alternative way to remove a product from a group is from the **Product Visibility** screen.
1. Select **Edit Product** under the Product Details section.
1. Select **Select** under the **Associated Product Groups** on the Product Details screen.
1. A screen where you remove the product from a group is accessed.

### Can I assign a product to more than one group?

Yes, you can assign a product to as many groups as you like.

### Is there a limit to how many products I can assign to a single group?

No, but at a certain point it makes sense to divide the products into more relevant groups. However, if you are grouping all products for a specific site, there could be thousands of products in a single group.

### Is there a minimum number of products to a group?

No. You do not have to assign any products at the time you create a group. You are free to set up what groups you think make sense, and name them according to a naming convention. You can then work on the more time-consuming task of product assignment at a later time.

### Can I pull the product group name as a dimension in Analyzer?

No. Product group is not an available dimension at this time. It is only available as a dimension filter.

## Related topic

[Products Overview](products-overview.md)
