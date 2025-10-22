---
title: Bidstream Creative Registration FAQ
description: Learn about Bidstream Creative Registration (BCR) FAQ(s)
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidstream Creative Registration FAQ

Frequently Asked Questions about Bidstream Creative Registration (BCR):


### What are the best practices for implementing Bidstream Creative Registration (BCR)?

- **Continue bidding:** Since registration is based on sampling, continue bidding with unregistered creatives until they are registered. Adjust your bidding logic to allow for this delay.
- **Populate required fields correctly:** Ensure all required fields (adm, adomain, crid, etc.) are correctly populated and formatted for each bid.
- **Monitor audit status:** Track the audit status of each creative. If your supply settings allow unaudited creatives, you can serve them while they are in pending status; otherwise, wait for audit approval before serving.
- **Error Handling:** Implement error handling for common issues like missing or invalid fields, long URLs, or audit failures.
- **Stay current:** BCR is in Beta, so review product updates and documentation regularly for any changes to requirements.

### Will the creative be registered on the first bid? 
Creatives are registered based on a sampling of bids. It may take several bids before a creative is captured and registered. Ensure your bidding logic accounts for this delay.  

 
### What is the timeframe for creative registration after the first bid?   
There is no fixed SLA. Registration speed depends on sampling percentage and bid frequency. If a creative is not registered within 24 hours, contact your account manager.


### What happens if my creative is rejected during audit? 
If a creative fails automated audit, it is sent to the human audit queue, which has limited capacity. You may need to revise and resubmit the creative. 


### Can I serve unaudited creatives?
Only if the publisher allows supply of unaudited creatives. Otherwise, the bid will be rejected until the creative is audited and approved.  

 
### What should I do if my native creative’s link exceeds the character limit?  
Shorten the URLs to ensure they do not exceed 2048 characters.  

 
### Where can I find ADM documentation?  
- [Banner Ad Markup bidding (ADM)](banner-ad-markup-bidding.md)
- [Video Ad Markup bidding (ADM)](video-ad-markup-bidding.md)
- [Native 1.2 Ad Markup bidding (ADM)](native-ad-markup-bidding.md)
- [Overview - ADM BiddingOverview - ADM Bidding](ad-markup-adm-bidding.md)

 
### Who should I contact for assistance with BCR? 
Contact your Microsoft Advertising Account Representative for Support or to enable this feature.
 