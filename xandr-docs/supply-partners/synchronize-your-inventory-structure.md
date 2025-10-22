---
title: Synchronize Your Inventory Structure
description: Learn why its important to synchronize your inventory structure with Xandr on a regular basis as not doing so can lead to the inventory being unsellable via Xandr.   
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Synchronize your inventory structure

You should synchronize your inventory structure with Xandr on a regular basis, ideally programmatically.
<!-- Tight synchronization allows you to:

- Analyze discrepancies between Xandr and your system.
- Investigate publisher or domain performance.
- Enforce ad quality and publisher blocking preferences to ensure that Xandr provides acceptable bids.
- Separate detectable and non-detectable inventory so that the impact of non-detectable inventory on overall selling can mitigated. -->

If inventory is not properly categorized and becomes non-detectable by Domain Detection, this will result in the inventory being unsellable via Xandr, because, without proper inventory grouping and classification, Xandr cannot reliably enforce its [Part of Service Policies](../policies-regulations/index.yml).

Use the [UI to synchronize your inventory structure](use-the-ui-to-synchronize-your-inventory-structure.md) and [Use the API to synchronize your inventory structure](use-the-api-to-synchronize-your-inventory-structure.md) pages to introduce you to the basic sell-side object hierarchy and then walk you through the process of mapping your supply to these Xandr objects using Xandr UI or the API.

## Inventory mapping

Publisher, Placement Group, and Placement objects have unique `id` and unique `code` fields. The `id` is an automatically generated integer upon object creation, while the `code` allows external partners to associate their `id` with a specific object. For example, if your publisher `'VeryCreativePublisherName'` has an ID of `8675309` and a code of `'123vcpubnname'`, passing `'123vcpubnname'` in the `site.publisher.id` field associates the request and transactional information with publisher `8675309` in our system’s lookup sequence.

> [!NOTE]
> Use the `code` field to map your bid requests to your publishers and placements. The `code` field is required for all external sellers at both the publisher and placement levels. It is also highly recommended for all other sellers to make their inventory as granular as possible. This ensures accurate investigation of quality issues, especially for domain detectability. For more details and examples, see [Bid request](bid-request.md) and [Integration FAQ](faq-integration-process.md).
>
> Requirements for the `code` field:
>
> - No two objects of the same type can have the same code.
> - The field is case-sensitive (e.g., 00071a ≠ 00071A).
> - The field is limited to 100 characters.
> - Values cannot contain spaces.
> - Values can contain a period (.), underscore (_), hyphen (-), and asterisk (*).

### Lookup sequence

When you receive a request, checks are made to determine the associated placement ID. The selling member ID is determined from the query string of the endpoint the request was sent to. For example, `https://Xample-useast.adnxs.com/openrtb2?member_id=1234`.

**Bid request example:**

```
{
    "imp":
    [
        {
            "tagid": "8675309"
        }
    ],
    "site":
    {
        "id": "90210-8675309",
        "publisher":
        {
            "id": "abc123xyz"
        }
    }
}
```

The lookup sequence steps for the preceding example are as follows:

1. If `bidrequest.imp.ext.appnexus.placement_id` doesn't exist, then go to step 2.
1. Check placements under the `member_id` `"1234"` with a `code` matching the `imp.tagid` value of `"8675309"`. If a placement exists with that `code`, then associate the request with this placement ID. If no placement matches the `member_id` and `code`, then go to step 3.
1. Check placements under the `member_id` `"1234"` with a `code` matching the `site.id` value of `"90210-8675309"`. If a placement exists with that `code`, then associate the request with this placement ID. If no placement matches the `member_id` and `code`, then go to step 4.
1. Check publishers under the `member_id` `"1234"` with a `code` matching the `site.publisher.id` value of `"abc123xyz"`. If a placement exists with that `code`, then associate the request with the publisher's default placement ID. If not, then go to step 5.
1. Check for a default placement ID on the `member_id` `"1234"`. If found, then associate the request with this placement ID. If not, then go to step 6.
1. The lookup sequence is exhausted, and the request is discarded with no customer-facing error logged.

The best ways to align inventory are those where the lookup sequence is successful in identifying a placement in steps 1–3. This enables you to:

- Analyze the discrepancies between Xandr and your system.
- Explore the performance of publishers or domains.
- Implement ad quality standards and preferences for blocking publishers to ensure acceptable bids from Xandr.
- Differentiate between detectable and non-detectable inventory, thereby mitigating the impact of non-detectable inventory on overall sales.
