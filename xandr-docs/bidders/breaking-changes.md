---
title: Bidders - Breaking Changes
description: In this article, learn the types of changes that are considered 'breaking changes' when it comes to the impression bus API and bidding protocol.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Breaking changes

Our impression bus API and bidding protocol are continually changing. The vast majority of changes are seamless additions of new functionality, but occasionally we introduce "breaking changes" that may require you to adjust your integration.

This page explains what changes qualify as "breaking changes" to our impression bus API and our bidding protocol. It also gives you examples of changes that do not quality as breaking changes.

> [!NOTE]
> Xandr reserves the right to fix bugs, adjust functionality to comply with our [Service Policies](../policies-regulations/index.yml) and legal obligations, and change features and products in alpha and beta without providing early notice.

## Impression bus API

In the context of our [Impression Bus API](impression-bus-api.md), the following types of changes qualify as breaking changes:

- Removal of a field.
- Change of a field from non-mandatory to mandatory.
- Addition of new validation rules.
- Modification of the data type of a field (e.g., array of IDs converted to array of objects).
- Modification of throttling of requests.
- Reduction in the number of objects returned by responses.

When we introduce a breaking change into our impression bus API, we will support two versions of the API in production, one with and one without the breaking change, for 60 days. We will announce these changes and how to correctly reach each version during the breaking changes period (see [Receiving Breaking Change Notifications](#receiving-breaking-change-notifications)).

## Bidding protocol

In the context of our [Bidding Protocol](bidding-protocol.md) (requests and responses), the following types of changes qualify as breaking changes:

- Removal of a field.
- Change of a field from non-mandatory to mandatory.
- Modification of the data type of a field (e.g., array of IDs converted to array of objects).

We will announce breaking changes to our bidding protocol at least 45 days before the changes take effect (see [Receiving Breaking Change Notifications](#receiving-breaking-change-notifications)).

## Examples of non-breaking changes

The following types of changes do not quality as breaking changes. Note that this list is not exhaustive; these are just some examples of non-breaking changes.

- Addition of a new non-mandatory field (API or bidding protocol).
- Addition of a new service (API).
- Addition of metrics/dimensions to reports (API).
- Addition of a new report type (API).
- Deprecation of a field without removing it (API or bidding protocol).
- Reduction or increase in the number of concurrent reports allowed (API).
- Change in order of fields in an object, objects in an array, etc. (API or bidding protocol).

## Receiving breaking change notifications

- If you have a Xandr user account, you will receive breaking change communications automatically.
- If you do not have your own Xandr user account, you can sign up to receive communications at the [Microsoft Advertising Xandr site](https://about.ads.microsoft.com/en-us/solutions/xandr/xandr-premium-programmatic-advertising).
