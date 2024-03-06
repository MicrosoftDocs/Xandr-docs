---
title: Viewing & Managing Cookie Segments
description: Explore efficient troubleshooting by viewing/managing segments, customizing cookie details, and effortlessly mimicking diverse user profiles.
ms.date: 10/28/2023
---

# Viewing & managing cookie segments

When troubleshooting an issue, it is sometimes helpful to: (1) see what Microsoft Advertising segments you belong to; and (2) override certain aspects of your cookie, such as what country, region, city, postal, and DMA you are in so that you can mimic different kinds of users. This page walks you through the process.

> [!NOTE]
> All browser cookie calls must use secure https protocols. Requests made using http will not generate valid results.

## Data security

In order to ensure data security and privacy, when using the cookie viewer, you must include your member ID and dongle. This ensures you will only see the segments that belong to your member.

```
https://ib.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE 
```

If you are unsure of your member ID and/or dongle, you can go to any placement in Monetize and run a debug auction. Your member ID and dongle will be in the URL of the debug auction.

## View your cookie attributes

When you navigate to the cookie viewer, you will see your Microsoft Advertising User ID, what geo overrides you have set, and all of the segments you belong to.

## Override your cookie attributes

During testing or debugging, it can be very helpful to override your cookie data. For example, if you are running a [debug auction](understanding-the-debug-auction.md), and you want a campaign to bid that is targeting users only in Brazil, but you are based in the US, you must override your country geo code to place yourself in Brazil. To do that, run the same URL string as before, but add the country code for Brazil at the end, like this:

```
https://ib.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&country=BR 
```

You can also override multiple geo codes simultaneously, like this:

```
https://ib.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&country=US&region=MT&dma=743 
```

The following table defines what codes are available for overriding, the corresponding API service to retrieve allowed values, and the API field that values are stored in:

| Geo Code | API Service | API Field |
|---|---|---|
| `Country` | [Country Service](../digital-platform-api/country-service.md) | code |
| `Region` | [Region Service](../digital-platform-api/region-service.md) | `iso_3166_2` |
| `DMA` | [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md) | code |
| `City` | [City Service](../digital-platform-api/city-service.md) | name |
| `Postal Code` | [Postal Code Service](../digital-platform-api/postal-code-service.md) | code |

## Remove your geo override

You can use the following to clear all your geo overrides:

```
https://ib.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&clear=geo 
```

## Segments

You can view the segments you belong to under the "Server-side Data" section. This section also tells you:

- the value associated with the segment,
- the last time you fired the segment,
- when you expire out of the segment, and
- whether the segment is active.

  The cookie viewer also allows you to see the cookie of other users besides yourself. To do this, you must know the  Microsoft Advertising user ID and use this format:

  ```
  https://ib.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&uid=USER_ID 
  ```

  If you are located in the US and want to view a European user's cookie or vice versa, you must hard code the user's data center ID into the URL:

- **For US Users**

  ```
  https://ib.nym1.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&uid=USER_ID 
  ```

- **For EU Users:**

  ```
  https://ib.ams1.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&uid=USER_ID 
  ```

- **For APAC Users:**

  ```
  https://ib.sin1.adnxs.com/cookie?member_id=MEMBER_ID&dongle=DONGLE&uid=USER_ID 
  ```

## Sample segment log

