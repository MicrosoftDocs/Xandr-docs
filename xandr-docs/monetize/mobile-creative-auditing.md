---
title: Microsoft Monetize - Mobile Creative Auditing
description: Learn about the mobile creative Auditing process. This page addresses questions on why there is a need for an alternative landing page URL, how to display rich media creatives from within mobile apps and what are Unbranded and Targeted creatives.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Mobile creative auditing

Depending upon the type of mobile creative that you're attempting to serve on the Microsoft Advertising platform, the audit process may vary. To ensure that your mobile creatives are successfully audited, you should adhere to our audit processes for mobile creatives.

## App download campaigns

To correctly audit creatives that promote app downloads, we have created several sensitive attributes, which include **Mobile App Downloads** and **Ringtones/Mobile Subscriptions**. Both of these categories can be seen in the creative trafficking workflow within the **Creative Quality** pane.

## Mobile landing pages

In order for a mobile creative with a deep link or mobile-specific landing page (opening an app or click-to-call) to pass our audit, you must provide an alternative landing page URL in the **Brand URL** field in the **Creative Quality** pane.

> [!NOTE]
> This URL should be a closely related landing page that is visible from a desktop browser. We strongly recommend that you verify if the landing page is visible from a desktop browser before submitting the creative for audit. You can add this in the **Creative Quality** pane of the creative trafficking workflow.

## MRAID creatives

[MRAID](https://www.iab.com/guidelines/mraid/) is a framework that allows rich media creatives to be displayed from within mobile apps.

> [!WARNING]
> If your mobile creative has a mobile-specific targeted landing page, such as a click-to-call creative, you must provide an alternative landing page URL in the **Brand URL** field of the trafficking workflow. This URL should be a closely related landing page that is visible from a desktop browser. We strongly recommend that you verify that the landing page is visible from a desktop browser before submitting the creative for audit. For more information about how you can serve MRAID creatives on your mobile [Run Rich Media Creatives on Mobile Inventory](run-rich-media-creatives-on-mobile-inventory.md).

To successfully pass our platform audit, all MRAID creatives must always display the appropriate branding from a desktop browser even when a mraid.js file isn't present. The Microsoft Advertising Audit team will verify that the MRAID creative contains the appropriate branding, but they will not flag any unusual or unexpected behavior since MRAID creatives may exhibit behavior that is incompatible with desktop browsers.

## Unbranded creatives

Many mobile supply partners are willing to accept creatives that do not show a brand in the creative image. To accommodate this, we added a **Sensitive Attribute Unbranded Creative (mobile only)**. As long as a creative is clearly a mobile creative (submitted with a Brand URL or as MRAID), an auditor can pass an unbranded creative with this flag. The brand must be implied by the creative, and the landing page should contain proper branding. Creatives will still have to click through to a branded landing page in order to have a brand associated with them. This will allow mobile creatives that do not have a brand in the creative image to still be associated with a brand in our systems.

The **Unbranded Creative (mobile only)** sensitive category will be enabled by default in all ad quality profiles. This will not affect web supply. For mobile supply, many sellers approve unbranded creatives, so this change will be in line with their policies.

## Targeted creatives

> [!WARNING]
> Before uploading targeted creatives, you must provide your representative with the following information for our internal audit team:
>
> - Creative IDs
> - Your targeting criteria with common targets grouped together to facilitate an audit.
>

**We highly recommend that you verify if you can view targeted creatives by manually overriding your web browser's User-Agent.**

Auditing targeted creatives is a best effort service. If the creatives are targeted to anything more specific than a mobile OS, your creative will probably not be auditable. For example, you can target Android, but not Android version 2.3 specifically.

## Related topics

- [Mobile Buying FAQ](mobile-buying-faq.md)
- [Buying Mobile Inventory](buying-mobile-inventory.md)