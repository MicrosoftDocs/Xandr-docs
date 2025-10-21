---
title: Microsoft Monetize - User Mapping (Visual and Walk-Through)
description: Learn how to map your internal user IDs and Microsoft Advertising user IDs using an example given in this page. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - User mapping (visual and walk-through)

[User ID Mapping](user-id-mapping-with-getuid-and-mapuid.md) describes how to map your internal user IDs and Microsoft Advertising user IDs so that you can pass Microsoft Advertising to your internal userdata that you will use to buy impressions. Here we describe visually what's happening and walk through the synching process.

In this example the advertiser Prostarr Sportswear stores the ID map on their end. They use the getuid call to obtain the Microsoft Advertising ID via querystring parameter.

## Example

Let's say Prostarr Sportswear has internal IDs on everyone who has visited their retail site, and some of those IDs are tied to past purchases. They want to sync user IDs with Microsoft Advertising, so that they can add this data to our server-side cookie store and use it to target users. They put an Microsoft Advertising getUID pixel on their homepage. Let's assume that Microsoft Advertising has "seen" this user before somewhere in their system and so has marked the user's browser cookie with an Microsoft Advertising user ID.

:::image type="content" source="media/usermap.png" alt-text="Sceenshot showing Microsoft Advertising getUID pixel on the homepage of Prostarr Sportswear.":::

**Step 1.** When the page loads, the browser makes this call/request to Microsoft Advertising: `https://ib.``adnxs``.com/getuid?https://prostarradserver.com/pixel?``adnxs``_uid=$UID`. The request includes the `ib.``adnxs``.com` browser cookie (which is passed in the header of the HTTP request). The cookie includes the Microsoft Advertising user ID.

**Step 2.** The Microsoft Advertising Impression Bus passes back the URL of Prostarr's ad server that was contained in the above querystring. In addition, it appends the Microsoft Advertising user ID (from the user's Microsoft Advertising browser cookie) in place of $UID. `https://prostarradserver.com/pixel?``adnxs``_uid=12345678.`

**Step 3.** The call in step 2 includes the Microsoft Advertising ID. In addition, Prostarr's browser cookie data is passed with the call. Prostarr's ad server can now link the two in their database.
