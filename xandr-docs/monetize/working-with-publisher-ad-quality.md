---
title: Working with Ad Quality
description: Explore managing Ad Quality by setting rules for attributes (buyer, brand), size, or session frequency to enhance creative effectiveness.
ms.date: 10/28/2023
---

# Working with Ad quality

Ad quality settings allow sellers to determine which creatives will be allowed to serve on their inventory. These rules are applied based on attributes of the creative such as the buyer or brand. Sellers may also determine which rules to apply based on other information about the impression such as the size of the creative or the user's session
frequency.

This topic provides an overview of the ad quality settings that can be configured by publisher users. For more  information about the configuration options available to network administrator users, see [Working with Network Ad Quality](working-with-network-ad-quality.md).

> [!IMPORTANT]
> For comprehensive information about our quality standards for creatives, see [Creative Standards](creative-standards.md).
> [!NOTE]
> If an Ad Quality (AQ) is set as `default_brand_status:banned` but the parent brand is set as `status:trusted`, the child brand overrides the setting in `default_brand_status` and it will be able to serve unless it is explicitly banned in the Ad Profile's brand override list.

## Reference

[Explore Publisher Ad Quality](explore-publisher-ad-quality.md) - A reference covering the major user interface elements and their functionality.

## How-tos

- [Create a Custom Profile](create-a-custom-profile.md) - Maintain a unique set of ad quality rules for one
  publisher.
- [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md) - Dynamically determine ad quality
  settings for each impression.

## Custom profiles

A Custom Profile creates a new collection of ad quality settings for one publisher. A Custom Profile may use an existing Publisher Template as a starting point; note that future changes to a Publisher Template are not applied to any Custom Profiles that inherit from that template. Use a Custom Profile if you want to maintain unique ad quality rules for one
publisher.

For more information, see [Create a Custom Profile](create-a-custom-profile.md).

## Publisher base and conditional rules

Publisher Base and Conditional Rules give you the ability to dynamically determine which collection of ad quality settings (i.e., Publisher Template or Custom Profile) you would like to apply to a particular impression based on attributes such as creative size, placement, or user frequency. The Base Rule is the publisher rule that is chosen when no
Conditional Rules exist, or when the existing Conditional Rules' targeting requirements are not met by an impression. Only one Base or Conditional Rule from the publisher is chosen in addition to the Network Profile.

For more information, see [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md).

## Related topics

- [Working with Network Ad Quality](working-with-network-ad-quality.md)
- [Explore Publisher Ad Quality](explore-publisher-ad-quality.md)
- [Selling Guide](selling-guide.md)
