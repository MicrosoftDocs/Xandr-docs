---
title: User ID Syncing with External Partners
description: In this page learn about user ID syncing that Microsoft Advertising initiates to have a user ID associated with all users in all ad calls. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# User ID syncing with external partners

> [!IMPORTANT]
> This feature is deprecated. Refer to [Asynchronous Usersync Pixels](asynchronous-usersync-pixels.md) for the current syncing process.

This document describes the user ID syncing that Microsoft Advertising initiates in order to have a user ID associated with all users in all ad calls. For more information about how members of the Microsoft Advertising platform can initiate ID syncing to map their proprietary data to an Microsoft Advertising user ID, see [User ID Mapping with getUID and mapUID](user-id-mapping-with-getuid-and-mapuid.md).

**Asynchronous Usersync Pixels**: We've updated how usersync pixels are fired from publishers' pages to increase user match rates without affecting page load times. For more detailed information about this change, see [Asynchronous Usersync Pixels](asynchronous-usersync-pixels.md).

## Why we sync user IDs with our external partners

There are three kinds of platform partners with whom we need to sync user IDs: supply partners, demand partners, and data providers. To sync user IDs, we use "usersync pixels."

## Supply partners

When we get an ad call, we have to know the user's Microsoft Advertising user ID so we can apply frequency and recency, segment, and other data. We can easily do this when our tag is on the page (i.e., the tag domain is ib.`adnxs``.com `or has been CNAMEd to `ib.``adnxs``.com`) because we can access the user's `ib.``adnxs``.com` browser cookie where we store an Microsoft Advertising ID.

For supply partners where we don't have a tag on the page, the supply partner passes us a user ID. This means that we must have a mapping of their IDs and our IDs in place in advance of the ad call so we can recognize this user. This mapping can be done at any time as long as it is in advance of the ad call. Then the mapping is stored either in the Microsoft Advertising database (our partner sends us their ID and we translate it) or in the supply partner's database (our partner sends us our ID) for use at the time of the ad call.

## Bidders

We initiate the usersyncing process with external bidders because these bidders need to be able to make purchasing decisions based on their own user data.

## Data providers

We sync with data providers because they send us more data to bid on. This leads to making better bidding decisions based on having better information available.

## Data security and partner/customer relationships

The only information collected with usersync pixels is a user ID. We do not use this process to collect other user data or allow our partners to collect user data through this access to the user.

We believe collecting this information benefits all members. Usersyncing enhances the pool of available inventory for buyers, helps monetize inventory for sellers, and generally lifts all boats. If you would like to limit usersyncing, you can turn it off for Supply Partners, Demand Partners, or Data Providers in the Publisher details under **Advanced** > **User ID Syncing**. To limit specific ad technology providers from appearing on your digital property, create an ad quality rule at the Publisher level and ban each provider under **Ad Profile** > **Ad Servers**.

## How we sync with usersync pixels

When we see a user with no Microsoft Advertising ID (whether in the Microsoft Advertising browser cookie or passed to us in an ad call), we think of this as "the first time we've seen that user." This may be because we really never have seen them before, because they cleared their cookies, or because their browser doesn't accept third-party cookies.

If our tag isn't on the page, we don't bid. If our tag is on the page, the following steps happen:

- After the auction is held, a creative is served to the webpage.

- We also drop a usersync pixel with one or more of our partners. For example, a supply partner may have a URL at which they want to receive the Microsoft Advertising user ID for storage in their database. This URL is formatted like so: `https://exchangea.net/pixel?id=$UID`. We then include this URL, populated with the user's newly set Microsoft Advertising ID in the `$UID` macro, along with the creative. Because the supply partner's browser cookie is included in the HTTP request, the partner can now store the mapping.

  In addition, we sometimes drop a usersync pixel in these additional cases:

  - After other `ib.``adnxs``.com` pixels fire, such as segment or conversion pixels.
  - On CNAME redirects.

## Cookieless users

When the session cookie did not persist, we have a `no_cookie_user` flag in the bid request. For certain campaigns we do not submit a bid for no cookie users (unless the "Show to users without cookies" box is checked).

- **CPA Optimization:** When there is no user ID, we cannot attribute conversions to anything, so we do not bid on behalf of campaigns that are using CPA optimization.
- **Frequency/Recency Caps:** If frequency or recency caps are in place, we must see the user's cookie to determine how recently they have last seen an ad.

## Initiate automatic user ID syncs with our external partners

Publishers and advertisers can automatically sync page visitors' user IDs with all Microsoft Advertising external partners by adding the following code to pages:

``` 
<iframe height="0" width="0" marginwidth="0" marginheight="0" scrolling="no"
         frameborder="0" src="//ib.adnxs.com/async_usersync_file" style="border: 0px; display:
         none;"></iframe>
```

The HTML `<iframe>` element uses the endpoint `async_usersync_file` to automatically force a Microsoft Advertising usersync process with all of our external partners. This is an user-syncing alternative that can replace using our hardcoded, usersync code or segment pixels.

## Related topics

- [User ID Mapping with getUID and mapUID](user-id-mapping-with-getuid-and-mapuid.md)
- [Asynchronous Usersync Pixels](asynchronous-usersync-pixels.md)