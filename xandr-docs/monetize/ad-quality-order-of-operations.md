---
title: Ad Quality Order of Operations
description: In this article, learn about the process by which the Microsoft Advertising system finds a collection of ad quality settings to apply to an impression.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Ad quality order of operations

In every auction, our system must decide which collection of ad quality settings it will apply to the impression up for bid. This document describes the steps our system goes through to find a collection of ad quality settings to apply to an impression.

## Step 1. Check for publisher base and conditional rules

Base and conditional rules allow you to dynamically determine which collection of ad quality settings (i.e., Publisher Template or Custom Profile) you would like to apply to a particular impression based on attributes such as creative size, placement, or user frequency.

If any Publisher Base and Conditional Rules are associated with this publisher, they are checked against the impression in priority order. If a match is found, the system goes to Step 3 below. Otherwise, it moves on to Step 2.

For more information, see the section on Publisher Base and Conditional Rules in [Working with Ad Quality](working-with-publisher-ad-quality.md), and [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md).

## Step 2. Check for a publisher template or custom profile

If the publisher has an associated Publisher Template or Custom Profile, then the settings from that template or profile are applied. For more information, see [Create a Publisher Template](create-a-publisher-template.md) or [Create a Custom Profile](create-a-custom-profile.md).

The system goes to Step 3 to find out whether such a template or profile is defined or not.

## Step 3. Apply the network profile

Finally, if a collection of publisher ad quality rules is selected during Steps 1 and 2, it is applied in addition to the Network Profile. If no publisher rules or templates were applied, the system defaults to using only the ad quality settings defined in the Network Profile. For more information, see [Update Your Network Profile](update-your-network-profile.md).

> [!NOTE]
> Only one collection of publisher ad quality settings (from Step 1 or Step 2) is selected and applied in addition to the settings defined by the Network Profile.

## Related topics

- [Working with Ad Quality](working-with-publisher-ad-quality.md)
- [Explore Publisher Ad Quality](explore-publisher-ad-quality.md)
- [Network Ad Quality Screen](network-ad-quality-screen.md)
- [Update Your Network Profile](update-your-network-profile.md)
- [Create a Publisher Template](create-a-publisher-template.md)
- [Create a Custom Profile](create-a-custom-profile.md)
- [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md)
- [Base and Conditional Rules](base-and-conditional-rules.md)
