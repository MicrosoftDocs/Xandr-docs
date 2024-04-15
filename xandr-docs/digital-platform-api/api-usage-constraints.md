---
title: Digital Platform API - API Usage Constraints
description: Learn about the constraints in API usage.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - API usage constraints

This article provides information about the constraints faced whilst using the APIs.

## Throttling

To prevent abuse of the API services, a rate limit is enforced for each service. The specific rate limit will depend on the endpoint being called by a user. This approach differs from the previous rate limiting, which focused on client limits. These limits are adjusted over time, so specific details are not provided. However, the rate-limited response will provide the necessary information to adjust your calls or scripts accordingly.

If you exceed the throttling limit, the API will respond with either the HTTP 429 (Too Many Requests – indicating you've made too many calls to this service) or the HTTP 503 (Service Unavailable – meaning the service is overwhelmed with requests and can't take more) response code. It will also provide relevant headers to help you understand why this happened and what to do next.

## Rate limit headers

When you receive a 429 error, it indicates that the request was rate-limited. For a 503 response, you'll need to check the headers to confirm if it was due to rate limiting. Look for the first listed header below, which signals that the 503 was caused by rate limiting.

1. `x-ratelimit-code`: This corresponds to the HTTP code returned when the call was rate-limited.
     1. A 429 indicates that the user has exceeded the per-user limit set by the service.
     1. A 503 indicates that the service is enforcing a rate limit based on total calls at that time.
     1. For both codes, a 'retry-after' header is included to specify when to attempt the request again.
1. `retry-after`: time in seconds to wait before retrying the request.
1. `x-ratelimit-count`: This shows the total number of calls the user has made within the limit period. Users can use this information to adjust call patterns when they encounter rate-limited requests.
     1. This header is included only if the status code is 429.

### Error messages

If you exceed the throttling limit, the API will respond with the HTTP 429 (Too Many Requests) response code.

If you're using a script, you should check for the 429 response code. If you receive this code, sleep your script for the number returned in the `Retry-After` field of the response header. This field tells you how long before your throttle limit is reset and you can continue processing API commands.

### 429 error header

```
< HTTP/1.1 429 Too Many Requests
< Server: nginx/1.11.10
< Date: Fri, 02 Feb 2018 15:58:18 GMT
< Content-Type: application/json; charset=utf-8
< Content-Length: 358
< Connection: keep-alive
< Retry-After: 9
< X-AN-RequestId: 9f53184f6e2c3cb9
< X-Count-Read: user:113,member:113,serviceHostUser:113,serviceHostMember:113,hostUser:113,hostMember:113,ip:0
< X-Count-Write: user:0,member:0,serviceHostUser:0,serviceHostMember:0,hostUser:0,hostMember:0,ip:0
< X-Rate-Limits: cru=113;crm=113;cwu=0;cwm=0;lru=1000;lrm=1000;lwu=60;lwm=60
< X-Ratelimit-Read: 1000
< X-Ratelimit-System: 1000-Default
< X-Ratelimit-Write: 60
```

### Debug parameter

In addition to the response code and response header, every response from the API will contain a `dbg_info` parameter. This parameter contains information about the API call and response. Below is an example of this debug output, which includes any warnings received from the API, the API version used for the call that generated this response, and the service used.

```
{
  "response": {
    "status": "OK",
    ...
    "dbg_info": {
      "warnings": [],
      "version": "1.18.349",
      "output_term": "user"
    }
  }
  }
```

### Pagination

The maximum number of objects that can be returned in a given GET response is 100. To retrieve more than 100 objects, you can paginate results by specifying `start_element` and `num_elements` in the query string of the GET request. For example, the following request would return the first 50 objects in the response:

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative?start_element=0&num_elements=50'
```

To retrieve the next 50, you would simply set `start_element=50`.

- The first element is element 0.
- All GET responses will have a "count" property showing the total number of elements matching that GET request.
- This will also apply to non-reporting services, such as the creative search service, that are requested with methods other than GETs.

### Example

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/segment?start_element=0&num_elements=100'
$ curl -b cookies -c cookies 'https://api.appnexus.com/user?start_element=0&num_elements=100'
```

## Authentication frequency

After authenticating, your token remains valid for 2 hours. You do not need to re-authenticate within this time. If you do re-authenticate, please note the following limitation: The API permits you to authenticate successfully 10 times per 5-minute period. Any subsequent authentication attempts within those 5 minutes will result in an error.

> [!TIP]
> It is best practice to listen for the "NOAUTH" error_id in your call responses and re-authenticate only after receiving it.

## Object limits

Xandr limits the number of line items, campaigns, creatives, publishers, sites, and placements that you can have on the platform. In addition, Xandr limits the number of domains that can be used in a single domain list and the number of certain targets that can be used in a single profile. You can use the [Object Limit Service](./object-limit-service.md) to view your limits and proactively monitor your usage.

> [!TIP]
> For all object types except creatives, both active and inactive objects are counted against the limit. For creatives, only non-expired objects are counted against the limit. A creative expires when it has neither served nor been modified in 45 days.

For most clients, the default object limits are as follows:

| Object | Limit |
|:---|:---|
| Creatives per member<br><br>**Note**: Only non-expired creatives are counted against this limit. | 10,000 |
| Campaigns per member | 10,000 |
| Line items per member | 3,000 |
| Placements per member | 20,000 |
| Sites per member | 10,000 |
| Publishers per member | 3,000 |
| Domains per domain list | 30,000 |
| Segments targeted per profile | 400 |
| Segment groups targeted per profile | 400 |
| Content categories targeted per profile | 300 |
| Platform content categories targeted per profile | 300 |
| Postal codes targeted per profile | 4000 |
| Inventory sources targeted per profile | **Deprecated** |
| Publishers targeted per profile | 300 |
| Placement Groups targeted per profile | 100 |
| Placements targeted per profile | 250 |
| Deals targeted per member (note: only deals with profiles are counted against this limit) | 1000 |
| Profiles targeted per member | 100 |

### FAQs

#### How will I know that I am approaching my limit for an object?

We send you an email notification when you reach 85% and 95% of your limit for an object and another email when you reach 100% of your limit.

#### Who receives object limit email notifications?

Object limit notification emails are sent to the email addresses specified in the `sherlock_notify_email` field of the [Member Service](./member-service.md). You can change the recipients at any time. Note, however, that this field controls the recipients for creative auditing emails as well.

#### What if I reach my limit for an object?

When you approach or reach your limit for campaigns, line items, placements, sites, or publishers, you should delete any inactive, unused, or unnecessary instances so you can stay under your limit. Deleted line items, campaigns, creatives, publishers, sites, and placements will continue to appear in reporting but cannot be undeleted.

When you approach or reach your limit for creatives, you should remove non-expired creatives. Non-expired creatives have the `is_expired` field set to `false`. Note that removing expired creatives will not impact your creative count.

#### What if I am already over my limit?

If you need to create additional objects but have already met or exceeded your limit as listed above, please delete unused objects or contact support for assistance. Our support team can help you identify inactive objects to delete.

#### Can my limit be raised?

In exceptional cases, a limit may be temporarily lifted by a small amount at the discretion of our engineering team. Please contact your Xandr representative to discuss this option.
