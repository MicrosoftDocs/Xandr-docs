---
title: Optimization levers
description: Explore optimizing legacy line items, override ALI bids with Optimization levers to enhance performance. Reduce character count.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Optimization levers

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

Certain users have the ability to override their learn bids through the use of levers in Optimization.

## Getting to optimization levers

In the **Buying Strategies** section, click **Edit** under **OTHER OPTIONS**.

> [!NOTE]
> The **OTHER OPTIONS** section (which includes the **Edit** option) is only visible if you have selected a buying strategy against which optimization levers can be applied:
>
> - When you set a **Performance Goal** on a Line Item. For more information, see [Add a Performance Goal to a Line Item](add-a-performance-goal-to-a-line-item.md).
> - When you optimize to a **Predicted CPC** or **CPA** goal.

## Defer to Line Item revenue with a \_ % margin

The more quickly a node is optimized, the less budget is spent trying to determine the best bid price. However, when a campaign is established, the action used for optimization is often the action that occurs with the least frequency. For example, if you are attempting to optimize acampaign selling bikes by measuring the number of bikes sold (CPA), and
each acquisition is a rare event, it will take you a very long time to optimize your bid. However, if you measure a more-frequently occurring event (e.g., measure when the user clicks on a page to provide an email address to receive more information), you can obtain data more quickly, thereby reaching optimization sooner.

Check the **Defer to Line Item revenue with a \_ % margin** button to temporarily change the level at which you learn (line item vs. campaign) while maintaining a specified profit margin percentage.

The results of a campaign can be thought of as a funnel, with the top level having the most frequent actions and each subsequent level having fewer actions. In the following example, the campaign has numerous conversion pixels, and we are going to alter the situation so that, instead of optimizing based on success events for **conversion pixel
\#4**, we are going to optimize based on **conversion pixel \#2**. Your campaign may have more or fewer conversion pixels, and you may choose to optimize to a different level.

- At the top level of the campaign, the user sees a creative (in this example, the impression is for a store selling bicycles). This is an impression.
- The user can click on the creative to see more information about the different types of bicycles for sale at this store. This is a click and it fires **conversion pixel \#1**.
- The user can click on a specific bike to learn more about it. This is another click and it fires **conversion pixel \#2** (in this example, this must be set up as a CPA goal in order to optimize to the line item).
- The user can then click on a link to get an email with additional information about this bike. This is a type of success event and it fires **conversion pixel** **\#3**.
- The user can then purchase a bike, which is an acquisition. This is the line item level, which fires **conversion pixel \#4**.

  Your campaign is set for a CPA goal of $4 for **conversion \#2**. When you decide to use the **Defer to Line Item**... setting, you must establish a line item CPA goal of $20
  for **conversion pixel \#4**.

1. The system achieves 33 success events (pixel fires) against **conversion pixel \#2**. At that point, we are optimized to this level. We designate a bid value based on that CPA goal (1000 \* $4 \* pixel \#2 conversion rate). We have reached an optimization level, but with less accurate data, so while the system can now  determine our bid value with greater accuracy, it is not accurate enough.
1. At the same time, the system continues to receive and count success events against **conversion pixel \#4** (just at a slower rate, as more users click for info as opposed to buying a bike). Even after **conversion pixel \#2** is optimized, this count continues
1. Once **conversion pixel \#4** has fired 33 times, the campaign is optimized to **conversion pixel \#4**, which has the most accurate data. The system changes the bid value to the line item goal (1000 \* $20 \* pixel \#4 conversion rate), which will result in the most accurate bid value.

After completing these calculations, the system accepts the margin percentage value that you entered (in the space before the % symbol) and adjusts the bid value to 
ensure that the margin amount is retained as profit by the network.

## Learn override

These options allow you to override the learn bid amounts that the system has come up with via standard optimization procedures. These options are viable if you wish to change your learn bid to win more impressions, or if you have information regarding this campaign that the optimization engine does not possess (e.g., a similar offer was executed
on a different system, and the data from that campaign indicates a different bid price). There are three override modes in the drop-down list:

> [!NOTE]
> Each of the following options requires you to set the **Override up to** amount. This is the number of impressions that you want to win per venue using these settings. After this threshold has been exceeded, the settings will revert to the standard optimization engine learn bid (i.e., any Learn Override settings are cancelled). It is important to
> set this accurately so that you do not collect so much data at the modified learn rate that you skew the results (i.e., the smaller your anticipated statistical sample, the lower this threshold should be set). The default is **40,000**.

- **Average RPM Bid** - Select this option to use the average winning bid amount as your bid in each venue. This option is best used when you have very little knowledge of the range of bids for this inventory, as it allows you to start with a bid that is appropriate for this venue. If you wish to further adjust your learn bids, you can use the **Multiply bid** field to modify the learn bid amount by a factor ranging from **0.5** (one-half of the current bid) to **5** (five times the current bid), thus altering the cost and number of impressions won.

  :::image type="content" source="media/learn-override-avg-rpm.png" alt-text= "The diagram illustrates how you override the learn bid amounts.":::

