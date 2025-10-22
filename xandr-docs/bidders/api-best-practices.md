---
title: Bidders - API Best Practices
description: In this article, find information on the best practices for using the API services to build and integrate your bidder.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# API best practices

We're thrilled that you're taking advantage of our platform by grabbing raw data, hooking in your own pieces of the ad serving puzzle, or otherwise building on top of our infrastructure. Follow the best practices to make sure you have the best experience possible, and to keep your applications healthy as our API evolves. Stay in touch with your implementation consultant as you get started building.

## Filter your results

Filtering allows you to specify a subset of objects to be returned. For example, the following call would return only active creatives:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?active=true'
```

For fields of the type int, double, date, or money, you can append `min_` or `max_` to the filter. For example, the following request would return only campaigns that have been modified on or after January 1, 2013:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?min_last_modified=2013-01-01 00:00:00'
```

> [!NOTE]
> For each service, you can find out which fields are filterable and sortable by appending `/meta` to the service URL. For more information, see [API Semantics](api-semantics.md).

## Paginate your results

Even though you might only have 5 creatives in the system now, you should still write your application in a way that it takes advantage of the pagination support since this number is likely to increase in the future. You can paginate results by specifying `start_element` and `num_elements` in the query string of the GET request. For example, the following request would return the first 50 objects in the response:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative?start_element=0&num_elements=50'
```

To retrieve the next 50, you would simply set `start_element=50`.

> [!NOTE]
> The maximum number of objects that can be returned, regardless of pagination, is 100. Please note that if you request over 100 objects, we will only return the first 100 and will not provide an error message. For more information, refer to the [API Semantics](api-semantics.md) page.

## Throttle your calls

There are limits to the number of requests you can make against our APIs per minute. We categorize these limits into read and write rate limits. Currently, the default read and write limit is 1000 per minute. These counters will reset at the end of the minute, but if you exceed the throttling limit, the API will respond with the **HTTP 429 (Too Many Requests)** response code. Retry the request in the number of seconds specified in the `Retry-After` field in the header.

There is also a concurrent request limit of 20 requests at a time. More than this limit will return an **HTTP 200**, but with an **error payload**.

Below is an example of the header values in response to a request that exceeded a member's rate limit.

```
HTTP/1.1 429 Too Many Requests
Content-Type: application/json; charset=utf-8
Retry-After: 16
X-AN-RequestId: 98472eb263664a7b
X-Count-Read: user:101,member:101,serviceHostUser:75,serviceHostMember:75,hostUser:101,hostMember:101,ip:0
X-Count-Write: user:0,member:0,serviceHostUser:0,serviceHostMember:0,hostUser:0,hostMember:0,ip:0
X-Ratelimit-Read: 100
X-Ratelimit-System: 100-Default
X-Ratelimit-Write: 60
Content-Length: 358
```

## Pass field values rather than relying on defaults

It's best practice to pass the field values that you want rather than relying on defaults. If default values change and you are relying on defaults, you may experience unexpected results.

## Avoid unnecessary updates

When updating objects, do not pass fields that are not changing. A good way to avoid this is to cache your GET calls, compare the cache to the changes you want to make, and then make PUT calls only for what's different.

## Avoid unnecessary authentication

You can authenticate successfully 10 times within a 5-minute period. Any subsequent authentication attempts within those 5 minutes will result in an error.

> [!NOTE]
> When you authenticate, you receive an authorization token that remains active for 2 hours. It is best practice to re-authenticate only after you receive the `"NOAUTH"` error_id in your call responses. If you follow this practice, the restraint above should have no impact on your implementation.

For authentication instructions, see [Authentication Service](authentication-service.md).

## Use a config-driven API end-point

Make sure that you can change the API base URL easily. In the example below, the API URL is defined as a variable and can be used throughout the code base. If that URL should ever need to change, it can be modified in a single location.

```
$config = "https://api..com";
```

## Build an API wrapper

Centralizing the code where you send requests and handle responses is a great practice. This will allow you to do logging, error handling and more in one location.

## Do not pull all reports at the same time

This can cause the reporting backend to be overloaded, resulting in delayed reports, and can even impact reports that are run later in the day.

## Read the entire API Wiki before using the API

There are many tips, tricks, and examples throughout the API Wiki that will be useful in developing your integration.

## Use integration codes

Rather than store Xandr IDs, you can use the integration codes to refer to object in the API. These codes must be unique across an object type and Xandr member. The example below uses an integration code to identify a campaign.

```
"creative":{
                "id":6,
                "active":true,
                "member_id": 5,
                "code": your_internal_code
}
```

## Do not assume an API call was successful

All successful API calls will receive a response containing a `"status"` of `"OK"`. If the response does not contain this status, the call failed for some reason. If the `"status"` is `"error"`, an error message will be included in the response. Below is an example of a successful response.

```
{
   "response": {
      "status": "OK",
      "campaign": {
         ...
      }
   }
}
```

## Allow for additional fields on responses

As our API team implements new features, it is necessary to include new fields on various API services. Your integration should be flexible enough to handle additional fields on each service that were not previously returned.

## Be aware of breaking changes

Our services change continually as we add new features, but we do our best to create stability so that the applications our clients build on top of our API can adapt gracefully as well.

When we introduce a breaking change, we will support two versions of the API in production, one with and one without the breaking change, for 60 days. We will announce these changes in our API Release Notes. For more details about what constitutes a breaking change, see our [Breaking Changes](breaking-changes.md) policy.

## Be mindful of object limits

Xandr limits the number of objects each member can create and use on the platform. This limit includes inactive and unused objects (e.g. campaigns set to inactive status, placements that have never served an impression, etc.). You should use the [Object Limit Service](../digital-platform-api/object-limit-service.md) to view your limits and proactively monitor your usage.
