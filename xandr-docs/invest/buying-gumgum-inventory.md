---
title: Microsoft Invest - Buy GumGum Inventory
description: In this article, learn how to buy a GumGum inventory to enhance user engagement and display a creative through GumGum's inventory.
ms.date: 10/28/2023
---

# Microsoft Invest - Buy GumGum inventory

You can enhance user engagement via [GumGum](https://www.gumgum.com) "in-image" or "in-screen" units, which are available programmatically through Microsoft Advertising. GumGum ad campaigns involve a few adjustments to the process of uploading standard display campaigns. This page will guide you through this process and explain how to display your creative via GumGum's inventory.

## Upload a third-party creative

Navigate to the **Creative Manager** screen. Select the **Create New** button and select your creative type from the menu. In the **New Creative** dialog box select the following values:

- **Type : Third Party Creative**
- **Creative Format**: **Third-Party Tag**
- **Tag Type: This tag is HTML**
- **Media Type: Banner: Standard Banner**
- **Template: Microsoft Advertising Standard**
- **Size:** See the table below for recommended sizes depending on your GumGum inventory selection. For example, "10x10" for the Studio 728x90.
- **Name:** Self classify the creative with the accurate brand.

> [!IMPORTANT]
> Do not submit for audit since the creative will only be able to render on GumGum's inventory and the Microsoft Advertising team cannot audit it.

| GumGum Product           | Microsoft Advertising Size |
|:-------------------------|:-----------|
| In-Image 728x90          | 10x10      |
| In-Image Animated        | 12x12      |
| In-Image                 | 13x13      |
| In-Image Canvas          | 16x16      |
| In-Screen                | 17x17      |
| In-Image Embedded Video  | 18x18      |
| In-Screen Embedded Video | 19x19      |

> [!NOTE]
> Custom Creative Configuration Required. All of GumGum products require a custom creative configuration that they will have to provide. The only exception is the in-image studio 728x90 creative, which you can leverage the existing 3rd party tags for a 728x90 used for display. GumGum can read that HTML tag and adjust it to fit their inventory.

## Check the rendering of GumGum creatives

> [!NOTE]
> This is not needed for the In-Image Studio 728x90 product because that can be rendered in console by using the actual size.

### Step 1: View the creative

Use the [https://gumgum.com/creative-preview](https://gumgum.com/creative-preview) to view creative.

### Step 2: Enter the HTML tag code

Enter the creative ad HTML code into the field in the bottom-half panel and select the correct product type.

### Step 3: Preview

Select **preview**.
