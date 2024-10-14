---
title: Edit the Details of a Product
description: In this article, explore step-by-step instructions on how to edit the details of a product.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Edit the details of a product

You can edit the details of a product on the Edit Product page.

1. On the **Find Products** page, search for the product. To the left of the product, select **Edit Product**. The **Edit Product** page appears.

    You can also access the **Edit Product** page by selecting **Edit Product** on the **Product Visibility** page.
1. In the upper section of the page, update the product name, external product ID (used to map the product to your ad server), product type, and default rate card CPM as needed.
1. In the **Seasonal Rate** panel, add and remove rate cards as needed.
    - To add a rate card, select **Add New**. In the rate card row that appears, select a date range or accept the default. Type the rate card CPM, and type the floor CPM.
    - To delete a rate card, to the left of the rate card row, select **Remove**.
1. In the **Associated Product Groups** page, add and remove the product from product groups as needed.
    - To add the product to a group, select **Select**. In the **Product Group** dialog that appears, select the groups to which you want to add the product. Select **Update**.
    - To remove the product from a group, to the left of the product group row, select **Remove**.
1. To change the target attributes of the product, at the bottom of the page, select **Modify Target**. The **Modify Target** page appears.
    1. On the left side of the page, in the **Lookup Criteria** panel, select the product attributes you want to use for your new product.
        - To start with the attributes of an existing product, select it from the **Products** list. The product you select will replace all the existing attributes assigned to the product.
        - To specify target attributes for the product, select them from the Attributes list. You can search for products/attributes by typing in the filter field at the top of each list. As you type, the list of products/product groups is narrowed accordingly.
    1. In the **Attribute Values** panel on the right side of the page, review the attributes you selected.  
        - To specify attribute values, select the **click to add attribute values** link, add the values you want to look up. Select **Update**. You can type the values you want to look up or you can choose them from a comprehensive list by selecting **Select**, and adding/removing values in the **Attribute Values** dialog.
        - By default, the attributes you selected in step 2 appear in the Products must match all of these criteria box. To have your product also match any of a set of criteria, select the **And any of these criteria** box. Select attributes from the **Add Attributes** panel, and then specify the values for the attributes you chose.
    1. Select **Update**. The **Edit Product** page is redisplayed.
1. To exclude a product from lookups in the system, at the bottom of the page, select **Inactivate**. Inactive products retain their history but do not collect new data after the date they're made inactive. Once a product has been made inactive, it can't be reactivated.
1. Select **Save**.

## Related topics

- [Products Overview](products-overview.md)
- [Find and View a List of Products](find-and-view-a-list-of-products.md)
- [View the Full Details of a Product](view-the-full-details-of-a-product.md)
