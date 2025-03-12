---
title: Microsoft Invest - Transparency and Consent Framework (TCF) for Universal Pixel
description: Learn about the Transparency and Consent Framework (TCF) for Universal Pixel and how to set it up in Invest.
ms.date: 01/23/2025
---

# Microsoft Invest - Transparency and Consent Framework (TCF) for Universal Pixel

The Interactive Advertising Bureau (IAB) has officially released version 2.0 of its Transparency and Consent Framework (TCF). Universal Pixel now integrates with IAB TCF v2.0, allowing you to pass consent signals directly or through a Consent Management Platform (CMP) to Universal Pixel.

This integration with IAB TCF v2.0 is supported starting August 1, 2024.

## Process overview

Universal Pixel can read and interpret the TCF v2.0 transparency and consent (TC) string. Consent management platforms (CMPs) that create TCF v2.0 strings based on user preferences can send consent signals to Universal Pixel. Associated pixels adjust their behavior based on the contents of the TC string.

## Transparency and Consent Framework v2.0 setup process

To enable your pixels to read the TCF v2.0 string, you must opt in by adding a code snippet above your tags. To enable TCF v2.0 support, you'll need to:

1. Make sure you're using a pixel on your site.
1. Adopt a TCF CMP.
1. Add the TCF code snippet before your pixel code.

Add the following code snippet above your pixel code on all pages where you have a Universal Pixel:

```
<script> 
!function(e,i)
    {if(!e.pixie)
        {var n=e.pixie\=function(e,i,a)
            {n.actionQueue.push({action:e,actionValue:i,params:a})
            };
            n.actionQueue\=\[\];var a=i.createElement("script");a.async\=!0,a.src="//acdn.adnxs.com/dmp/up/pixie.js";var t=i.getElementsByTagName("head")\[0\];
            t.insertBefore(a,t.firstChild)
        }
    }
    (window,document);  

pixie('config', 'tcf', { 'enabled': true}); 
pixie('init', 'REPLACE\_WITH\_UP\_PIXEL\_ID'); 
pixie('event', 'PageView'); 
</script> 
<noscript\>
<img width="1" height="1" NormalTextRun SpellingErrorV2Themed CommentHighlightRest SCXW105250476 BCX8">display:none;" src\="https://ib.adnxs.com/pixie?
pi\=REPLACE\_WITH\_UP\_PIXEL\_ID&e\=PageView&script\=0&gdpr\=REPLACE\_WITH\_A\_1\_OR\_0&gdpr\_consent=REPLACE\_WITH\_TCF\_STRING"/> 
</noscript\>;
```

## Universal Pixel behavior with the Transparency and Consent Framework  

The TCF uses “Purposes” to organize data processing. Each purpose has a corresponding "Registered Lawful Basis". Here is how Universal Pixel handles requests that contain the consent string:

| Purpose | Microsoft's Registered Lawful Basis | Description | Impact to Microsoft Advertising if missing |
| --- | --- | --- | --- |
| 1 | Consent | Store and/or access information on a device. | Cookies will not be created or used by Microsoft Advertising for measurement or personalization. Remarketing lists will not accumulate data for unconsented users, and attribution reports may be more limited. |
| 3 | Consent | Create profiles for personalised advertising. | Events are not eligible for ads personalization, and are not used for remarketing lists. Users already added to audience lists are unaffected. |
| 4 | Consent | Use profiles to select personalised advertising. | Events are not eligible for ads personalization, and are not used for remarketing lists. Users already added to audience lists are unaffected. |
| 7 | Consent | Measure advertising performance. | Microsoft Advertising requires this purpose for all conversions. If this purpose is not present, we will not record the conversion. |
| 9 | Consent | Understand audiences through statistics or combinations from different sources. | Microsoft Advertising requires this purpose for all conversions. If this purpose is not present, we will not record the conversion. |
| 10 | Consent | Develop and improve services. | Microsoft Advertising requires this purpose for all conversions. If this purpose is not present, we will not record the conversion. |

Universal Pixel tags only accept TCF strings that are correctly implemented according to the TCF policies and technical specifications. If your CMP doesn't respond within 500 milliseconds or you see a status of “error”, “stub”, or “loading”, the tag will continue to function without TCF support.

## Related topics

- [Universal Pixel Service](..\digital-platform-api\universal-pixel-service.md)
- [Universal Pixel SDK](..\mobile-sdk\universal-pixel-sdk.md)