- **Base CPM Bid** - You can specify the CPM bid amount and use that amount for all learn bids in all venues. If you select this option, the **Bid a Base $** field appears, allowing you to enter the desired CPM amount. This option is best used when you have information which indicates a bid price different than that suggested by the standard optimization engine.

  :::image type="content" source="media/learn-override-base-rpm.png" alt-text= "Diagram that illustrates base CPM bid amount.":::

- **Bid Multiplier** - You can multiply the optimization-determined learn bids for all venues by a factor between **0.5** (one-half of the learn bid) to **5** (five times the learn bid). If you select this option, the **Bid Multiplier** field appears, where you can choose the multiplication factor from the drop-down list.

  :::image type="content" source="media/learn-override-bid-multiplier.png" alt-text= "Diagram that illustrates bid multiplier fields.":::

  > [!WARNING]
  > The more data you acquire, the greater the range of learn bid amounts. Therefore, you may not wish to use this setting when you have a lot of data, as you may not know the entire range of learn bid amounts that you are multiplying.
  > For example, if you have one venue using a learn bid of `$.30`, and another venue using a bid of `$2.50`, and you select a multiplier of `3.0`, the first venue will bid `$.90`(which may be acceptable), and the second venue will bid `$7.50` (which may be too high). Therefore, the more data you have accumulated, the more likely it is that applying the Bid Multiplier could result in extremely high (or low) learn bids. Upon reaching this point, you should use either the **Venue Average bid** or the **Base CPM bid** option to adjust your learn bid.

There are three settings in the Buy Third Party Inventory section which can limit your bid amount, regardless of which learn override control you employ:

- **Bid at most $ \_ CPM in Learn Phase**
- **Bid CPM: max $ \_ CPM in Optimized Phase**
- **Bid CPM: min $ \_ CPM in Optimized Phase**

If you apply these settings, you establish hard limits for those bids. Therefore, if you have selected one or more of these options, even if you apply the **Bid Multiplier** in a way that generates an extremely high bid (e.g., a bid of **$35** for inventory normally costing **$1**), and your maximum bid is set to **$3**, your bid will be reduced to **$3**.

## Segment price and modifier

You can apply a **Segment Modifier** or a **Segment Price** to update the bid determined by the optimization engine based on additional information that optimization does not have. This is often done based on in-house client calculations.

- Segment modifiers alter the optimization-determined bid price by a specific multiplier. Therefore, if you have a modifier of **1300**, and the optimization engine determines a bid of **$1.00**, the actual bid in the auction will be $1.00 \* (1300/1000) = **$1.30**.
- Segment prices override the bid price determined by the optimization engine. Therefore, no matter what the optimization engine bid determines as the appropriate bid price, if the segment price is **$0.75**, the actual bid in the auction will be **$0.75**.

For information on uploading modifiers and associating them to a campaign, see [Segment Modifier](segment-modifier.md).

> [!NOTE]
> Do not set a segment price and use the **Learn Override** setting **Base CPM Bid** at the same time. Since these both set an exact bid price, this can have unintended consequences. For the same reason, you should not set both a segment modifier and a segment price at the same time.

## Phase thresholds

The **Phase Thresholds** slider allows you to choose how many successful learn events are required to move a node from the learn phase to the optimized phase. You can set the value by moving the pointer as needed; the minimum number of events is **1**, while the maximum number is **15**.

For more information about the learn and optimized phases, see [What is an Optimization Node?](what-is-an-optimization-node.md).

## Restore defaults

Select this option on the dialog to erase any alterations that have been made to these levers and return them to a default or neutral status.

## Cadence modifier

> [!NOTE]
> This setting is not in the **Optimization Levers** dialog window. It appears on the screen below the **OTHER OPTIONS** heading.

This setting determines if the cadence modifier is applied to the advertiser as a whole or to each creative. Based on the **Frequency** (the number of times the user has seen a specific creative or anycreative from one advertiser over a given period) and **Recency** (how recently the user has seen a specific creative or any creative from one advertiser) values, the system will adjust the bid value in an attempt to win more or fewer impressions. You can set this to **Advertiser** or **Creative** to determine how the cadence is measured.

If an advertiser has a limited number of creatives and they have a similar appearance, you should probably set this value to **Advertiser**. If an advertiser's creatives are highly differentiated from each other, you can set this to **Creative**.

When you are set to **Bid a Base CPM**, you can limit the upper and lower limits of the bid by completing the **Pay CPM: Max $** and **Min $** settings. These values serve as absolute limits; bids outside of this range are not used.

> [!IMPORTANT]
> The default setting is **Advertiser**.

:::image type="content" source="media/cadence-modifier.png" alt-text= "Diagram that displays other options where you can enable the cadence modifier and choose the cadence type.":::

## Related topics

- [Optimization In-Depth](optimization-in-depth.md)
- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [Targeted Learn FAQ](targeted-learn-faq.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [What is Valuation?](what-is-valuation.md)
- [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)
- [Sell-Side Optimization](sell-side-optimization.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
- [Segment Modifier](segment-modifier.md)
