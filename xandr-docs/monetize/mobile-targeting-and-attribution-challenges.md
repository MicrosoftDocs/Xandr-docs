---
title: Microsoft Monetize - Mobile Targeting and Attribution Challenges
description: Learn how it's difficult to perform cross-device targeting and conversion attribution on mobile inventory. On this page, we provide an overview of the key challenges that must be overcome.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Mobile targeting and attribution challenges

In [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md), we discussed the technical realities that are keeping mobile buying features from reaching full parity with display (for now). The most difficult problem is to reliably perform cross-device targeting and conversion attribution on mobile inventory. On this page, we provide an overview of the key challenges that must be overcome.

> [!TIP]
> Each of the sections below corresponds to a numbered section of the diagram for easier reference.

:::image type="content" source="media/mobile-attribution-and-targeting-challenges.png" alt-text="Screenshot of mobile attribution.":::

## 1. Cross-Screen targeting and attribution

Also known as: **Desktops vs. Mobile Devices**

**Problem**: It is hard to identify users across devices. This makes it difficult to target, frequency cap, and attribute conversions across devices.

**Solution**: We believe a combination of technology and partnerships with data providers will eventually provide the best solution. For now, watch this space.

## 2. App-to-Browser targeting and attribution

Also known as: **Mobile Browsers vs. Apps**

**Problem**: Apps and browsers offer different methods for identifying users. This creates several issues:

- Cannot retarget and frequency cap the same user across an app and the browser.
- Cannot track app downloads on iOS-powered devices when a user clicks on an ad in a browser. This is because of the situation with **Mobile Safari Cookies** (described below).

**Solution**: Possible solutions include integration with one or more device recognition vendors, partnerships with major carriers, or both.

## 3. Inter-App targeting and attribution

Also known as: **Apps vs. Apps**

**Problem**: Android and some older iOS devices have no standardized methods for identifying a user across apps. This creates several issues:

- Frequency capping and retargeting across Android apps may not always work.
- Tracking app download conversions may not work on older iOS versions.

**Solution**:

- Use Apple's "identifier for advertising" (`idfa`) on iOS 6 an above and `openudid` for older iOS devices.

- Use Google's advertising identifier (`aaid`) or standardize on the `sha1` device ID for Android devices.

  Microsoft Advertising associates multiple device IDs to one Microsoft Advertising cookie IDs. This allows us to do frequency capping using the mechanisms we already have in place. For more information about `idfa`, `sha1`, and the other mobile device IDs we support, see the [Mobile Ad Call Reference](mobile-ad-call-reference.md).

## 4. Mobile safari cookies

Also known as: **Safari vs. The World**

**Problem**: Mobile Safari (the default browser on iOS devices) does not accept third party cookies, which impacts our ability to segment, re-target, and apply frequency caps.

**Solution**: Like **App-to-Browser Targeting and Attribution**, possible solutions include integration with one or more device recognition vendors, partnerships with major carriers, or both.

## Related topics

- [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md)
- [Welcome to Mobile](welcome-to-mobile.md)
- [Mobile Buying FAQ](mobile-buying-faq.md)