---
title: Best Practices - Reporting Product Strategy
description: Improve product strategy reporting with clear tools and distinct naming for enhanced clarity and differentiation.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Best practices - Reporting product strategy

## Reporting products overview

Reporting products are products that are generally not sold, but are used for reporting purposes only. Reporting products can be used as shortcuts to:

- Aggregating meaningful pools of inventory
- Breaking out consumption and optimizing campaigns
- Finding, upselling, and cross-selling opportunities

Reporting products are created in, and typically exist in Yield Analytics only. This is contrary to rate-card products or custom products, which are typically imported from the ad server or order management system.

## Create useful reporting products

There are a few rules that we recommend in creating reporting products:

**Differentiate your naming convention**

Naming conventions are very important for all products in your system. This is for easy access, and to understand what products refer to without having to look at their targeting expression. The same is true for reporting products: They are only useful when they are well-organized.

You can filter specifically to reporting products in all areas of Yield Analytics by using the Product Type element. It is recommended to use some kind of element in the product name itself. You frequently desire to build reports that are specific to a single or minimal amount of reporting products. Filtering based on naming convention makes in easier to build those reports quickly.

Many publishers use an abbreviation of an existing element that is already present in their products. This eliminates the need to add a new product: You just change an existing element. (Normally this inconsistency isn’t something you’d want to introduce to a naming convention. It is used in this case because the inconsistency identifies a distinction between products).

For example: Your site is the technology news site **TechCrunch**. You set your site variable set as `TechCrunch` for all your Rate Card Products, but use `TC` as the site variable for your reporting products.

An example of possible rate card products:

- **TechCrunch_Desktop_USOnly_News_Startups_Apps_728x90**
- **TechCrunch_Desktop_USOnly_News_Startups_Apps_300x600**
- **TechCrunch_Desktop_USOnly_News_Startups_Apps_160x600**

A reporting product could be named:
**TC_Desktop_USOnly_News_Startups_Apps_AllSizes**

In this way, the core of the product is identical between the rate card products and the reporting product. The site parameter has only been changed. If you needed to find the reporting product that was a parent to one of the rate card products, you’d immediately know how it would be named. It would be based on the rate card product name.

## Create reporting products using combinations of inventory assets

The recommended way to initially create reporting products, is by creating various combinations of your core inventory assets. This allows you to track your effective yield, capacity, and consumption over time - against basic elements. The goal is to be able to isolate different variables by using reporting products. This allows you to create useful reports in the future.

Create a host of products based on the below items. You can create reporting products for:

**Geography** - Every county / state / DMA.  
**Example**: Tracking_Geo_ROS_Arizona_AllSizes, Tracking_ROS_Arkansas_AllSizes, etc.

**Content** - Every combination of site / section / topic / subtopic.
**Example**: Tracking_Content_SportsSite_ProfessionalLeague_MLB_Yankees

**Audience** - Every combination of audience type / value.
**Example**: Tracking_ROS_Audience_Demo_Gender_Male, Tracking_ROS_Audience_Purchase_Auto_Luxury, etc.

**Ad Unit**  - Every combination of ad unit.
**Example**: Tracking_AdUnit_ROS_Video_AllSizes, Tracking_ROS_Display_AllSizes

**Platform** - Every platform.
**Example**: Tracking_Platform_ROS_Mobile_AllSizes

**Page Template** - This is a rarely used element, but one that can be especially insightful for optimization and viewability metrics.
**Example**: Tracking_Template_ROS_ArticlePages_AllSizes, Tracking_Template_ROS_Slideshows_AllSizes

Once you have these basics in place, consider where it may be applicable to do cross category combinations. Perhaps you desire a platform-specific version of every content reporting product, or an audience-specific version of every geo product.

> [!NOTE]
> A reporting product for every conceivable permutation of ad parameters is unnecessary. The actual amount depends on the business. Most publisher accounts have 5,000 - 10,000 reporting products. This is typically based on a ratio of 2 - 4X their number of rate card products.

## Use product groups

Once you have some reporting products created, it is recommended to start assigning them to groups. Groups will make it easier to create reports quickly, because they will help filter reporting results and product searches.

The major risk in product groups is using too many groups, to the point where it’s cumbersome to search the groups. Do create groups for primary types (Geo vs. Audience, Content vs. Platform). Do not create groups for every content section or subsection (Sports_Baseball vs. Sports_Football vs. Sports_Basketball). This would create hundreds or thousands of groups. It is recommended to rely on a strong naming convention, and search for what you need.

A product group probably isn’t that valuable if it contains less than 10 products that could have a common and unique element in their name. It can make sense to have small groups if you want to create them for specific stakeholders in your organization. Example: The finance team analyzes data in a specify fashion, so their life is made easier by always filtering reports with a single product group.

You can read more about Product Group Strategy in a separate Yield Analytics Best Practice doc.

## Related topic

[Reports Overview](reports-overview.md)
