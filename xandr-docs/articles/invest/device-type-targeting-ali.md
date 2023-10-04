---
title: Microsoft Invest - Device Type Targeting
description: In this article, learn about device type targeting, which focuses on delivering ads to specific device categories, such as smartphones, tablets, desktop computers, or smart TVs.
---

# Microsoft Invest - Device type targeting

To access device type targeting options, expand the Targeting section of the line item setup. By default, your line items will target the following physical device types, which correspond to `device_type_targets` in the [Profile Object](../digital-platform-api/profile-service.md#ProfileService-DeviceTypeTargets) associated to the line item, as well as to the Device Type dimension in [Device Analytics Reporting](device-analytics-report.md).

- **Desktops**
  - corresponds to `pc` in the profile api service
  - corresponds to `desktops and laptops` in device analytics reporting
- **Tablets**
  - corresponds to `tablet` in the profile api service
  - corresponds to `tablets` in device analytics reporting
- **Mobile**
  - corresponds to `phone` in the profile api service
  - corresponds to `mobile phones` in device analytics reporting
- **CTV**
  - corresponds to `tv/gameconsole/stb` in the profile api service
  - corresponds to `tv/gameconsole/set top box` in device analytics
    reporting
- **Connected Audio** - only available if ad type is **Audio**
  - corresponds to `mediaplayer` in the profile api service
  - corresponds to `media players` in device analytics reporting

  see [Create an Augmented Line Item](create-an-augmented-line-item-ali.md) to restrict the device types you are targeting, uncheck any device types you wish to exclude.

  > [!NOTE]
  >
  > - **Connected Audio** is only available in Invest.
  > - When targeting devices models **Targeting &gt; System &gt; Device Model** with **Make** = **Apple**, you should include the following device models to avoid under-delivery. For Example: **iPad (300)** and **iPhone (301)**.

## Related topics

- [Buy-Side Targeting](buy-side-targeting.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Augmented Line Items (ALI)](augmented-line-items-ali.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Object Hierarchy](object-hierarchy.md)
- [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md)
