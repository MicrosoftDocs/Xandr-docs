---
title: Bidder Best Practices
description: In this article, explore information about a number of services, bidder fields, and best practices recommended for our partners.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder best practices

As you integrate your bidder and get set to go live, there are a number of wiki pages and bidder settings we recommend using to ensure that you have the best experience possible on our platform. This page highlights a number of services, bidder fields, and practices that are commonly overlooked but prove very useful to our partners.

## Good reads

- [Platform Member Service](platform-member-service.md) - Read-only service that provides you with the most up-to-date list of sellers on our platform and shows information about data providers.
- [Content Category Service](content-category-service.md) - Allows you to see what content categories are registered and their corresponding IDs.
- [Inventory Attribute Service](inventory-attribute-service.md) - Allows you to see what inventory attributes are registered in Xandr's system.
- [Creative Standards and Auditing](creative-standards-and-auditing.md) - Highlights our Creative Audit Policy and standards.
- [Audit Notification Request](audit-notify-request.md) - Alerts you to any changes in the creative audit status (including creative approvals and rejections).
- [Bid Request](outgoing-bid-request-to-bidders.md) - Provides all of the fields sent in the bid request to you bidder.

## Recommended

We recommend to set the `audit_notify_email` and `sherlock_notify_email` fields in the [Member Service](member-service.md) to valid email addresses. This will ensure you are notified when your creatives are audited and will enable you to take action, where needed.

## Not recommended

A practice that we do **not** typically recommend is setting your bidder profile to run exclusively on a allowlist by domain. While this is possible, there is a very good chance you will be severely limiting the traffic you are seeing mainly because publishers reserve the right to mask domains or not provide any domain detail at all. If you find there is a publisher that is not providing the level of transparency you desire, contact your Xandr representative.

## Related topics

- [Auction Configuration & Feedback](auction-configuration---feedback.md)
- [Integrate a Bidder](integrate-a-bidder.md)
- [API Services](api-services.md)
- [Bidder Profile - FAQ](bidder-profile---faq.md)
- [Legacy Bidder Profile Service](legacy-bidder-profile-service.md)
