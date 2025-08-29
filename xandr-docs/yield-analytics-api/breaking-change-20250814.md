---
title: August 14, 2025 – Update to Yield Analytics API Service 
description: We are introducing a breaking change to our Audio, Video, and Analytics reports in Yield Analytics API.
ms.date: 08/14/2025
ms.topic: release-notes
ms.author: shsrinivasan
---


# August 14, 2025 – Update to Yield Analytics API service  

We are introducing a breaking change to the Yield Analytics API host configuration service. This change will take effect in 56 days, on October 6, 2025.

As a part of this change:

- We are updating the current API host address endpoint for Yield Analytics from `yieldanalytics.xandr.com` to point to the new host address endpoint `api.appnexus.com/imf`.
- This change will require you to update your application configurations to point to the new host.
- Authentication to the new host will be managed through your Microsoft Monetize credentials.
    - **Existing Microsoft Monetize users:** We have already granted the required access to your existing Monetize account.
    - **Users without Microsoft Monetize accounts:** We have created a Monetize account for you and shared a setup email on July 24, 2025. You must complete the setup using the link in that email to ensure continued access to the API endpoint.

> [!NOTE]
> The [Query Engine Service](query-engine-service.md) is not impacted by this breaking change.

Please update your API configurations accordingly and test your integration to confirm access and functionality to uphold continued compatibility and seamless integration.

To learn more about breaking changes and their implications, see our [Breaking Changes Policy](breaking-changes.md). If you have any questions or require assistance with this update, please reach out to your account representative or contact [Product Support](https://support.ads.microsoft.com/).


