---
title: Working with Network Ad Quality
description: Explore managing ad quality, set rules for creative attributes, size, or user session frequency to control inventory display. Reduce characters.
ms.date: 10/28/2023
---

# Working with network ad quality

Ad quality settings allow sellers to determine which creatives will be allowed to serve on their inventory. These rules are applied based on attributes of the creative such as the buyer or brand. Sellers may also determine which rules to apply based on other information about the impression such as the size of the creative or the user's session
frequency.

This document provides an overview of the ad quality settings that can be configured by network administrator users. For more information about the configuration options available to publisher users, see [Working with Ad Quality](working-with-publisher-ad-quality.md).

> [!IMPORTANT]
> For comprehensive information about our quality standards for creatives, see [Creative Standards](creative-standards.md).

## Network profiles

A *Network Profile* is a collection of ad quality settings that is created by a network administrator. These settings are applied to every impression across all publishers associated with a network. As a result, publisher-level settings may only be more strict than the Network Profile, never less; restrictions set in Network Profiles cannot be loosened at the publisher level. For example, if an outside network's demand (Let's call it Network **X**) is banned by the Network Profile, and then a publisher's Publisher Template or Custom Profile is updated with a rule enabling creatives from Network **X**, those creatives will still be banned from serving on that publisher's inventory.

For more information, see [Update Your Network Profile](update-your-network-profile.md).

## Publisher templates

A Publisher Template, like a Network Profile, is a collection of ad quality settings. Publisher Templates ease publisher creation and set-up by allowing a network administrator to define common ad quality settings for a number of publishers at once. When a template is edited, all publishers using that template will inherit the updated settings. Use a Publisher Template if you want to maintain a group of publishers' ad quality settings together. Note that associating a publisher with a Publisher Template is strictly optional.

For more information, see [Create a Publisher Template](create-a-publisher-template.md).

## In this section

- [Network Ad Quality Screen](network-ad-quality-screen.md): A description of the screen elements and what they do.
- [Update Your Network Profile](update-your-network-profile.md): Determine ad quality settings for all the
  impressions across your network.
- [Create a Publisher Template](create-a-publisher-template.md): Create a collection of ad quality settings that
  can be reused across multiple publishers.
- [Ad Quality Order of Operations](ad-quality-order-of-operations.md): How our system decides what ad quality
  settings to apply to each impression.
- [Opt Out of Gambling Ads](opt-out-of-gambling-ads.md): What to do if you don't want gambling ads to run on your
  inventory.

## Related topic

[Working with Ad Quality](working-with-publisher-ad-quality.md)