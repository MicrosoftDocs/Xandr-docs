---
title: Ad Podding for Publishers
description: In this article, find information on what ad pods are, what video bumpers are, and how to enable ad podding for a placement.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Ad podding for publishers

An ad pod specifies a sequenced group of video ads that are played back-to-back within a single video placement. In traditional television, an ad pod would correlate to a commercial break during an episode. Ad Pods can be scheduled in pre-roll, mid-roll, and post-roll placements, as shown in the following diagram.

:::image type="content" source="media/ad-pod-diagram.png" alt-text="Diagram that shows the different placements of Ad Pods.":::

Ad pods are delivered using VMAP 1.0.1. VMAP is a wrapper for VAST ads. The following diagram shows the structure of a VMAP document.

:::image type="content" source="media/ad-pod-vmap-diagram.png" alt-text="Diagram that shows the structure of a VMAP document.":::

## Video bumpers

Video bumpers are small video ads (usually 3-10 seconds in length) at the very beginning, or at the end of an ad pod. As a Publisher, you will also be able to add bumpers to your video placements. The following diagram shows how bumpers work within an ad pod.

:::image type="content" source="media/bumper-example.png" alt-text="Diagram that shows the working of bumpers in an ad pod.":::

By default, video placements do not have bumpers associated with them. Bumpers must be explicitly added to video placements. As a Publisher, you can set a default creative for bumpers. At this time, only managed campaigns can bid on bumpers.

## API

The `/vmap` endpoint is available for VMAP responses (use `/ssvmap` for server-side requests). `/vmap` is similar to `/ptv`, but the response is VMAP instead of VAST. When using [Prebid Server Premium](prebid-server-premium.md), you can use `/vmap` or `/ssvmap` or, see the documentation for [Long-Form Video Service](../digital-platform-api/long-form-video-service.md).

To enable video placements for ad podding:

- On the placement, make sure that `maximum_number_ads` is greater than `1` and the `max_duration_secs` is greater than `0`.
  
  > [!NOTE]
  > The `max_duration_secs`, `max_num_ads`, and `max_ad_duration` fields do not apply to bumpers.

- If the video context is mid-roll, set the `start_delay_secs` attribute on the placement to greater than `0`.
- Use either the `/vmap` or `/ssvmap` endpoint.

> [!WARNING]
> If you are making a secure call to the `/vmap` endpoint, any ad break placement that does not also support a secure url will be eliminated from the `/vmap` response.
