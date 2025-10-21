---
title: Microsoft Monetize - Add a Creative
description: In this article, find step-by-step instructions for how to add a creative.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Add a creative

You can add a creative by either uploading a spreadsheet or the creative files directly from your computer. Only secure content is supported.

To serve on our platform, all creatives must adhere to our creative guidelines and specifications, creative standards, and other guidelines that apply to all creative types. For more information, see [Creative Guidelines and Specifications](creative-guidelines-and-specifications.md), [Creative CTV Guidelines and Specifications](creative-ctv-guidelines-and-specifications.md), and [Creative Standards](creative-standards.md).

> [!NOTE]
> When uploading in the UI, the total size of any hosted banner and video creatives should not exceed 1 GB. The current maximum size for creatives that can be uploaded through the API is approximately 220 MB. It is advisable to use the UI to upload creatives, particularly videos.

1. Go to **Advertisers** > **Creative Manager**.

1. Select an advertiser.

1. Click **New** and select the appropriate creative type from the menu that displays.

    The **Create New** screen displays.

1. Provide the creative file using one of the following methods:
    - If the creative is being hosted with Microsoft Advertising, upload the file by clicking the **Select Files** button to upload the appropriate assets.

      > [!NOTE]
      > For native creatives, you can upload a main image and icon simultaneously.

    - If the creative is being hosted on your own platform or trafficked through a third-party ad server, enter a secure URL.

    If you're adding a video or audio creative, you'll have to select one of the following tabs in order to provide the creative file:
    - **Hosted File**: For video and audio creatives that are being hosted through Microsoft Advertising's platform.
    - **Third-Party URL**: For video and audio creatives that are being trafficked through a third-party ad server.

    > [!TIP]
    > When uploading creative files, you can hold down the **Command** (if using a Mac) or **CTRL** (if using a PC) key until you've selected all the necessary files from your computer, and then click **Open**.
    >
    > For native creatives, keep the following in mind:
    >
    > - You can also upload images and icons using the **Composition** section. You can specify which native image and icon file should be used by selecting one of the files that were previously uploaded from the **Image** and **Icon** menus.
    > - To replace any of the selected files, click the **Image** and **Icon** menus in the **Composition** section and click **Select Files** or **Enter a URL**.

1. Provide basic information for the creative in the **Basic Setup** section:

    1. Enter a new name for the creative in the **Name** field, or leave the original name that currently displays.
    1. Enter a landing page URL in the **Landing Page** field that the users will be redirected to when clicking the creative, or select the **Set on the Line Item level** radio button to set it at the line item level.

        For more information, see [Dynamic Landing Pages](dynamic-landing-pages.md).

    1. For banner creatives, select a media type from the menu pull-down.

        A standard Microsoft Advertising template is selected by default. You can click the **X** in the search field next to the menu pull-down and select a different template. For more information, see [Applying Media Types and Templates to Banner Creatives](applying-media-types-and-templates-to-banner-creatives.md).

    1. For HTML5 creatives, select one of the following media types: **Standard**, **Interstitial**, or **Expandable**.
    1. For HTML5 and banner creatives, select a creative size.
    1. Beginning in September 2025, fill in the European Union (EU) political declaration. The default declaration available for all new creatives is non-political. However, if your creative is political advertising, you must declare it and also declare whether you intend to serve the ad in the EU.

1. For video and audio creatives, do any of the following:

    | Action | More Information |
    |---|---|
    | Search and select VAST features and extensions from the VAST Features section. | For more information, see [Supported VAST Features](supported-vast-features.md) and [Create a VAST Extension](create-a-vast-extension.md). |
    | Search and select companions from the Companions section. | Companions are supported if the third-party ad server supports it. You cannot associate HTML or JS banners. To serve on Spotify, associate one 640 x 640 image creative as a companion. For more information, see [Companions](companions.md). |

    For more information, see [Video Creatives](video-creatives.md) and [Audio Creatives](audio-creatives.md).

1. For native creatives, enable automatic resizing of the main native creative and icon by clicking the **Allow smart image adjustments** toggle and selecting one of the following radio buttons:

    - **Include white bars to fill placement**: Adds white space above and below the image and icon within the placement.
    - **Crop image to fit placement**: Enlarges or reduces the size of the image and icon so that they fill the entire placement.

    You can preview the image and icon files to determine which of these options are most appropriate before saving by clicking **Preview adjusted examples** and selecting one of the following radio buttons:
    - **Include white bars to fill placement**
    - **Crop image to fit placement**

    Two previews, one with the widest extreme and the other with the tallest extreme, display for each option. For more information, see [Smart Image Adjustments for Native Creatives](smart-image-adjustments-for-native-creatives.md).

    Additionally, you can add details for the native image and icon files in the **Composition** section. Click the **Additional Assets** menu to add additional fields. For more information about each asset specification, see [Native Creative Asset Specifications](native-creative-asset-specifications.md).

1. Click the **Preview** button in the left pane to preview the creative.

    For native creatives, the **Preview** button won't display until the landing page URL has been added.

1. **Optional:** [Configure tracking parameters](configuring-tracking-for-creatives.md).

1. **Optional:** [Associate the creative to the appropriate line item](associate-line-items-with-a-creative.md).

1. **Optional:** [Exclude competitive brands](exclude-competitive-brands-for-a-creative.md).

1. **Optional:** [Exclude competitive offer categories](exclude-competitive-offer-categories-for-a-creative.md).

1. [Select the appropriate audit option](select-an-audit-option-for-a-creative.md).

1. Click **Save**.

## Related topics

- [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md)
- [Native Creatives](native-creatives.md)
- [Banner and HTML5 Creatives](banner-and-html5-creatives.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
