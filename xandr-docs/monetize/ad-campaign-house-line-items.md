---
title: House Line Items
description: Learn house line items in Microsoft Monetize to promote internal campaigns, utilizing ad inventory for brand awareness, engagement, and fallback ads.
ms.date: 10/28/2023
---

# House line items

In Microsoft Monetize, house line items (HLI) are a specific type of advertising campaign used by publishers to promote their own products, services, or initiatives. These campaigns are internal marketing efforts where the publisher utilizes its own ad inventory to showcase and promote its offerings.

## Purpose and setup

House line items are used to run **in-house campaigns**, which are non-revenue generating and hold the lowest priority compared to other campaigns. These campaigns can be configured with the following settings:

- **$0 revenue value**
- **Unlimited lifetime budget**
- **Unlimited daily budget**

These campaigns are typically used to increase brand awareness, drive engagement, or cross-promote different products or services within the publisher's ecosystem.

### Fallback campaign

House line items can serve as **fallback campaigns** when no other ads are eligible to serve. This ensures that ad space is utilized even when there are no external ads available.

> [!NOTE]
> To create HLIs on your seat, contact your account manager.

## Create a House Line Item on Microsoft Monetize

You can create a new house line item (HLI) from the **Line Items** screen. For more information, see [Monitor Line Items](monitor-line-items.md).

1. Select **Advertisers** >  **Line Items** from the vertical navigation menu on left
1. Click **+ New**.
1. Select **Line Item**
1. Select the **House Ad** option.
3. Select the associated **Advertiser**
4. Select the associated **Insertion Order** drop-down, 
5. Click **Next** to open the **Create New House Ad Line Item** screen.

## Basic settings

You can set the name, state, and ad type of the HLI from the **Basic settings** section. You can also optionally assign an external code.

### Insertion Orders

You can change the associated insertion order to the line item by doing the following:

1. Click the **pencil** icon above the existing insertion order.
2. A list of corresponding insertion orders (if any) will display automatically.
3. Search for the appropriate insertion order you want to select.
4. Select the corresponding checkmarks to associate the insertion order with the line item.
5. Click **Save**.

### Name

Enter a unique name for the line item that you will use for searching and reporting.

> [!NOTE]
> > The name of the line item must be unique per advertiser.

### External Code (Optional)

To report on a line item using your own code (rather than the **internal ID** that Microsoft Advertising assigns automatically), click **+External Code** and enter a code. External codes must follow these guidelines:

- They can only contain alphanumeric characters, periods, underscores, or dashes.
- Codes are not case-sensitive (uppercase and lowercase characters are treated the same).
- Each advertiser must use a unique code for each object. For example, two line items cannot both use the code "ABC."

### State

Set the line item **state** to **Active** or **Inactive**. We recommend that you set the state to **Inactive** until everything for the line item has been set up and verified.

### Ad type

Select one or more appropriate ad types for the line item. The ad type must match the creative types that you will associate with the line item and will also be used to improve forecasting accuracy.

### Priority

Set a priority for the line item in the **Priority** drop-down menu. Flexible priorities allow users to manage delivery across line items. The default priority for HLIs is 1.

## Budgeting & scheduling

### Add flight dates

Select the start date and end date for your line item.

### Daypart

Add any necessary settings to target users based on the day and time when they see impressions. For more information, see [Daypart Targeting](daypart-targeting.md).

### Daily pacing allocation

Select an option:

- **Evenly**: Unspent daily budget will be distributed evenly throughout the remainder of the flight.
- **ASAP** (default): Unspent daily budget will be spent as quickly as possible based on your line item settings to ensure the highest probability of delivering your budget in its entirety.

## Inventory and brand safety

From the **Inventory and Brand Safety Targeting** section, you can specify the type of inventory that you want to buy (supply source), target universal or custom content categories, specify whether to advertise on web or app inventory, create and/or apply blocklists or allowlists, define brand safety settings, and set up ads.txt targeting.

## Geography targeting for a line item

From the **Audience & Location Targeting** section, you must target users based on at least one geographic element such as country, region, city, metro code, or postal code. You can optionally set up other geographic inclusions or exclusions.

## Enable cross-device targeting and measurement for a Line Item

From the **Audience & Location Targeting** section, you can optionally enable cross-device targeting on a line item to apply frequency caps, conversion attribution, and audience targeting settings for individual users across multiple devices.

## Segment targeting on a Line Item

From the **Audience & Location Targeting** section, you can set up a line item to target segments from third-party data providers or segments you've created.

## Frequency and recency Caps

From the **Audience & Location Targeting** section, you can set the number of times (frequency) and how often (recency) creatives can be shown to a given user.

## Viewability and environment targeting for a Line Item

From the **Viewability & Environment Targeting** section, to narrow your ad campaign's reach to the most valuable inventory, you can set up viewability threshold, device type, system, and page property targeting settings.

## Related topics

- [Working with Line Items](working-with-line-items.md)
- [View Line Item Details](view-line-item-details.md)
- [Augmented Line Items (ALI)](augmented-line-items-ali.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Update Line Items](update-line-items.md)
- [Create a Guaranteed Delivery Line Item](create-a-guaranteed-delivery-line-item.md)
- [Using Multiple Campaigns with a Guaranteed Line Item](using-multiple-campaigns-with-a-guaranteed-line-item.md)
- [Guaranteed Delivery Pacing](guaranteed-delivery-pacing.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Object Hierarchy](object-hierarchy.md)
- [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md)
- [Buy-Side Targeting](buy-side-targeting.md)
