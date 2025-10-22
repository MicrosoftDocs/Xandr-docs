---
title: Digital Platform API - API Best Practices
description: Learn about the best practices while using APIs to keep your applications healthy.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - API best practices

We're thrilled that you're taking advantage of our platform by grabbing raw data, hooking in your own pieces of the ad serving puzzle, or otherwise building on top of our infrastructure. There are a few ground rules that will make sure you have the best experience possible, and keep your applications healthy as our API evolves. Stay in touch with your implementation consultant as you get started building.

## API Dos

**Retrieve only the objects you need.**

### Get multiple objects by ID

Most services support the retrieval of multiple specific objects by ID. To do this, you append a comma-separated list of IDs to the query string. For example, the following request would return only the publishers with the specified IDs.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/publisher?id=2,3,5,8,13,21'
```

### Filter your results

Filtering allows you to specify a subset of objects to be returned. For example, the following call would return only line items that have the `"active"` state:

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?state=active'
```

For fields of the type int, double, date, or money, you can append `min_` or `max_` to the filter. For example, the following request would return only line items that have been modified on or after January 1, 2013.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?min_last_modified=2019-01-01+00:00:00'
```

If your API call returns an error with **"Request failed due to timeout or memory issue"**, you can **append add_mappings=false** to your query parameters. Adding this parameter will only return the top-level API objects, but not their nested children.

For example,

```
$ curl -b cookies -c cookies "https://api.appnexus.com/publisher?id=2,3,5,8,13,21&add_mappings=false"
```

### Paginate your results

You should write your application to take advantage of our pagination support. You can paginate results by specifying `start_element` and `num_elements` in the query string of the `GET` request. For example, the following request would return the first 50 objects in the response:

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative?start_element=0&num_elements=50'
```

To retrieve the next 50, you would simply set `start_element=50`.

> [!TIP]
> The maximum number of objects that can be returned, regardless of pagination, is 100. .
 note that if you request over 100 objects, we will only return the first 100 and will not provide an error message.

### Throttle your calls

There are limits on the number of requests you can make against our APIs per minute. If you exceed the throttling limit, the API will respond with the HTTP 429 (Too Many Requests) response code along with an error message in the response contents. We also return a response header with a `Retry-After` field that specifies the number of seconds to wait before attempting more API calls.

If you make API calls using curl, you can retrieve the response header by including the -v parameter in your request.

```
curl -b cookies -v 'https://api.appnexus.com/advertiser
 
> GET /advertiser HTTP/1.1
> Host: api-test.appnexus.com
> User-Agent: curl/7.43.0
> Accept: */*
...
< Retry-After: 31
< X-Route: /advertiser
< X-Route-Time: 86
...
```

In this case, you can retry your request in 31 seconds (the value of the `Retry-After` field).

If you're calling the API from a script, you should check for the 429 response code when you make your API calls. If you receive this code, sleep for the time returned by the `Retry-After` field of the response header. After sleeping for the specified amount of time, your script can continue on.

There is also a concurrent request limit of 15 requests at a time. More than this limit will return an **http code 200**, but with an **error payload**.

See [API Usage Constraints](./api-usage-constraints.md) for more details on rate limits.

### Update arrays with `"append=true"`

When updating array values with the API, an object's array values will be overwritten with whatever values are provided in the `PUT` request. This is fine if the intended behavior is to clear out an array's values and replace it with your updated data. However, a flag can be used to append data to an array rather than replace it. This is particularly useful when updating very lengthy arrays. The query parameter `append=true` can be added to a `PUT` request to set an update to append mode.

For our example, say that we had a simple Profile Object with the following `country_targets` array:

#### Profile object, before update

```
// Before Append
{
        "profile": {
                "code": "Test Profile",
                "country_targets": [
                {
                  "country": "US",
                  "name": "United States"
            }
          ]
        }
}
```

If we were to use `append=true` in the `PUT` call to update to this object, we could use the following JSON data without fear of overwriting our profile's existing `country_targets` data:

#### JSON update data

```
// Update Object
{
    "profile": {
        "country_targets": [
                        {
                                "country": "GR",
                                "name": "Greece"
                }
        ]
    }
}
```

We would use the following CURL command (replacing \<`profile_ID`\> with the appropriate value).

#### CURL example

```
$ curl -b cookie -c cookie -X PUT -s -d '@json/profile.json' "https://api.appnexus.com/profile?id=<profile_ID>&append=true"
```

As a result. our profile object would be updated to reflect the following:

#### Resulting profile object

```
// After Append
{
        "profile": {
                "code": "Test Profile",
                "country_targets": [
                {
                        "country": "US",
                        "name": "United States"
            },
                        {
                                "country": "GR",
                                "name": "Greece"
                }
        ]
        }
}
```

### Use a config-driven API endpoint

Make sure that you can change the API base URL easily. In the example below, the API URL is defined as a variable and can be used throughout the code base. If that URL should ever need to change, it can be modified in a single location.

```
$config = "https://api.appnexus.com";
```

### Build an API wrapper

Centralizing the code where you send requests and handle responses is a great practice. This will allow you to do logging, error handling and more in one location.

