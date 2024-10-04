---
title: Microsoft Invest - Troubleshoot Creatives
description: In this article, learn how to troubleshoot your creatives and analyze error messages, types, descriptions, and resolutions in detail.
ms.date: 10/28/2023
---

# Microsoft Invest - Troubleshoot creatives

> [!NOTE]
> This feature is part of a functionality that is presently in Open Beta. It is currently under development and may be subjected to change without notice. Contact your Microsoft Advertising Account Representative to get it enabled.

The Troubleshooting tab on the **Creative Manager** window provides troubleshooting information and creative setup analysis depending on the ad format (banner, video, native, and audio) of the creative. You can choose to run additional validations on creatives by navigating to the **Troubleshooting Tab**, where a list of validations will run on the creative and its corresponding troubleshooting information is displayed on the creative details panel.

To access the **Troubleshooting Tab**:

1. Navigate to the **Creative Manager** pane by selecting **Creative &gt; Creatives**.
1. Select an advertiser.
1. Select the appropriate creative for which you need to view the troubleshooting information. This will open up the **details** panel.
1. Select the **Troubleshooting Tab** on the **details** panel to view the troubleshooting information under the **Creative Setup Analysis** pane.

## Creative set up analysis (Troubleshooting tab)

### Errors

| Ad Type | Error Message | Type | Description | Analysis | Resolution |
|:---|:---|:---|:---|:---|:---|
| **Generic** | Click tracking test failed. | Error |  | The creative failed to pass the click scan test. | For more information on resolving common click scan issues, see [Click Track Test](click-track-test.md). |
| **Generic** | Include secure URLs to deliver on secure inventory. | Error |  | The media file URL(s) for the videos uses non-secure protocols (HTTP). | Re-upload the media files with secure URLs (HTTPS). |
| **Generic** | SSL Checking failed. | Error |  | The creative failed to pass the SSL test. | Check to make sure all portions of the creative utilizes HTTPS secure protocol. |
| **Native** | Creative not rendered correctly, it appears to be blank. | Error |  | The native creative failed to render. | Re-upload a correct creative to preview it. For more information, see [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md).<br><br> **Note:** If the creative is third-party hosted, ensure the service is not blocking the **adnxs.com** or **adnxs.net** domains. |
| **Banner** | No third-party pixels fired. | Error |  | The third party pixels associated with the banner did not fire successfully. |  |
| **Banner** | Creative not rendered correctly, it appears to be blank. | Error |  | The banner creative failed to render. | Re-upload a correct creative to preview it. For more information, see [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md).<br><br> **Note:** If the creative is third-party hosted, ensure the service is not blocking the **adnxs.com** or **adnxs.net** domains. |
| **Banner** | Creative uses HTML local storage, which is not allowed. | Error |  | The banner creative uses local browser storage. | Remove logic utilizing local browser storage and re-upload the banner creative. |
| **Banner** | Creative is adding X cookies to browser, which is over the allowed limit. | Error |  | The banner creative adds more than 20 cookies to the browser. | Re-upload the creative with less than 20 cookies added to the browser. |
| **Banner** | Asset of type (For example, HTML) Tag does not match selected template. | Error |  | The content type of the banner creative does not match its template. (For example, template is HTML (Tag) and the content type is Javascript). | Either update the template to match the creative content, or update the creative content to match the expected format of the template. |
| **Video** | Video must have a duration greater than 00:00:00. | Error | Invalid Duration | This occurs most often when the video content does not exist, or when the duration of the video either doesn't exist or is zero. | The duration of the creative must be greater than 00:00:00 seconds. Re-upload the creative and ensure the video has a valid content and a proper duration. |
| **Video** | Invalid formats detected. These are not supported by Microsoft Advertising Player. | Error |  | The video file type is neither mp4 nor webm. This is not supported by our Microsoft Advertising Player.<br><br>**Note:** The video may still be eligible for publishers like Netflix depending on their requirements. | Re-upload the creative with a supported format. |
| **Video** | No recommended formats were detected. | Error | Invalid File Type Detected When Accessing VAST. | No format listed when accessing VAST. The video creative must be created using one of the following file types: 3G2 (3GPP2), 3GP (3GPP), Advanced Systems Format (ASF), Audio Video Interactive (AVI), M2V, M4V, MKV, MOV, M4P, MPE, MPEG, MPEG-2 (MP2), MPEG-4 (MP4), MPG, MPV, OGG, OGV, QuickTime (QT), RM, SWF, TS, VOB, WebM, and Windows Media Video (WMV). | Convert the creative to the [correct file type](../monetize/video-creative-guidelines-and-specifications.md) and re-upload the creative. |
| **Video** | VAST creative with MP4 format is required for CTV inventory. | Error |  | For non-VPAID creatives, the MP4 file type is missing. | Re-upload the creative with a supported file type. |
| **Video** | A negative media file attribute was detected. Ensure height, width, and bitrate are positive. | Error |  | For non-VPAID creatives that have an MP4 file, the height, width and bitrate are less than 0. | Re-upload the creative with positive attributes. |
| **Video** | Creative not rendered correctly, it appears to be blank. | Error |  | The video creative failed to render. | Re-upload a correct creative to preview it. For more information, see [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md).<br><br> **Note:** If the creative is third-party hosted, ensure the service is not blocking the **adnxs.com** or **adnxs.net** domains. |

