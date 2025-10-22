---
title: Bidders - VAST Check
description: Explore VAST and VPAID video creative checks for bidders, understanding potential outputs, and implementing corrective actions with third-party XML.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - VAST check

When adding a third-party VAST or VPAID video creative, a series of checks are performed on the XML. This page describes the different outputs you may see and corrective action that can be taken.

## VAST check requirements

- **Duration**: A duration with format 00:00:00 is required.
  - Creatives longer than 30 seconds may not deliver on Instream inventory due to duration limits; targeting Outstream is recommended.  
- **Formats**: To deliver on all player types, the following formats are recommended:
  - VAST: Flv, Mp4, WebM
  - VPAID: application/JavaScript, application/x-shockwave/flash
- **Secure**: All URLs inside the VAST document must be prefixed with `https://` to serve on secure inventory.
- **Click Tracking:** Xandr automatically wraps third-party creatives to provide impression, click, and playback
  tracking.
  - To view the Xandr wrapper of your creative: `ib.adnxs.com/cr?id=[INSERT_ID]&amp;format=vast`
- **\<Wrapper\> tags**  

  > [!NOTE]
  > To manually inspect the elements of your XML file, paste the VAST URL into a browser.

## Possible VAST check outputs

- All attributes are present and valid  
- Invalid creative: some attributes need attention
- Some adjustments are suggested
- Unable to run VAST check
- The VAST XML appears to no longer exist

**All attributes are present and valid**

If VAST check was successful, it means that your VAST document has satisfied all of the requirements above.

**Invalid creative: some attributes need attention**

If VAST check returns this message, your creative contains errors that will prevent it from saving. Open your VAST file by pasting the VAST URL into a browser to check the missing information.

### Video duration is undefined

**Cause**: The `Duration` information for the video creative is missing or invalid. A creative must have a duration declared to be eligible to serve on the Open Exchange. If your creative has a duration but you are seeing this error, the duration format may be invalid. Durations must have format "00:00:00".

**Corrective action**: Reach out to your third-party ad server to add the missing duration information or revise the format. Valid duration example:

   :::image type="content" source="media/valid-duration.png" alt-text="Screenshot that instructthe users and resolve video duration issues by contacting ad server, add or adjust details using provided screenshot steps.":::

### No recommended video formats detected

**Cause**: The MediaFile information for the video creative contains none of the recommended video formats. At least one video format must be present for the creative to save.

**Corrective action**: Reach out to your third-party ad server to update the creative with at least one of the recommended video formats. 

  **Sample XML with recommended VAST formats**

  :::image type="content" source="media/recommended-vast-format.png" alt-text="Screenshot that illustrates the process of contacting a third-party ad server to update a creative with at least one of the recommended video formats.":::

  **Sample XML with recommended VPAID formats**

   :::image type="content" source="media/sample-xml.png" alt-text="Screenshot that illustrates Sample XML with recommended VPAID formats:":::

### Some adjustments are suggested

If your VAST check returns this message, your creative is valid and can be saved. The VAST check will however provide suggested adjustments that may improve the reach of your creative and ensure it serves on all
player types.  

### Video duration is greater than 30 seconds

No corrective action is required. Long-form creatives are flagged because they may not be eligible to serve on Instream inventory with duration limits. Targeting Outstream inventory is recommended as it will typically not have the same duration limits as Instream.  

### Some recommended video formats not detected

**Cause:** The `MediaFile` information for the video does not declare all of the recommended formats for VAST or VPAID.

Including all recommended video formats will allow your creative to play in a larger variety of player types and environments. We recommend avoiding trafficking creatives that use Flash as the **only** media type. VPAID 2.0 supports HTML5 (media type application/JavaScript) which allows VPAID creatives to play in non-Flash environments.

> [!WARNING]
> Effective July 2017, Google Ad Manager has blocked all flash-only video creatives.

**Corrective action:** Reach out to your third-party ad server to update the creative with the recommended video formats.

For sample XML snippets with the recommended formats, see the [No recommended video formats detected](vast-check.md#no-recommended-video-formats-detected) section.
  
### \<Wrapper\> element(s) detected

**Cause:** A `<Wrapper>` element indicates that the location of the `<InLine>` tag from which to retrieve the video creative is not located directly in the current VAST document. The location of that tag must then be retrieved from another VAST document. In addition, `<Wrapper>` element may refer to a VAST document that contains `<Wrapper>` element. Each redirect to another VAST document increases the time taken to reach the actual creative.

> [!NOTE]
> If there are more than two `<Wrapper>` redirects in the VAST response to a bid request, some supply sources (e.g., Google Ad Manager) will reject your creative.

**Corrective action:** Avoid multiple chained `<Wrapper>` elements in your VAST documents.

Excerpt of a VAST document with a `<Wrapper>` element pointing to an \<InLine\> tag:

:::image type="content" source="./media/excerpt-of-a-vast.png" alt-text="Screenshot that provides guidance on taking corrective actions by avoiding the use of multiple chained Wrapper elements in VAST documents.":::

**Unable to run VAST check**

If VAST check is unable to run successfully, it means your creative either has no content, or cannot be scanned. You will see one of the error messages listed below. Please contact your third-party ad server for further troubleshooting.

- There was an error with the request: VAST Wrapper URL is not valid.
- There was an error with the request: Ad node not present in XML returned from: \[VAST URL\]. Please reach out to your third-party ad server for assistance.

> [!NOTE]
> VAST check must be able to fetch your XML in order to traffic it on our exchange. VAST check extracts required metadata, such as duration and mime types, from the VAST file. Some SSPs block non-human traffic (nht). You can use the ${is_preview} macro to inform ad servers not to block our request. The value of the macro will be "1" when the call from VAST check is made.

There are many reasons why a VAST check cannot be completed including, but not limited to timeout errors, parser errors, or server errors. If you encounter this error, run a manual check to validate the presence of all attributes to ensure maximum delivery. Complying with a complete VAST XML file will increase the delivery potential of your video campaign.

See [VAST Check Requirements](vast-check.md#vast-check-requirements) to verify and incorporate required information.

**The VAST XML appears to no longer exist**

The VAST check feature is in the beta stage and may not return data. If the "**VAST XML appears to no longer exist**" message displays, manually check your VAST XML document. Open the document and ensure that all the necessary components are present as listed in the [VAST Check Requirements](vast-check.md#vast-check-requirements) section.
