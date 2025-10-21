---
title: Forecast-Shaped Pacing 
description: Explore Forecast-Shaped Pacing which governs daily pacing schedules for all impression-based guaranteed line items on the platform.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---
# Forecast-Shaped Pacing (FSP)

Microsoft Advertising applies pacing throughout the lifetime of a line item to ensure that each line item meets its delivery goal in full and at a steady rate. Forecast-Shaped Pacing (FSP) enhances pacing logic for impression-based guaranteed line items by aligning delivery rates with forecasted inventory capacity for each line item. 

FSP provides high precision in delivery and enables publishers to increase revenue from RTB through [Open Dynamic Allocation and Flexible Priorities](open-dynamic-allocation-and-flexible-priorities.md).

> [!IMPORTANT]
> At this time, FSP hourly budget distribution is not used during the final day of the Line item’s flight. More aggressive pacing is in place for the last day to ensure full delivery. FSP logic that accounts for last day delivery is currently in development. See [Daily Pacing](daily-pacing.md) for more information on last day pacing. 

## Pacing methodology 

Microsoft Monetize offers two forecast shaped pacing methodologies: 

- **Hourly budget distribution**
    - Inventory capacity typically fluctuates throughout the day. A basic pacing system that distributes delivery evenly across all hours may struggle to meet hourly goals during low-inventory periods (e.g., early morning), leading to under-delivery. To compensate, the system may accelerate pacing later in the day, potentially resulting in overspending and early completion of the daily budget. 
    - Forecast-Shaped Pacing (FSP) addresses this by setting hourly delivery goals based on a high-fidelity inventory forecast specific to each line item. For example, if less inventory is expected at 2:00 AM than at 2:00 PM, FSP will assign a lower delivery target for the early morning and a higher one for the afternoon. This approach ensures that delivery aligns with actual supply patterns throughout the day. 
    - FSP hourly budget distribution is applied to all impression-based Guaranteed Delivery line items and cannot be disabled. It does not apply to line items with an Exclusive delivery type. 

- **Daily budget distribution** 
    - FSP also incorporates forecasted inventory patterns across multiple days. Rather than distributing the lifetime budget of a guaranteed line item evenly across each day of the flight, FSP adjusts daily budget allocations based on expected inventory capacity for each day of the week. 
    - For instance, if higher impression volume is forecasted for weekends, FSP will allocate a greater portion of the budget to Saturday and Sunday. Conversely, if weekdays are expected to have lower inventory, the system will reduce spend accordingly. This feature helps improve delivery consistency and yield, particularly for line items that end on days with limited inventory. 
    - This feature is on by default for impression-based Guaranteed Delivery line items created through the Monetize UI. To enable this feature, toggle the Day of Week option in the Budgeting & Scheduling section of the Create or Edit Line item screen. 

 
## Key highlights 

- **Improved Yield via RTB:** FSP increases a publisher's yield through Open Dynamic Allocation. By pacing according to a forecasted supply curve, guarantees don't have to "try as hard" to deliver impressions when inventory is scarce (such as late night or early morning, or weekends). In other words, the predicted CPM (pCPM) of the guaranteed line item can be significantly lower during hours or days when there is less supply. This allows the publisher to take advantage of high CPMs from RTB throughout all hours of the day and days of the week. 
- **Improved delivery:** FSP not only optimizes how often guaranteed lines items deliver in full, but also how frequently they deliver through the last hour of the day. Analysis has shown that with FSP, 90 – 95% of line items deliver through the last hour of the day, a 15-20% improvement over pre-FSP pacing mechanics. This improvement is the result of fewer adjustments having to be made throughout the day to meet delivery goals than were historically required. 

> [!NOTE]
> Daily budget distribution is re-evaluated each day based on forecasted inventory during the remainder of the flight. For flights less than seven days, or once a flight has seven days remaining or less, the distribution curve will no longer be updated and will use the most recent day-of-week distribution curve. Flights lasting two days or fewer won’t be assigned a day-of-week distribution curve. 

