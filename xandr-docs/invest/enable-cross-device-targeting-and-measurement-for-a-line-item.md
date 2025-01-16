---
title: Microsoft Invest - Enable Cross-Device Targeting and Measurement for a Line Item
description: In this article, learn how to optionally enable the cross-device targeting and measurement feature on a line item to set up actions for individual users across multiple devices.
ms.date: 10/28/2023
---

# Microsoft Invest - Enable cross-device targeting and measurement for a line item

You can optionally enable the cross-device targeting and measurement feature on a line item to apply frequency caps, conversion attribution, and audience targeting settings for individual users across multiple devices.

The **Cross-Device** pull-down menu appears in the **Audience & Location Targeting** section. It is disabled by default.

> [!NOTE]
> Cross-device targeting carries a cost-per-mille (CPM) or cost-per-thousand-impressions charge, which is noted next to the name of the identity provider you select. Microsoft Advertising clears this charge with the data provider, and it is included in your total costs in reporting.
> [!WARNING]
> Cross-device functionality is available to sellers when running line items that purchase inventory from the ad exchange using RTB. It's not available when sellers are running managed campaigns on their own inventory.

For more information about how identity graphs and cross-device targeting works, see [Cross-Device Targeting and Measurement](cross-device-targeting-and-measurement.md).

To enable cross-device tracking and measurement, select the identity graph you want to use to connect users across devices.

- Microsoft Advertising (US + EU) graph to use Microsoft Advertising's information to target and attribute across multiple devices in the U.S. and Europe. Microsoft Advertising  continues to invest in enriching the Microsoft Advertising graph in Europe and the U.S. and to work closely with new market-leading data partners.
  > [!IMPORTANT]
  > European cross device coverage is currently limited to the following key countries or regions:
  > - France
  > - Italy
  > - Germany
  > - United Kingdom
  > - Spain
  > - Switzerland
  > - Austria
  > - Belgium
  > - United Kingdom
  > - Netherlands
  > - Poland
  > - Portugal
  > - Denmark
  > - Norway
  > - Sweden
  > - Finland
  > - Iceland
  > - Ireland

- Tapad (Global excluding EU) graph to use Tapad's information to target and attribute across multiple devices.

When the line item starts running, the selected device graph will be applied for frequency capping purposes, conversion attribution, and audience extension.

> [!NOTE]
> Cross-device audience targeting for CTV devices is now available in the US and EU.

## Related topics

- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Set Up Cross-Device Attribution](set-up-cross-device-attribution.md)
