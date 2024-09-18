---
title: Builder Tab
description: The article explains how you can access builder tab and build your target expressions on builder screen.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Builder tab

Clicking the **Builder** tab accesses the Builder screen. This is where you build your target expressions.

## Button descriptions and functionality

| Button/Field | Description |
|--|--|
| Target Expression Editor | Clicking the Target Expression verbiage allows you to view the target expression on a user-friendly screen. Target expressions are often very lengthy, and could be hundreds of lines long. The target expression is editable from this screen. You can make changes and select **Update**. The **Create Product** screen is displayed, and the values are updated accordingly. |
| Select Attributes or Product | Target expressions are either built from an existing product(s), or the particular attributes must be specified. Clicking **Select Attributes** accesses the Select Attributes screen. From this screen, you are able to choose attributes. Likewise, selecting **Product** accesses the Select Product screen, where you can choose products.<br>Clicking the information icon to the right of the Select Attribute or Product verbiage provides very basic general information about the workflow. |
| Vary By | This allows you to vary base targeting criteria by selected variant targeting criteria. It builds multiple targeting strings by combining each variant with the base targeting. Using the Vary By option will create multiple products – one for each unique combination of vary by attributes and values.|
| Undo | This clears the last action that you entered. |
| Clear All | This clears all of your entries, and allows you to start over.|
| Create Product | This will create the product(s) using the configured settings. It will turn your lookup expression into a product.|

## Build a target expression using attributes

There are two methods of building a target expression:

### Method 1

This method is recommended if you know exactly what you are looking for, and your target expression is small.

- Click **Type Attribute**. This allows you to type directly into the window. Start typing, and a list of the available attributes appears.
- Scroll down the list and select the attributes you desire. Select enter, and it automatically goes to the next one.

### Method 2

This method is recommended if you do not know specifically what you are looking for. You can start by doing a high-level search, and drill down further until you get the results you are looking for.

- Click **Select Attributes**. This accesses the **Select Attributes** screen. There are three main windows and three search windows.
- The list in the left-hand window is every attribute that you have available to you.
- You can limit the attributes by specified criteria.
- There is extensive search capability. The Contains and Search windows at the top of the screen allow you to drill down into the search.
- The four options in the search criteria are: Contains, Starts with, Ends with, Equals.
- Once the attribute has been identified and selected, the values for that attribute are displayed in the middle column of the screen. Then you can further drill-down into your search by applying the same search functionality to those results.
- If you want to select multiple attributes at once, you can do so by holding down the shift key while making your selection.
- There is also a **Select All** button, if you would like to select all the attributes listed in that window.
- The result of the search is displayed in the right-hand window.
- The right-hand window also has include/exclude functionality. You can exclude attributes from your final selection.
- When you are satisfied with your selection, select **Update**. You will now see the attributes listed on the Builder screen.
- If you would like to delete an attribute, mouse-over the attribute and select on the `x` in the upper right-hand corner.
- If you want to add other attributes, select Attributes again, and the entire list is displayed again. The previous selections will still be displayed in the right-hand column.

## Build a target expression for products

- You can select a product as base targeting and then add additional targeting as described in one of the two attribute methods above.
- If you have existing products in the system that you want to look up, then select **Select Product**. This accesses the Select Product screen, which displays a list of products.
- You can start your search by Name or Product ID.
- The additional four options in the search criteria are: Contains, Starts with, Ends with, Equals.
- There are five checkboxes at the top of the screen: Rate Card, Reporting, Seasonal, Custom, Inactive. By default, Rate Card and Reporting are selected. These filters are used to narrow down your search, especially if you have a lot of products.
- Click **Cancel** to cancel this entry.
- When you are satisfied with your selection, select **Update**.

## Related topics

- [Create a Product](create-a-product.md)
- [Organize Products](organize-products.md)
