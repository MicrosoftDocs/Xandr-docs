---
title: Managing seed segments 
description: Modeled Audiences is a new feature available for Microsoft Curate that allows curators to take their first-party segments and expand them to similar users for targeting.
ms.date: 09/16/2025
ms.author: shsrinivasan
---

# Managing seed segments 

Only first-party segments can be used as seed segments with Modeled Audiences. You can create first-party segments in a number of ways: 
- Create an audience segment directly in your Curate member. You can populate this segment with users via the Batch Segment Service. See [Create a segment pixel](create-a-segment-pixel.md) and [Digital Platform API - Batch Segment Service](../digital-platform-api/batch-segment-service.md).
- Create a Universal Pixel. You can export this Universal Pixel as a Javascript tag which you can place on your website to construct audiences. See [Microsoft Curate - Universal Pixel](the-universal-pixel.md) for more information. Universal Pixels you create directly in your Curate member as well as Universal Pixels you share to your Curate member using the Batch Segment Service are considered first-party. 
- Partner with a Data Management Platform (DMP) to onboard your audience segments. The DMP will need to use the [Segment API service](../digital-platform-api/segment-service.md) to set your segment’s `object_type to first-party`. Please reach out to your DMP account representative to confirm this setting has been configured. 

> [!NOTE]
> - Some customers use multiple members on the Microsoft Advertising platform. For example, you might use one member to upload and manage your first-party audience segments using the [Digital Platform API - Batch Segment Service](../digital-platform-api/batch-segment-service.md), and share those segments with your Curate member using the [Member Data Sharing Service](../data-providers/member-data-sharing-service.md). 
- If you use this setup, you can update your first-party audience segments using the [Segment API service](../digital-platform-api/segment-service.md) and set their object_type to first-party. This will make them eligible as seed segments for modeling in your Curate member. 