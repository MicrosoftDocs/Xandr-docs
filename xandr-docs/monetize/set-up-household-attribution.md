---
title: Microsoft Monetize - Setting Up Household Attribution 
description: Learn about setting up household attribution for Microsoft Monetize.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Setting up Household Attribution

When you enable the household conversion feature, IP conversions are included in the CPA calculation alongside traditional post-click and post-view conversions. Without this feature, the CPA calculation and optimization depend solely on post-click and post-view conversions. IP conversions directly impact CPA optimization performance, and enabling this feature significantly increases the number of recorded conversions, either following an impression or a click. 

You can enable or disable Household Attribution for a Line item. To use Household Attribution, you need to meet the following requirements: 


### Household Attribution pre-requisites

| Name | Description |
|---|---|
| Pixels | Create and use a [Conversion Pixel](create-a-conversion-pixel.md) or a [Universal Pixel](the-universal-pixel.md), to track conversions on your website or application. |
| Cookieless targeting | Toggle Cookieless Targeting to “on”, in the Line-item settings, to allow Microsoft to use IP addresses as an alternative identifier, enabling attribution in cookieless environments. |


1. **Step 1. [Navigate to the Create New Line item Screen](navigate-to-the-create-a-new-line-item-screen-monetize.md)**
<br>
You can create a new Line item from the Create New Line item screen and fill out the basic set up details. For more information, see [Create a New Line item](working-with-line-items.md) 

1. **Step 2. [Set Up Line item Optimization](set-up-line-item-optimization.md)**
<br>
In the Optimization section, you can enable or disable Microsoft Advertising optimization for a Line item. To enable Household attribution on the Line item: 
    - Add conversion tracking.
        - Click Edit to associate conversion tracking or universal pixel to this Line item which was previously created in the pre-requisite step above. These pixels can be used to track the Line item’s performance.  
    - Enable IP Attribution  
        - If you select a conversion pixel, an Enable IP Attribution toggle is displayed. Toggle the Enable IP Attribution to "on", in the Line-item settings, to incrementally attribute conversions by matching IP addresses to ads served on devices.  
When enabled, if the IP address sees an impression, and the same IP address sees a conversion pixel, a conversion is activated. 
 
> [!NOTE]
> - Household Attribution works best when the IP address remains consistent, is unique to a single household, and isn't masked by a VPN or a proxy. 
> - Household Attribution currently uses only IPv4 IP addresses for attribution.


## Related topics

- [Household Attribution Overview](household-attribution.md)
- [Household Attribution Reporting](household-attribution-reporting.md)
- [Household Attribution FAQ](household-attribution-faq.md)
