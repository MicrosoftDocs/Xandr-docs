---
title: Microsoft Monetize - User ID Mapping with getUID and mapUID
description: Learn how getUID and mapUID can be used to map your internal user IDs and Microsoft Advertising user IDs in order to match user IDs on future requests.   
ms.date: 10/28/2023
---


# Microsoft Monetize - User ID mapping with getUID and mapUID

You may have internal offline data about users that you need to insert into the Microsoft Advertising [Server Side Cookie Store](server-side-cookie-store.md) so that it is available for decisioning. If so, we must first map your internal user IDs and Microsoft Advertising user IDs in order to be able to match user IDs on future requests. Depending on whether you will store the mapping in your system or in ours, there are two ways to do this through pixel calls: mapUID and getUID.

The **getUID** service retrieves the Microsoft Advertising ID so you can coordinate it with your own in-house ID server side or in your own cookie space. Then you can pass in an offline data feed that says, "update Microsoft Advertising user ABC with the following segment data." The **mapUID** service passes your internal ID to us for mapping to the Microsoft Advertising ID within the Microsoft Advertising cookie store.

> [!NOTE]
> Note that the Microsoft Advertising user ID macro described below is `$UID`. Unlike many of our other macros, it does not have curly braces.

## A basic mapping example

|  |  |
|--|--|
| **Prostarr User ID** | PS123 |
| **Microsoft Advertising User ID** | 2894234234 |
| **Shoe buyer Segment ID** | 0005 |

If the advertiser Prostarr tells us that user `PS123` is in segment `0005`, this will mean nothing to us. Instead, they have to tell us that user `2894234234` is in segment `0005`.

To do this, Prostarr has done a previous mapping of all Microsoft Advertising and Prostarr Sportswear user IDs using the GetUID service and stored that mapping in its internal database. A GetUID call looks like

``` 
https://ib.adnxs.com/getuid?URL 
```

where the URL is the the one you want the mapping directed to. This pixel is placed on Prostarr's webpages, and when it fires, the Impression Bus inserts the Microsoft Advertising user ID into the URL by replacing the `$UID` macro.

> [!TIP]
> For a detailed walk-through of how this works, see the [User Mapping Visual and Walk-Through](user-mapping-visual-and-walk-through.md).

## The getUID service

A URL of your choice will receive a client-side call with the Microsoft Advertising user ID as a querystring parameter. During the ad call, Microsoft Advertising redirects the user to the member's desired URL. The Impression Bus inserts the Microsoft Advertising user ID into the URL, either by replacing a `$UID` macro, or by appending it to the end of the URL. When the user does not have an Microsoft Advertising cookie, "0" is returned and Microsoft Advertising attempts to create one. However, if the user is encountering the getuid call for the first time, "0" will not be returned.

## Code

The format of the getUID Service is fairly simple:

``` 
https://ib.adnxs.com/getuid?URL 
```

The secure version uses this format:

``` 
https://secure.adnxs.com/getuid?URL 
```

Users without cookies or users who have opted out will be redirected with a user ID of 0. If you would prefer not to receive user IDs of 0, use this format:

``` 
https://ib.adnxs.com/getuidnb?URL 
```

If you need the URL to remain URI-encoded, use this format:

``` 
https://ib.adnxs.com/getuidu?URL 
```

## JSON support

To return the Microsoft Advertising user ID in a JSON response with CORS support, use the format:

``` 
https://ib.adnxs.com/getuidj 
```

You will receive a JSON-formatted response like this:

``` 
{"uid":1680598911678123849} 
```

To return a JSONP response with CORS support:

``` 
https://ib.adnxs.com/getuidp?callback=ABC 
```

(Where `callback` is the callback function as defined on the query string.) You will receive a JSONP-formatted response like this:

``` 
ABC({"uid":1680598911678123849}) 
```

## A getUID example

In most cases, it will be necessary to pass the user ID into a specified parameter within the query string of the URL. To accomplish this, you may use the `$UID` macro:

> [!NOTE]
> In case TCF signals are available on the page, "gdpr" and "gdpr_consent", GET parameters must be included at the end of the /getuid url:

```
https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID&geo=35&referrer=https://www.website.com&gdpr_consent=CPaPwEAPaPwEAACAKAFRBWCgAP_AAH_AAAqIHttf_X__b3_j-_59__t0eY1f9_7_v-0zjhfdt
```

