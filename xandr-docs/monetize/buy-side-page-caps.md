---
title: Buy-Side Page Caps
description: Learn what is a Page Cap and how it can be used. This page also covers examples to show in more detail how buy-side page caps work.
ms.date: 10/28/2023
---


# Buy-side page caps

When you run multi-tag auctions via [Microsoft Advertising's seller tag](../seller-tag/seller-tag.md), you get the ability to set page caps. Page caps can be used to restrict advertisers, line items, campaigns, or brands from winning more than one ad slot per AST ad call.

Buy-side page caps (advertiser, line item, and campaign) can be used to exclude similar campaigns from serving with each other. However, they don't cover the use case where you only want one impression per brand to show on an AST ad call, no matter the buyer. That use case is covered by [Sell-Side Page Caps](sell-side-page-caps.md).

> [!IMPORTANT]
> This feature is not available to clients by default. If you would like to enable this feature, please speak with your Microsoft Advertising representative.
>
> Buy-side page caps are also enforced on OpenRTB calls.

## Enable page caps for an advertiser

To set up buy-side page caps, select **Advertisers** \>  **All Advertisers**. Select the appropriate advertiser and click the **Edit** button that appears to the right of the advertiser name.

On the **Edit Advertiser** page, expand the **Frequency & Recency** section. Toggle to turn **Caps On**. Select **Serve only 1 imp per page**.

> [!NOTE]
> Frequency and Recency options are also available at the line item, campaign, and creative level. See [Frequency and Recency Caps](frequency-and-recency-caps.md) for more information.

:::image type="content" source="./media/buyside-page-caps.png" alt-text="Screenshot to set up buy-side page caps.":::

> [!IMPORTANT]
> Note that roadblocks are counted as single creatives when applying per page frequency caps.

## Example buy-side scenarios

The following examples show in more detail how buy-side page caps work.

### Example buy-side cap in action, enforcing correctly

Let's say you have the following setup:

- A page with a single AST ad call for two ad slots
- Two campaigns for Coca-Cola under the same advertiser, both at priority 5
- A single campaign for Nike, at priority 4
- You never want to show both Coca-Cola campaigns at the same time to one user

If you apply page caps to the Coca-Cola advertiser and run the AST ad call, the following will happen:

- Ad slot 1 goes to the first Coca-Cola campaign at priority 5
- The second Coca-Cola campaign is excluded from winning ad slot 2, so Nike wins instead
- Bids are returned to the Impbus and external bidders (if allowed) can bid
- Coca-Cola wins ad slot 1, Nike wins ad slot 2

### Example buy-side cap in action, enforcing correctly, but not as expected

Let's say you have the same setup as described above. If you apply page caps to the Coca-Cola advertiser and run the AST ad call, the following could happen:

- The two Coca-Cola campaigns and the single Nike campaign are returned to the Impbus for decisioning
- External bidder comes in and bids $10 CPM for a Coca-Cola ad in ad slot 2
- If the $10 CPM bid has a higher expected network revenue than the Nike bid, then it will win
- Ad slots return to the page, user sees Coca-Cola ads in both slots

To avoid this outcome, we recommend enabling [Sell-Side Page Caps](sell-side-page-caps.md).

## Related topics

- [Create a Campaign](create-a-campaign.md)
- [Buying Guide](buying-guide.md)
- [Seller Tag (AST)](../seller-tag/seller-tag.md)
- [Sell-Side Page Caps](sell-side-page-caps.md)
