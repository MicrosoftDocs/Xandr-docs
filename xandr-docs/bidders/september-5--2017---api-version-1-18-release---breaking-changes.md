---
title: September 5, 2017 - API Version 1.18 Release - Breaking Changes
description: This page announces the release of version 1.18 of the AppNexus Imp Bus API and the breaking changes.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# September 5, 2017 - API version 1.18 release - Breaking changes

We are pleased to announce the release of version 1.18 of the AppNexus Imp Bus API.  

> [!WARNING]
> ImpBus API
>
> In addition to new features, this release includes breaking changes. We will therefore support two versions of the API for the next 60 days, as stated in our [Breaking Changes](breaking-changes.md) policy. The changeover date is **November 13, 2017**.
>
> **Version 1.17**: This version **does not** include breaking changes. The `https://api.adnxs.com` endpoint will continue to point to version 1.17 for 60 days. After that time, this endpoint will point to version 1.18. 
>
> **Version 1.18**: This version **does** include breaking changes and new features. For the next 60 days, to use this version, you must point directly to it in your calls, e.g., `https://api.adnxs.com/v1.18`.

## Authentication and security changes

**dbg, dbg_info, and X-Rate-Limits Header**

As of version 1.18, the `dbg` and `dbg_info` output in API responses is being deprecated. Instead, [rate limit information ](api-usage-constraints.md) can be found in the headers of the API responses. All older `X-Ratelimit` headers are being replaced with a single `X-Rate-Limits` header that has the following structure:

Rate limit information has three dimensions:

- **Count vs Limit:** whether the value is the current count or the total limit
- **Read vs Write:** whether the value applies to API reads or writes
- **User vs Member:** whether the value applies to the user ID or the member seat associated with it

Each value has an attribute from each dimension, resulting in eight total combinations:

- `cru`: the count for user reads
- `crm`: the count for member reads
- `cwu`: the count for user writes
- `cwm`: the count for member writes
- `lru`: the limit for user reads
- `lrm`: the limit for member reads
- `lwu`: the limit for user writes
- `lwm`: the limit for member writes

These will appear as a single header value composed of key-value pairs. For example:

``` 
X-Rate-Limits: cru=1;crm=1;cwu=1;cwm=1;lru=100;lrm=100;lwu=60;lwm=60
```

We offer this information for troubleshooting purposes, but you should **not** attempt to parse the `X-Rate-Limits` header to use the counts and limits for retry logic. Instead, use the HTTP status 429 as the indication that you need to pause and retry and use the `Retry-After` header to determine the number of seconds you should wait before trying again. This will allow you to take advantage of the opportunity to exceed your rate limits when our platform has the free capacity to handle your API calls.

**HTTPS authentication**

For your security, all production and test API access should be performed over HTTPS. Currently, authentication over HTTPS is possible but not required. As of Version 1.18, if authentication is attempted over HTTP, AppNexus will return an HTTP 308 response redirecting queries to HTTPS.

Our ultimate goal is for all our clients to authenticate and access the API using HTTPS only. In order to minimize disruption during this transition, we still support access to other API services over HTTP once you authenticate with HTTPS. However, we strongly recommend that you switch to using HTTPS in all cases if you're not already doing so.

## Changed services

**Browser Service**

In the [Browser Service](browser-service.md), the `platform_type` field is now deprecated.

**Device Model Service**

The following fields are being deprecated from the [Device Model Service](device-model-service.md):

- `supports_js`
- `supports_cookies`
- `supports_flash`
- `supports_geo`
- `supports_html_video`
- `supports_html_audio`

**Region service**

The field `code` has been deprecated in the [Region Service](region-service.md).

**Tinytag service**

Previously, `default_referrer_url` for the [TinyTag Service](tinytag-service.md) could be set to any value. Going forward, the value must be preregistered before it can be used. To register a new referrer URL, please open a [support ticket](https://help.xandr.com/s/login/).

## Changed reports

**Report service**

As of 1.18, the syntax for the Imp Bus [Region Service](region-service.md) has been updated to match the syntax for the Console [Report Service](report-service.md). Previously, you would specify the report ID after a forward slash. As of 1.18, you should use `?id=REPORT_ID` instead.

For example,  in 1.17, the old command to obtain a report was:

``` 
GET https://api.adnxs.com/report/REPORT_ID
```

In 1.18, the new syntax is:

``` 
GET https://api.adnxs.com/report?id=REPORT_ID
```

Similarly, the deprecated syntax for downloading a report was

``` 
GET https://api.adnxs.com/report-download/REPORT_ID
```

and is now

``` 
GET https://api.adnxs.com/report-download?id=REPORT_ID
```

In the Report Service, buyer_platform_billing will be deprecated.

**Saved report service**

As of 1.18, the syntax for the Imp Bus [Saved Report Service](saved-report-service.md) has been updated to match the syntax for the Console [Saved Report Service](saved-report-service.md). Previously, you would specify the report ID after a forward slash. As of 1.18, you should use `?id=REPORT_ID` instead.

For example, in 1.17, the old command to add a new saved report was:

``` 
GET https://api.adnxs.com/saved-report/REPORT_ID
```

In 1.18, the new syntax is

``` 
GET https://api.adnxs.com/saved-report?id=REPORT_ID
```
