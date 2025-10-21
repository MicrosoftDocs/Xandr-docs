---
title: Vertical Video Formats
description: This page provides an overview on Vertical Video formats and explains steps to setup a Vertical Video.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Vertical video formats

Vertical video formats are designed for display on smartphones, and use an aspect ratio that can be square, or longer than it is wide. For example, unlike a traditional tall creative for HDTV measuring 1920 x 1080 pixels, a vertical version might be 1080 pixels wide and 1920 pixels tall. A square video creative might be 600 x 600 pixels.

Vertical videos can be displayed either in a "native" or full-screen mode. Native mode displays the video alongside other on-screen content. Full-screen mode shows video controls overlaid on the creative. In either case, the video is displayed in its true vertical aspect ratio, without pillarboxing or letterboxing.

Currently, vertical video is only supported for outstream video placements, which use Microsoft Advertising's seller tag (AST). Supported aspect ratios are 9:16, 3:4, and 1:1. For more information about using AST, see the documentation for [AST](../seller-tag/seller-tag.md) and the [AST API Reference](../seller-tag/ast-api-reference.md).

To set up vertical video:

1. Create a video placement that includes the width and height of the creative.
    > [!NOTE]
    >  If you want to filter out bids that don't correspond to the preferred aspect ratio, set the aspect ratio on the placement using the Video Settings tab of the Inventory Manager and select the **Buyer creatives must match aspect ratio** checkbox.

1. In the `rendererOptions` parameter of the `defineTag` element in the AST, specify the desired aspect ratio as shown in the example:

    ``` 
    rendererOptions: {
        "aspectRatio": "9:16",
    }
    ```

1. Optionally, enable and set a maximum height for the player as shown in the following example. The player will adjust to maintain the aspect ratio.

    ``` 
    "maxHeight": {
        "enabled": true,
        "height": 480
    }
    ```

    > [!NOTE]
    > If you set a maxHeight lower than 300, the player control bar will not be visible on the player. Keep in mind that if you have also enabled skippability, the skip text may need to be updated to fit in the player window. For mobile devices, the `maxHeight` setting is only applied when the aspect ratio is 9:16.

1. If you want vertical video to render correctly in sidestream mode, define its width in `rendererOptions`, as shown in the following example. Note that the height parameter has been removed. When you specify either width or height but not both, the other (width or height) value is automatically calculated to match the aspect ratio needed for vertical presentation.

    ``` 
    rendererOptions: {
         "aspectRatio": "9:16",
         "sideStream": {
              "enabled": true,
              "maxPageOverlay": 30, 
              "width": 300, 
              "position": "bottom-right", 
              "xOffset": 0, 
              "yOffset": 0 
         },
    }
    ```

    > [!TIP]
    > If you previously deployed vertical video without specifying `maxHeight`, and your vertical ad display is too tall, you can use the **Max Video Height** setting on the **Video** tab of the Placement UI to limit the player height.