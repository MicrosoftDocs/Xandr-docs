---
title: Microsoft Monetize - Mobile Debug Auction Tips
description: This page describes how to spoof various mobile ad call parameters so that you can successfully run mobile debug auctions. Learn about two ways to spoof the OS using query string parameters, or using developer tools.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Mobile debug auction tips

In order to run a debug auction on mobile inventory, you must pass additional mobile device parameters beyond those described in [Understanding the Debug Auction](understanding-the-debug-auction.md) in on the ad call. This page describes how to spoof various mobile ad call parameters so that you can successfully run mobile debug auctions.

## Call format

> [!NOTE]
> All debug auction and browser cookie override calls must use secure https protocols. Requests made using http will not generate valid results.

Here's an example of an ad call that will run a mobile debug auction:

``` 
https://mobile.adnxs.com/mob?id=[TAG_ID]&size=[WIDTH}x[HEIGHT]&ua=[user_agent_string]&carrier=carrier-[carrier_id]&devmake=[dev_make_code]&devmodel=[dev_model_code]&debug_member=[BUYER_MEMBER_ID]&dongle=[PASSWORD]
```
There are query string parameters that tell the impression bus the user agent, carrier, and device make and model. See the sections below for more information about how to get valid information to pass in via these parameters.

> [!TIP]
> For documentation on all of the mobile query string parameters we accept, see [Mobile Ad Call Reference](mobile-ad-call-reference.md).

## Spoof operating system

Our ad server uses the device's User Agent to determine the operating system. This gives us two ways to spoof the OS: using query string parameters, or using developer tools.

### Using query string parameters

By passing in a different value for the `ua` query string parameter, we can tell the impression bus what operating system we use, since the impression bus determines the device OS from the User Agent. In this example, we set the User Agent so that we appear to be running an iPhone:

``` 
https://mobile..com/mob?id=1280178&size=320x50&debug_member=2048&dongle=DEBUG_AUTH&ua=Mozilla/5.0%20(iPhone;%20CPU%20iPhone%20OS%206_0%20like%20Mac%20OS%20X)%20AppleWebKit/536.26%20(KHTML,%20like%20Gecko)%20Version/6.0%20Mobile/10A5376e%20Safari/8536.25
```

### Using developer tools

Chrome offers the ability to spoof many different devices directly in the header of the HTTP request. To enable it, do the following:

1. Right click the page, and select **Inspect Element**.
1. Follow the instructions from [Chrome's documentation](https://developer.chrome.com/docs/devtools/) to emulate the operating system of your choice.
1. Verify that the browser is appearing as the OS you chose by checking the results of the [Understanding the Debug Auction](understanding-the-debug-auction.md) (search for "Operating System" in the output).

## Example output

Based on the information above, the output on the debug auction would look like this:

``` 
Browser: Safari (all versions) (9)
Operating System: iPhone (8)
Operating System (Extended): OS 6_0 (72)
Device Make: Apple (26)
Device Model: iPhone (301) 
```

## Spoof carrier

In order to spoof the carrier, you will need to add the query string parameter `carrier` to the mobile ad call, along with a numeric carrier code. For example `carrier 80`, like this:

``` 
&carrier=carrier-80
```
To find the code that corresponds to the carrier you'd like to spoof,
you can use one of the following methods:

- Refer to our [Mobile Carrier Codes](mobile-carrier-codes.md).
- Use the API's [Carrier Service](../digital-platform-api/carrier-service.md) to see all of the available codes.

## Spoof device make and model

The query string parameters for spoofing the device make and model are `devmake` and `devmodel`, respectively.

You can use the following read-only API services to see what device makes and models are available in the system:

- The [Device Make Service](../digital-platform-api/device-make-service.md).
- The [Device Model Service](../digital-platform-api/device-model-service.md).

## Related topics

- [Understanding the Debug Auction](understanding-the-debug-auction.md)
- [Onboarding Mobile Supply](onboarding-mobile-supply.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)
