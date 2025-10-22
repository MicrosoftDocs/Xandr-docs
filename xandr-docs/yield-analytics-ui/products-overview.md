---
title: Products Overview
description: In this article, learn information about the Products tab in Yield Analytics.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Products overview

From the **Products** tab in yield analytics, you can:

- View a summary of product performance across your network.
- Analyze how products overlap each other.
- Create new products.
- Edit existing products.
- Organize products into groups for easier product management.

## About products

Products are used to represent inventory within a structure that carries pricing and/or reporting metadata. The default targeting attributes for your products are determined by your ad server implementation. You can view and edit these attributes in Yield Analytics.

> [!TIP]
> Yield Analytics maintains a continuous history across all previous versions of a product's targeting.

## Product types

Products are divided into four types:

- Rate Card –  Product that is sold frequently by the sales team and represents the product catalog (e.g., ROS 728x90).
- Reporting – Product that is used for reporting purposes, but is not generally not sold (e.g., Top three ad sizes in the Sports section).
- Custom – Product that represents a unique combination of attributes - that is not typically sold - but may have been trafficked in the ad server (e.g., ROS 728x90, DMA=NY, LA). Unique products referenced by order lines in the ad server are imported into Yield Analytics as custom products.
- Seasonal Model – Set of products that represents the seasonal patterns of traffic on your site. The full set of seasonal model products must comprehensively account for all the impressions in your network. Seasonal model products cannot overlap each other, and each seasonal model product must reflect all the distinct seasonality patterns observed in your network.

## Product statuses

The status of a product determines the data that's available for it in Yield Analytics - as follows.

- Active – Historical data is collected and forecasting is made for future performance.
- Inactive – Historical data is preserved, but no forecasting is available.
- Pending – Forecasting can be made for future performance, but no historical data is collected. Pending products that are not referenced by an order line and/or are not converted to Active status expire from yield analytics after a specific period of time.

The status of a product is determined by the product type and how the product was created.

## Related topics

- [Anatomy of the Products Dashboard Page](anatomy-of-the-products-dashboard-page.md)
- [Anatomy of the Find Products Page](anatomy-of-the-find-products-page.md)
- [Anatomy of the Audience Planner Page](anatomy-of-the-audience-planner-page.md)
- [Anatomy of the Product Visibility Page](anatomy-of-the-product-visibility-page.md)
- [Find and View a List of Products](find-and-view-a-list-of-products.md)
- [Analyze Product Overlaps](analyze-product-overlaps.md)
- [Overlap Types](overlap-types.md)
- [Create a Product](create-a-product.md)
- [Builder Tab](builder-tab.md)
- [Organize Products](organize-products.md)
- [View the Full Details of a Product](view-the-full-details-of-a-product.md)
- [Edit the Details of a Product](edit-the-details-of-a-product.md)
- [Best Practices - Product Group](best-practices-product-group.md)
