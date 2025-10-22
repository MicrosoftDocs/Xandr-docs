---
title: Throttling Pagination and Filtering
description: In this article, learn about the concepts such as, Throttling, Pagination, and Filtering, accompanied by examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Throttling Pagination and Filtering

## Throttling

To prevent abuse of the API services, a rate limit is enforced for each service. The specific rate limit will depend on the endpoint being called by a user. This approach differs from the previous rate limiting, which focused on client limits. These limits are adjusted over time, so specific details are not provided. However, the rate-limited response will provide the necessary information to adjust your calls or scripts accordingly.

If you exceed the throttling limit, the API will respond with either the HTTP 429 (Too Many Requests – indicating the user has made too many calls to this service) or the HTTP 503 (Service Unavailable – meaning the service is overwhelmed with requests and can't take more) response code. It will also provide relevant headers to help you understand why this happened and what to do next.

## Rate limit headers

When you receive a 429 error, it indicates that the request was rate-limited. For a 503 response, you'll need to check the headers to confirm if it was due to rate limiting. Look for the first listed header below, which signals that the 503 was caused by rate limiting.

1. `x-ratelimit-code`: This corresponds to the HTTP code returned when the call was rate-limited.
     1. A 429 indicates that the user has exceeded the per-user limit set by the service.
     1. A 503 indicates that the service is enforcing a rate limit based on total calls at that time.
     1. For both codes, a 'retry-after' header is included to specify when to attempt the request again.
1. `retry-after`: This shows the time in seconds to wait before retrying the request.
1. `x-ratelimit-count`: This shows the total number of calls the user has made within the limit period. Users can use this information to adjust call patterns when they encounter rate-limited requests.
     1. This header is included only if the status code is 429.

## Pagination

The API limits responses to any request to 100 objects. Pagination will allow you to use multiple requests to retrieve more than 100 objects in total, though each single request is still limited to 100 objects. This is accomplished by using the `start_element` and `num_elements` querystring parameters. In the below example, we use multiple HTTP `GET` calls to retrieve many creatives.

> [!NOTE]
> The output has been abbreviated to save space.

### Pagination: Example

```
$ curl -c cookies -b cookies 'https://api.appnexus.com/creative?start_element=0&num_elements=100'
{
  "response": {
    "status": "OK",
    "creatives": [...],
    "count": 203151,
    "start_element": 0,
    "num_elements": 100
  }
}
$ curl -c cookies -b cookies 'https://api.appnexus.com/creative?start_element=100&num_elements=100'
{
  "response": {
    "status": "OK",
    "creatives": [...],
    "count": 203151,
    "start_element": 100,
    "num_elements": 100
  }
}
$ curl -c cookies -b cookies 'https://api.appnexus.com/creative?start_element=200&num_elements=100'
{
  "response": {
    "status": "OK",
    "creatives": [...],
    "count": 203151,
    "start_element": 200,
    "num_elements": 100
  }
}
```

## Filtering

Filtering allows you to specify a subset of objects to be returned by the API. The most common, and arguably most useful filter is `min_last_modified`, which only returns objects that have been changed since the date specified. In the example below, we use filtering in an API `GET` request to return only those creatives modified after 05/14/2013 00:00:00 UTC.

> [!NOTE]
> The output of the API call has been abbreviated to save space.

### Filtering: Example

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative?min_last_modified=2013-05-14+00:00:00'
{
  "response": {
    "status": "OK",
    "creatives": [
      {
        "id": 298390,
        "last_modified": "2011-07-13 16:08:32",
        ...
      },
      {
        "id": 298391,
        "last_modified": "2011-07-13 16:08:32",
        ...
      },
      {
        "id": 317677,
        "last_modified": "2011-07-13 04:44:04",
        ...
      },
      {
        "id": 317678,
        "last_modified": "2011-07-13 04:12:57",
        ...
      },
      {
        "id": 328516,
        "last_modified": "2011-07-13 18:18:21",
        ...
      },
      {
        "id": 328531,
        "last_modified": "2011-07-13 18:57:12",
        ...
      }
    ],
    "count": 1740,
    "start_element": 0,
    "num_elements": 6
  }
}
```
