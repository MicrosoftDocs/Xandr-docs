---
title: Native Video with AST
description: In this article, learn about Native Video with AST, video players, and how to implement it with a detailed set of examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Native video with AST

Native video gives publishers the ability to render ads on their site from within their preferred video player. A video file is delivered to the publisher, who then has control over how and where that ad is played.

Working with native video is similar to working with any other type of native creative in that the publisher is responsible for correctly inserting the content provided by the bidder onto the site. However, in place of the creative, a native bid response will contain a string that has the full XML VAST for the video.

## AST implementation

The AST implementation of native video closely mirrors the [standards set by the IAB](https://iabtechlab.com/standards/openrtb-native/).

When you define your AST tag, include the video specifications in the **native** field:

```
apntag.defineTag({
  native: {
    title: {required: true},
    ...
    video: {
      required: true,
      min_duration: 10000,
      max_duration: 60000
    },
    ...
  }
  ...
}
```

For more information on defining your AST tag, see [Define Tag](define-tag.md).

The bid request must include the video object. Required fields in the bid request video object are:

- `min_duration`: Minimum video ad duration in milliseconds.
- `max_duration`: Maximum video ad duration in milliseconds.

Here is an example of what you might see in the AST bid request:

```
"native":{
    "renderer_id":1,
    "placement_type":"in-feed",
    "layouts":[
        {
            "video":{
            "required":true,
            "min_duration":10000,
            "max_duration":60000,
            "mime_type":[
                "video/mpt",
                "x-flv"
            ],
            "protocol":[
                "VAST_1.0",
                "VAST_2.0"
            ]
        }
    }
```

The bid response will include the VAST XML string for the video. For example:

```
{
        "version": "3.0.0",
        "tags": [
          {
            "uuid": "99999ccc-1111-4848-acac-fec7873fac6e",
            "tag_id": 123,
            ...
            "ads": [
              {
                "content_source": "rtb",
                "ad_type": "video",
                ...
                "rtb": {
                  "native": {
                    "video": {
                      "duration_ms":55000,
                      "playback_methods":["auto_play_sound_off"],
                      "frameworks":["vpaid_1_0","vpaid_2_0"],
                      "content": "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?><VAST version=\"2.0\">..."
                    }
                  },
          ...
      }
```

Notice the **content** field in the response. This field contains the VAST XML string for the full video content. The complete XML is not shown in this example. For full XML examples of what would be returned in a response, see the [IAB VAST Test Examples](https://www.iab.com/insights/vast-2-0-xml-samples-for-testing/).

## Video players

Xandr Vast Player is a stand-alone video player which knows how to play a single ad as delivered by VAST XML. The player is loaded via a Javascript script url and it supports an API which is used to pass in the VAST XML and any other player options. If publishers using AST are also using the Native Assembly templates that are provided, they are automatically opted into using Xandr Vast Player. If they're writing their own rendering logic from scratch, then they may choose to use another player (like JW player). The Xandr Vast Player may be given either a URL which returns a VAST XML document or it can be given the VAST XML directly as a string. The player then parses the VAST XML, selecting the most appropriate rendition from the XML to play. The player then renders the selected rendition, using any player options that were passed in to configure the playback. The player is responsible for monitoring the playback and user interaction and reports any trackable event that was detected and for which tracking urls were provided.

## Related topics

- [Seller Tag](seller-tag.md)
- [AST API Reference](ast-api-reference.md)
