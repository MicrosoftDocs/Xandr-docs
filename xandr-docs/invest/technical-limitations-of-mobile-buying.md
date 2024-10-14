---
title: Microsoft Invest - Technical Limitations of Mobile Buying
description: Explore mobile buying limitations such as, user identification, frequency capping, device and geographic targeting, and more.
ms.date: 10/28/2023
---

# Microsoft Invest - Technical limitations of mobile buying

In [Welcome to Mobile](welcome-to-mobile.md), we provided an overview of the differences between web and mobile app buying (Summary: they're mostly the same). We also mentioned that where feature disparity exists between web and mobile app, the disparity is often due to technical limitations. This document will describe some of these limitations, which include:

- Identifying users and frequency capping across devices.
- Limited post-view conversion attribution capabilities.
- Geographic targeting.

## Identify user and cap frequency

Frequency capping on mobile devices works on a per-device basis; in other words, if you switch devices, your frequency cap is reset. This is because reliably identifying users across multiple devices is currently an unsolved problem. For example, if you see an ad multiple times from your Android phone and hit the frequency cap defined by the line item serving that ad, you shouldn't see that ad anymore. If you switch to your iPad later in the evening for some bedtime reading, you won't be identified as the same user by the line item, and you may see ads from that same line item again.

In addition, very strict frequency caps are less reliable than they are on web inventory. This is due to the fact that our ad server waits longer to count mobile impressions than web. For more information about why we do this, see [Managing Mobile Discrepancies](managing-mobile-discrepancies.md). As a result, when simultaneous or almost simultaneous auctions occur for the same inventory, very strict frequency caps can be broken. This can occur on slices of inventory where there are lots of biddable impressions per available user.

Also, third-party cookies are not always available on mobile devices, since not all mobile browsers accept these cookies. For more information, see [Mobile Targeting and Attribution Challenges](mobile-targeting-and-attribution-challenges.md). In ord6er to compensate for the lack of third-party cookies, Microsoft Advertising associates the device IDs used by different apps running on the same device with the same Microsoft Advertising cookie ID; this lets us do frequency capping across apps and the browser on the same device. For example, an app might pass in the device ID value `idfa=123` on a mobile ad call. If Microsoft Advertising has already seen that device and associated it with a cookie ID, frequency capping and user identification will work normally. Furthermore, a single Microsoft Advertising cookie ID can be mapped to many different device IDs. That way if a device sends us an `idfa` from one app, an `openudid` from another, we can still tie it all back to the same Microsoft Advertising ID for user identification and frequency capping purposes. For more information about the device ID parameters that can be sent to Microsoft Advertising using our mobile ad call, see the [Mobile Ad Call Reference](mobile-ad-call-reference.md).

## Target device and report caveats

In some cases, mobile device targeting (and subsequent reporting) will display logical inconsistencies. For example, an iPhone could be mapped to an iPad user agent (UA). This inconsistency can occur because of the following technical issues:

- We look up OS and Browser from the UA ourselves, but we retrieve device info from a third party. The two sources are not logically verified.
- OpenRTB integrations allow suppliers to override individual device fields.
- Apps are responsible for sending a UA, which isn't always reliable.
- On a single click, suppliers may send some data from an app UA, and some from a browser UA.

## Conversion attribution

The following table shows whether conversion attribution works in different mobile scenarios. Note that post-view conversion attribution is only possible across non-Safari mobile browsers at this time.

| Conversion Type | Browser to Browser (non-Safari) | Browser to Browser (Safari) | App to Browser (iOS + Android) | App to App Store Download | Browser to App Store Download |
|:---|:---|:---|:---|:---|:---|
| Post-click | Yes | Yes | Yes*** | Yes** | Yes** |
| Post-view | Yes | No | No | No | No |

- \* Functional for 5-10% of Safari users who have previously clicked on an ad.
- \*\* Functional using a third party conversion tracking partner. For more information, see [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md).
- \*\*\* Functional when the conversion happens in the same browser that the app opens for click through. For example, if the app opens an in-app browser, the conversion needs to occur in the in-app browser.

> [!IMPORTANT]
> There is currently no way to do conversion attribution that links an event on a mobile device (such as a view) to a later conversion that happens in a desktop browser.

## Geographic targeting

If the [SDK](../mobile-sdk/xandr-mobile-sdks.md) a mobile app uses to show ads has permission from the user to provide their current latitude/longitude data, you'll be able to use it for mobile targeting. If not, you can still use [Geography Targeting](additional-geo-restrictions-ali.md), which uses the device's IP address, if any is available. This is less precise than lat/long, but more commonly available. Some apps also allow you to do geo-targeting based on the zip code of the user when they signed up for the app.

> [!NOTE]
> About 15-30% of mobile impressions carry lat/long information.

## Related topics

- [Frequency and Recency Caps](frequency-and-recency-caps.md)
- [Welcome to Mobile](welcome-to-mobile.md)
- [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md)
- [Managing Mobile Discrepancies](managing-mobile-discrepancies.md)
- [Mobile Targeting and Attribution Challenges](mobile-targeting-and-attribution-challenges.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)
