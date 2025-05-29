---
title: Microsoft Monetize - Upload a Hosted Video Creative
description: Learn how to upload VAST video creatives and other steps to work with this type of creative. This page is a step-by-step guide to add a creative, preview the creative and save the creative. 
ms.date: 10/28/2023
---


# Microsoft Monetize - Upload a hosted video creative

Microsoft Advertising supports hosting VAST ([video ad serving template](https://www.iab.com/guidelines/vast/)) creatives. VAST is used to serve on in-stream and some non-linear placements, per publisher specifications. Microsoft Advertising currently supports VAST 2.0 and VAST 3.0. This page explains how to upload VAST video creatives and other considerations for working with this type of creative.

## Subscribing to video creative hosting

If you are interested in hosting video creatives on Microsoft Advertising, please talk to your Microsoft Advertising representative about pricing, your use case, and technical specifics.

> [!IMPORTANT]
> Use of the Video Creative Hosting platform requires a contract addendum unless specified in your Master Services Agreement (MSA).

## Specifications for hosted VAST video creatives

- **Max Video File Size**: 180 MB
- **Minimum Bit Rate**: 2500kbps
- **Minimum Size**: 1280x720px
- **File Types**: x-flv, mp4, webm, x-ms-wmv, ogg, x-msvideo, mpeg, quicktime, 3gpp, 3gpp2, x-m4v

> [!NOTE]
> The letterbox is not cropped for standard size videos.

## Add a creative

- [Microsoft Monetize - Upload a hosted video creative](#microsoft-monetize---upload-a-hosted-video-creative)
  - [Subscribing to video creative hosting](#subscribing-to-video-creative-hosting)
  - [Specifications for hosted VAST video creatives](#specifications-for-hosted-vast-video-creatives)
  - [Add a creative](#add-a-creative)
    - [Step 1. Get started](#step-1-get-started)
    - [Step 2. Upload the file](#step-2-upload-the-file)
    - [Step 3. Preview the creative](#step-3-preview-the-creative)
    - [Step 4. Define the creative content](#step-4-define-the-creative-content)
    - [Step 5. Select audit options](#step-5-select-audit-options)
    - [Step 6. Add companion banner creatives (optional)](#step-6-add-companion-banner-creatives-optional)
    - [Step 7. Attach third-party and segment tracking pixels (optional)](#step-7-attach-third-party-and-segment-tracking-pixels-optional)
    - [Step 8. Save the creative](#step-8-save-the-creative)
  - [Related topics](#related-topics)

### Step 1. Get started

- Navigate to the **Creative** screen (**Advertisers** > **Creative Manager**)
- Select the associated Advertiser
- Select **New**, then select **Video**


### Step 2. Upload the file

Select the **Hosted File** tab. Browse your computer, or drag and drop your file. For instructions about how to add a third-party hosted creative, see [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

**MP4**

| Size (px) | Bit Rate (kbps) |
|--|--|
| 1280x720 | 2500 |
| 1280x720 | 1100 |
| 1280x720 | 500 |
| 768x432 | 1700 |
| 768x432 | 1100 |
| 768x432 | 500 |

**WebM**

| Size (px) | Bit Rate (kbps) |
|--|--|
| 1280x720 | 2000 |
| 1280x720 | 600 |
| 768x432 | 1500 |
| 768x432 | 500 |

**Flash**

| File Type | Size (px) | Bit Rate (kbps) |
|--|--|--|
| x-flv | 768x432 | 1100 |
| x-flv | 768x432 | 500 |

### Step 3. Preview the creative

The creative preview is available for you to review once it is fully uploaded. You have the option to choose a different file, if required.

> [!NOTE]
> **.mov** videos will only play in preview on the Safari browser.

### Step 4. Define the creative content

The **Name** field is auto-populated with the name of your file. Enter a **Click-through URL** to redirect the user upon clicking.

### Step 5. Select audit options

On the **Creative Attributes** tab, select whether you want to submit the creative for Microsoft Advertising audit, classify the creative yourself, or exempt the creative from auditing entirely.

- **Platform Audit** - Submit the creative for auditing by the Microsoft Advertising audit team.

    Audit process includes:
  - checking technical and content criteria

  - offer type categorization to enable the seller protection features on the platform

  - requirements of sellers

    Microsoft Advertising audit is mandatory but you can opt out of other platform specific audits.

  - Select your audit **priority**.

    > [!NOTE]
    >  Business days are from 9:00pm Sunday to 11:59pm Friday ET.

    For more information about content standards for creatives running on the Microsoft Advertising platform, see [Creative Standards](creative-standards.md).

- **Self-Audit** - Classify the creative yourself.
  
  > [!NOTE]
  > - Self-auditing may reduce access to inventory outside of the ones you manage or own, as many sellers allow only Microsoft Advertising audited creatives. For further guidance on self-classifying, see [Self-Auditing Creatives](self-auditing-creatives.md).
  > - You must check the **I confirm compliance** checkbox in order to save the creative.

- **No Audit** - An unaudited creative can run **only** on your managed publishers. It will not be eligible to run on third-party inventory unless the seller has opted into allowing unaudited creatives to run on their inventory.

### Step 6. Add companion banner creatives (optional)

You can now add companion banners to your video creatives. Search for, and select banner ads that you have previously uploaded via the normal upload process.

> [!NOTE]
> You can only use banner creatives that have been previously uploaded.

### Step 7. Attach third-party and segment tracking pixels (optional)

Microsoft Advertising records all impressions. If you wish to use another system to track impressions in addition, you can attach third-party tracking pixels to your creative.

To attach an existing **third-party pixel** to this creative, select the type of pixel from the **Event** drop-down menu.

Enter **URLs** for each tracking pixel event.

You can also attach **segment pixels** to your creative. Search for existing segment pixels and select from the list.

### Step 8. Save the creative

Once you have defined your creative and populated the associated fields as necessary, click **Save**. The creative will be listed under **Creatives** on the **Creative Manager** screen.

## Related topics

- [Working with Creatives](working-with-creatives.md)
- [Creative FAQ](creative-faq.md)
- [Creative Audit Best Practices](best-practices-for-submitting-creatives-for-audit.md)
- [Self-Auditing Creatives](self-auditing-creatives.md)