<!--
``` 
 https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID&geo=35&referrer=https://www.website.com 
```
-->

The `$UID` macro will be replaced with the Microsoft Advertising user ID by the Impression Bus and the user will be directed to the following URL:

```
https://ad.adserver.com/pixel?adnxs_uid=19241908471992&gdpr=1&geo=35&referrer=https://www.website.com&gdpr_consent=CPaPwEAPaPwEAACAKAFRBWCgAP_AAH_AAAqIHttf_X__b3_j-_59__t0eY1f9_7_v-0zjhfdt
```

<!--
``` 
 https://ad.adserver.com/pixel?adnxs_uid=19241908471992&geo=35&referrer=https://www.website.com 
```
-->

> [!NOTE]
> For both endpoints, if TCF parameters are passed in the redirect URL, Xandr will utilize these parameters to determine if a cookie sync can be performed. If the signals received are interpreted as having insufficient legal basis, Xandr will be unable to process the cookie sync request, and it will return the following error message: "Request failed due to privacy signals." Additionally, if TCF signals cannot be provided when calling our URLs, partners must append the **consent** parameter to the URL. The **consent** parameter accepts binary values: **1** if the user has given consent, and **0** if consent has been denied. This parameter must be included to perform user syncs in certain geographical areas.



## Use case: piggyback on a pixel call

An easy way to create this mapping is to piggyback the getUID Service off of one of your existing pixel calls. You can adjust your pixel so that when the pixel call is made, there will be an immediate redirect to the Microsoft Advertising getUID service, which will pass back the user ID within the URL indicated by Microsoft Advertising Monetize.

For example, let's assume the following pixel exists on a publisher site today:

``` 
 <img src="media/pixel?id=234123" width=1 height=1/> 
```

Instead, fire the Microsoft Advertising getuid pixel, providing the URL of the adserver.com pixel:

``` 
 https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?id=234123&adnxs_uid=$UID 
```

The getUID service redirects to the specified URL with the Microsoft Advertising user ID in place of the `$UID` macro:

``` 
https://ad.adserver.com/pixel?id=234123&adnxs_uid=19241908471992 
```

When `adserver.com` receives this call, the Microsoft Advertising user ID can be inserted into `adserver.com`'s server-side user data store where this mapping of user IDs can be used by future impression and pixel calls through the Microsoft Advertising Impression Bus.

## The mapUID service

> [!TIP]
> The mapUID service has fees associated with it. If you're interested in using this option, please speak with your Microsoft Advertising representative.

The **mapUID** Service inserts your in-house ID into the Microsoft Advertising [Server Side Cookie Store](server-side-cookie-store.md).

The format for a client-side pixel that maps your ID to ours in our system is

``` 
https://ib.adnxs.com/mapuid?member=MEMBER_ID&user=USER_UD 
```

where the member ID is the ID assigned to your company by Microsoft Advertising and the `USER_ID` is your company's user ID. If you don't know your member ID, you can find out by making a `GET` request to the [Member Service](../digital-platform-api/member-service.md).

If you have more than one user ID, you can separate them with semicolons; for example:

``` 
https://ib.adnxs.com/mapuid?member=123&user=ABC;DEF;GHI 
```

## Expiration of mappings

The average time to live (TTL) for mapUID mappings is around 2.5 weeks. Therefore it's very important that you fire the mapUID pixel as frequently as possible and on as many pages as possible to keep your mappings live.

## Piggybacking a segment call off of a mapUID call

You can add user IDs to one or more segments in the Microsoft Advertising cookie store at the same time that you map their ID to ours.

Here is the syntax:

``` 
https://ib.adnxs.com/mapuid?member=[MEMBER_ID]&user=[USER_ID]&seg=[SEG_ID],[SEG_ID],[SEG_ID]

https://ib.adnxs.com/mapuid?member=123&user=12abc34565&seg=1,2,3
```

To pass in values for each segment use colons. (This example used segment codes instead of IDs.)

``` 
https://ib.adnxs.com/mapuid?member=123&user=[USER_ID]&seg_code=[code1]:[code1value],[code2]:[code2value],[code3]:[code3value] 
```

## Sending us your segment data offline

For more information about how to send us your segment data offline, see he API's [Batch Segment Service](../digital-platform-api/batch-segment-service.md).

## Related topics

- [User ID Syncing with External Partners](user-id-syncing-with-external-partners.md)
- [Asynchronous Usersync Pixels](asynchronous-usersync-pixels.md)