### Keep your reports lean and focused

Here are some tips for preventing your reports from being unnecessarily large or taking a long time to process:

- Shorten the `report_interval` (i.e., from lifetime to last_48_hours)
- Add more higher-level filters (i.e., for a specific publisher, advertiser, line item, etc.)
- Avoid combining granular buy-side and sell-side dimensions (i.e., creative and placement), as this increases the number of rows exponentially. If you need to report on such combinations, consider using [Bulk Reporting Feeds](./bulk-reporting-feeds.md) or [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md).

If you must pull very large reports, use the instructions in [Report Pagination](./report-pagination.md).

### Allow for additional fields on responses

As our API team implements new features, it is necessary to include new fields on various API services. Your integration should be flexible enough to handle additional fields on each service that were not previously returned.

### Be aware of breaking changes

Our services change continually as we add new features, but we do our best to create stability so that the applications our clients build on top of our API can adapt gracefully as well.

When we introduce a breaking change, we will support two versions of the API in production, one with and one without the breaking change, for 60 days. We will announce these changes in our API Release Notes. For more details about what constitutes a breaking change, see our [Breaking Changes policy](./breaking-changes.md).

> [!TIP]
> When two versions of the API are being supported for 60 days, the breaking change will be implemented in the *newer version*.
>
> - In order to access the *current version* (with *no* breaking changes) use a format like:
>   - `https://api.appnexus.com/`
>   - `https://api.appnexus.com/current/`
> - In order to access the *newer version* (with the breaking change features) use a format like:
>   - `https://api.appnexus.com/v1.16/`

### Be mindful of object limits

We limit the number of objects each member can create and use on the platform. This limit includes inactive and unused objects (such as line items set to inactive status, placements that have never served an impression, and so on). You should use the [Object Limit Service](./object-limit-service.md) to view your limits and proactively monitor your usage.

### Be mindful of your process scheduling

If possible, schedule your processes so that they do not overlap with each other. If there is no business need to perform your bulk operations during business hours, try to schedule these processes on off-peak hours so that you maximize your API usage throughout the day. Remember, you are allotted a certain amount of READ and WRITE calls per minute. Try to take advantage of the times at which you are not making any calls to the API so that you have additional headroom at the times that you need it, and prioritize your time-sensitive operations.

## API Don'ts

### Don't assume an API call was successful

All successful API calls will receive a response containing a `"status"` of `"OK"`. If the response does not contain this status, the call failed for some reason. If the `"status"` is `"error"`, an error message will be included in the response. Below is an example of a successful response.

```
{
   "response": {
      "status": "OK",
      "line-item": {
         ...
      }
   }
}
```

### Don't rely on default fields

It's best practice to pass the field values that you want rather than relying on default field values. If default values change, and you are relying on defaults, you may experience unexpected results.

### Don't make unnecessary updates

When updating objects, you can avoid making unnecessary updates by passing only the fields that are changing to the API. A good way to ensure this practice is to cache your `GET` calls, compare the cache to the changes you want to make, and then make `PUT` calls only for what's different.

If you need to update all of the objects in a set - for instance, updating the `cost_cpm` on all placements on a site - you should not iterate through each of the objects blindly making `PUT` calls. Instead, issue a `GET` call to retrieve the current state for each of the objects in your set. Where possible, be sure to use the filtering and sorting functionality documented in [API Semantics](./api-semantics.md) to retrieve only the objects which will need an update. Compare the current state of the returned objects to the desired state, and issue a `PUT` only for those objects which actually require an update.

### Don't authenticate unnecessarily

When you authenticate, your token remains valid for 2 hours. You do not need to re-authenticate within this time. If you do re-authenticate, . note the following limitation: The API permits you to authenticate successfully 10 times per 5-minute period. Any subsequent authentication attempts within those 5 minutes will result in an error.

> [!TIP]
> It is best practice to listen for the `"NOAUTH"` `error_id` in your call responses and re-authenticate only after receiving it.

For authentication instructions, see [Authentication Service](./authentication-service.md).

### Don't pull all reports at the same time

This can cause the reporting backend to be overloaded, resulting in delayed reports, and can even impact reports that are run later in the day. For more information see the **Report Throttling** section of the [Report Service](./report-service.md) page.

### Don't make bulk requests to the reporting service

If your architecture calls for multiple requests from the reporting service per hour or day, investigate higher-level reports with more data to see if you can get the data you need with fewer calls to the API.

For example, if you're requesting hourly reports for all advertisers and publishers in your network, determine if using the [Network Analytics Report](./network-analytics.md) would meet your needs. Consider using it as an alternative to making individual requests for [Advertiser Analytics](./advertiser-analytics.md) or [Publisher Analytics](./publisher-analytics.md) reports, ensuring a better match with your use case.

For more information on all of the available reports and their fields, see the API documentation on the [Reporting Service](./report-service.md).

> [!TIP]
> If you find that higher level reports do not fulfill your needs, consider making use of the [Bulk Reporting Feeds](./bulk-reporting-feeds.md) or [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md).
