---
title: Microsoft Monetize - Associate Segment Pixels with Creatives
description: In this article, learn how to associate specific segment pixels with your creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Associate segment pixels with creatives

You can associate specific segment pixels with your creatives. Users will be added to the segment pixels when they're viewing and/or clicking the creative.

This method of adding users to segment pixels is different than the standard method of placing a segment pixel on the page. Whereas the standard method takes place on the client (the pixel loads in the browser), the method described here is entirely server-side. Nothing loads in the browser, but instead a server-side request tells Microsoft Advertising to add the user to the specified segment pixel once the user has viewed and/or clicked the creative.

> [!NOTE]
> Because this method is entirely server-side, if the segment pixels to which you are adding the user have any piggyback pixels, those piggyback pixels will not fire. Also, this method will not call any usersync pixel with external partners, which is very important for serving on Google Ad Manager inventory. Usersync pixel calls will cause the creative to fail the Google Ad Manager creative audit process and result in a `invalid_fourth_party_call` disapproval reason since the technology vendors we sync with are likely not declared for the creative. For more information, see [User ID Syncing with External Partners](user-id-syncing-with-external-partners.md) and [Google Ad Manager Creative Audit Process](adx-creative-audit-process.md).

1. From the **Create New** or **Edit** screen, go to the **Segment Pixels** section.
1. Enter the partial/full name or ID of the existing segment pixel in the search field.
1. Select the segment pixel from the list of search results that displays.
1. Select an event (**Impression** or **Click**) that the segment pixel will trigger on.

## Related topics

- [Add a Creative](add-a-creative.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
- [Working with Segments](working-with-segments.md)
