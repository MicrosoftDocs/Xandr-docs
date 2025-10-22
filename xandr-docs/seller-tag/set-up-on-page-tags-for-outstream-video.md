---
title: Set Up On-Page Tags for Outstream Video
description: Set up on-page tags for Outstream video. Outstream Video uses AST tags that can be defined, loaded, and shown in the page body.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Set up on-page tags for Outstream video

Xandr Outstream Video uses Microsoft Advertising's Seller Tag (AST). AST is an asynchronous JavaScript tag that runs in the header of the page. AST tags are defined and loaded in the page header and are activated by "showing" the tags in the page body.

> [!TIP]
> For select use cases, AST can also be defined, loaded, and shown in the page body.

## How it works

An outstream video ad unit can be added to a web page in the following page positions:

- at the start of an article
- in between paragraphs of text in an article
- at the end of an article

In each of the scenarios outlined above, the outstream video ad unit is included as a hidden `<div>` element in the page body. The `<div>` element in the page body refers to the video ad unit using a Target Identifier, which corresponds to a definition of that Target Identifier in the page header. When the container comes into view, the outstream video ad unit is activated for playback and expands on the page to show the content.

## Example

AST lets you define the tag (placement) you intend to call. When defining an outstream placement, you can pass additional options to specify how the player should be displayed on the page and how it should behave. The following example shows a call to `defineTag` for an outstream placement.

```
    apntag.defineTag({
        //required params
        targetId: 'outstream_div',
        tagId: 31,
        sizes: [1, 1],
        allowedFormats: ['video'],
        targetingParams: {},
        video: {
            frameworks: [1,2]
        },
        //the options object is passed to the renderer which creates the outstream player on the page
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
            }
        }
    });
```

## Implementing SafeFrame with Outstream video

SafeFrame was created to avoid disruptive ad behavior and the potential security risks of serving ads inline with the page. The complete spec for SafeFrame is available on the [IAB website](https://iabtechlab.com/wp-content/uploads/2016/03/SafeFrames_v1.1_final.pdf).

For video creatives, SafeFrame is currently available only for Outstream video.

To enable SafeFrame for Outstream, set the `enableSafeFrame` option in the `apntag` definition, as shown in the following example:

```
apntag.defineTag({
  enableSafeFrame : true,
  sizes: [640, 414]
  ...
```

## Defining player size for SafeFrame

Because `autoInitialSize` is not yet supported for SafeFrame, you need to set the exact dimensions for the final player in `apntag`, as shown in the previous example. Typically, you'll need to set up mobile and desktop placements differently to accommodate different player sizes.

You can calculate the necessary width and height of the player as shown in the following example.

When your target width = 640 and the aspectRatio=16:9:

- 640 / (16/9) = 360px player height
- 24px = top bar adds 24px to height
- 30px = if control position set to below (and not over), add 30px to height

In this example, the sum of the heights adds up to 414 for a size of [640, 414].
