---
title: Set Up On-Page Tags for Bannerstream Video
description: This article explains about Bannerstream video. Bannerstream video uses seller tag (AST), an asynchronous JavaScript tag that runs in the header of the page.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Set up on-page tags for Bannerstream video

Xandr Bannerstream Video uses Microsoft Advertising's Seller Tag (AST), an asynchronous JavaScript tag that runs in the header of the page. These tags are defined and loaded in the page header and are activated by "showing" the tags in the page body.

> [!TIP]
> For select use cases, AST can also be defined, loaded, and shown in the page body.

## How it works

An in-banner video ad unit can be added to a web page in any place where a regular banner might be displayed. The Bannerstream video ad unit is included as a `<div>` element in the page body. The `<div>` element in the page body refers to the video ad unit using a Target Identifier which corresponds to a definition of that Target Identifier in the page header.

## Example

Using AST, you can define the tag (placement) you intend to call. When defining a in-banner video placement, there are additional options that you can pass to specify how you would like the player to appear and behave on your page. A sample call to `defineTag` is shown here:

```
    apntag.defineTag({
        //required params
        targetId: 'banner_div',
        tagId: 31,
        sizes: [320, 250],
        allowedFormats: ['video'],
        targetingParams: {},
        video: {
            frameworks: [1,2]
        },
        //the options object is passed to the renderer which creates the player on the page
        rendererOptions: {
            playerTechnology: [
                'flash',
                'html5'
            ],
            adText: 'Ad',
            showMute: true,
            showVolume: true,
            showProgressBar: true,
            autoInitialSize: true,
            allowFullscreen: true,
            skippable: {
                videoThreshold: 10,
                videoOffset: 5,
                skipLocation: 'top-right',
                skipText: 'Video can be skipped in %%TIME%% seconds',
                skipButtonText: 'Continue'
            },
            preShow: {
                type: "image",
                url: "http://example.com/images/pre-show-image.jpeg"
            },
            postShow: {
                type: "image",
                url: "http://example.com/images/post-show-image.jpeg"
            },
            fallback: {
                type: "image",
                url: "http://example.com/images/post-show-image.jpeg"
            }
        }
    });
```
