---
title: Microsoft Monetize - Mobile User Segment Targeting
description: This page covers three methods for creating mobile in-app user segments on Microsoft Advertising along with best practices and limitations of targeting mobile users.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Mobile user segment targeting

> [!NOTE]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

This page offers tips and recommendations for how to use and create Microsoft Advertising segments for mobile users. Because traditional cookies are not used in in-app mobile inventory, segment targeting relies on different processes. In the sections below, you can learn about targeting in-app mobile users and the limitations of this kind of targeting.

## How to create segments of mobile users on Microsoft Advertising

There are three methods for creating mobile in-app user segments on Microsoft Advertising:

### Method 1: Add users who view or click on a creative to a segment

- When uploading a creative, you can choose to add users to a segment "on-view" or "on-click." This functionality works the exact same way in mobile and display. You can read more on this in [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

### Method 2: Add users who have converted on mobile offers using reporting and batch segment service\*

- Using the Log-Level Data Feed, you can gather the list of Microsoft Advertising User IDs for users who have converted on your account.
- Once you have your list of user IDs, you can load them into segments using the [Batch Segment Service](../digital-platform-api/batch-segment-service.md).
- This will be a standard batch segment upload.

\*Requires API access and [Batch Segment Service](../digital-platform-api/batch-segment-service.md).

### Method 3: Use the batch segment service to upload your own list of device IDs\*

- If you have a list of device IDs gathered from your advertisers or external attribution tracking system, you can also add these to segments using the [Batch Segment Service](../digital-platform-api/batch-segment-service.md).
- Be sure to use [SEPARATOR5](../digital-platform-api/bss-avro-file-format.md) to designate that you will be uploading device IDs and instead of the standard Microsoft Advertising user IDs.

\*Requires API access and [Batch Segment Service](../digital-platform-api/batch-segment-service.md).

## Best practices for targeting mobile users

While the same best practices for targeting users in display are also relevant for mobile, there are two best practices that are particularly important to consider when targeting mobile users:

1. Avoid mixing mobile web and mobile in-app buying in the same campaign
    - Separating these campaigns will keep your user groups separate. This, in turn, ensures you will gain access to the users and supply you intend in your campaign setup.
    - While there are many differences between mobile web-optimized and mobile in-app traffic, the most important to remember for targeting is that web-optimized traffic tracks users with cookies while in-app traffic tracks device IDs with Microsoft Advertising user IDs mapped to them.
1. Limit additional campaign targeting
    - Because of the additional technical complications that come with tracking mobile users, it is important to limit additional targeting on these campaigns as much as possible for optimal reach. For more information, see [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md).

## Limitations for mobile user targeting

While mobile user targeting is a helpful tool to reach mobile users you want to connect with, there is a limitation:

- Our current mobile SSP integrations do not cookie sync on mobile web inventory for Safari, making it impossible to target users. Mobile in-app supply is not affected by this limitation as users are identified by device-IDs.
