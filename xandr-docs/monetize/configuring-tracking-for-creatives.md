---
title: Microsoft Monetize - Configuring Tracking for Creatives
description: Configure creative tracking by setting parameters like caps and pixels in the Pixels section when adding creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Configuring tracking for creatives

When adding creatives, you can set a variety of tracking parameters from the **Pixels (optional)** section, such as frequency and recency caps, third-party tracking pixels, and segment pixels.

- **[Click Tracking](click-tracking.md)**: The system automatically runs a click tracking test when the creative is uploaded. If the system fails to automatically run a click tracking test for your creative when using the single creative workflow to upload one creative, you can manually click the **Run Test** button from the **Pixels (optional)** section.
  
   > [!NOTE]
   > If the click tracking test is unsuccessful, which is indicated by a red **X**, re-upload the file or update the landing page URL and click the **try again** link that displays in the **Pixels (optional)** section.

- **[Frequency and Recency Caps](frequency-and-recency-caps.md)**: You can specify the number of times and pace in which a creative can be shown to a given user. For more information, see [Frequency and Recency Caps](frequency-and-recency-caps.md).
- **[Third-Party Tracking Pixels for Creatives](third-party-tracking-pixels-for-creatives.md)**: You can create third-party tracking pixels at either the advertiser or Network level and then associate them with your creatives.
You can also associate custom third-party tracking pixels with your creatives if you want to use another system to track impressions by selecting the **Format** (**Image URL**,**HTML**, **URL**, **JavaScript URL**, or **Raw JavaScript**) for the pixel and entering URLs (**Secure** and **Non-Secure**) for each tracking event.
  
The following tracking events are supported:

| Tracking Event | Creative Type | Description |
|--|--|--|
| Click | All | Tracks all clicks. |
| Error | Video and Audio | Tracks issues related to the video player. |
| Impression | All | Tracks all impressions. |
| Player | Video and Audio | Tracks the following player events:<br> - Mute<br> - Pause<br> - Player Collapse<br> - Player Expand<br> - Resume<br> - Rewind<br> - Skip<br> - Unmute<br>**Note**: Mute, pause, player collapse, player expand, resume, rewind, and unmute are only supported on VAST versions 4.1 and 4.2. Skip is supported on VAST version 2.0 and higher. |
| Progress | Video and Audio | Tracks the percentage of a video creative that has been viewed. The percentages are broken down as follows:<br> - 0% (Start)<br> - 25% (Complete)<br> - 50% (Complete)<br> - 75% (Complete)<br> - 100% (Complete)<br>This tracking event is supported on VAST version 2.0 and higher. |

> [!NOTE]
> If the inventory that you are serving on is secure, then each tracking pixel must have a secure URL.

  Here's a list of pixel formats that are supported per creative type:

| Creative Type | Supported Format |
|--|--|
| Video and Audio | Image URL |
| Native | - Image URL<br> - JavaScript URL |
| Banner | - Image URL<br> - HTML URL<br> - JavaScript URL<br> - Raw JavaScript |

- **[Associate Segment Pixels with Creatives](associate-segment-pixels-with-creatives.md)**: You can associate specific
  segment pixels with your creatives.
  
  > [!NOTE]
  > The more segment pixels that you add to a creative will result in more latency for end users.

- **AdChoices**: You can append the AdChoices icon to your creatives, giving your audience control over how information about their interests is used for relevant advertising.

  > [!NOTE]
  > AdChoices can be enabled for all creative types. AdChoices is supported on VAST version 3.0 and higher.
