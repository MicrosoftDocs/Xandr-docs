---
title: Forecast Builder in Microsoft Monetize
description: Forecast Builder in Microsoft Monetize enables users to explore inventory and forecasting data directly within the Monetize platform.
ms.date: 07/25/2025
ms.author: shsrinivasan
---
# Forecast Builder in Microsoft Monetize

## Overview

Forecast Builder in Microsoft Monetize enables users to explore inventory and forecasting data directly within the Monetize platform. This feature integrates the forecast-inventory-multi service into the Monetize ad server, streamlining workflows and improving the overall user experience. 

With this integration, users can seamlessly transition from data insights to actions, without leaving the Microsoft Monetize platform. Forecast Builder supports inventory analysis at the network level, allowing publishers to gain a deeper understanding of their available inventory and make data-informed decisions to optimize yield. 

## Key highlights 

- Inventory forecasting and analysis are embedded in Microsoft Monetize, enabling quick responses to insights. 
- List and inspect detailed forecasting outcomes for selected inventory criteria. 
- Visualize capacity and impression forecasts through interactive graphs. 
- Identify contending line items: View a list of line items that compete for the same inventory based on selected targeting attributes. 
- A faster way to explore inventory availability, right within Microsoft Monetize, without having to create a line item.  
- Surfaces real-time capacity and active bookings to help avoid overselling.  
- Allows targeting and filter refinements for more accurate forecasts.  
- Supports earlier decision making in the planning process.  

## Types of inventory forecasting 

Inventory forecasting provides key metrics to help you evaluate available ad inventory. The following data points are available: 
- **Capacity:** The total inventory available for the selected targeting and date range. 
- **Availability:** The portion of inventory that is not booked and matches the line item's targeting criteria and flight dates. 
- **Contention:** The number of existing line items competing for the same inventory based on the specified targeting and time frame. 

## Navigate the forecast builder 

> [!NOTE] 
> This feature is limited and enabled only to a subset of customers, contact your Microsoft Advertising representative for more information.  
- To access the Forecast builder in Microsoft Monetize, navigate to the vertical navigation pane on the left and select Forecasting. 
-  The Forecast Builder screen opens which contains two primary sections: 
    - Forecast Overview 
    - Competing Line Items 

### Forecast Overview 

The Forecast Builder helps you analyze inventory availability and identify contention across line items. A chart visualizes the delivery goals and capacity for the selected line item. 
- To commit to an advertiser’s budget, publishers need to forecast how much inventory is available and understand if other line items are competing for the same inventory, this is known as inventory contention. The Forecasting pane displays: 
 - Available Impressions 
 - Total Capacity 
- The Availability and Capacity graph can be viewed across the following timeframes:  
    - Next 7 days 
    - Next 14 days 
    - Next 30 days 
    - This week (Today – Sat) 
    - This month 
    - This quarter 
    - This year 
    - Next week (Sun – Sat) 
    - Next month 
    - Next quarter 
    - Custom 
- Similar to GDALIs, you can set the inventory and environment targeting to define key line item attributes. To configure inventory and environment targeting, select Set Targeting and set the appropriate fields to target and select Apply to update the forecast based on your selection. To edit these fields, click the pencil icon next to it to open the targeting screen and edit the values accordingly.  
> [!NOTE] 
> Targeting selected here will be used for forecasting purposes only and will not affect line item delivery. 
- These fields include: 
    - **Ad Type:** You can select one or more appropriate ad types for the line item. The ad type must match the creative types that you will associate with the line item and will also be used to improve forecasting accuracy. 
    - **Inventory:** You can target or exclude the following inventory: 
        - **Universal Categories:** These are defined by Microsoft Advertising. When Microsoft Advertising reviews inventory, we apply these categories based on the inventory's content. For example, a car dealership placement group would be assigned to the "Autos & Vehicles" category. Sellers can apply universal categories when self-reviewing inventory as well. 
        - **Custom Categories:** These are defined by sellers. Sellers create these and apply them to slices of their inventory to package their inventory for specific buyers to target. Manage your member’s custom categories in the Network tab (for more information, see [Manage Custom Content Categories](manage-custom-content-categories.md)). 
        **NOTE:** When targeting more than one universal category, the categories have an OR relationship. For example, if you target the "News" and "Finance" categories, you will target inventory that is in either category. The inventory does not need to be in both categories. 
        - **Direct Inventory:** You can narrow your targeting to include or exclude specific managed publishers, placement groups (sites), or placements. Select Browse to search by name or ID of an object, or Text to paste a list of IDs. 
        **NOTE**: When targeting more than one custom category, the categories have an OR relationship. For example, if you target two custom categories, you will target inventory that is in either category. The inventory does not need to be in both categories. 
    - **Key Value:** You can select your own keys and their corresponding values to make full use of publisher data and help advertisers reach their intended audience. Microsoft Advertising allows you to create custom key/value sets that can be used in advertising campaigns to target specific types of customers. For more information, see [Key/Value Targeting](key-value-targeting.md). 
    - **Geography:** You can target users based on one or more geographic elements such as country, region, city, metro code, or postal code. You may optionally set up other geographic inclusions or exclusions. To set up geography targeting, navigate to the Geography field and select any applicable checkboxes for country-level targeting. 
    - **Daypart:** You can select any necessary settings to target users based on the day and time when they see impressions. For more information, see [Daypart Targeting](daypart-targeting.md). 
    - **Audience & Location Segments:** You can target segments from third-party data providers or segments you've created. To set up audience and location segment, select the My Segments tab in the Audience & Location Segment Targeting screen (for more information, see [Set Up Segment Targeting on a Line Item](set-up-segment-targeting-on-a-line-item.md)). 
    - **Ad Size:** You can select standard or custom ad sizes for your forecast. To add ad size values: 
        - Click in the Ad Size field, scroll or search for sizes, and select appropriate sizes (you can select more than one size at a time). You can also add more values to the list of Selected Sizes by clicking in the Ad Size field and selecting additional sizes. 
        - (Optional) To add custom ad sizes, click + Add Custom Size, enter appropriate values for Width and Height, and click + Add. 
    - **System:** You can target users based on their operating systems, browsers, language, device model, or carrier. For more information, see System Targeting. 
    - **Device Type:** You can narrow the device types you are targeting by checking any device type you do not want to target. GDALIs target the following device types by default: 
        - Desktops
        - Mobile 
        - Tablets 
        - CTV
    - **Inventory Type:** Select an inventory type from the Inventory Type drop-down: 
        - App & Web - Includes inventory types 
        - App Only - Includes applications installed on mobile tablets, phones, and Windows 8 devices. 
        - Web Only - Includes standard websites and those optimized for browsers on mobile Video Content devices.
    - **Player:** Select video player targeting, which includes:  
        - playback method 
        - ad pod position 
        - player width 
