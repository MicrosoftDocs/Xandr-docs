---
title: Integrate Accelerated Mobile Pages with PSP
description: In this article, find information about how to set up accelerated mobile pages (AMP) inventory with PSP.
ms.date: 10/28/2023
---

# Integrate accelerated mobile pages with PSP

Both Microsoft Monetize Ad Server and Direct Supply customers must follow the below guidelines to integrate their accelerated mobile pages (AMP) inventory with PSP.

## Context

When a publisher calls Microsoft Advertising using the `/prebid/amp` endpoint, Microsoft Advertising responds with key-values for each adapter and the top bid. This happens regardless of whether the client has a consolidated or bidder-specific line item setup. Microsoft Advertising Prebid bid response includes Prebid key-values (bidder, price, deal, and so on) for each SSP (Microsoft Advertising and/or SSP demand partners with PSP) that submitted a valid bid into the auction.

## Implementation

To set up AMP inventory with PSP:

1. Follow the [Prebid AMP Implementation Guide](https://docs.prebid.org/dev-docs/show-prebid-ads-on-amp-pages.html). More context on the AMP use case can be found [here](https://docs.prebid.org/prebid-server/use-cases/pbs-amp.html).

1. Update the `rtc-config` as shown in the example below:

    ```
    <amp-ad width="300" height="250"
      type="doubleclick"
      data-slot="/1111/universal_creative"
      rtc-config='{"vendors": {"prebidappnexuspsp": {"PLACEMENT_ID": "13144370"}}, "timeoutMillis": 500}'>
    </amp-ad> 
    ```

1. Exclude any demand partners that are [supported through PSP](prebid-server-premium-demand-partner-integrations.md) from the `rtc-config`. Retain vendors like `prebidappnexuspsp` and any partners who do not support PSP.
1. Set up [PSP-supported demand partners](prebid-server-premium-demand-partner-integrations.md) in Monetize by navigating to **Publishers** > **Prebid Server Premium** > **Demand Partner Configurations**. For more information, see [Add, Edit, or Delete a PSP Configuration](add-edit-or-delete-a-psp-configuration.md).

    > [!IMPORTANT]
    > Any publisher client with Google Ad Manager (GAM) as their ad server should ensure the following elements are in place:
    >
    > - Enable the checkbox **Serve into a SafeFrame** of Prebid Universal Creatives set up in GAM. This ensures viewability tracking.
    > - All relevant ad sizes are included on the creatives in GAM.
    > - Any optional `hb_bidder` targeting must include all relevant PSP demand partners, not just Microsoft Advertising.

## Related topics

- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Integrate Apps with PSP](integrate-apps-with-psp.md)
- [Prebid Server Premium Identity & User Syncing](prebid-server-premium-identity-and-user-syncing.md)
- [PSP supported formats and integration paths](./prebid-server-premium-supported-formats-and-integration-paths.md)
