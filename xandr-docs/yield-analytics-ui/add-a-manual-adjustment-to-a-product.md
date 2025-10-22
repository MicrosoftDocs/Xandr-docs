---
title: Add a Manual Adjustment to a Product
description: In this article, follow our step-by-step instructions to add a manual adjustment to a specific product.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Add a manual adjustment to a product

Add a manual adjustment to a specific product to make a temporary override to it (e.g., if a sale is driving traffic to a particular site).

1. Check the impression capacity for the product for which you want to add a manual adjustment.  

    Or, in the **Capacity Tasks** panel, select **Adjust Manual Forecast**, select the product in the **Products** panel, and then in the Product detail preview select **View** > **Forecast Visibility**.

1. On the Forecast Visibility page, below the Capacity Forecast, in the **Adjustments Influencing Forecast** section, select the **Add/Edit** button. The page is redisplayed with the **Edit Manual Adjustment** section at the top.

1. In the **Edit Manual Adjustment** section, select **Add New**. A new adjustment row appears.

1. In the **Name** column, enter a name for the adjustment.

1. In the **Type** column, select the type of adjustment:
    - Absolute – Changes the forecast by adding or subtracting the value you enter.
    - Relative – Changes the forecast based on the percentage that you enter.
    - Replace – Changes the actual forecast value (number of impressions) with the value you enter.
    - Ceiling – Creates an impressions cap over a period of time, above and beyond spike detection and mitigation.

1. In the **Start** and **End** columns, enter the start and end dates for the adjustment as needed.

1. In the **Daily Amount** column, enter the number of daily impressions the product should receive. If you selected **Absolute** or **Relative** for the adjustment type, you can enter a negative number using the minus sign (-).

1. In the **Status** column, specify the adjustment's status:
    - Active – The change takes effect on the dates you selected.
    - Inactive – The change doesn't take effect until you edit the adjustment to make it active.
  
1. (Optional) Select **Preview Changes** to see the adjustment applied in the Capacity Forecast area, as the Modified Manual Adjusted Forecast (Unsaved Changes) line. The original forecast is still displayed in blue. Child products affected by the adjustment appear in the **Affected Rate Card Products** list below the forecast.

1. Make any additional changes as needed to the adjustment, and then select **Save**. The manual adjustment line turns orange, and the original forecast line stays blue.

The changes to the forecast are only reflected in the Forecast Management area. They are not reflected in other parts of Yield Analytics or in the actual placement of ads until the system processes data overnight.

## Related topics

- [About Forecasts and Adjustments](about-forecasts-and-adjustments.md)
- [View the Forecast for Your Products](view-your-products-forecast.md)
- [Anatomy of the Capacity Dashboard Page](anatomy-of-the-capacity-dashboard-page.md)
- [Anatomy of the Forecast Visibility Page](forecast-visibility-page-anatomy.md)
- [Check Impression Capacity for a Product Group](check-impression-capacity-for-a-product-group.md)
- [Edit a Seasonal Adjustment for a Seasonal Product](edit-a-seasonal-adjustment-for-a-seasonal-product.md)
