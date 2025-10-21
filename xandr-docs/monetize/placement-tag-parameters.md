---
title: Placement Tag Parameters
description: In this article, find information about the parameters associated with placement tags along with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Placement tag parameters

> [!NOTE]
> Microsoft Advertising now supports a domain, [adnxs-simple.com](http://adnxs-simple.com/), which does not send or read browser cookies on requests. Clients can leverage this cookie-free domain when there is no consent to use personal data. Relevant calls initiated by Microsoft Advertising will automatically use this domain when there is no consent or when cookies are not required for the function. For more information, see [Part of Service Policies](../policies-regulations/index.yml).

When you export a placement tag, you can include placeholders to pass in additional query string parameters to the Microsoft Advertising platform during the ad call. This document describes the allowed parameters. For the parameters used for video placements, see [Target Video Attributes via Query String Parameters](target-video-attributes-via-query-string-parameters.md).

## Placement tags

> [!NOTE]
>
> - Currently the Microsoft Advertising click tracking macro, (`${CLICK_URL}` or `${CLICK_URL_ENC}`), and the cache buster macro, `${CACHEBUSTER}`, **DO NOT** work in placement tags. You need to use a publisher-supplied third-party click tracker and/or third-party cache buster/time stamp.
> - There is a maximum of 5 custom targeting parameters per placement (used for query string targeting on the campaign) that will be processed by the Microsoft Advertising platform.
> - Placement tag parameters, for example age and gender, or any unique parameter you choose to add, can be included in the tag in order to allow more granular targeting when working with managed inventory. To learn more about how this kind of targeting works, see [Query String Targeting via Placement Tags and Segments](query-string-targeting-via-placement-tags-and-segments.md).

## Parameters

| Parameter | Description |
|---|---|
| **age** | The numerical age, birth year, or hyphenated age range of the user. <br> Examples: `age=56`, `age=1974`, `age=25-35` |
| **cb** | Publisher-supplied cache buster. This is just a placeholder into which the publisher can insert their own cache buster. |
| **custom_pub_data** | **Deprecated**. The contents of `custom_pub_data` should be 70 characters or less (after that it is truncated). It is permissible to pass more than 70 characters, but only the first 70 will be logged. The characters newline `("\n")`, tab `("\t")`, and backslash `("\")` are not allowed. Otherwise, all characters that can be displayed by the standard C library function `isprint` are allowed. |
| **ext_inv_code** | A predefined value passed on the query string that can be used in reporting. The value must be entered into the system before it is logged. For more information, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). <br> Example: `ext_inv_code=10039` |
| **gender** | The gender of the user. Allowed values: `m` for male, `f` for female <br> Example: `gender=m` |
| **id**, **ID** | The identification number (integer) belonging to a placement. <br> Example: `id=5202` |
| **inv_code** | The code entered on the placement. This can be used instead of placement ID, but must be used with `member_id` as well. <br> Example: ``inv_code=ABC&member=1`` |
| **loc** | The user's location expressed in latitude and longitude, in the format: `snnn.ddddddddddddd,snnn.ddddddddddddd`. Up to 13 decimal places of precision are allowed. |
| **position** | The position of the tag on the page. Can be `above` (above the fold) or `below`. <br><br> **Note**: This option is not available from the UI but can be appended to the placement tag. Also, `above` and `below` must be in lower case. <br><br> Example: `position=above` |
| **private_sizes** | The additional sizes that are allowed to serve only for custom deals or packages when private sizes are allowed by the deal or package. <br> Example: `private_sizes=150x300,320x480` |
| **promo_alignment** | Allowed values: `none` or `center`. <br> Example: `promo_alignment=center` |
| **promo_sizes** | Allow additional sizes to use this placement. <br><br> **Note**: The placement needs to be set to `sizeless` and the actual size will need to be passed in the `size` parameter below. <br><br> Example: `promo_sizes=728x90,150x300` |
| **psa** | If `true`, PSAs will serve if the auction has no winner. Otherwise, an empty `200 OK` HTTP response will be returned. This could be useful for clients who wish to try filling unsold impressions from a different inventory source. Instead of serving a static tag as a default creative, the blank response can offer more flexibility in treating unsold impressions. <br> Allowed values: `true`, `false`, `1`, or `0`. <br> Example: `psa=0` |
| **pt1**, **pt2**, **pt3**, **pt4**, **pt5**, **pt6**, **pt7**, **pt8**, **pt9** | These can be used to pass custom data through managed placements to managed 3rd-party creatives. For more information, see [Create a Placement Tag Macro](create-a-placement-tag-macro.md). <br> Example: `pt1=products:ipad,ios,iphone` |
| **pubclick** | Publisher-supplied URL for third-party click tracking. This is just a placeholder into which the publisher can insert their own click tracker. This parameter should be used for an **unencoded** tracker. This parameter is expected to be the last parameter in the URL. Please note that the click tracker placed in this parameter will only fire if the creative winning the auction is using Microsoft Advertising click tracking properly. <br> Example: `pubclick=https://click.adserver.com` |
| **pubclickenc** | Publisher-supplied URL for third-party click tracking. This is just a placeholder into which the publisher can insert their own click tracker. This parameter should be used for an **encoded** tracker. This parameter does not need to be the last parameter in the URL. Please note that the click tracker placed in this parameter will only fire if the creative winning the auction is using Microsoft Advertising click tracking properly. <br> Example: `pubclickenc=https%3A%2F%2Fclick.adserver.com` |
| **referrer** | **Deprecated**. Microsoft Advertising performs domain detection automatically. |
| **reserve** | The reserve price for this inventory, which is the minimum net amount the placement will accept for placing a creative. This parameter will override a preset price and will set the hard floor (and soft floor where relevant) if Yield Management is not being used or if the reserve price is greater in value than the YM Floor wherein the Floor Rule has the override setting on. <br><br> **Note**: This option is not available from the UI and must be appended to the placement tag manually. <br><br> Example: `reserve=5.00` |
| **size** | The size of the placement - required if sizeless. This parameter will NOT override a preset size format. Allowed format: `widthXheight`. <br> Example: `size=300x250` |
| **truncate_ip** | If `1` or `true`, the last octet of the user's IP address will be truncated in the bid request. Use this flag for ad tags in jurisdictions where IP address is considered personally identifiable information. The full IP address will continue to be used for operational purposes and security, of course. For more details about privacy, see [Part of Service Policies](../policies-regulations/index.yml). <br> Example: `truncate_ip=1` |
| **use_cookies** | If `0`, do not use any data that Microsoft Advertising stores on the user for this impression. This includes data used for segment targeting, frequency capping, and conversion attribution. For more information on cookie-related settings, see [Publisher Service](../digital-platform-api/publisher-service.md) and [Creative Macros](creative-macros.md). <br> Example: `use_cookies=0` |

## Example

```
<!-- BEGIN IFRAME TAG - Fancy Cracker Homepage < - DO NOT MODIFY --> 
<IFRAME SRC="https://ib.sand-08.adnxs.net/tt?id=5202&cb=[CACHEBUSTER]&age=[AGE]&pubclick=[INSERT_CLICK_TAG]" FRAMEBORDER="0" SCROLLING="no" MARGINHEIGHT="0" MARGINWIDTH="0" TOPMARGIN="0" LEFTMARGIN="0" ALLOWTRANSPARENCY="true" WIDTH="728" HEIGHT="90"></IFRAME> 
<!-- END TAG -->
```

## Related topics

- [Create a Placement](create-a-placement.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)
- [Export Placement Tags](export-placement-tags.md)
