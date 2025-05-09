---
title: Microsoft Monetize - Household Attribution FAQ
description: Learn about household attribution FAQ(s) Microsoft Monetize.
ms.date: 10/19/2024
ms.author: shsrinivasan
---

# Microsoft Monetize - Household Attribution FAQ

Frequently Asked Questions about Household Attribution: 
 
### Is there an additional cost associated with this feature?
No  

### How can I check if my member is enabled for this feature?
To determine if the feature is enabled for your member, check at the Line item level. Look for the "Household Attribution Enabled" toggle to see if it is displayed.  

### Is it permissible to target the same creative under two different Line items (LIs)?
Yes, you can target the same creative under two different Line items (LIs). However, in such cases, the conversion will be attributed to both Line items and will not be deduplicated. This behaviour applies to any pixel and is not specific to IP Attribution.     

 
### Will this feature affect the delivery of my campaigns?  
No, this feature will not affect the delivery of your campaigns. It will not prevent the Line item from bidding, winning, or transforming impressions. The IP-specific address in the ad request does not influence bidding behaviour. IP matching occurs during the ingestion of the conversion event and solely impacts the attribution logic, not the delivery of your campaigns. 


### Does IP Attribution work with commercial/business IP addresses or cellular/wireless IP addresses? 
No, this feature uses Digital Envoy to filter out non-residential IP addresses and only considers residential IP addresses for attribution. 


### How does IP Attribution work for residential buildings where multiple units share the same IP address? 
In cases where multiple units within the same residential building share the same IP address, it will not be possible to distinguish between individual units. 

 
### What happens if someone resets their router or their ISP assigns a new IP address between the impression and conversion events? 
If someone resets their router or their ISP assigns a new IP address between the impression and conversion events, it can disrupt our ability to attribute the conversion.  

 
### Does Xandr store or truncate IP addresses? 
Xandr does not truncate IP addresses before anonymizing and storing them. IP addresses from impressions are first hashed/anonymized and then stored for up to 30 days. Only IP addresses that meet all privacy requirements are used in this process.  

 
### Is this feature available in all countries? 
Yes, this feature is available worldwide, with the exception of countries on Microsoft's exclusion list. 

 
### Is this feature compliant with GDPR and CCPA regulations?  
Yes, this feature is compliant with GDPR and CCPA regulations, as it requires proper consent to count a household conversion.  

 
### Is this feature available across all devices?  
Yes, this feature is available across all devices, which includes: 
- CTV  
- Mobile 
- Tablet, and  
- Desktop


### Is this feature available across all ad formats?  
Yes, this feature is available across all ad formats, which includes 
- Banner 
- Video 
- Native, and 
- Audio  
> [!NOTE]
> This feature is available across all ad formats, except DOOH. 
 
 

## Related topics

- [Household Attribution Overview](household-attribution.md)
- [Set Up Household Attribution](set-up-household-attribution.md)
- [Household Attribution Reporting](household-attribution-reporting.md)