**NOTE:** This option is only available when the ad type is video.
- Forecast data updates automatically when you modify any targeting criteria that affects forecasting. To update the graph, select Advanced Filters at the top of the screen and adjust the following fields as appropriate and select Apply to refresh the chart with updated availability and capacity data. These fields include:
    - **Priority:** Set a priority for the line item in the Priority drop-down. Flexible priorities allow users to manage delivery across line items. To optimize yield, it's recommended that you consolidate GDALIs within a single priority tier below the reselling priority. The default priority depends on the delivery type: 
        - Impressions delivery types have a default priority of 14. 
        - Exclusive delivery types have a default priority of 19. 
    - **Frequency caps:** Enter a number for impressions per interval and select an appropriate interval in the drop-down. For more information, see Set a Frequency Cap. 
    - **Competitive exclusion:** Select an advertiser to prevent creatives from competing brands or offer categories from appearing on the same page. This ensures brand safety and category exclusivity during ad delivery. 
    **NOTE:** Brands that are excluded are defined in the advertiser’s profile. 
    - **Show 1 imp per page:** Enable this option to limit the number of impressions a single advertiser can serve per page in multi-tag auctions.  
    **NOTE:** When selected, the forecast assumes the line item will serve only one impression per page, which may reduce the projected availability. 
> [!NOTE]
> Priority must be set for forecast builder and is defaulted to 14. 

### Competing Line Items 

The Competing Line Items section shows other line items that are contending for the same inventory based on your selected targeting, priority, pacing, frequency capping, overlapping impressions, and flight dates. This section displays: 

- The number of competing line items 
- Details of each line item currently targeting the same inventory 
- To view more information, select a line item from the list. You’ll be redirected to the Line item screen for further analyzis or editing. 
- Competing line item fields include: 
    - **Line item Name:** The name of the contending Line item 
    - **ID:** The ID of the contending Line item 
    - **Advertiser:** The associated advertiser 
    - **Status:** The status of the Line item 
    - **Start Date:** The start date of the Line item 
    - **End Date:** The end date of the Line item 
    - **Delivery Type:**  Has the following two types: 
        - **Impressions:** this delivery type has an impression-based goal and typically has priorities that range from 11-17. 
        - **Exclusive:** this delivery type has a percentage-based (or "share-of-voice") goal and typically runs at higher priorities that range from 18-20. 
    - **Priority:** The priority associated with the line item. 
    - **Revenue Type:** The way the advertiser has agreed to pay you (CPM, Viewable CPM, or Fixed Fee). 
    - **Revenue:** The revenue an advertiser has allocated for you to spend in impressions or percentage. 
    - **Overlapping Impressions:** The number of contending impressions. 

## History 

The History feature allows publishers to review and manage previous forecast results and track forecast history over time. Each forecast run by a user is saved automatically and stored for 30 days. The results are stored in the user's local storage and remain there until they are manually cleared. 
> [!NOTE] 
> Forecast results are temporarily saved. 
- Users can:  
    - View and delete previous forecast results. 
    - Re-run a forecast as-is from the results table, if the date range is still in the future. 
        - If the start and end dates are in the future, the forecast is re-run using the original start and end dates without modification. 
        - If the start date is in the past and end date is in the future, the forecast is re-run from the current date (today) to the originally selected end date. 
        - If both the start and end dates are in the past, the forecast is re-run for a new range starting from today and ending 7 days later. 
- To view the forecast history of the past performances: 
    - Select the History icon in the top-right corner of the screen. 
    - A history pane will appear, showing a list of saved forecasts. 
    - You can hover over the three dots that appear next to the timestamp to view the dropdown menu and choose one of the following options: 
        - **View targeting:** Displays the targeting configuration used for a particular forecast. 
        - **Use selection builder:** Reopens Forecast Builder with the saved filters and advanced targeting options applied. This allows you to view and analyze the graph based on the previous setup. 
        - **Delete:** Removes the forecast entry from the history list. 



## Related topics
- [Set Up Segment Targeting on a Line Item](set-up-segment-targeting-on-a-line-item.md) 
- [Key/Value Targeting](key-value-targeting.md)
- [Daypart Targeting](daypart-targeting.md)

 