---
title: Microsoft Monetize - Set Up Line Item Optimization
description: Explore optimizing line items, set goals, priorities, and link with conversion pixels for effective performance control.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up line item optimization

You can enable or disable Microsoft Advertising optimization for a line item. If you enable Microsoft Advertising optimization,you must first set a performance goal and goal priority, then associate
the line item with conversion pixels for those goals.

The **Optimization** section provides several settings related to optimization, goals, goal priority, and conversion tracking and viewability (if enabled). For more information, see the [Optimization Guide ALI](optimization-guide-ali.md).

1. Turn on optimization.

   If the **Optimization Method** toggle has been turned on, the Microsoft Advertising optimization engine will consider your goal value and goal type when bidding on inventory.

   If the **Optimization Method** toggle is turned off, automatic optimization is disabled, including the algorithms for bid valuation, inventory discovery, and allocation. When optimization is off, adaptive pacing will still shade bids in response to delivery.

1. Set a goal type.

   This option is visible only if optimization is turned on.

   Goal types can be used in conjunction with revenue types if an advertiser wants to track and report against a goal that is different from the payment types that they have chosen (e.g., an advertiser wants to pay CPM but would like you to track against a $50 CPA goal).

    You can optimize to:

    - **Viewable CPM**

      Select this option if your advertiser wants to track and report against a goal based on viewable impressions. Set the **Viewable CPM** field to the goal your advertiser has given you. This option is not available when your revenue type is **CPC**.

    - **CPCV**

      Select this option if your advertiser wants to track and report against a goal based on video completes. A video complete requires  the video ad to play for its full duration. Set the **CPCV** field to the goal your advertiser has given you. This option is only available if you selected **Video** as the **Ad Type** in **Basic Settings**. When your revenue type is also **CPCV**, optimization will inherit the goal value from your revenue value.

    - **VCR**

      Select this option if your advertiser wants to optimize to a video completion rate percentage. Enter the desired percentage in the text field. This option is only available if you selected **Video** as the **Ad Type** in **Basic Settings**.

      > [!NOTE]
      > VCR optimization is not available if you selected **Managed** as the **Supply Strategy** for the line item.

    - **CTR**

      Select this type if your advertiser wants to optimize to a clickthrough rate percentage. Enter the desired percentage in the text field.

    - **CPC**

      Select this type if your advertiser wants to track and report against a cost per click goal. Enter the CPC amount in the text field. If your revenue type is **CPC**, optimization will inherit the goal value from your revenue value.

    - **CPA**

      Select this type if your advertiser wants to achieve a cost per action goal. When choosing this goal type, you have the option to optimize to only post-click conversions or to both post-click and post-view conversions.

    If your advertiser wants to optimize to both post-click and post-view conversions:

   1. Select **CPA** and enter the CPA amount in the text field.

   1. If this is a retargeting line item (a line item that targets users who have already shown interest in the advertiser), select **Retargeting** and ensure that the line item targets at least one retargeting segment (a segment not in the Data Marketplace).

   1. If this is a prospecting line item (a line item that targets a wide spread of users who may become interested in the dadvertiser's brand), select **Prospecting**.

      > [!NOTE]
      > CPA prospecting optimization is not recommended if you're optimizing to a rare event (an event with infrequent conversions). In that case, we recommend that you optimize to a higher-level conversion event that has more data.

   1. Attach a conversion pixel.

    If your advertiser wants to optimize to only post-click conversions:

      1. Select **CPA** and enter a CPA amount in the text field.
      1. Select **Post-click Only**.
      1. Enter a CPC amount in the text field. (If your Revenue Type is **CPC**, the CPC goal is inherited automatically).
      1. Attach a conversion pixel.

    > [!NOTE]
    > A CPC goal is required for [inventory discovery](discovery.md) and [bid valuation](valuation.md).

1. Set the goal priority.

    Goal priority is used to indicate which goal should be given greater emphasis when bidding.

    - **Delivery** will prioritize impression volume by multiplying bids up to 2x in response to delivery. When you optimize to clicks, it will also allow line items to discover inventory with historical CPCs up to 10x the goal. This might cause margin and performance to be deprioritized, possibly resulting in a negative margin.
    - **Performance** will prioritize your advertiser goal over impression volume and profit.
    - **Margin** reduces optimized bids by your desired profit margin. Additional margin can be earned through adaptive pacing if your revenue type is **CPM**, **Dynamic CPM**, **Viewable CPM**, **CPC**, or **CPCV**.

      > [!NOTE]
      > The **Margin** option will not display if you selected **Cost Plus** from the **Revenue Type** drop-down in the **Basic Setup** section.

1. Add conversion tracking.

    Click **Edit** to associate conversion tracking pixels to this line item. These pixels can be used to track the line item’s performance.

   > [!NOTE]
   > If you have selected CPA optimization, the targeted conversion pixel must be one of the conversion tracking pixels selected here.

1. If you select a conversion pixel, an **Enable IP Attribution** toggle is displayed. When enabled, if the IP address sees an impression, and the same IP address sees a conversion pixel, a conversion is activated.

   > [!NOTE]
   > The **IP Attribution** feature is in **Alpha**. It is subject to change without notice and is only available to select clients. Please consult your Account Manager if you'd like to be added to the alpha test.

## Related topic

[Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
