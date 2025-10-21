---
title: Microsoft Monetize - Create a Third-Party Advertiser Pixel for Your Creatives
description: In this article, find step-by-step instructions on how to create and set up third-party creative pixels at the advertiser level for display creatives under that advertiser. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Create a third-party advertiser pixel for your creatives

You can create third-party creative pixels at the advertiser level and then apply these pixels to some or all display creatives under that advertiser.

1. Navigate to the **Advertiser Details** screen.

1. Click **Third-party Pixels**.

1. Select the associated advertiser

1. Click **New** to create a new third-party pixel.

    The **Create New Third-Party Pixel** dialog displays.

1. Enter a name for your pixel.

1. Click the **All Advertiser Creatives** button to apply the pixel to all creatives at the advertiser level, or click the **Individual Creatives** button to apply the pixel to individual creatives.

1. Click the **Serve on Secure Inventory** toggle if you want the pixel to serve on secure inventory.

1. Select the appropriate format from the **Type** menu and enter the necessary information in the corresponding text boxes.

    If you decided to serve your pixel on secure inventory, you will be prompted to provide a secure link as well as a standard link. For a list of the creative macros that you may want to append to your pixel, see [Creative Macros](creative-macros.md). For example, if you wanted to append the `CACHEBUSTER` macro to a URL format pixel, you would add the macro to the URL as follows in the **image** field: `http://www.myurl.com`**`?key=${CACHEBUSTER}`**

1. Select whether you want the pixel to also serve on Google Ad Manager inventory by doing the following:
    1. Click the **AdX** toggle.

        To render the pixel on Google Ad Manager inventory, it must be in full compliance with Google Ad Manager creative policies. For
        more information, see [Creative Standards](creative-standards.md).

    1. Click the **AdX requires vendor to be declared** to specify that your Google Ad Manager-approved pixel vendor must be declared.
    1. Search and select the necessary vendors using the search field.

        For more information, see [Google's list of external vendors that require declaration](https://developers.google.com/third-party-ads/adx-vendors?visit_id=638394332858482751-2365684177&rd=1).

1. Click **Save**.

    Once you have saved your pixel, it will have a pending audit status and is generally approved within 24 hours of submission. This will not cause the creative to be re-audited. If the pixel's status is active, then it will attain an approved audit status and begin serving on any creatives that it has been attached to. If the pixel is subsequently found to be associated with malicious activity, any creatives that it has been attached to will be suspended.

## Related topics

- [Working with Creatives](working-with-creatives.md)
- [Creative Standards](creative-standards.md)
- [Working with Advertisers](working-with-advertisers.md)
