---
title: Microsoft Invest - Household Attribution
description: Learn about household attribution on Microsoft Invest.
ms.date: 10/19/2024
ms.author: shsrinivasan
---

# Microsoft Invest - Household Attribution

Household Attribution is a feature that enables Microsoft to match ads served on any device to conversions occurring on any device connected to the same network using the IP address.  

> [!NOTE]
> This feature is available across all ad formats, except DOOH. 

With Household Attribution: 

- You can improve the measurement of your campaigns and the effectiveness by increasing optimization signals.  
- You can capture more conversions that are influenced by your ads, especially for high-consideration products or services that require further research or comparison. 
- You can gain more insights into the cross-device behaviour of your target audience and how they interact with your ads across different screens. 


## Household Attribution process 
 

Microsoft uses the following process to attribute conversions once the Household Attribution for a line item is enabled: 
 
> [!NOTE]
> Microsoft prioritizes cross-device attribution over IP Attribution and avoids double counting any conversions. If a conversion is attributed to an ad using both cross-device attribution and IP Attribution, Microsoft counts it only as a cross-device conversion. 

- When an ad is served on a device, Microsoft will initially record the IP address of the device and the impression ID. 
- When a user visits a website or application and triggers an event through the conversion pixel, Microsoft will then record the IP address of the device and the conversion ID. 
- Thereafter, Microsoft will look for a match between: 
    - The IP address and the impression ID of the ad 
    - The IP address and the conversion ID of the conversion event 
    - If a match is found, Microsoft will attribute the conversion to the ad using the Household Attribution. 
- Microsoft leverages a verification partner to remove any known commercial and cellular IP addresses, limiting Household Attribution to residential IPs alone. 



## Related topics

- [Set Up Household Attribution](set-up-household-attribution.md)
- [Household Attribution Reporting](household-attribution-reporting.md)
- [Household Attribution FAQ](household-attribution-faq.md)