<!--
# Forecast-shaped pacing

Microsoft Advertising applies pacing throughout the lifetime of a line item to ensure that each line item meets its delivery goal in full and at a steady rate. Forecast-Shaped Pacing (FSP) – which governs daily pacing schedules for all impression-based guaranteed line items on the platform – takes standard pacing methods a step further by ensuring
line items deliver at a rate that reflects the forecasted inventory available for the line item.

FSP provides a great amount of precision in delivery and allows publishers to realize increased revenue from RTB through [Open Dynamic Allocation and Flexible Priorities](open-dynamic-allocation-and-flexible-priorities.md).

## How it works

Availability of inventory typically changes throughout the day. One challenge of a naïve pacing system that tries to pace a line item evenly across the hours of a day is that it becomes difficult to fulfill hourly delivery goals during the less-trafficked, lower inventory times of day. This lack of inventory could prevent the line item from meeting its pacing goals during those low-inventory times and therefore make it seem as if it's underdelivering. To account for this, pacing speeds up. As more inventory becomes available later in the day, this increased pace will start to overspend. Pacing again will adjust. Oftentimes this continuing need to adjust leads to spend completion before the day is over.

Forecast-Shaped Pacing (FSP) solves this problem by setting hourly delivery goals for a guaranteed delivery line item according to an inventory forecast specific to that line item. For example, there may be less inventory available to that line item in the early morning hours (say, 2:00 AM) than in the afternoon. FSP can predict this variance and
will therefore set a much lower delivery goal for the line item at 2 AM than at 2 PM. In the afternoon, FSP sets delivery targets to be higher because more supply is expected to be available than in the early morning. And if – as is often the case – inventory starts to drop again during the end of the day, the FSP-governed line item will have less
delivery scheduled accordingly.

To summarize: FSP takes into account the variability of inventory throughout the day, setting hourly delivery goals that map to high-fidelity, line-item specific forecasts powered by the [Yield Forecasting Engine](../yield-analytics-ui/yield-analytics-overview.md).

> [!NOTE]
> Microsoft Advertising uses FSP for all impression-based Guaranteed Delivery line items. It does not apply to line items with an **Exclusive** delivery type.

What FSP means to publishers

FSP has proven overall to positively impact both revenue from RTB as well as delivery accuracy.

### Increased yield from RTB

FSP increases a publisher's yield through Open Dynamic Allocation. By pacing according to a forecasted supply curve, guarantees don't have to "try as hard" to deliver impressions when inventory is scarce (such as late night or early morning). In other words, the predicted CPM (pCPM) of the guaranteed line item can be significantly lower during these hours when there is less supply. This allows the publisher to take advantage of high CPMs from RTB throughout all hours of the day.

> [!IMPORTANT]
> **FSP Analysis**
>
> An early analysis of production data showed that this relaxed pressure during low-supply hours resulted in guaranteed line items using FSP were able to bid a 25-35% lower pCPM on average than without FSP. A lower pCPM means the opportunity cost of serving guaranteed is lower and publishers can capture more of their most valuable RTB demand, which, in this analysis, translated to 15-20% more RTB revenue on average.

### Delivery throughout the day

FSP not only optimizes how often guaranteed lines items deliver in full, but also how frequently they deliver through the last hour of the day. Analysis has shown that with FSP, 90 – 95% of line items deliver through the last hour of the day, a 15-20% improvement over pre-FSP pacing mechanics. This improvement is the result of fewer adjustments having to be made throughout the day to meet delivery goals than were historically required.

## Restrictions

At this time, FSP is not used during the final day in the lifetime of the line item. More aggressive pacing is in place for the last day to ensure full delivery. FSP logic that accounts for last day delivery is currently in development. See [Daily Pacing](daily-pacing.md) for more ##information on last day pacing.
-->

### Related topics

- [Guaranteed Delivery](guaranteed-delivery.md)
- [Create a Guaranteed Delivery Line Item](create-a-guaranteed-delivery-line-item.md)
- [Daily Pacing](daily-pacing.md)
