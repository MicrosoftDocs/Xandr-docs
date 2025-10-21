---
title: Microsoft Monetize - Advanced Frequency Management
description: In this article, learn what Advanced Frequency Management (AFM) is, how to enable AFM, and how to get reports on AFM capping.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Advanced frequency management

Advanced Frequency Management (AFM) is an innovative frequency-capping feature that lets you control the number of impressions seen by users who opt out of including traditional identifiers in ad requests ("cookieless users").

> [!NOTE]
> This feature is only applicable to ALI (Augumented Line Items) using **Open** and/or **Deal** supply sources.

Historically, frequency capping for digital advertising has entirely relied on the presence of ad-request identifiers to identify and assign impression-cap rules for users. However, an increasing number of ad requests no longer include an identifier.

Though the AFM model is built using data-containing identifiers, it doesn't actually require users to pass any identifiers within ad requests to function. This allows advertisers to meet their reach and **unique impression** goals without dependency on device environment. Assuming a user has visited "website A", Microsoft Advertising can predict the likelihood that the user will visit "website B". In fact, Microsoft Advertising can determine the probability of a user having visited multiple websites (website B, C, and D), given that they've already visited website A. Ultimately, Microsoft Advertising can estimate how many creatives have already been delivered to a user within a particular time frame, based on the website from which the ad request was received.

## How to enable AFM

AFM will be automatically actived to help adhere to your frequency cap on impressions without identifiers once you toggle “**Include users without cookies**” and select a daily frequency cap on your Line item.

> [!NOTE]
> This activation is limited to line item objects and are not applying to frequency caps set on advertisers, insertion orders, and creatives.

## AFM reporting

As with traditional frequency caps, you can find your line item's **unique impressions per user/device** involved in AFM capping in the [Buyer Reach and Frequency Report](buyer-reach-and-frequency-report.md). There are now three frequency cap types in this report: **Classical**, **Advanced**, and **None**.

> [!NOTE]
> Ensure that you only reference **identified imps** and **imps per identified device** when analyzing your AFM performance in the **Buyer Reach and Frequency Report**.
