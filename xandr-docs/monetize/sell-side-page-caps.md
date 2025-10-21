---
title: Sell-Side Page Caps
description: Learn what are Page Caps and how it can be used to restrict brands, advertisers, line items, or campaigns from winning more than one ad slot per AST ad call. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Sell-Side page caps

> [!IMPORTANT]
> This feature is not available to clients by default. If you would like to enable this feature, please speak with your Microsoft Advertising representative.
>
> [Microsoft Advertising's seller tag](../seller-tag/seller-tag.md) (AST, which makes a `/ut` http ad request) is the primary tag that supports multi-tag auctions. The legacy `/mtj` is no longer supported. Note that we will refer to a "single AST ad call" throughout this document - this represents a single http request (to the `/ut` endpoint), however, it is possible to split up these ad calls (and thus the http requests) using the AST library. The features described on this page do not apply across http requests. For the examples on this page, will we assume that all tags on a page are included in a single AST ad call.
>
> Sell-side page caps are also enforced on OpenRTB calls.

When you run multi-tag auctions via [Microsoft Advertising's seller tag](../seller-tag/seller-tag.md), you get the ability to set page caps. Page caps can be used to restrict brands, advertisers, line items, or campaigns from winning more than one ad slot per AST ad call. Sell-side page caps apply to brands, while buy-side page caps apply to advertisers, line items, and campaigns.

Sell-side page caps are enabled on a per-publisher basis. In other words, you need to turn on page caps on a publisher-by-publisher basis.

Exceptions can be set at both the member level and the publisher level. You can allow certain brands to serve more than once per page by setting exceptions as follows:

- On the member level, as described in [Set Page Caps for the Entire Network](#set-page-caps-for-the-entire-network) below. These exceptions will apply to all publishers that have page caps enabled.
- On the individual publisher level, as described in [Set Brand Exceptions on a Per-Publisher Basis](#set-brand-exceptions-on-a-per-publisher-basis) below. These exceptions will apply only to this publisher, combined with any member level brand exceptions. In other words, the list of exceptions applied to a given publisher consists of **both** the member-level and publisher-level exceptions.

> [!IMPORTANT]
> Sell-side page caps will **strictly** enforce one brand per page for any given AST ad call. The only automatic exception is for **roadblock** campaigns, which will show kas many creatives as they win.

## Enable page caps for a publisher

To enable sell-side caps for a publisher, select **Publishers** \> **All Publishers** from the top navigation menu. Click on one of your publishers, and then click **Edit**.

In the dialog that appears, under **Advanced**, toggle to activate **Enable Sell-side Page Capping**. Add the brands for which you would like to override page caps in the table that appears below. For more information, see [Set Brand Exceptions on a Per-Publisher Basis](#set-brand-exceptions-on-a-per-publisher-basis).

## Set sell-side page cap exceptions

You can set brand exceptions on the member level (which applies to all publishers) or on the individual publisher level (which applies to just that publisher). These brands will be allowed to serve more than once per AST ad call.

> [!IMPORTANT]
> Brand 1, the "Unknown" brand, is a "wildcard" brand that includes all unaudited managed ads. We recommend you set it as a network-level exception so your managed ads serve correctly.

### Set page caps for the entire network

To set brand exceptions for the network, select **Network** \> **Tools** \> **General** from the top navigation menu, and click on the **Sell-side Page Caps** tab. Click **Add** to add the brands you'd like to allow to serve more than once per page on your enabled publishers from the **Available Brands** list. They'll be inserted into the **Excepted Brands** list.

### Set brand exceptions on a per-publisher basis

When you enable page caps for a publisher, the **Page Cap Exceptions** tab will appear. At the top of the page are a list of your **Network-Level Sell-Side Page Caps**. These are the brand exceptions enabled across your entire network, as described in [Set Page Caps for the Entire Network](#set-page-caps-for-the-entire-network).

To add an **additional** brand exception that will be applied to this publisher (beyond the existing network-level exceptions), click **Add** in the **Available Brands** list. The brand will be added to the **Excepted Brands** list.

## Example sell-side scenarios

The following examples explain in detail how sell-side page caps work.

### Example sell-side cap in action

Let's say you have the following setup:

- A page with a single AST ad call for two ad slots
- Two campaigns for Coca-Cola under the same advertiser, both at priority 5
- Two campaigns for Nike, both at priority 4
- You never want to show more than one ad per brand at any time

If you apply page caps to the publisher and run the AST ad call, the following will happen:

- Coca-Cola wins both ad slots in the bidder, Nike is in second place, and the bid array is returned to Impbus for decisioning
- External bidder comes in and bids $10 CPM for Coca-Cola in ad slot 1
- If the $10 CPM bid has a higher expected network revenue than either Coca-Cola bid, then it will win ad slot 1
- Your managed bid for Coca-Cola will be excluded from winning ad slot 2, and Nike will win instead

## Related topics

- [Buy-Side Page Caps](buy-side-page-caps.md)
- [Seller Tag (AST)](../seller-tag/seller-tag.md)