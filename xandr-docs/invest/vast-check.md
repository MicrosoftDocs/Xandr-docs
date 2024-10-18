---
title: Microsoft Invest - VAST Check
description: This article describes the different outputs you may see, and corrective action that can be taken when adding a third-party VAST and VPAID video creatives.
ms.date: 10/28/2023
---

# Microsoft Invest - VAST check

When adding a third-party VAST or VPAID video creative, a series of checks are performed on the XML. This page describes the different outputs you may see and corrective action that can be taken.

> [!IMPORTANT]
> **New to VAST Check**
>
> CTV Eligibility Check: Ensure that your uploaded creative meets the suggested format and quality requirements for CTV inventory.
>
> Hosted Asset Scanning: Microsoft Advertising-hosted video assets will now be checked in addition to third-party creatives.

## VAST check elements

- Duration: A duration with format 00:00:00 is required.
- Formats: To deliver on all player types, the following formats are recommended:
  - VAST: Flv, MP4, WebM
  - VPAID: application/JavaScript, application/x-shockwave/flash
- Secure: All URLs inside the VAST document must be prefixed with https:// to serve on secure inventory.
- Click Tracking: Microsoft Advertising automatically wraps third-party creatives to provide impression, click, and playback tracking.
- Wrappers: A maximum of two `<Wrapper>` tags is recommended.

## OTT eligibility

OTT (over-the-top video, sometimes known as connected TV or "CTV" content) is TV content delivered via an internet connection, often via
smart TVs, streaming devices, gaming consoles, and IP-enabled set-top boxes. OTT content is generally delivered in a full-screen setting with engaged viewers watching high-quality video content. This includes home theater experiences and similar viewing setups. OTT is considered premium digital video, and it is the highest-quality format available programmatically, with completion rates as high as 90%. For this reason we recommend uploading higher quality assets to ensure your creatives will be eligible to serve on this inventory.

Minimum recommended OTT creative specifications:

- VAST creative with an MP4 format
- minimum resolution of 1280x720
- minimum bitrate of 2000 kbps

> [!NOTE]
> All VPAID creatives will be ineligible for OTT inventory. To serve on OTT inventory, use VAST creatives with an MP4 format.

## Possible VAST check outcomes

**Unable to run:** VAST Check cannot access the creative. The creative can't be saved.

- There was an error with the request: No valid ad information was found.
- There was an error with the request: We are unable to detect content from this tag.

**Fail:** VAST Check runs and the creative fails a required check. The creative can't be saved.

- Invalid creative: some attributes need attention.

**Pass:** VAST Check runs and may or may not recommend changes that are not required. The creative can be saved.

- Some adjustments are recommended.
- All attributes are present and valid.

## VAST check unable to run (invalid/inaccessible creative)

### Error: No valid ad information was found

> [!NOTE]
> Full Error:
>
> Error: There was an error with the request: No valid ad information was found. This may occur if the tag has no content, or if it is specifically blocking our VAST Check Service. Please reach out to your third-party ad server for assistance.

**What it means:**

- VAST Check detects an XML file, but it contains no valid ad information

- The URL may lead to a rotating, deactivated, or targeting-enabled tag that only selectively returns a full XML response

  :::image type="content" source="./media/unable-to-run.png" alt-text="Screenshot of the error message stating that no information was found.":::

**Actions to take:**

- If you paste the VAST URL into a browser and no content is returned, the creative is either invalid, disabled, or utilizing some sort of targeting. The tag provider will need to address this before the creative can be trafficked.

- If you paste the VAST URL into a browser and see a full valid XML file for the creative, then the third-party ad server is likely blocking Microsoft Advertising VAST Check specifically. The tag provider will need to address this before the creative can be trafficked.
- To remove a block, it may also help to inform the ad server that our VAST Check user agent will appear as: **connection.setRequestProperty("User-Agent","AppNexus Vastbot/1.0");**
- To see what the VAST URL is returning when called by VAST Check, make the following API call with your VAST URL inserted: `curl -L -v -H "User-Agent: ``AppNexus`` VastBot" "VAST_URL"`
  - If there isn't any XML or a blank XML response is returned, the ad server isn't responding to our VAST Check properly.

### Error: We are unable to detect content from this tag

> [!NOTE]
> Full Error:
>
> Error: There was an error with the request: We are unable to detect content from this tag. This may occur if the tag has no content, or if it is specifically blocking our VAST Check Service. Reach out to your third-party ad server for assistance.

**What it means:**

- VAST Check is not detecting any XML content or ad information from the provided URL.
- The URL may not be a valid video creative, or it may be a rotating, deactivated, or targeting-enabled tag that only selectively returns a full XML response.

**Actions to take:**

- If you paste the VAST URL into a browser and no content is returned, the creative is either invalid, disabled, or utilizing some sort of targeting. The tag provider will need to address this before the creative can be trafficked.

