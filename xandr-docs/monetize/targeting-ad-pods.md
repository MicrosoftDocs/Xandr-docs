---
title: Targeting Ad Pods
description: In this article, learn how to target ad pod slot positions through profiles.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Targeting ad pods

An ad pod specifies a sequenced group of video ads that are played back-to-back within a single video placement. In traditional television, an ad pod would correlate to a commercial break during an episode.

Any video creative with `{{duration_ms}} > 0` can serve on placements that allow ad pods. As an advertiser, you can target the following ad pod slot positions through profiles:

- Intro bumper
- Outro bumper
- First ad pod slot position
- Last ad pod slot position
- Any ad pod slot position

> [!IMPORTANT]
> Ad pod targeting is not currently supported for augmented line items.

## Setting up targeting

To target a position in an ad pod:

1. In the Campaign object, under **Targeting**, click **Edit** next to **Video**.
1. Select the position you want to target. By default, your ad can serve in any position within any pod.

## Competitive exclusion

If you have identified Brand IDs with your creatives or at the advertiser level, competitive exclusion for ad pods applies across all slots and across all pods that are included in a single `/vmap` request. If a publisher sends a separate `/vmap` request for ad pods (one placement per `/vmap` request), competitive exclusion will only apply within the single ad pod.

## Frequency capping

Creatives are not allowed to serve more than once per ad pod. This functionally applies to all creatives and is not configurable. If you want to bypass this functionality, you can create another creative with the exact same content.

Unlike competitive exclusion, which applies across all ad pods in the request, frequency capping only applies within a single ad pod, even if the request has multiple ad pods.
