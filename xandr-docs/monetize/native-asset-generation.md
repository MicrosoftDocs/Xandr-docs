---
title: Microsoft Monetize - Native Asset Generation
description: This article outlines the process of Native Asset Generation for Microsoft Monetize.
ms.date: 08/25/2025
---

# Microsoft Monetize - Native Asset generation 

> [!NOTE]
> This feature is currently in Open Beta and might undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative. Alternatively, you can contact our support team by completing the [Customer Support Form](https://support.ads.microsoft.com).

This article outlines the process of Native Asset generation, that streamlines the creation of advertising assets by automating the generation of images and text based on user inputs or webpage content.

With Native Asset generation:
- You can increase efficiency by using AI to generate advertising assets at scale, including headlines, descriptions, and images, reducing the time and effort required to create content. 
- You can manage campaigns more effectively by swiftly adapting to market changes or consumer behaviour with optimized assets that resonate with your target audience and drive engagement.

> [!NOTE]
> Microsoft Advertising will not incur additional costs for the use of this feature. It is provided free of charge.

## Native Asset generation process

The Native Asset generation is a streamlined process that guarantees a diverse range of text and image options, enhancing the quality of the generated Native ad assets.  
1. **Crawling and rendering:** The system retrieves raw HTML from the target page and stores it temporarily. A headless browser then renders this page to ensure precise data retrieval. 
1. **Image and text generation:**
    1. The system collects images from HTML `img` tags and Bing image search by using the target domain to find relevant images to supplement the selection. 
    1. A large language model (LLM) generates text assets, ensuring they are contextually relevant.
    > [!NOTE] 
    > This feature is available only for Native.
1. **UI integration:** The user interface (UI) seamlessly integrates the retrieved images and generated text, forming high-quality native ad components, ensuring a high-quality and relevant ad experience.

## Set up Native Asset

Follow the step-by-step instructions to add creatives using the Native Asset generation workflow.

> [!IMPORTANT]
> This feature only supports specific media types. If the crawler pushes a creative that doesn't match the expected media type (For example, .tif), and the user selects it, the data won't save during the creative setup. You can create the creative and click Save, but when you re-edit the creative, it will appear blank.

1. Navigate to **Creative Manager** pane by selecting **Advertisers** > **Creative Manager**.
1. Select an advertiser to associate the creative with. For more information see, [Create an advertiser.](create-an-advertiser.md)
1. Select the **New** dropdown menu and select **Asset Generation**.
1. Enter a valid **Landing Page URL** to view the recommendations.
    > [!NOTE]
    > Only landing page URLs with the advertiser's domain name can be used. The website must be valid and secure. All URLs are automatically converted to secure URLs, enabling the crawler to retrieve and display content effectively.
1. Select a creative from the recommendations that closely aligns, and click **Continue**.
    > [!NOTE]
    > During the creative creation process, the crawler suggests the only available image for selection, preventing the addition of an icon in the initial step. To include an icon, first save the creative, then re-edit it. This allows you to select and upload the icon asset.
1. Provide basic information for the creative in the **Basic Setup** section:
    1. Enter a new name for the Native Asset in the **Name** field.
    1. Select an appropriate **Title**, and **Body Text**, from the text asset recommendations.
    1. Beginning in September 2025, fill in the European Union (EU) political declaration. The default declaration for all new creatives is non-political. However, if your creative is political advertising, you must declare it and also declare whether you intend to serve the ad in the EU.

1. To automatically resize the main Native creative and its icon, select the **Allow smart image adjustment** toggle, then choose one of the available radio buttons:
    1. **Include white bars to fill placement:** Adds white space above and below the image and icon within the placement.
    1. **Crop image to fit placement:** Enlarges or reduces the size of the image and icon so that they fill the entire placement. <br>
1. You can preview the image and icon before saving, to determine which option works best by clicking **Preview adjusted examples**. For more information, see [Smart Image Adjustments for Native Creatives](smart-image-adjustments-for-native-creatives.md).
1. You can see two different previews available for each option, one with the widest extreme and the other with the tallest extreme. For more information, see [Smart Image Adjustments for Native Creatives](smart-image-adjustments-for-native-creatives.md). 
1. **Optional:** [Configure tracking parameters](configuring-tracking-for-creatives.md). 
1. **Optional:** [Associate the creative to the appropriate Line item](associate-line-items-with-a-creative.md). 
1. **Optional:** [Exclude competitive brands.](exclude-competitive-brands-for-a-creative.md)
1. **Optional:** [Exclude competitive offer categories.](exclude-competitive-offer-categories-for-a-creative.md)
1. Select the appropriate [audit option](select-an-audit-option-for-a-creative.md) for the creative.
1. Click **Save**.
