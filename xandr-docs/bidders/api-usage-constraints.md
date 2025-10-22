---
title: Bidders - API Usage Constraints
description: In this article, find information about the constraints placed on API usage.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# API usage constraints

## Input and output throttling

To ensure good performance, all accounts are limited to 100 reads per minute and 60 writes per minute. This limit is enforced programmatically by the API on a member level. That means if there are two API users for a single member, they will share the throttling limit (i.e., two users can average 50 reads per minute each, four users can average 25 reads per minute each). If you require more reads or writes per minute, please reach out to your Xandr account representative.

Every response includes a `"dbg_info"` object that conveys information about the API call and response that is for Xandr internal use only and may be requested during a support inquiry.

## Pagination

The maximum number of objects that can be returned in a given GET response is 100. To retrieve more than 100 objects, you can paginate results by specifying `start_element` and `num_elements` in the query string of the GET request. For example, the following request would return the first 50 objects in the response:

```
$ curl -b cookies -c cookies 'https://api.adnxs.net/creative?start_element=0&num_elements=50'
```

To retrieve the next 50, you would simply set `start_element=50`.

- The first element is element 0.
- All GET responses will have a "count" property showing the total number of elements matching that GET request.
- This will also apply to non-reporting services, such as the creative search service, that are requested with methods other than GETs.

### Examples

```
$ curl -b cookies -c cookies 'https://api.adnxs.net/segment/1?start_element=0&num_elements=100'
$ curl -b cookies -c cookies 'https://api.adnxs.net/creative/1?start_element=0&num_elements=100'
```

## Authentication frequency

After authenticating, your token remains valid for 2 hours. You do not need to re-authenticate within this time. If you do  re-authenticate, please note that the API permits you to authenticate successfully 10 times per 5-minute period. Any subsequent authentication attempts within those 5 minutes will result in an error.

> [!TIP]
> It is best practice to look for the "NOAUTH" error_id in your call responses and re-authenticate only after receiving it.

## Object limits

Xandr limits the number of non-expired creatives that you can have on the platform. In addition, Xandr limits the number of domains that can be used in a single domain list and the number of certain targets that can be used in a single profile. For all object types except creatives, both active and inactive objects are counted against the limit. For creatives, only non-expired objects are counted against the limit. A creative expires when it has neither served nor been modified in 45 days.

> [!TIP]
> You can use the [Object Limit Service](object-limit-service.md) to view your limits and proactively monitor your usage. Also, for frequently asked questions about object limits, see [Object Limits - FAQ](object-limits---faq.md).