```
User ID: 5947483712413990772 Client Data Geo Overrides Country: Region: City: Postal: DMA: 0 Segments (112) Num segments: 112 Segment 6755 - seen 3746 minutes ago, doesn't expire Segment 6755 - seen 3738 minutes ago, doesn't expire Segment 7222 - seen 7259 minutes ago, doesn't expire Segment 7222 - seen 3746 minutes ago, doesn't expire Segment 7222 - seen 3738 minutes ago, doesn't expire Segment 8230 - seen 7259 minutes ago, doesn't expire Segment 8230 - seen 3746 minutes ago, doesn't expire Segment 8230 - seen 3738 minutes ago, doesn't expire Segment 15397 - seen 7259 minutes ago, doesn't expire Segment 15397 - seen 3746 minutes ago, doesn't expire Segment 15414 - seen 3746 minutes ago, doesn't expire Segment 15414 - seen 3738 minutes ago, doesn't expire Segment 15492 - seen 20378 minutes ago, doesn't expire Segment 15541 - seen 70374 minutes ago, doesn't expire Segment 7012 - seen 40061 minutes ago, doesn't expire Segment 6987 - seen 40061 minutes ago, doesn't expire Segment 7018 - seen 40061 minutes ago, doesn't expire Segment 18446 - seen 7259 minutes ago, doesn't expire Segment 18446 - seen 3746 minutes ago, doesn't expire Segment 18446 - seen 3738 minutes ago, doesn't expire Segment 18794 - seen 3738 minutes ago, doesn't expire Segment 19090 - seen 3738 minutes ago, doesn't expire Segment 19090 - seen 3746 minutes ago, doesn't expire Segment 19650 - seen 73520 minutes ago, doesn't expire Segment 19652 - seen 73520 minutes ago, doesn't expire Segment 6755 - seen 22618 minutes ago, doesn't expire Segment 8230 - seen 22618 minutes ago, doesn't expire Segment 19648 - seen 71841 minutes ago, doesn't expire Segment 5038 - seen 15601 minutes ago, doesn't expire Segment 20035 - seen 7259 minutes ago, doesn't expire Segment 20035 - seen 3746 minutes ago, doesn't expire Segment 20035 - seen 3738 minutes ago, doesn't expire Segment 21970 - seen 3746 minutes ago, doesn't expire Segment 21970 - seen 3738 minutes ago, doesn't expire Segment 21971 - seen 7259 minutes ago, doesn't expire Segment 21971 - seen 3746 minutes ago, doesn't expire Segment 21973 - seen 7259 minutes ago, doesn't expire Segment 21973 - seen 3746 minutes ago, doesn't expire Segment 21973 - seen 3738 minutes ago, doesn't expire Segment 22594 - seen 7259 minutes ago, doesn't expire Segment 22594 - seen 3746 minutes ago, doesn't expire Segment 22594 - seen 3738 minutes ago, doesn't expire Segment 22606 - seen 7259 minutes ago, doesn't expire Segment 22606 - seen 3746 minutes ago, doesn't expire Segment 22606 - seen 3738 minutes ago, doesn't expire Segment 23297 - seen 7259 minutes ago, doesn't expire Segment 23297 - seen 3746 minutes ago, doesn't expire Segment 23297 - seen 3738 minutes ago, doesn't expire Segment 24366 - seen 3738 minutes ago, doesn't expire Segment 24724 - seen 30887 minutes ago, doesn't expire Segment 17515 - seen 67311 minutes ago, doesn't expire Segment 12221 - seen 64197 minutes ago, doesn't expire Segment 15529 - seen 20378 minutes ago, doesn't expire Segment 6919 - seen 40061 minutes ago, doesn't expire Segment 6920 - seen 40061 minutes ago, doesn't expire Segment 5195 - seen 61323 minutes ago, doesn't expire Segment 5206 - seen 61323 minutes ago, doesn't expire Segment 21755 - seen 60112 minutes ago, doesn't expire Segment 19522 - seen 60109 minutes ago, doesn't expire Segment 12753 - seen 60112 minutes ago, doesn't expire Segment 17878 - seen 60111 minutes ago, doesn't expire Segment 5205 - seen 32508 minutes ago, doesn't expire Segment 11653 - seen 59249 minutes ago, doesn't expire Segment 20182 - seen 57430 minutes ago, doesn't expire Segment 21783 - seen 57814 minutes ago, doesn't expire Segment 12817 - seen 57823 minutes ago, doesn't expire Segment 23399 - seen 45648 minutes ago, doesn't expire Segment 18039 - seen 53006 minutes ago, doesn't expire Segment 22199 - seen 52815 minutes ago, doesn't expire Segment 21765 - seen 52708 minutes ago, doesn't expire Segment 12752 - seen 52706 minutes ago, doesn't expire Segment 21556 - seen 51162 minutes ago, doesn't expire Segment 21782 - seen 51162 minutes ago, doesn't expire Segment 21828 - seen 49771 minutes ago, doesn't expire Segment 19090 - seen 22618 minutes ago, doesn't expire Segment 21970 - seen 7259 minutes ago, doesn't expire Segment 18794 - seen 22618 minutes ago, doesn't expire Segment 21973 - seen 22618 minutes ago, doesn't expire Segment 20035 - seen 22618 minutes ago, doesn't expire Segment 21971 - seen 3738 minutes ago, doesn't expire Segment 15414 - seen 22618 minutes ago, doesn't expire Segment 15397 - seen 3738 minutes ago, doesn't expire Segment 22216 - seen 47770 minutes ago, doesn't expire Segment 10072 - seen 31419 minutes ago, doesn't expire Segment 11251 - seen 47276 minutes ago, doesn't expire Segment 22606 - seen 22618 minutes ago, doesn't expire Segment 22594 - seen 22618 minutes ago, doesn't expire Segment 15508 - seen 20378 minutes ago, doesn't expire Segment 6858 - seen 40061 minutes ago, doesn't expire Segment 23397 - seen 18157 minutes ago, doesn't expire Segment 7222 - seen 22618 minutes ago, doesn't expire Segment 24622 - seen 24684 minutes ago, doesn't expire Segment 21827 - seen 24086 minutes ago, doesn't expire Segment 20180 - seen 23849 minutes ago, doesn't expire Segment 25316 - seen 3738 minutes ago, doesn't expire Segment 25321 - seen 22618 minutes ago, doesn't expire Segment 18446 - seen 22618 minutes ago, doesn't expire Segment 19521 - seen 22485 minutes ago, doesn't expire Segment 20172 - seen 21832 minutes ago, doesn't expire Segment 25266 - seen 20425 minutes ago, doesn't expire Segment 12812 - seen 18953 minutes ago, doesn't expire Segment 25321 - seen 3738 minutes ago, doesn't expire Segment 26035 - seen 18119 minutes ago, doesn't expire Segment 26813 - seen 3034 minutes ago, expires in 40166 min Segment 26840 - seen 3034 minutes ago, expires in 40166 min Segment 26859 - seen 3034 minutes ago, expires in 40166 min Segment 27022 - seen 3034 minutes ago, expires in 40166 min Segment 26840 - seen 16616 minutes ago, doesn't expire Segment 26859 - seen 16616 minutes ago, doesn't expire Segment 27280 - seen 3034 minutes ago, expires in 40166 min Segment 27286 - seen 3034 minutes ago, expires in 40166 min Segment 27330 - seen 3034 minutes ago, expires in 40166 min ACB cookies (0) ID Member Size Expires in (s) URL Server-side Data Total imps: 0 Total sessions: 0 Session imps: 0 Num segments: 74 Segment 5038 - seen 3015 minutes ago, doesn't expire Segment 5195 - seen 1080 minutes ago, doesn't expire Segment 5205 - seen 1080 minutes ago, doesn't expire Segment 5206 - seen 1080 minutes ago, doesn't expire Segment 6755 - seen 3738 minutes ago, doesn't expire Segment 6858 - seen 1080 minutes ago, doesn't expire Segment 6919 - seen 1080 minutes ago, doesn't expire Segment 6920 - seen 1080 minutes ago, doesn't expire Segment 6987 - seen 1080 minutes ago, doesn't expire Segment 7012 - seen 1080 minutes ago, doesn't expire Segment 7018 - seen 1080 minutes ago, doesn't expire Segment 7222 - seen 3738 minutes ago, doesn't expire Segment 8230 - seen 3738 minutes ago, doesn't expire Segment 10072 - seen 3015 minutes ago, doesn't expire Segment 11251 - seen 1080 minutes ago, doesn't expire Segment 11291 - seen 3015 minutes ago, expires in 40185 min Segment 11653 - seen 1080 minutes ago, doesn't expire Segment 12221 - seen 1080 minutes ago, doesn't expire Segment 12752 - seen 1080 minutes ago, doesn't expire Segment 12753 - seen 1080 minutes ago, doesn't expire Segment 12812 - seen 1080 minutes ago, doesn't expire Segment 12817 - seen 1080 minutes ago, doesn't expire Segment 15397 - seen 3738 minutes ago, doesn't expire Segment 15414 - seen 3738 minutes ago, doesn't expire Segment 15492 - seen 1080 minutes ago, doesn't expire Segment 15508 - seen 1080 minutes ago, doesn't expire Segment 15529 - seen 1080 minutes ago, doesn't expire Segment 15541 - seen 1080 minutes ago, doesn't expire Segment 17515 - seen 1080 minutes ago, doesn't expire Segment 17878 - seen 1080 minutes ago, doesn't expire Segment 18039 - seen 1080 minutes ago, doesn't expire Segment 18446 - seen 3738 minutes ago, doesn't expire Segment 18794 - seen 3738 minutes ago, doesn't expire Segment 19090 - seen 3738 minutes ago, doesn't expire Segment 19521 - seen 1080 minutes ago, doesn't expire Segment 19522 - seen 1080 minutes ago, doesn't expire Segment 19648 - seen 1080 minutes ago, doesn't expire Segment 19650 - seen 1080 minutes ago, doesn't expire Segment 19652 - seen 1080 minutes ago, doesn't expire Segment 20035 - seen 3738 minutes ago, doesn't expire Segment 20172 - seen 1080 minutes ago, doesn't expire Segment 20180 - seen 1080 minutes ago, doesn't expire Segment 20182 - seen 1080 minutes ago, doesn't expire Segment 21556 - seen 1080 minutes ago, doesn't expire Segment 21755 - seen 1080 minutes ago, doesn't expire Segment 21765 - seen 1080 minutes ago, doesn't expire Segment 21782 - seen 1080 minutes ago, doesn't expire Segment 21783 - seen 1080 minutes ago, doesn't expire Segment 21827 - seen 1080 minutes ago, doesn't expire Segment 21828 - seen 1080 minutes ago, doesn't expire Segment 21970 - seen 3738 minutes ago, doesn't expire Segment 21971 - seen 3738 minutes ago, doesn't expire Segment 21973 - seen 3738 minutes ago, doesn't expire Segment 22199 - seen 1080 minutes ago, doesn't expire Segment 22216 - seen 1080 minutes ago, doesn't expire Segment 22594 - seen 3738 minutes ago, doesn't expire Segment 22606 - seen 3738 minutes ago, doesn't expire Segment 23297 - seen 3738 minutes ago, doesn't expire Segment 23397 - seen 1080 minutes ago, doesn't expire Segment 23399 - seen 1080 minutes ago, doesn't expire Segment 24366 - seen 3738 minutes ago, doesn't expire Segment 24622 - seen 1080 minutes ago, doesn't expire Segment 24724 - seen 1080 minutes ago, doesn't expire Segment 25266 - seen 1080 minutes ago, doesn't expire Segment 25316 - seen 3738 minutes ago, doesn't expire Segment 25321 - seen 3738 minutes ago, doesn't expire Segment 26035 - seen 1080 minutes ago, doesn't expire Segment 26813 - seen 3034 minutes ago, expires in 40166 min Segment 26840 - seen 3034 minutes ago, expires in 40166 min Segment 26859 - seen 3034 minutes ago, expires in 40166 min Segment 27022 - seen 3034 minutes ago, expires in 40166 min Segment 27280 - seen 3034 minutes ago, expires in 40166 min Segment 27286 - seen 3034 minutes ago, expires in 40166 min Segment 27330 - seen 3034 minutes ago, expires in 40166 min User info for 1 bidders Bidder 25: {"uid":"ck82lxav3ano"} Server-side Discrepancies 6755 - seen 8 earlier on client side 7222 - seen 3521 earlier on client side 7222 - seen 8 earlier on client side 8230 - seen 3521 earlier on client side 8230 - seen 8 earlier on client side 15397 - seen 3521 earlier on client side 15397 - seen 8 earlier on client side 15414 - seen 8 earlier on client side 15492 - seen 19298 earlier on client side 15541 - seen 69294 earlier on client side 7012 - seen 38981 earlier on client side 6987 - seen 38981 earlier on client side 7018 - seen 38981 earlier on client side 18446 - seen 3521 earlier on client side 18446 - seen 8 earlier on client side 19090 - seen 8 earlier on client side 19650 - seen 72440 earlier on client side 19652 - seen 72440 earlier on client side 6755 - seen 18880 earlier on client side 8230 - seen 18880 earlier on client side 19648 - seen 70761 earlier on client side 5038 - seen 12586 earlier on client side 20035 - seen 3521 earlier on client side 20035 - seen 8 earlier on client side 21970 - seen 8 earlier on client side 21971 - seen 3521 earlier on client side 21971 - seen 8 earlier on client side 21973 - seen 3521 earlier on client side 21973 - seen 8 earlier on client side 22594 - seen 3521 earlier on client side 22594 - seen 8 earlier on client side 22606 - seen 3521 earlier on client side 22606 - seen 8 earlier on client side 23297 - seen 3521 earlier on client side 23297 - seen 8 earlier on client side 24724 - seen 29807 earlier on client side 17515 - seen 66231 earlier on client side 12221 - seen 63117 earlier on client side 15529 - seen 19298 earlier on client side 6919 - seen 38981 earlier on client side 6920 - seen 38981 earlier on client side 5195 - seen 60243 earlier on client side 5206 - seen 60243 earlier on client side 21755 - seen 59032 earlier on client side 19522 - seen 59029 earlier on client side 12753 - seen 59032 earlier on client side 17878 - seen 59031 earlier on client side 5205 - seen 31428 earlier on client side 11653 - seen 58169 earlier on client side 20182 - seen 56350 earlier on client side 21783 - seen 56734 earlier on client side 12817 - seen 56743 earlier on client side 23399 - seen 44568 earlier on client side 18039 - seen 51926 earlier on client side 22199 - seen 51735 earlier on client side 21765 - seen 51628 earlier on client side 12752 - seen 51626 earlier on client side 21556 - seen 50082 earlier on client side 21782 - seen 50082 earlier on client side 21828 - seen 48691 earlier on client side 19090 - seen 18880 earlier on client side 21970 - seen 3521 earlier on client side 18794 - seen 18880 earlier on client side 21973 - seen 18880 earlier on client side 20035 - seen 18880 earlier on client side 15414 - seen 18880 earlier on client side 22216 - seen 46690 earlier on client side 10072 - seen 28404 earlier on client side 11251 - seen 46196 earlier on client side 22606 - seen 18880 earlier on client side 22594 - seen 18880 earlier on client side 15508 - seen 19298 earlier on client side 6858 - seen 38981 earlier on client side 23397 - seen 17077 earlier on client side 7222 - seen 18880 earlier on client side 24622 - seen 23604 earlier on client side 21827 - seen 23006 earlier on client side 20180 - seen 22769 earlier on client side 25321 - seen 18880 earlier on client side 18446 - seen 18880 earlier on client side 19521 - seen 21405 earlier on client side 20172 - seen 20752 earlier on client side 25266 - seen 19345 earlier on client side 12812 - seen 17873 earlier on client side 26035 - seen 17039 earlier on client side 26840 - seen 13582 earlier on client side 26859 - seen 13582 earlier on client side 
```
