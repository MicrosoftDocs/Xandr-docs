---
title: Microsoft Monetize - Creative Spreadsheet Conventions
description: In this article, find details about the supported spreadsheet templates along with the different columns to be included for the various creative types.
ms.date: 08/25/2025
---

# Microsoft Monetize - Creative spreadsheet conventions

We support the use of spreadsheet templates for uploading multiple creatives simultaneously.

Feel free to leverage the following spreadsheet templates:

- [Microsoft Advertising Third-Party Creative Template](https://download.microsoft.com/download/e8a333c9-76b7-4c88-9068-60733aceb1dd/xandr-generic-template-third-party.xlsx)
- [Microsoft Advertising Hosted Creative Template](https://download.microsoft.com/download/e8a333c9-76b7-4c88-9068-60733aceb1dd/xandr-generic-template-hosted.xlsx)
- [Microsoft Advertising Native Creative Template](https://download.microsoft.com/download/e8a333c9-76b7-4c88-9068-60733aceb1dd/xandr-generic-template-native.xlsx)

> [!NOTE]
> Only XLS and XLSX file formats are supported with a file size limit of 8 MB.

## New spreadsheet templates (For political ads in EU)

> [!NOTE]
> Declare whether your ad is political and is intended to serve in the EU, using the new templates below. Learn more about upcoming updates to Monetize Creative Standards regarding [political ads](https://learn.microsoft.com/en-us/xandr/monetize/creative-standards). Learn more about how political advertising is [defined](https://help.ads.microsoft.com/#apex/ads/en/60380/-1). If you continue to use the old templates without the "Political Declaration" column, it will be considered as a declaration that your ad is non-political.

New spreadsheet templates:

- [Microsoft Advertising Third-Party Creative Template](https://download.microsoft.com/download/08ef68cd-d330-487c-b555-ccd4a9b12e03/third-party-creative-template.xls)
- [Microsoft Advertising Hosted Creative Template](https://download.microsoft.com/download/08ef68cd-d330-487c-b555-ccd4a9b12e03/hosted-creative-template.xls)
- [Microsoft Advertising Native Creative Template](https://download.microsoft.com/download/08ef68cd-d330-487c-b555-ccd4a9b12e03/native-creative-template.xls)


## Third-party creatives

When you prepare your Excel files for upload, the following information must be included in your file: creative name, content tag, secure content tag, and political declaration. For automatic column mappings, follow these column name mapping conventions when creating your Excel file:

| Mapping Option | Column Name |
|---|---|
| External Identifier (optional) | For automatic External Identifier mappings, use one of the following column names in your Excel file: <br> - **Placement ID** <br> - **External Identifier** |
| Name | For automatic Name mappings, use one of the following column names in your Excel file: <br> - **Name** <br> - **File Name** <br> - **Placement Name** |
| Secure Content | For automatic Secure Content mappings, use one of the following column names in your Excel file: <br> - **Tag Content Secure** <br> - **Tag Content** <br> - **JavaScript Tag** <br> - **Legacy JavaScript Tag** <br> - **URL** <br> - **Secure URL** |
| Political Declaration | For Political Declaration mapping, use the following column name in your Excel file: <br> - **Political Declaration** |
| Size (optional) | For automatic Size mappings, use one of the following column names in your Excel file: <br> - **Dimensions** <br> - **Size** |
| Tracker (optional) | For automatic Tracker mappings, use one of the following column names in your Excel file: <br> - **Tracker** <br> - **Pixel** <br> - **Pixel URL** <br> - **Third-Party Pixel**. |

## Hosted creatives

When preparing your Excel files for upload, the creative type and name must be included in your file. For automatic column mappings, follow these column name mapping conventions when creating your Excel file:

| Mapping Option | Column Name |
|---|---|
| Creative Type | For automatic Creative Type mappings, use one of the following column names in your Excel file: <br> - **Creative Type** <br> - **Type** |
| External Identifier (optional) | For automatic External Identifier mappings, use one of the following column names in your Excel file: <br> - **Placement ID** <br> - **External Identifier** |
| Landing Page URL (optional) | For automatic Landing Page URL mappings, use one of the following column names in your Excel file: <br> - **Landing Page** <br> - **Landing Page URL** <br> - **Click URL** |
| Name | For automatic Name mappings, use one of the following column names in your Excel file: <br> - **Name** <br> - **File Name** <br> - **Placement Name** |
| Tracker (optional) | For automatic Tracker mappings, use one of the following column names in your Excel file: <br> - **Tracker <br> - Pixel** <br> - **Pixel URL** <br> - **Third-Party Pixel** |

## Native creatives

When preparing your Excel files for upload, the creative name and image file name must be included in your file. For automatic column mappings, follow these column name mapping conventions when creating your Excel file:

| Mapping Option | Column Name |
|---|---|
| Body Text (optional) | For automatic Body Text mappings, use one of the following column names in your Excel file: <br> - **Body Text** <br> - **Description** |
| Call to Action (optional) | For automatic Call to Action mappings, use one of the following column names in your Excel file: <br> - **Call-to-Action** <br> - **Call to Action** |
| External Identifier (optional) | For automatic External Identifier mappings, use one of the following column names in your Excel file: <br> - **Placement ID** <br> - **External Identifier** |
| Icon (optional) | For automatic Icon mappings, use one of the following column names in your Excel file: <br> - **Icon** <br> - **Icon Name** <br> - **Icon Image** <br> - **File Name (Icon)** <br> - **Logo** |
| Image | For automatic Image mappings, use one of the following column names in your Excel file: <br> - **Image** <br> - **Main Image** <br> - **File Name (Image)** |
| Landing Page URL (optional) | For automatic Landing Page URL mappings, use one of the following column names in your Excel file: <br> - **Landing Page** <br> - **Landing Page URL** <br> - **URL** |
| Name | For automatic Name mappings, use one of the following column names in your Excel file: <br> - **Name** <br> - **Creative Name** <br> - **File Name** <br> - **Placement Name** |
| Sponsored By (optional) | For automatic Sponsored By mappings, use **Sponsored By** as your column name in your Excel file. |
| Title (optional) | For automatic Title mappings, use **Title** as your column name in your Excel file. |
| Tracker (optional) | For automatic Tracker mappings, use one of the following column names in your Excel file: <br> - **Tracker** <br> - **Pixel** <br> - **Pixel URL** <br> - **Third-Party Pixel** |
| Video (optional) | For automatic Video mappings, use one of the following column names in your Excel file: <br> - **Video** <br> - **Video Name** <br> - **File Name (Video)** |

## Related topics

- [Video Creatives](video-creatives.md)
- [Audio Creatives](audio-creatives.md)
- [Native Creatives](native-creatives.md)
- [Banner and HTML5 Creatives](banner-and-html5-creatives.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
