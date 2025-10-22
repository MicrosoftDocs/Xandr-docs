---
title: August 14, 2015 - Batch Segment Service Breaking Changes
description: Find the release notes for the breaking changes made to the Batch Segment Service.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# August 14, 2015 - Batch segment service breaking changes

We are making several breaking changes to the [Batch Segment Service](batch-segment-service.md).

These changes will take place 60 days from today, on **October 7th, 2015**.

Specifically, we are:

- Reducing the number of objects we return when you ask for your file upload history (via the `batch_segment_upload_job` field) to the last 30 days’ worth.
- Changing the API response to return secure (SSL-encrypted) upload URLs via the `upload_url` field.
- Limiting file upload sizes to 0.5 GB.

For more information about what constitutes a breaking change, please see our [Breaking Changes Policy](breaking-changes.md). If you have any questions about this change, please reach out to your AppNexus representative.
