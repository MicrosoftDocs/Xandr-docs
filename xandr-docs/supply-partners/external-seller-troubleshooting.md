---
title: External Seller Troubleshooting
description: In this article, explore the common challenges encountered by external sellers, along with troubleshooting guidance to help resolve them.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# External seller troubleshooting

This page describes some of the common issues facing external sellers and instructions to help resolve those issues. For additional information see the [Integration Process FAQ](faq-integration-process.md).

## Deals troubleshooting

If you're experiencing non-delivery of specific deals, here are some steps to take:

1. **Ensure the deal exists in the Xandr system**. Use the [Deal Service](../digital-platform-api/deal-service.md) to confirm that the deal exists, is active, and is offered to the correct Xandr buyer member. For full instructions on creating deals, see [Selling Deals on Xandr](selling-deals-on-xandr.md).
1. **Check that requests are being sent for this deal**. The code field in the Xandr deal object must match the deal ID that is sent in the OpenRTB request (`pmp.deals.id`). For examples, see [Selling Deals on Xandr](selling-deals-on-xandr.md).
1. **Requests for this deal must meet our general specifications and point to valid, active objects in our system.** See [General Delivery Troubleshooting](#general-delivery-troubleshooting) below.
1. **Ensure the buyer is targeting the deal.**

      If you've confirmed steps 1 - 3, the next course of action is to reach out to the buyer and ensure that they are actively targeting the deal. If so, the buyer should then submit a support ticket via the [Customer Portal](https://support.ads.microsoft.com) in order for our buyside support team to troubleshoot.

## General delivery troubleshooting

Most commonly, general delivery issues point to a lack of demand for the specific inventory. If you’re experiencing issues with delivery in the open marketplace, you may consider setting up a deal with a specific buyer to monetize your inventory. Also, note that supply sold in the Xandr open exchange is analyzed and vetted to ensure that inventory represents the most direct, transparent, and efficient path to purchase for our buyers. Impressions that do not meet these requirements may be ineligible for RTB selling, but may be sold via deals. You can refer to our [Supply Partner Best Practices](best-practices.md) page for more information on these standards. If you are not eligible for deals, see our [Deal Eligibility Requirements](deal-eligibility-requirements.md).

The following steps will guide you through troubleshooting non-delivery in the open marketplace.

1. **Check that the requests are valid according to Xandr specifications.**

    All requests being sent must follow the [Xandr OpenRTB spec](incoming-bid-request-from-ssps.md).
1. **Ensure that the sent requests include valid site/app and publisher IDs.**

    [Requests](incoming-bid-request-from-ssps.md) must include a site ID (tagid, site.id) or app ID (app.id) that corresponds with an existing placement object in the Xandr system. For specific examples on where to include these IDs, see the [Xandr OpenRTB spec](incoming-bid-request-from-ssps.md). The ID sent in the request can be either the ID of the **placement** object or the value set in the `code` field of the **placement** object. If the request does not contain either a site or an app ID, or if the ID sent in the request does not exist in the Xandr system, the request will not be considered valid. The same is true for a publisher: the ID included in the request must map to a valid, active publisher in the Xandr system. If a publisher ID is not included in the request, the site/app included still must map to a placement that exists under an active publisher and site (placement group) in our system as well. For a full explanation of our object hierarchy and instructions and best practices regarding inventory mapping, see [Synchronize Your Inventory Structure](synchronize-your-inventory-structure.md). Use the following API services to check whether each object in the hierarchy is active and maps to the codes sent in the request:

    - [Publisher Service](../digital-platform-api/publisher-service.md)
    - [Site (Placement Group) Service](../digital-platform-api/site-service.md)
    - [Placement Service](../digital-platform-api/placement-service.md)
1. **Verify that the corresponding placements have been deactivated.**

    Placements may be deactivated by our system for reasons related to inventory quality. If the site or app ID sent in a request maps to a deactivated placement, this request will not be valid and will receive a 400 MALFORMED HTTP error. For more information on inventory quality deactivations, see [Inventory quality deactivations](#inventory-quality-deactivations).
1. **Instruct the buyer to submit a support ticket.**

    If the preceding steps did not resolve the issue and there is a specific buyer involved who is unable to transact on your inventory, the next course of action is to have the buyer submit a support ticket via the [Customer Portal](https://support.ads.microsoft.com) so our buyside support team can further troubleshoot.

## Malware or policy violation escalations

Any escalations regarding malware or violations of our [Service Policies](../policies-regulations/index.yml) can be submitted to our Anti-Malvertising Team via the [Customer Portal](https://support.ads.microsoft.com) under the category **Anti-Malvertising**. This team will be able to review the offending creative and domain for platform-blocklist purposes.

- **Domains**: If the escalation involves a specific domain or list of domains, make sure to include the reason for flagging the domain, as well as a report from a third party scanning vendor (such as [The Media Trust](https://www.themediatrust.com/) or [RiskIQ](https://www.riskiq.com/)) if applicable.
- **Creatives**: If the escalation involves a specific creative, ensure that one or all of the following is included in your support request (listed here in order of importance):
  - Corresponding report from a third party scanning vendor (such as [The Media Trust](https://www.themediatrust.com/) or [RiskIQ](https://www.riskiq.com/)) if applicable.
  - Creative ID pulled from the final page content (for example, `<!-- Creative 36110421 served by Member 958 via Xandr. -->`) or from the **crid** parameter of the bid response.
  - One of the following URLs:

    - `ib.adnxs.com/if?`
    - `ib.adnxs.com/click?`
    - `ib.adnxs.com/ab?`
    - `ib.adnxs.com/vevent?`
  - A full list of network calls made to the page at the time of the incident.

## Ad quality blocks & escalations

Creatives that do not contain malicious elements or violate any platform buying policies can still be blocked either seller-wide or on specific publishers for issues such as brand conflicts, incompatible videos, etc. These ad quality blocks are mainly handled dynamically via OpenRTB, specifically using the following parameters:

- **badv**: top-level advertiser domains that correspond to brand URLs in the Xandr system
- **bcat**: content categories
- **btype**: creative media types
- **battr**: technical attributes

To block specific creatives or set the above ad quality settings in the Xandr system, use the [Ad Profile Service](../digital-platform-api/ad-profile-service.md). For best practices regarding the use of ad quality, see [Define Ad Quality Rules](define-ad-quality-rules.md). Settings applied in the Xandr system will work in conjunction with those sent dynamically in the OpenRTB request; the most restrictive block between the two will always apply. To preview a buyer's creative, you can use the URL present in the **iurl** field of the bid response.

If you're encountering creatives that do not meet these ad quality settings (either passed into the OpenRTB request or set in the Ad Profile service) serving on your inventory, this can be escalated to our Anti-Malvertising Team via the [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) under the category **Anti-Malvertising**.

## HTTP responses

Expected HTTP responses to bid requests are listed below:

- 200 OK: A valid bid response has been returned.
- 204 NO CONTENT: No bid has been returned.  
- 400 MALFORMED: The [incoming bid request](incoming-bid-request-from-ssps.md) contains a site ID (tagid, site.id), app ID (app.id), or publisher ID (app.publisher, id or site.publisher.id) that maps to an inactive publisher or placement object in the Xandr system. For more information, see [General delivery troubleshooting Step 2](#general-delivery-troubleshooting) above.

If you are receiving no response at all and/or the request is timing out, check to ensure that your global auction timeout settings provided during the initial integration are correct. If these settings have changed, or if you are unsure of the timeout settings that were initially submitted, submit a support ticket via our [Customer Portal](https://support.ads.microsoft.com) to confirm and provide the correct settings to our teams.

## Discrepancies

When multiple systems are involved in adserving, some level of discrepancy in reporting between these systems is to be expected. Historically, industry standards have considered discrepancies of up to 10% to be reasonably acceptable. If you're experiencing a higher discrepancy, one of the below scenarios might be the root cause.

### Difference in timeouts for cached ads

Impression counting for external sellers relies on the system receiving a win notify call (/ab, /it, /openrtb_win, /vast_track); any timeout differences in external systems can cause discrepancies in impression counting. On the Xandr platform, timeouts for each media type (relative to the time of the auction generated by the OpenRTB request) are as follows:

- banner: 5 minutes
- native: 360 minutes
- video: 360 minutes

In regards to click tracking, similar timing differences will account for discrepancies as well. The expiration for our click tracking URL (/click) is 120 minutes relative to the the time of the logged impression; clicks that occur outside of this window will not be counted.

### Tracking on different events

As described above, Xandr relies on a win notify call in order to count an impression. Display discrepancies can arise when an outside system is tracking impressions at a different time in the ad call chain than the firing of this call (for example, on creative render vs. on delivery of creative content to the page).

Similarly, video discrepancies are most commonly caused by a difference in the VAST tracking event that is used to count the impression. Xandr counts a VAST impression when the impression tracking URL in our VAST wrapper is fired, which, as per the [IAB spec](https://www.iab.com/guidelines/iab-display-advertising-guidelines/), should be sent by the player once the first frame of the video is rendered. If an outside system is tracking impressions on the delivery of the ad content, the start event, or any other VAST tracking event, the impression numbers recorded in this system are NOT likely to line up with those recorded by Xandr.

### Incorrect handling of auction price macro

As shown in the [OpenRTB spec](outgoing-bid-response-to-ssps.md), auction prices from outside systems are passed to Xandr using the macro `${AUCTION_PRICE}`. If this macro is not filled with a valid win price, our system will not be able to record this price, which can lead to financial discrepancies.

## Inventory quality deactivations

When a placement object is deactivated for a reason related to inventory quality, notifications including **object ID** and **reason for deactivation** will be sent to emails specified in the `audit_notify_email` field under the [Member Service](../digital-platform-api/member-service.md).

If you are employing creative scanning that loads /ab URLs and these scanner endpoints are causing inventory quality deactivations, ensure that the header "X-is-test: 1" is included with each call to the /ab URL from these endpoints. This header will indicate that the corresponding call to the /ab URL is a test, and will prevent our system from logging it. If you are still experiencing issues with this header in place, also confirm that your scanner's endpoint resolves to a DNS name; using an IP that does not resolve to a DNS name will cause deactivations regardless of whether the test header is used.

> [!NOTE]
> The test=1 query string parameter (used for test requests) does NOT work for /ab URLs.

## Object limits

To view your current object limits, use the [Object Limit Service](../digital-platform-api/object-limit-service.md). Both active and inactive objects will count towards object limit counts. Object limit notifications are sent to emails specified in the `sherlock_notify_email` field under the [Member Service](../digital-platform-api/member-service.md). If you are nearing your object limits, you can delete unused objects using the corresponding API service, as deleted objects do NOT count against this limit.

- [Publisher Service](../digital-platform-api/publisher-service.md)
- [Site (Placement Group) Service](../digital-platform-api/site-service.md)
- [Placement Service](../digital-platform-api/placement-service.md)

## Unexpected behavior

If you are experiencing behavior that is not in line with our documentation or specifications, submit a support ticket via our [Customer Portal](https://support.ads.microsoft.com) with relevant logs exhibiting the issue and/or steps to reproduce.
