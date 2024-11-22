---
title: Microsoft Curate - Universal Pixel Audiences and Conversions
description: Learn about universal pixel audiences and conversions. The universal pixel allows for setting up specific audiences and conversions based on complex rules. 
ms.date: 11/16/2023
---

# Microsoft Curate - Universal Pixel audiences and conversions

After you have set up standard or custom event tracking, you can use the data you collect to identify audiences and conversions.

An **audience**, or audience segment, consists of a collection of users who have interacted on a website in a similar way. After you have one or more audiences configured, you can target the audience from a line item. A **conversion** is a specific type of interaction that indicates the successful downstream effects of an ad campaign.

The Universal Pixel lets you set up highly specific audiences and conversions based on complex rules. Rules combine one or more **conditions** to determine what user interactions you will use to create the event or conversion. These conditions can be based on the URLs, standard events, and parameters your pixel is tracking. For example, you might determine that a user who has selected an offer, viewed three or more TVs, and accessed product details for a TV that cost over $1000 should be added to an audience segment called High-End TV Buyers.

You combine conditions using the Boolean AND and OR operators to identify highly specific audiences or conversion criteria. The data you have already collected using events and parameters will guide the way you create rules.

> [!NOTE]
> A rule can either have all conditions joined by AND operators or all conditions joined by OR operators. You can’t combine AND and OR in the same ruleset.

## Related topics

- [Set Up Audiences with Universal Pixel](./set-up-audiences-with-universal-pixel.md)
- [Set Up Conversions with Universal Pixel](./set-up-conversions-with-universal-pixel.md)
- [Universal Pixel Log-Level Data](../log-level-data/universal-pixel-feed.md)
