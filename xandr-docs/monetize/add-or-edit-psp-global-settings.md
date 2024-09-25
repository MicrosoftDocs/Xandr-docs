---
title: Add or Edit PSP Global Settings
description: In this article, find information about how to add or edit PSP global settings.
ms.date: 09/25/2024
---

# Add or edit PSP global settings

Once inventory has been [Integrated with Prebid Server Premium (PSP)](integrate-with-psp.md), Global Settings should be reviewed and updated via the UI or the [Cross-Partner Settings API Service](../digital-platform-api/cross-partner-settings-service.md). Global Settings apply to all auctions across all demand partners and can be edited at any time.

1. Starting in the Monetize UI, hover over the **Publishers Menu** then select **Prebid Server Premium**.
1. Select **Global Settings** in the left-hand navigation bar on the **Demand Partner Configurations** screen. This will load the **Global Settings** section and the **Demand Partners** list. For more information on the Demand Partners list, see [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md).
1. To change the default settings, select the **Edit** button (next to the words "Global Settings"). This opens the **Edit Global Settings** pane.

The following configurations can be set:

## Demand partner timeout

The maximum time, in milliseconds, that Prebid Server Premium partners and other bidders in our marketplace are given to respond. If set, this global PSP timeout applies in place of the member-wide (or default) auction timeout, but can be overridden by setting a placement or
request-level timeout. See the [Full Timeout Hierarchy](#full-timeout-hierarchy) section below for more details.

> [!NOTE]
> This value should be slightly lower than any prebid.js configuration timeout set on the client side.

### Request-level timeouts

- Timeout for AMP inventory can alternatively be set at the request level via the timeout field and override any higher level timeouts (placement, PSP, member). Contact Microsoft Advertising to have Microsoft Monetize's settings updated to allow the timeout field to override other timeouts.
- Monetize Ad Server clients can similarly set the request-level timeout via the `auction_timeout_ms` field. Request-level timeout values longer than 450 ms will be floored to 450 ms.

### Full timeout hierarchy

The full timeout hierarchy in order from highest to lowest priority is:

1. [Debug Auction timeout value](understanding-the-debug-auction.md) (2000ms) [if debug=1/true]
1. Ad Request `auction_timeout_ms` value set by the publisher
    1. For AMP, see above.
    1. For Android, see guidance [here](../mobile-sdk/set-the-auction-timeout-for-android.md).
    1. For iOS, see guidance [here](../mobile-sdk/set-the-auction-timeout-for-ios.md).
1. Placement-level `auction_timeout_ms` value. Contact Microsoft Advertising to set this value.
1. PSP Global Settings (Cross Partner) Timeout value set by the publisher. See guidance above.
1. Member-level `default_auction_timeout_ms` value for the given data center. Contact Microsoft Advertising to set this value.
1. Member-level `default_auction_timeout_ms` value. Contact Microsoft Advertising to set this value.
1. Microsoft Advertising data center / global default (150ms)

## Price granularity

> [!NOTE]
> By default, PSP demand competes with Microsoft Advertising demand in a unified auction. **Monetize Ad Server** customers do not need to set up line items for PSP demand and can ignore price granularity settings entirely, as well as price bucket currency.

This field defines the CPM price buckets into which Demand Partner bids will be grouped. The setting should reflect a client's [Prebid price granularity settings](https://docs.prebid.org/adops/price-granularity.html) and their line item setup in their non-Monetize Ad Server with respect to price points (`hb_pb` or `hb_pb_{partner}` key-value targeting).

Customers can choose from the five system-defined options, or "custom" to define price buckets. When a currency other than USD ($) is selected, the price buckets will be reflected in that currency which will also be used when requests are matched to ad server line items. Note that the examples shown below use USD as currency.

- **Low:** $0.50 buckets, capped at $5 CPM. Buckets would be:
  - $0.00 to $0.50
  - $0.51 to $1.00
  - ...
  - $4.51 to $5.00
- **Medium:** $0.10 buckets, capped at $20 CPM.
- **High:** $0.01 buckets, capped at $20 CPM.
- **Auto:** Applies a sliding scale to determine granularity as shown in the **Auto Granularity** table. For more information, see [Prebid's Auto Granularity table](https://docs.prebid.org/dev-docs/publisher-api-reference/setConfig.html#autoGranularityBucket).
- **Dense**: Like **Auto**, but the bid price granularity uses smaller increments, especially at lower CPMs. For more details, see [Prebid's Dense Granularity table](https://docs.prebid.org/dev-docs/publisher-api-reference/setConfig.html#denseGranularityBucket).
- **Custom:** (advanced setting options) Define up to 10 price bucket granularity groups by specifying each bucket's **Upper Bound** and **Increment**.

## Price bucket currency

This specifies the currency used for price buckets and **does not apply to Monetize Ad Server customers**. Specifically, targeting keys, not bids, are converted into the selected currency. Select the currency that aligns with the line items in the publisher's ad server. Any currency [supported by Microsoft Advertising](currency-support.md) can be chosen.

> [!NOTE]
> This is independent of the Monetize currency selection and only applies to Prebid Server Premium auctions.

### Bid response currency

Targeting keys:

- When using the /openrtb2/prebid (and have specifically set it to override targeting keys in response) or /ut/v3/prebid endpoints, targeting keys within bid responses use the transaction currency that you have set via the [Publisher Service API](../digital-platform-api/publisher-service.md). If you need to override that currency selection, use the [Prebid.js currency module](https://docs.prebid.org/dev-docs/modules/currency.html#currency-module).
- When using another integration method, targeting keys within bids use the currency selected for PSP price buckets independently of the [Publisher Service API](../digital-platform-api/publisher-service.md).

## Related topics

- [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md)
- [Add, Edit, or Delete a PSP Configuration](add-edit-or-delete-a-psp-configuration.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
