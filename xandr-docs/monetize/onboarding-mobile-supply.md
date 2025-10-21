---
title: Onboarding Mobile Supply
description: Explore mobile supply integration via ad calls, detailing supported integrations, including supply type and query parameters.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Onboarding mobile supply

> [!NOTE]
> Microsoft Advertising now supports a domain, `adnxs-simple.com`, which does not send or read browser cookies on requests. Clients can leverage this cookie-free domain when there is no consent to use personal data. Relevant calls initiated by Microsoft Advertising will automatically use this domain when there is no consent or when cookies are not required for the function. For more information, see [Part of Service Policies](../policies-regulations/index.yml).

There are several ways to onboard mobile supply. The type of mobile supply you are bringing on will determine the type of ad call your publishers need to make.

This page lists the exact mobile ad calls you must make for each type of mobile supply integration we support. For each call, we describe the required supply type for that inventory, and the required and recommended query string parameters.

> [!WARNING]
> Sellers using the `/mob` or `/ssmob` calls must ensure that this traffic is **mobile app traffic only**. Any non-app traffic coming through these handlers will be rejected.
> [!IMPORTANT]
> Currently, Monetize does not export mobile ad tags directly. You must [Export Placement Tags](export-placement-tags.md) and then edit them to include the parameters described below.

## Differences between server and client-side

For both app and mobile web inventory, there are two types of ad calls that can be generated: one that comes directly from the device (the client-side), and one that comes from the server.

When an ad call comes directly from the device (client-side), the application or website calls the Microsoft Advertising Impression Bus directly. This means that Microsoft Advertising has direct access to important metadata such as the User Agent and IP address.

On the other hand, a server-side call means that an external server calls the Microsoft Advertising Impression Bus on behalf of the client (the device). In this case, Microsoft Advertising does not have direct access to necessary metadata that would make the impression attractive to buyers such as the IP address and the User Agent. Since this data is not supplied by the server-side call, it must be appended to the request by your mobile ad tag. The instructions below show you which tags you must add to your placement tags depending on the type of integration.

This diagram shows the difference between how server-side and client-side mobile ad calls are made:

:::image type="content" source="media/server-vs-client.png" alt-text= "Diagram that illustrates the distinctions between server-side and client-side mobile ad call processes.":::

## Server-side integrations

Follow the instructions in this section to set up a server-side integration with a mobile publisher. Use either Mobile App or Mobile Web.

## Mobile app

### Required parameters

Server-side mobile app traffic should only use the `/ssmob` endpoint. Server-side traffic coming through `/mob` calls runs the risk of being rejected.

Technically, the minimum required URL for a server-side ad call coming from a mobile app looks like:

```
https://mobile.adnxs.com/ssmob?id=PLACEMENT_ID&size=WIDTHxHEIGHT&format=json 
```

where `PLACEMENT_ID` is your placement ID (e.g., "123459") and `WIDTHxHEIGHT` is the width and height of the ad slot (e.g., "320x50"). The `format` parameter is required to ensure that the server requesting the ad is getting the response in the format it needs.

Even though this call will fetch an ad, it doesn't provide as much information as it could to make the impression attractive to buyers; see the next section for a list of recommended parameters.

### Recommended parameters for server-side ad calls

We recommend that you include the following parameters (in the table below) on server-side ad calls from mobile apps. For more information about how to properly format mobile ad calls, see the [Mobile Ad Call Reference](mobile-ad-call-reference.md).

> [!TIP]
> We recommend creating separate placements for Android and iOS.

