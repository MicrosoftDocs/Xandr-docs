---
title: Onboarding video supply
description: Explore onboarding video strategies, adjust placements, update media types, test tags for seamless integration in learning.
ms.date: 10/28/2023
---

# Onboarding video supply

> [!NOTE]
> Microsoft Advertising now supports a domain, `adnxs-simple.com`, which does not send or read browser cookies on requests. Clients can leverage this cookie-free domain when there is no consent to use personal data. Relevant calls initiated by Microsoft Advertising will automatically use this domain when there is no consent or when cookies are not required for the function. For more information, see [Part of Service Policies](../policies-regulations/index.yml)

This page explains how to modify placement settings to accept video creatives and how to export and test placement tags.

## Placements

To allow video creatives on your placements, update the **Allowed Media** settings for the placement. Use the [Create a Placement](create-a-placement.md) workflow to navigate to the **Allowed Media** section and select the appropriate media type under the Video section.

New **Video Settings** and **Advanced Video Settings** sections will appear. Configure the remaining video placement options within these sections.

- For **In-stream only**, select a **Position**:

  - **Pre-roll**
  - **Mid-roll**
  - **Post-roll**

- Enter the **Player Width** and **Height** (in pixels). **Unknown** is the default option.
- Enter the acceptable **Max Duration** (in seconds) of video creatives. Creatives that are equal to or shorter than the specified duration will be served.
- Select a **Playback Method** from the drop-down menu:

  - **Auto-play, sound on**
  - **Auto-play, sound off**
  - **Click-to-play**
  - **Mouse-over**
  - **Auto-play**, **sound unknown** (default)

- Specify whether your player allows **Not Skippable** or **Skippable** creatives.

- Select a **Framework**. **Unknown** is the default option if none of the framework options are checked.

## Tagging

When you [export placement tags](export-placement-tags.md) for a placement that allows VAST video creatives, the placement tag generated is a URL that automatically includes the /ptv or /vmap handler (depending on the placement), which ensures that ad calls will return the XML your publisher's video player uses to serve the desired
creative. For ptv tags, the end result looks something like this: `https://ib.adnxs.com/ptv?id=5523324`.

For vmap tags, the end result should look something like this: `https://ib.adnxs.com/vmap?id=11029144`.

Note that ad pods will only work with vmap tags.

The end result looks something like this:

```
https://ib.adnxs.com/ptv?id=1234. 
```

Once you have the tag, simply provide it to your publisher. Be sure to instruct the publisher to copy the URL into the video player rather than place it directly on the page. For details on tagging video, see [Target Video Attributes via Query String Parameters](target-video-attributes-via-query-string-parameters.md).

## Testing Placement Tags

If your publisher isn't able to provide you with a test page, you can use an online VAST validator to determine if the placement tag is functioning properly. There are several available online, including at [VAST Inspector](https://developers.google.com/interactive-media-ads/docs/sdks/html5/vastinspector).

## Recording impressions

VAST impressions are always recorded after serving, per the IAB guidelines [PDF](https://www.iab.net/media/file/dig_vid_imp_meas_guidelines_final.pdf). If you test VAST by loading in a browser, you should not see any impressions recorded. It is only when the VAST response is parsed by a video player and the impression tag is called that the impression is recorded.

## Related topics

- [Create a Placement](create-a-placement.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)
- [Export Placement Tags](export-placement-tags.md)
- [Placement Tag Parameters](placement-tag-parameters.md)
