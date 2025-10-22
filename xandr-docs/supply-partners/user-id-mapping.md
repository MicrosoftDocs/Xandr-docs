---
title: Supply Partners - User ID Mapping
description: In this article, learn how to store the user ID mapping in your system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Supply Partners - User ID mapping

To store the mapping in your system, you must place a 1x1 image pixel on your pages that calls the **getUID** service and returns Xandr UUIDs to you for storage. Format the pixel as follows:

```
<img src="https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?user_id=$UID&geo=35
&referrer=https://www.website.com" height=1 width=1>
```

A redirect URL should be specified in the `getUID` call, and it should contain the `$UID` macro. This macro will be replaced with the Xandr UUID when redirecting to the final URL, allowing the UUID to be taken in and mapped by your server.

Here's what happens when a user views a page containing the pixel:

1. The browser calls the **getUID** service.

1. The **getUID** service replaces the `$UID` macro in the redirect URL with the Xandr user ID (retrieved from the Xandr browser cookie).

1. The call is redirected to the final URL, where you receive the Xandr user ID, map it to your ID for the user, and store the mapping in your system.

Since you store the mapping on your end, you can include Xandr user IDs in your bid requests.

## Client-testing URLs

```
https://ib.client-testing.adnxs.net/getuid?https://ad.adserver.com/pixel?user_id=$UID
https://ib.client-testing.adnxs.net/mapuid?member=MEMBER_ID&user=USER_ID
```

## Secure URLs

```
https://secure.adnxs.com/getuid?https://ad.adserver.com/pixel?user_id=$UID
https://secure.adnxs.com/mapuid?member=MEMBER_ID&user=USER_ID
```

## Secure client-testing URLs

```
https://secure.ib.client-testing.adnxs.net/getuid?https://ad.adserver.com/pixel?user_id=$UID
https://secure.ib.client-testing.adnxs.net/mapuid?member=MEMBER_ID&user=USER_ID
```
