---
title: Streaming Server-Side Segmentation
description: In this article, learn about the use cases and workflow for streaming server-side segmentation.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Streaming server-side segmentation

> [!NOTE]
> This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.

The Instant Audience Service is a server-side method that streams user data to the Xandr platform, via the API. This is useful if you have real-time audience remodeling requirements.

## Use cases

- **Search or time sensitive retargeting in RTB:** As a buyer or DMP, this service is useful if you like to mimic search retargeting capabilities. As a user enters search keywords, you would receive a signal server-side that triggers a server-side association to the segments. Subsequently, the user will then see ads that are relevant to his or her search. This lets you to capitalize on the immediate relevancy of the content for the user. Subsequently, the user will then see ads that are relevant to his or her search.
- **Page performance sensitive targeting:** This service helps you avoid page load strain and having to increase the pixels on the page when conducting retargeting.
- **Alternative real time audience targeting:** The Instant Audience Service can also be used for transactional retargeting, where user scores are computed based on off-line data or modeling that only requires an additional trigger to have the user added to a segment that you wish to buy against in real time. A concrete example is, based on Clickstream data, a buyer computes score for a user that has browsed three products in the kitchen category of its site and pushes a segment value to Xandr based on this user score to immediately show them an ad for additional kitchen items.
- **De-targeting users who have converted:** This enables you to quickly de-target users who have already converted, in order to use your budget as efficiently as possible.

## Process flow

- **Step 1:** Complete the process described in [User ID Mapping with getUID and mapUID](../monetize/user-id-mapping-with-getuid-and-mapuid.md) in Xandr documentation.
- **Step 2:** Associate individual users to segments using the [Instant Audience Service](../digital-platform-api/instant-audience-service.md).

## Related topics

- [Instant Audience Service](../digital-platform-api/instant-audience-service.md)
- [Check Usage Statistics](../digital-platform-api/check-usage-statistics.md)
