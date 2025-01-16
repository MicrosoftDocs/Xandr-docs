---
title: Optimization - FAQ
description: In this article, explore answers to frequently asked questions (FAQs) about optimization.
ms.date : 10/28/2023
---

# Optimization - FAQ

## Data for optimization

### What data is available for optimization

Buyers of inventory may optimize their purchasing logic using any of the fields sent in the [Bid Request](outgoing-bid-request-to-bidders.md). The most common fields used are:

- `selling_member_id` - The member ID of the seller.
- `url` - The most granular information about the url of the impression that can be passed to the bidder. This is determined by the seller's business rules and the data that was passed to Xandr for that impression.
- `country` - The country or region from which the user is viewing the impression.

Additional data that may be used for optimization includes the following:

- `publisher_id` - The unique ID of the publisher. This ID cannot be dereferenced, but impressions from a given publisher may perform similarly and thus be considered an optimizable chunk. For most sellers on the platform, `publisher_id` is the top level in the hierarchy.
- `site_id` - The unique ID of the site. This ID cannot be dereferenced, but impressions from a given site may perform similarly and thus be considered an optimizable chunk. Sites are below publishers in the Xandr hierarchy, so any publisher will have one or more sites.
- `id` (within the tags array) - The unique ID of the tag. This ID cannot be dereferenced, but impressions from a given tag may perform similarly and thus be considered an optimizable chunk. Tags are below site in the Xandr hierarchy, so any site will have one or more tags.
- `inventory_audits` - See the Inventory Audits in the [Inventory - FAQ](inventory---faq.md).
- `position` - When available, this indicates whether the ad tag is above or below the fold.

## Related topics

- [Bid Request](outgoing-bid-request-to-bidders.md)
- [Inventory - FAQ](inventory---faq.md)
