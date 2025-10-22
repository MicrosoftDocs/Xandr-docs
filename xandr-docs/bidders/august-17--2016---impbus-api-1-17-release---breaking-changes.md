---
title: August 17, 2016 - ImpBus API 1.17 Release - Breaking Changes
description: Find release notes for AppNexus ImpBus API version 1.17 and the breaking changes introduced in this version.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# August 17, 2016 - ImpBus API 1.17 release - Breaking changes

We are pleased to announce the release of version 1.17 of the AppNexus ImpBus API.

> [!WARNING]
> In addition to new features, this release includes breaking changes. We will therefore support two versions of the API for the next 60 days, as stated in our [Breaking Changes Policy](breaking-changes.md). The changeover date is **October 17, 2016**.
>
> **Version 1.16**: This version **does not** include breaking changes. The `https://api.adnxs.com` endpoint will continue to point to
> version 1.16 for 60 days. After that time, this endpoint will point to
> version 1.17.
>
> **Version 1.17**: This version **does** include breaking changes and new features. For the next 60 days, to use this version, you must point directly to it in your calls, e.g., `https://api.adnxs.com/v1.17`.

## Breaking changes

All of the changes described in this section are only present in version 1.17.

### Endpoint changes

We are discontinuing the endpoints for versions `https://api.adnxs.com/v1.14` and `https://api.adnxs.com/v1.15`.

> [!NOTE]
> Despite the names, these endpoints already point to version 1.16.

### Changed services

#### Authentication service

The [Authentication Service](authentication-service.md) no longer supports the GET method for user name and password. Use the POST method instead.

#### Creative service

The following changes are being made to the [Creative Service](creative-service.md):

- The `status` object has been added to specify how the creative is hosted and whether the creative is ready to serve or not. `user_ready` specifies whether the creative is ready to serve to users. Possible values are `"true"` or `"false"`.

    `hosted_assets_association_complete` (read-only) specifies the status of the creative uploaded by AppNexus' internal systems. Possible values are `"true"` or `"false"` for hosted creatives, `"null"` for third-party creatives.
- The following fields are now read-only:
  - The `adservers` field, which specifies the ad servers that deliver the creative or that are called for data collection purposes during the delivery of the creative.
  - The `active` field, which specifies the state of the creative. Possible values are `"true"` or `"false"`.
- The following fields are being removed:
  - `google_audit_feedback`
  - `google_audit_status`
  - `msft_audit_status`
  - `msft_audit_feedback`
  - `msft_external_audit_status`
  - `msft_external_audit_feedback`

    `Google_audit_feedback` and `google_audit_status` have been replaced by `adx_audit`, a read-only object that contains information about the status and feedback related to the Google AdExchange audit of the creative.

#### Creative template service

The [Creative Template Service](creative-template-service.md) no longer supports the `content_xml` field.

#### Deprecated reporting dimensions

Currently, several reports include dimensions that are concatenations of the object ID and object name fields. For example, the Network Analytics report includes the dimension `advertiser`, which is a concatenation of `advertiser_ID` and `advertiser_name`. These concatenated fields are being deprecated as redundant. The individual component fields (ID and name) will remain. In the given example, there will no longer be an `advertiser` reporting dimension, but you can still use `advertiser_ID` and `advertiser_name`.

#### Buyer platform billing

The following fields are being eliminated from the [Bidder Billing Report API](bidder-billing-report-api.md):

- `bidder`
- `buyer_member`
- `publisher`
- `seller_member`

#### Platform buyer

The following fields are being eliminated from the [Bidder Platform Buyer Report](bidder-platform-buyer-report.md):

- `bidder`
- `buyer_member`
- `content_category`
- `creative`
- `publisher`
- `seller_member`
- `site`
- `tag`

#### Platform seller

The following fields are being eliminated from the [Platform Seller Report](platform-seller-report.md):

- `bidder`
- `buyer_member`
- `publisher`
- `seller_member`
- `site`
- `tag` 

#### Seller platform billing

The following fields are being eliminated from the [Seller Platform Billing Report](seller-platform-billing-report.md):

- `bidder`
- `buyer_member`
- `publisher`
- `seller_member`
- `site`

### Changed error messages

#### Authentication expires

If your authentication token has been in continuous use for 24 hours, it will expire. Attempts to connect will be rejected with the status code `401` for an unauthorized connection. Previously, this error produced status code `200 OK`.

#### Rate limits

If you exceed the rate limits specified by the [API Best Practices](api-best-practices.md), the error status returned will be `429` and the number of seconds to wait before retrying will be specified by the `Retry-After` header. Previously, the error returned was status `405`.
