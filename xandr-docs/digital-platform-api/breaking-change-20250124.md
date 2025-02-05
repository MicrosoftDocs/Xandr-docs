---
title: January 23, 2025 – Update to Context Array Object in Profile Service API 
description: We are introducing a breaking change to the Outstream Video Targeting options to the Profile service API.
ms.date: 01/23/2025
ms.topic: release-notes
ms.author: shsrinivasan
---

# January 23, 2025 – Update to Context array object in Profile service API 

We are introducing a breaking change to the Outstream Video Targeting options in the [Profile service](profile-service.md) API. This change will take place 60 days from today, on March 24, 2025. 

We are introducing a change to the name field within the `video_targets.context` array object in our API. 
- The possible name value for `Id = 4` within the Context array object is being updated from `Outstream` to `In-Article`. 
- As a part of this change, effective March 24, 2025, to align with industry standards, Line items currently targeting `Outstream Id` 4 will be updated to target the following formats: 
    - In-Article 
    - In-Feed
    - In-Banner, and 
    - Interstitial

Please update your API configurations accordingly to uphold continued compatibility and seamless integration. 

For detailed information, please refer to the [Profile service](profile-service.md) documentation. 

To learn more about breaking changes and their implications, see our [Breaking Changes Policy](breaking-changes.md). If you have any questions or require assistance with this update, please reach out to your account representative or contact [Product Support](https://help.xandr.com/s/login/). 
