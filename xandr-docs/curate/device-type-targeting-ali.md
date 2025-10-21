---
title: Microsoft Curate - Device Type Targeting
description: This article provides instructions to access device type targeting options.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Device type targeting

To access device type targeting options, expand the **Targeting** section of the line item setup. By default, your line items will target the following physical device types, which correspond to `device_type_targets` in the [Profile Object](../digital-platform-api/profile-service.md) associated to the line item, as well as to the Device Type dimension in [Device Analytics Reporting](../invest/device-analytics-report.md).

- **Desktops**
  - corresponds to `pc` in the profile API service
  - corresponds to `desktops and laptops` in device analytics reporting
- **Tablets**
  - corresponds to `tablet` in the profile API service
  - corresponds to `tablets` in device analytics reporting
- **Mobile**
  - corresponds to `phone` in the profile API service
  - corresponds to `mobile phones` in device analytics reporting
- **CTV**
  - corresponds to `tv/gameconsole/stb` in the profile API service
  - corresponds to `tv/gameconsole/set top box` in device analytics reporting
- **Connected Audio** - only available if ad type is **Audio**
  - corresponds to `mediaplayer` in the profile API service
  - corresponds to `media players` in device analytics reporting

  To restrict the device types you are targeting, clear any device types you wish to exclude.

  > [!NOTE]
  > - **Connected Audio** is only available in Invest.
  >
  > - When targeting devices models **Targeting** > **System** > **Device Model** with **Make** = **Apple**, you should include the following device models to avoid under-delivery. For Example: **iPad (300)** and **iPhone (301)**.

## Related topics

- [Buy-Side Targeting](./buy-side-targeting.md)
- [Create an Insertion Order](./create-an-insertion-order.md)
- [Create a Curated Deal Line Item](./create-a-curated-deal-line-item.md)
- [Object Hierarchy](./object-hierarchy.md)
