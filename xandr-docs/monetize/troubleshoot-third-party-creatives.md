---
title: Microsoft Monetize - Troubleshoot Third-party Creatives across Microsoft Advertising Inventory 
description: Microsoft Advertising supports creatives served by third-party ad servers. These creatives are subject to the same policies and quality standards as hosted creatives on our Microsoft Monetize platform.
ms.date: 06/13/2025
ms.author: shsrinivasan
---

# Microsoft Monetize - Troubleshoot third-party creatives across Microsoft Advertising inventory 

## Overview

Microsoft Advertising supports creatives served by third-party ad servers. These creatives are subject to the same policies and quality standards as hosted creatives on our platform. All creative and inventory content must comply with Microsoft Advertising’s foundational policies. As part of this requirement, third-party creatives undergo an audit to ensure compliance. 

This guide explains a common rejection reason (i.e. “Creative does not display properly”) and provides actionable insights to help resolve this issue. 

## Possible reasons for creative display failures 

When a creative fails to render correctly, it may be disapproved during the audit process. Below are common technical causes for this issue: 
 
- **Invalid ad tag code:** Ensure the tag code is correctly implemented. For more information, see [Ad Tags](../industry-reference/ad-tags.md). 
- **Inactive or disabled tag:** Confirm with your creative provider that the tag is active and serving correctly. 
- **Geotargeting restrictions:** The creative may include geotargeting parameters that limit where it can render. For more information, refer to allowing our audit IPs and domain section within the [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md) document. 
- **Expired creative:** A creative is automatically deactivated if: 
    - It has not served impressions, and 
    - It has not been modified within 15 days for external bidder creatives and 45 days for platform creatives. 
    - Creatives are reactivated automatically once bidding resumes. 
- **Ad verification scripts:** If the creative uses third-party verification tools (e.g., Adsafe), ensure they are correctly integrated. For more information, refer to allowing our audit IPs and domain section within the [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md) document. 
- **JavaScript without proper HTML markup:** All JavaScript code must be enclosed within valid HTML tags. See [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md) document for code requirements. 
- **Unsupported use of rich media or expandables in iFrames:** Creatives using expandable or rich media formats may not render when the Serve in iFrame option is enabled. For supported configurations, see [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md) document. 
- **Incorrect size configuration:** A mismatch between the selected size and the creative's actual dimensions may result in truncated or distorted rendering. For more information, see [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md). 
- **Non-renderable native creative:** If a native creative (e.g., ${CREATIVE_ID}) fails to render, it may be due to a mismatch between the expected response and the actual content returned during the auction. This typically occurs when Microsoft expects a dynamic response and receives a null value instead. The bidder must verify that their creative meets the placement-side requirements for the target inventory. 

## Video specific: 
- Video creative returns empty VAST:
    - The creative returns a VAST response, but the response contains no media assets (i.e., an empty VAST XML). While the creative may have previously passed the initial VAST validation, it can later fail to render if the VAST content is changed or removed further down the wrapper chain. 
    - Ensure the final VAST response includes valid media files and is not empty. Review all wrapper levels to confirm that the creative remains properly configured end-to-end. 

## Best practices to troubleshoot creative display issues 

Follow these recommendations to ensure your creative displays correctly across Microsoft Advertising inventory:

- **Review and preview the creative:** Always preview your creative to verify that it renders as expected on the platform. 
- **Update and correct the creative as needed:** If the creative fails to display properly, make the necessary updates to the code, assets, or settings before resubmitting. 
- **Use third-party rendering tools:**
    - For video creatives, use Google Video Suite Inspector to validate rendering and VAST structure. 
    - For display creatives, tools like JSFiddle can help you inspect and test HTML/JavaScript behavior. 
- **Use Microsoft’s creative preview tool:** Access a cached preview of your creative by visiting: [https://creative-preview-an.com/cached/creative/<creative_id>](https://creative-preview-an.com/cached/creative/<creative_id>)


## Related topics
- [Ad tags ](../industry-reference/ad-tags.md)
- [Bid error codes ](../bidders/bid-error-codes.md)
- [Creatives ](../industry-reference/creatives.md)
- [Creative Troubleshooting FAQ ](../bidders/creative-troubleshooting-faq.md)
- [Native ad markup bidding ](../bidders/native-ad-markup-bidding.md)
