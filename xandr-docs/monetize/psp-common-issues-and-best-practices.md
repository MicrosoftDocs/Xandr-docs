---
title: PSP Common Issues and Best Practices
description: Navigate PSP integration with tips on maximizing performance, troubleshooting errors, and optimizing collaboration with demand partners.
ms.date: 10/28/2023
---

# PSP common issues and best practices

This page highlights some of the common challenges when integrating and setting up Prebid Server Premium (PSP), along with best practices for maximizing performance and resolving issues. Key focus areas are managing connections from inventory to Monetize, troubleshooting developer tools errors, and optimizing collaboration with demand partners.

## Connections from Inventory to Monetize

- Review [overall PSP documentation](prebid-server-premium.md), especially [integration](integrate-with-psp.md) and [setup](set-up-prebid-server-premium.md) content.
- **Page Setup Guidance**: See guidance on page setup for both [instream and outstream video here](video-guidance.md).
- **Global Timeout**: Affects PSP demand partners as well as all other bidders in our marketplace to ensure fair competition. To safeguard user experience, a starting timeout of around 250ms is advised. Gradually increase the timeout from there to gauge the tradeoff between revenue and user experience.
- **Demand Partners and Contracts**: Each seller must have a contract with each demand partner (typically another SSP). Objects must be created in those platforms before they can be mapped to Monetize inventory via PSP configurations.
- **Optimal Number of Demand Partners**: There is no optimal number of demand partners for every publisher, although it is recommended to start with around 3 to 4. Additional partners should be added, monitored, and optimized from there. Underperforming partners should be removed. Typically, the more demand partners in an auction, the lower the win rate. Lower win rates tend to cause SSPs to bid less often.

### Developer Tools errors

When investigating connections from web pages to Monetize, common errors seen in Chrome Developer Tools include:

- **Member**: The member ID does not match the publisher or placement. Correct the values in the page setup to match the objects in Monetize.
- **Unknown**: This is often due to HUMAN security identifying and blocking the traffic as fraudulent. This can occur when attempting to emulate a mobile environment on a desktop/standard web where HUMAN correctly identifies the traffic as fraudulent. This can be addressed by adding `&apn_test=true` to the query string.
- **Other**: This can be due to transactions that violate our buyer policy, such as those with U.S. sanctioned individuals, entities, and countries.

## Connections from Monetize to Demand Partners

- Review [overall PSP documentation](prebid-server-premium.md), especially [analytics content](prebid-server-premium-analytics.md) to understand how to access data and insights.
- **Leverage Monetize Reports**: Use the Delivery Analytics and Inventory Analytics reports to track final delivery and revenue.
- **PSP Health Analytics Report**: Leverage [this report](prebid-server-premium-health-analytics-report.md) for deeper troubleshooting (detailed errors) and proactive optimization. This report is based on a sample of log data multiplied to estimate the full volume of activity. Documentation includes suggested actions to address each type of error.
- **Monetize Insights Tab**: [Review trends](monetize-insights-for-publishers.md) of PSP monetization against other paths (channel views) and for Monetize against each demand partner (SSP views).
- **PSP Request Response Sampler**: Use the [PSP Request Response Sampler](prebid-server-premium-request-response-sampler.md) to find examples of specific errors from Health Analytics to then troubleshoot with demand partners.
- **Configuration Targeting**: Ensure the targeting of configurations covers all scenarios. For example, if there is only one configuration targeting the United States, but a publisher sends requests for inventory in Germany, the requests for Germany will not be passed to PSP demand partners.
- **Best Practice**: Use a default/global/run-of-site configuration with a low configuration rank. More specific configurations with a higher rank can supersede this to send buyers better signals and increase revenue.
- **Response code 204**: When viewing sample bid responses in the PSP Requests Sampler tab, response code 204 from a demand partner means "no bid." This could simply mean there is no demand for the inventory, or that the buyers expect certain signals in bid requests that are not present.

## Prebid Server Premium architecture

This section outlines the architectural framework of Prebid Server Premium (PSP). Understanding this architecture will aid in effective integration, troubleshooting, and performance enhancement.

:::image type="content" source="media/psp-architecture-updated.png" alt-text="A screenshot of Prebid Server Premium architecture.":::

## Related topics

- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Integrate Apps with PSP](integrate-apps-with-psp.md)
- [Integrate Accelerated Mobile Pages with PSP](integrate-accelerated-mobile-pages-with-psp.md)
- [Non-prebid Integrations with PSP](non-prebid-integrations-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)
