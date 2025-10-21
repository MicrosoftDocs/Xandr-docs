---
title: Understanding Performance Goals
description: In this article, find information about performance goals and how to adjust performance goals to balance campaign delivery and performance. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Understanding performance goals

> [!IMPORTANT]
> Performance goals are not available for use with Guaranteed Line Items.

Performance goals are a line item feature that empower network clients to manage the trade-off between delivery and performance so that their campaigns are as effective as possible. As both delivery and performance are used to determine renewals and budget increases, having more nuanced control over each can help secure more renewals and more revenue.

Performance goals provide a user-friendly way to do the following:

- Track actual performance against your advertiser's stated goals
- Leverage optimization to stop buying inventory that does not meet your advertiser's goals

This page explains how performance goals work and outlines some basics about when and how to use performance goals.

> [!TIP]
> **Looking for detailed performance goals or line item setup instructions?** For a how-to that explains performance goal setup, see [Add a Performance Goal to a Line Item](add-a-performance-goal-to-a-line-item.md).

## Performance goals process

Performance goals are set on the line item and work on campaigns in both learn & optimized states. Here's a summary of the process:

1. A standard campaign in the learn phase will bid on all inventory initially as the Microsoft Advertising platform collects success events and the data needed to create a valuation.
1. During learn, the Microsoft Advertising platform will continuously review the campaign's performance and exclude low-performing inventory to help the campaign optimize faster.
1. Once the campaign moves into the optimization phase, performance goals on the line item perform a bid/no bid check using the data collected in the learn phase to determine a valuation.
1. Based on the results of the bid/no bid check, campaigns only bid on inventory that is most likely to meet the performance goals as set on the line item.

> [!NOTE]
> While the Microsoft Advertising platform does exclude low-performing inventory during the learn phase, the performance goal "bid/no bid" check will not take effect until after a campaign has moved beyond the learn stage of optimization, which has a default of three success events.

## Performance goals applications

Performance goals are most applicable in situations when you are being paid by your advertiser on a flat CPM but the advertiser is using another metric to track goals.

For example, let's say an advertiser is paying a network $1,000 for 1M impressions, and has also stated they would like to pay around $5 per signup, but you think this may be a bit aggressive and that $7.50 might be a more realistic target. In this case, you can set your line item budget according to the $1,000/1M impressions payment info from the advertiser, and set a CPA performance goal that tracks the advertiser's desire to pay $5 per signup. You can also set a bid/no bid decisioning limit of $7.50 using a separate field, to help ensure campaigns do not bid on inventory that does not meet this limit.

In the image below, the advertiser goal is set at $5 CPA under **Post-click** in the **Track performance against client goal of $_** field. The bid/no bid decision is set at $7.50 under **Post-click** using the **Do not bid if post-click eCPA is above $_** checkbox.

:::image type="content" source="media/PG-scenario-a.png" alt-text="Screenshot that shows the post-click performance goals fields.":::

This scenario demonstrates how easily performance goals allow you to keep track of revenue metrics while also tracking how campaigns are translating revenue into performance and delivery.

> [!NOTE]
> To limit your bids, you must set a bid/no bid decisioning limit using the **Do not bid if...** checkbox.

## Using performance goals to fine-tune performance and delivery

After your campaigns have been active for a little while, you can edit your performance goal to fine-tune the balance between performance and delivery. The objective is to help ensure that your campaigns are functioning as successfully as possible according to your advertiser's goals. If it seems that the performance goal is hindering delivery, you can increase the goal to a number that seems more realistic. If you are pacing well but believe the advertiser could spend less per conversion without hurting the delivery trend, you can reduce the goal to reign in spending.

### Improve delivery

To go back to the example [above](#performance-goals-applications), let's say you started serving the campaign with the CPA performance goal of $5 per sign-up, but the campaign is not delivering well. You might consider bumping up the per sign-up average - that is, the bid/no bid check - higher to $10 to help ensure that the campaign is delivering.

:::image type="content" source="media/trade-performance-for-delivery.png" alt-text="Screenshot that shows how to update the performance goals when the campaign is not delivering well.":::

### Improve performance

Now let's say you come back to the same campaign to find that with the $10 bid limit, the campaign is delivering easily, and even outpacing the advertiser's stated expectations. In this case, you can further adjust the performance goals settings to improve campaign performance while maintaining strong campaign delivery. Knowing that a $7.50 bid limit compromises delivery but a $10 bid limit is too generous, you try a bid limit to $8 to better balance performance with delivery. You check back in a few days, and find that the campaign is delivering at a healthy pace and the advertiser is not spending too much per conversion: congratulations - you've successfully balanced performance and delivery!

:::image type="content" source="media/trade-delivery-for-performance.png" alt-text="Screenshot that shows how to update the performance goals to improve campaign performance while maintaining campaign delivery.":::

These three examples - with the $7.50 bid limit, the $10 bid limit, and the $8 bid limit - are shown together in the table below:

| Attempt | Adv Goal | Bid Limit | Performance | Delivery | Results |
|---|---|---|---|---|---|
| 1 | 5.00 CPA | $7.50 eCPA | Good | Poor | Campaign performance is good, but campaign delivery should be better. |
| 2 | 5.00 CPA | $10 eCPA | Poor | Excellent | Campaign is delivering, but advertiser is spending too much. |
| 3 | 5.00 CPA | $8 eCPA | Good | Good | Campaign spending meets advertiser expectations, and delivery is also strong. |

## Related topics

- [Add a Performance Goal to a Line Item](add-a-performance-goal-to-a-line-item.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md)
