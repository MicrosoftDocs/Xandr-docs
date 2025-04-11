---
title: Insertion Order Auto Allocation 
description: The Insertion Order Auto Allocation feature enables customers to set a budget at the Insertion order (IO) level and distribute it across Augmented line items evenly.
ms.date: 04/12/2025
ms.author: shsrinivasan
---

# Insertion Order Auto Allocation 

> [!NOTE]
> This feature is currently in Alpha/Beta and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative. 

The Insertion Order Auto Allocation feature enables customers to set a budget at the Insertion order (IO) level and distribute it across Augmented line items evenly. The system dynamically optimizes budget allocations based on delivery objectives by continuously monitoring real-time spending and retains the ability to manually override allocations whenever necessary, ensuring greater control over budget distribution. 

The functionality is designed to ensure that budgetary targets are consistently met while minimizing the need for manual intervention by continuously monitoring the delivery of each line item and strategically reallocating budgets from underperforming line items to those successfully meeting delivery objectives. The system evaluates the delivery rate of each line item, up to six times per day, at intervals of four hours to dynamically redistribute the budget to optimize overall delivery performance.

> [!NOTE]
> The system dynamically reallocates up to 20% of a given Line item's daily budget every 24 hours to mitigate abrupt fluctuations, ensuring operational continuity. 

The allocation mechanism supports two key modes: 
-  You can adjust Augmented Line item budgets based on delivery ensuring higher investment in top-performing Line items thus reducing the manual of shifting budgets from one Augmented Line item to another. 
- You can prioritize budget distribution to maximize spend across all Augmented Line items, reducing under delivery.

## Key features

- **Optimized budget allocation:** The system reallocates budgets from underperforming to high-performing Line items. 
- **Improved delivery rates:** Ensures the IO budget is fully utilized, preventing premature halts in ad delivery. 
- **Reduced manual effort:** Eliminates the need for customers to frequently adjust Augmented Line item budgets. 
- **Increased adoption:** Simplifies budget management, making the platform more efficient for strategic customers. 
- **Minimized errors:** Prevents budget discrepancies between IO and Line items, reducing the risk of underspending. 

## Access the Insertion Order Auto Allocation feature 

Customers can enable auto-allocation at the IO level within the Microsoft Invest DSP UI. Once activated, the system dynamically distributes the IO budget across active Augmented Line items. To access the Insertion Order Auto Allocation feature: 

- Step 1. **[Navigate to the Insertion orders screen](working-with-insertion-orders.md)**
If you do not have an existing Insertion Order (IO), you can create one by navigating to the Create New Insertion Order screen. For more information, see [Create an Insertion order](create-an-insertion-order.md).
- Step 2. **Set up pacing**
The pacing determines how quickly budget is spent over the lifetime of the insertion order. In the Pacing section, you can configure your Insertion Order (IO) budget and choose one of the following options: 
    - **Base daily allocation on the average of the remaining billing period budget:** This option automatically distributes the remaining budget evenly across the remaining days in the billing period. 
    - **Use Daily Budget:** This option allows you to set a custom daily budget, giving you full control over pacing. 
> [!NOTE]
> If you select **Set pacing on the Line Item**, budget allocation will not be available.

- Once pacing is configured, you can enable or disable the Auto Allocation feature at the Insertion Order (IO) level through the user interface. To activate this feature, select the **Automatically allocate this Insertion Order’s budget across its augmented Line items** checkbox. This allows the system to dynamically optimize and distribute budget allocations across Line items based on delivery metrics. 

> [!NOTE]
> If the Insertion Order (IO) Auto Allocation is enabled, Microsoft Invest overrides the pacing, budget, sub-flight, and daypart settings of augmented line items, adjusting allocations dynamically based on delivery performance. If the feature is disabled, the system reverts to the original budget values configured by the advertiser, thus ensuring that budget distribution is optimized in real-time while maintaining transparency and control. 

- Once the feature is enabled, Microsoft Invest will automatically distribute the Insertion Order (IO) budget evenly across all child line items, overriding any budget and pacing settings configured at the Line item level. 
- Select **Save** to save the Insertion order details. 

> [!NOTE]
> Users are still required to specify the initial Line item budgets when creating a line item in the **Create a Line item** screen. However, these values will be overridden by the system. A flag within the line item will indicate that its settings are being overridden.

> [!IMPORTANT]
> Setting any Line item to ASAP under the **Underspend Catch-Up** section on the Line Item screen may disrupt budget allocation throughout the day. To maintain stability, it is recommended to use Evenly pacing. 


## Related topics

- [Working with Insertion orders](working-with-insertion-orders.md)
- [Create an Insertion order](create-an-insertion-order.md)
