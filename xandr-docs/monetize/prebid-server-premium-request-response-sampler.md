---
title: Prebid Server Premium Request Response Sampler
description: Use Prebid Server Premium to send bid requests, analyze responses, and optimize revenue with the Request Response Sampler Tool.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Prebid Server Premium Request Response Sampler

Prebid Server Premium's core functions are to send publisher bid requests to demand partners (typically SSPs), collect bid responses, auction responses, and forward them to Microsoft Monetize. The Request Response Sampler Tool provides examples of these JSON objects, and is best used with the PSP Health Analytics report to find instances of prevalent errors as defined in [the report's documentation](prebid-server-premium-health-analytics-report.md). Share samples with demand partners to optimize activity and unlock additional revenue.

> [!IMPORTANT]
> Samples from the tool may contain data for multiple demand partners. Thoroughly review and filter any output from the tool before sending it to ensure demand partners only receive data relevant to their platform.

To use the Request Response Sampler Tool:

1. Starting in the Monetize UI, hover over the **Publishers Menu**, then click **Prebid Server Premium**.

1. Click **Requests Sampler** in the left-hand navigation bar.

1. Requests can be searched in 24-hour segments at a time for up to 7 days in the past. It is recommended to leave the Start Date and End Date as the default.

1. Enter either a specific Placement ID or search for a specific Demand Partner. These filters are mutually exclusive and will allow the tool to retrieve samples of relevant requests and responses. In the future, the tool will allow open-ended queries to pull any random request-response pair as well as offer additional filters.

1. Click **Generate API Sample**.
1. If a relevant sample can be found, the tool will display it in the next section. The high-level sections are:

    - `request_from_monetize_to_psp`: Monetize forwards the publisher's original request to PSP in the appropriate format with relevant Monetize (e.g., yield management floors) and PSP (e.g., demand partner parameters) settings included. This helps determine if a potential problem stems from the page/app, Monetize, or PSP.
    - `request_from_psp_to_bidder`: PSP sends an OpenRTB request to each demand partner configured (mapped) for the inventory with that partner's parameters and enabled user identifiers. The exact request to (`requestbody`) and response from (`responsebody`) each partner is included. The `uri` represents the partner's endpoint as defined in their [GitHub.yaml](https://github.com/prebid/prebid-server/tree/master/static/bidder-info) file. Status 204 means the partner chose not to bid.
    - `response_from_psp_to_monetize`: PSP responds to Monetize with a summary of bid responses from all demand partners. Partners can be identified via `seatbid.bid.ext.prebid.meta.adaptercode`. Various diagnostic information like the response time from each partner (`ext.responsetimemillis`) can be found here as well.

1. If needed, click **Copy Request to Clipboard** to bring the output to another app.
1. By default, samples are pulled from real auctions. Use the **Run Auction without Test Flag** toggle to run a simulated debug auction with the `test:1` flag, which could increase the chances of getting a response. The test flag might also lead to different results for some demand partners.

## Related topics

- [Prebid Server Premium Analytics](prebid-server-premium-analytics.md)
- [Prebid Server Premium](prebid-server-premium.md)
- [Prebid Server Premium Health Analytics Report](prebid-server-premium-health-analytics-report.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [PSP Supported Formats and Integration Paths](prebid-server-premium-supported-formats-and-integration-paths.md)
