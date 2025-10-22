---
title: Audit Notify Request
description: In this article, learn what an audit notify request is and the JSON fields associated with this request along with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Audit notify request

An audit notify request will be sent via HTTP POST to the `audit_notify_uri` (specified with the [Bidder Service](bidder-service.md)) for each creative whose audit status has changed.

## JSON fields

Information about the creative will be provided in the following JSON format:

| Field | Scope | Type | Description |
|---|---|---|---|
| `audit_feedback` | some | string | Feedback from our platform auditor, such as why the creative could not be audited. |
| `code` | all | string |  |
| `creative_id` | all | string |  |
| `description` | some | string | Description of the creative as entered by the member that uploaded the creative. |
| `facebook_audit_feedback` | some | string | **Note**: This field is no longer in use. |
| `facebook_audit_status` | some | enum ("approved", "rejected", "pending") | **Note**: This field is no longer in use. |
| `google_audit_feedback` | some | string | Feedback from our platform auditor about why the creative may not have been approved to run on Google Ad Manager. |
| `google_audit_status` | all | enum ("approved", "rejected", "pending") |  |
| `msft_audit_feedback` | some | string | Feedback from our platform auditor about why the creative may not have been approved to run on Microsoft inventory. |
| `msft_audit_status` | all | enum ("approved", "rejected", "pending") |  |
| `new_audit_status` | all | enum ("audited", "rejected", "pending","unauditable") |  |
| `new_brand_id` | some | int | Included if the brand id on the creative is changed. |
| `old_audit_status` | all | enum ("audited", "rejected", "pending","unauditable") |  |
| `old_brand_id` | some | int | Included if the brand id on the creative is changed. |
| `old_facebook_audit_status` | some | enum ("approved", "rejected", "pending") | **Note**: This field is no longer in use. |
| `old_google_audit_status` | some | enum ("approved", "rejected", "pending") |  |
| `old_msft_audit_status` | some | enum ("approved", "rejected", "pending") |  |

## Example

For example, you may receive an audit notify request in the following form:

```
{
   "creative_id":"123",
   "new_audit_status":"audited",
   "old_audit_status":"pending",
   "audit_feedback":"",
   "description":"sample_creative_160x600",
   "google_audit_status":"approved",
   "google_audit_feedback":"",
   "old_google_audit_status":"pending",
   "msft_audit_status":"approved",
   "msft_audit_feedback":"",
   "old_msft_audit_status":"pending",
   "new_brand_id":42
}
```

## Related topic

[Bidder Service](bidder-service.md)