### Warning

| Ad Type | Warning Message | Type | Description | Analysis | Resolution |
|:---|:---|:---|:---|:---|:---|
| **Banner** | Creative rendered correctly. There are X errors and Y warnings that might impact performance and functionality. | Warning |  | The banner creative was rendered with some errors and/or warnings. |  |
| **Banner** | Creative is loading X files which is over the allowed limit. | Warning |  | The banner creative was loaded with more than 20 files. | Re-upload the creative with less than 20 files. |
| **Banner** | Creative is loading X Kb which is over the allowed limit. | Warning |  | The banner creative was loaded with a file size of more than 4 MB. | Re-upload the creative with a file size of less than 4 MB. |
| **Video** | Invalid formats video/x-flv detected. These are not supported by Microsoft Advertising Player. | Warning | This creative has a Flash based transcoding, which may not be supported by all video players. | This video format is not accepted. The video creative must be created using one of the following file types: 3G2 (3GPP2), 3GP (3GPP), Advanced Systems Format (ASF), Audio Video Interactive (AVI), M2V, M4V, MKV, MOV, M4P, MPE, MPEG, MPEG-2 (MP2), MPEG-4 (MP4), MPG, MPV, OGG, OGV, QuickTime (QT), RM, SWF, TS, VOB, WebM, and Windows Media Video (WMV). | Re-upload the creative with a supported format to preview the creative. |
| **Video** | Targeting Outstream is recommended for creatives over 30 seconds. | Warning | 15-30 seconds is the normal accepted range for Instream videos. | Your video creative is over 30 seconds and therefore does not meet industry standards. It may be limited in serving on all inventory. | For more information, see [Instream vs. Outstream Video Ads](https://www.brid.tv/instream-vs-outstream-video-ads/). |
| **Video** | To serve on CTV inventory, upload a VAST creative with MP4 format, minimum resolution of 1280x720 and minimum bitrate of 2000 kbps. | Warning |  | For VPAID creatives, if the MP4 file type is missing, the following error message will be displayed. | Re-upload the creative with a supported file type and recommended specifications. |
| **Video** | VAST with format video/x-flv. Provide video/mp4 and/or video/webm formats to maximize reach. | Warning | This creative has a Flash based transcoding, which may not be supported by all video players. | Flash-based video file format is only accepted by some publishers. It is more likely to be accepted by publishers if the file format used is mp4 or webm. | Re-upload the creative with video/mp4 and/or video/webm formats to maximize reach. |
| **Video** | Max provided resolution and bitrate do not meet recommended CTV specifications of 1280x720 and minimum bitrate of 2000 kbps. | Warning |  | For non-VPAID creatives that have an MP4 file, either the height and/or width and/or bitrate is above the max height/width/bitrate specifications. | Re-upload the creative with the recommended CTV specifications. |

### Success

| Ad Type | Success Message | Type | Description |
|:---|:---|:---|:---|
| **Generic** | SSL Checking Passed. | Success | The banner creative successfully passed the SSL. |
| **Generic** | Click tracking test passed. | Success | The creative successfully passed the click scan test. |
| **Generic** | Creative URLs have secure prefixes. | Success | The media file URL(s) for the videos uses secure HTTPS. |
| **Banner** | Asset of type (Ex: HTML) Tag correctly entered. | Success | The content type of the banner creative matches its template. (For example, template is HTML (Tag) and the content type is HTML). |
| **Banner** | X third-party pixels fired. | Success | The third party pixels associated with the banner fired successfully. |
| **Banner** | Creative does not use HTML local storage. | Success | The banner creative does not use local browser storage. |
| **Banner** | Creative is adding X cookies to browser of 20 allowed. | Success | The banner creative adds 20 or less cookies to the browser. |
| **Banner** | Creative rendered correctly and no javascript issues were detected. | Success | The banner creative was rendered with no errors or warnings. |
| **Banner** | Creative is loading 73.6 kB which is less than the 4 MB allowed. | Success | The banner creative loads are less than 4 MB. |
| **Video** | Creative meets recommended CTV inventory specifications. | Success | For VPAID creatives, the MP4 file type is present. |
| **Video** | VAST with formats (video/xxx, video/yyy, etc). | Success | The video/audio is valid and has the following formats video/mp4 and/or video/webm. |
| **Video** | VPAID with format application/javascript. | Success | This creative was detected with VPAID, which is an accepted format by Microsoft Advertising. |

## Related topics

- [Add a Creative](add-a-creative.md)
- [Update Creatives in bulk](update-creatives-in-bulk.md)