| Name | Parameter | Description |
|--|--|--|
| App ID | `appid` | The app ID is a string used to identify an app running on Android or iOS. Many buyers set line item targeting and reporting based on app ID. Failing to supply a correct `appid` will make your inventory unattractive to these buyers. Therefore, passing this field is **strongly recommended**. For more information about the `appid` parameter, see our [Mobile Ad Call Reference](mobile-ad-call-reference.md). |
| IP Address | `ip` | The IP address parameter provides Microsoft Advertising with the geographic location of the user, as well as the carrier whose network the device is connected to. Many buyers use carrier or geo targeting. Including this information on an ad call is important in order to capture mobile demand. |
| User Agent | `ua` | The User Agent parameter provides us with the device's operating system as well its make and model. Many buyers are targeting based on these parameters and not including them will restrict demand. |
| IDFA (for iOS) | `idfa` | This is the user's unique identifier for iOS devices and is tied to a user ID. If you don't provide this information on the ad call, demand partners who have implemented frequency capping and/or a buying strategy that requires conversion tracking will not buy your inventory. Not providing the user's unique ID will severely restrict demand. |
| AAID (for Android) | `aaid` | This is the user's unique identifier for Android devices that use Google Play Services and is tied to a user ID. If you don't provide this information on the ad call, demand partners who have implemented frequency capping and/or a buying strategy that requires conversion tracking will not buy your inventory. Not providing the user's unique ID will severely restrict demand. |
| Unique Device ID (Android) | `md5udid`, `sha1udid` | This is the user's unique identifier for Android devices that do not use Google Play Services and is tied to a user ID. If you do not provide this information on the ad call, demand partners who have implemented frequency capping and/or a buying strategy that requires conversion tracking will not buy your inventory. Not providing the user's unique ID will severely restrict available demand. |

## Mobile web

### Required parameters for a server-side ad call

Technically, the minimum required URL for a server-side ad call coming from a mobile website looks like

```
https://mobile.adnxs.com/ttj?id=PLACEMENT_ID&size=WIDTHxHEIGHT 
```

where `PLACEMENT_ID` is your placement ID ("123459"), and `WIDTHxHEIGHT` is the width and height of the ad slot ("320x50").

Even though this call will fetch an ad, it doesn't provide enough information to make the impression attractive to buyers; see the next section for a list of recommended parameters.

### Recommended parameters for a server-side ad calls

We recommend that you include the following parameters on server-side ad calls from mobile websites:

| Name | Parameter | Description |
|--|--|--|
| Location | `loc` | This is the user's location expressed in latitude and longitude, to allow geo-targeting. |

> [!TIP]
> For a complete list of the query string parameters you can pass on our `/tt` and `/ttj` calls, see [Placement Tag Parameters](placement-tag-parameters.md).

## Client-side integrations

Follow the instructions in this section to set up a client-side integration with a mobile publisher. Refer to Mobile App or Mobile Web as needed.

## Mobile app in client-side integration

### Required parameters for client-side mobile app integration

To do a client-side mobile app integration, use one of our [Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md). We have SDKs for Android and iOS, and they are designed so that you don't have to build the correct mobile ad calls yourself. The SDK will generate calls with the required parameters for you.

For a complete list of our mobile ad call parameters, see our [Mobile Ad Call Reference](mobile-ad-call-reference.md).

## Recommended parameters

In order to get the SDK to send the device's location and carrier info, and thus make the impression more valuable to buyers, you will need to do the following:

- Configure the SDK during installation to enable the permissions that will allow it to send location-based data to advertisers.
- Use the SDK to get the user's location and send it on the ad call.

For instructions on enabling location permissions and sending user data, see [Android SDK Integration](../mobile-sdk/android-sdk-integration.md) and [iOS SDK Integration](../mobile-sdk/ios-sdk-integration.md).

## Mobile web in client -side mobile web integration

Client-side mobile web integrations should use the `/ttj` placement tag that is exported by Monetize. This is the same ad tag used for display impressions. Our ad server will retrieve the browser's User Agent and the device's IP address using the same methods used for display. For instructions on exporting a placement tag, see [Export Placement
Tags](export-placement-tags.md).

### Required parameters for a client-side ad calls

A client-side ad call coming from a mobile website only requires a couple of parameters:

```
https://ib.adnxs.com/ttj?id=PLACEMENT_ID&size=WIDTHxHEIGHT 
```

### Recommended parameters for client-side ad calls

We recommend that you include the following parameters on client-side ad calls from mobile websites:

| Name | Parameter | Description |
|---|---|---|
| Location | `loc` | This is the user's location expressed in latitude and longitude, to allow geo-targeting. |

For a complete list of the query string parameters you can pass on our `/tt` and `/ttj` calls, see [Placement Tag Parameters](placement-tag-parameters.md).

## Related topics

- [Placement Tag Parameters](placement-tag-parameters.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)
- [Managing Mobile Discrepancies](managing-mobile-discrepancies.md)
- [Mobile Debug Auction Tips](mobile-debug-auction-tips.md)
