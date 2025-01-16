---
title: Microsoft Curate - System Targeting
description: Target users based on their operating systems, browsers, language, device model, or carrier. By default, all operating systems, browsers, and languages are targeted.
ms.date: 11/15/2023
---

# Microsoft Curate - System targeting

You can target users based on their operating systems, browsers, language, device model, or carrier. In the **Targeting** section of a line item, select the **Edit** button next to **System**.

By default, all operating systems, browsers, and languages are targeted. On the **System** dialog, you can narrow your targeting to include or exclude specific systems.

- The **OS Family** tab shows all operating system families (for example Microsoft Windows or Apple Mac) and operating systems (for example Windows 8 or 10.8 Mountain Lion) available for targeting. You can either include or exclude OS families and operating systems.

- The **Browser** tab shows all browsers available for targeting. You can either include or exclude browsers.
  
  To target the Safari browser on both desktop and mobile, ensure you include both the "Safari" and "iPhone" browsers in your targeting. This step is necessary for accurate delivery.

- The **Language** tab shows all the languages available for targeting. You can either include or exclude languages.
  
  > [!NOTE]
  > The language that is targeted here for excluding and including is the browser language, not the language of the content.

- The **Device Model** tab shows all the device makes and models available for targeting. You can either include or exclude devices.
- The **Carrier** tab shows all the carriers and the countries or regions where they are available. You can either include or exclude carriers.
- The **Summary** tab shows a summary of the selected targeting settings.

> [!WARNING]
> All system targeting types can be used but with some limitations. Due to inconsistent user agent naming conventions used by app providers and mobile carriers, the device type, device make/model, and OS targeting methods for mobile apps are only available for a small portion of inventory. Targeting these items will limit reach on mobile apps.
>
> Additionally, since a significant portion of all impressions are delivered to unknown browsers, operating systems, or both, you should consider targeting **Unknown** operating systems and browsers to avoid severely restricting reach.