- If you paste the VAST URL into a browser and see valid XML content for the creative, then the third-party ad server is likely blocking Microsoft Advertising VAST Check. The tag provider will need to address this before the creative can be trafficked.
- To remove a block, it may also help to inform the ad server that our VAST Check user agent will appear as: **connection.setRequestProperty("User-Agent","AppNexus Vastbot/1.0");**
- To see what the VAST URL is returning when called by VAST Check, make the following API call with your VAST URL inserted: `curl -L -v -H "User-Agent: ``AppNexus`` VastBot" "VAST_URL"`
  - If there isn't any XML or a blank XML response is  returned, the ad server isn't responding to our VAST Check properly

## Failed creative: Some attributes need attention

If VAST check returns this message, the creative was scanned but contains errors that will prevent it from saving. Review the VAST Check output to see what information is missing. Below are the possible attributes that will cause VAST Check to fail if they are missing.

### Video duration is undefined

**What it means:**

- The duration information for the video creative is missing or invalid. A creative must have a duration declared to be eligible to serve on the Open Exchange. If your creative has a duration but you are seeing this error, the duration format may be invalid. Durations must be in the "00:00:00" format.

**Actions to take:**

- Select **Run check again** button to initiate the re-scanning of the creative XML document.

   :::image type="content" source="./media/run-check-again.png" alt-text="Screenshot of the Run Check Again button.":::

  This feature would address the following scenarios where:
  - Scanner failed to run during the upload.
  - Scanner timed out while scanning.
  - Scanner detected an issue such as missing or wrong duration, missing or wrong media file format, etc.
  - VAST XML content is updated on the ad server, but needs to be updated at Microsoft Advertising platform and back-end.

- Reach out to the tag provider to add the missing duration information or revise the format. For example,

  :::image type="content" source="./media/video-duration.png" alt-text="Screenshot that shows how to add the missing duration information or revise the format.":::

### No video formats detected

**What it means:**

- The MediaFile information for the video creative contains none of the recommended video formats. At least one video format must be present for the creative to be saved.

**Actions to take:**

- Select **Run check again** button to initiate the re-scanning of the creative XML document.

  :::image type="content" source="./media/run-check-again.png" alt-text="Diagram that shows the Run Check Again button.":::

  This feature would address the following scenarios where:
  - Scanner failed to run during the upload.
  - Scanner timed out while scanning.
  - Scanner detected an issue such as missing or wrong duration, missing or wrong media file format, etc.
  - VAST XML content is updated on the ad server, but needs to be updated at Microsoft Advertising platform and back-end.
- Reach out to the tag provider to update the creative with at least one of the recommended video formats.
Sample XML with recommended VAST formats:
  :::image type="content" source="./media/video-formats.png" alt-text="Screenshot of sample XML with recommended VAST formats.":::

  Sample XML with recommended VPAID formats:

  :::image type="content" source="./media/media-files.png" alt-text="Screenshot of sample XML with recommended VPAID formats.":::

## Some adjustments are recommended (valid creative)

If your VAST check returns this message, your creative is valid and can be saved. The VAST check will provide recommended adjustments that may improve the scale of your creative.

### Video duration is greater than 30 seconds

No corrective action is needed here. We flag long-form creatives because they may not be eligible to serve on Instream inventory with duration limits. Targeting Outstream inventory is recommended as it will typically not have the same duration limits as Instream.

### Some recommended video formats not detected

**What it means:** The MediaFile information for the video does not declare all of the recommended formats for VAST or VPAID.

Including all recommended video formats will allow your creative to play in a larger variety of player types and environments. We recommend avoiding trafficking creatives that only use Flash as a media type. VPAID 2.0 supports HTML5 (media type application/JavaScript), which allows VPAID creatives to play in non-Flash environments.

**Actions to take:** Reach out to your tag provider to update the creative with the recommended video formats.

For sample XML snippets with the recommended formats, see the [No video formats detected](#no-video-formats-detected).

### `<Wrapper>` element(s) detected

**What it means:** A `<Wrapper>` element indicates that the location of the `<InLine>` tag from which to retrieve the video creative is not located directly in the current VAST document. The location of that tag must be retrieved from another VAST document. In addition, a `<Wrapper>` element may refer to a VAST document that contains a `<Wrapper>` element. Each redirect to another VAST document increases the time taken to reach the actual creative.

> [!NOTE]
> If there are more than two `<Wrapper>` redirects in the VAST response to a bid request, some supply sources (e.g., Google AdX) will reject your creative.

**Actions to take:** Avoid multiple chained `<Wrapper>` elements in your VAST documents.

Excerpt of a VAST document with a `<Wrapper>` element pointing to an `<InLine>` tag:

:::image type="content" source="./media/wrapper-vast.png" alt-text="Screenshot of an excerpt of a VAST document with a wrapper element pointing to an inline tag.":::

## All attributes are present and valid (valid creative)

If VAST check was successful, it means that the VAST file has satisfied the following requirements:

- Video duration is defined - Duration (in seconds) of the video creative is defined in a valid format. The time is auto-populated in the Duration field in the creative workflow.
- All recommended video formats are included
  - For VAST creatives, the three recommended formats (FLV, MP4 and WebM) are included in the XML document.
  - For VPAID creatives, the two recommended formats (application/JavaScript, application/x-Shockwave/Flash) are present in the XML document.
- Video creative URLs have secure prefixes - All URLs inside the VAST document are prefixed with https:// and can serve on secure inventory.
- There aren't any multiple nested wrappers
