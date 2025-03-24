---
title: Assign a Default Creative to a Placement
description: In this article, find step-by-step instructions on how to assign a default creative to a placement.
ms.date: 10/28/2023
---

# Assign a default creative to a placement

> [!TIP]
> To promote in-house products, services, or initiatives, use House Line Items to manage creatives across multiple placements or publishers. For more details, see [House line items](ad-campaign-house-line-items.md).

In order to prevent serving blanks or [Default PSAs](default-psas.md), you can set up your own default creative and assign it to a placement. This can either be a hosted creative or a third-party URL or tag that sends the impression to another ad server.

- **Defaulting to a third-party ad server**

  When you default to a third-party ad server, you are still filling the impression and therefore will pay the publisher for this default.

- **Defaulting to a Publisher's ad server**

  If you are defaulting to a publisher's ad server and you pay them on a CPM basis, then you will not want to count that impression towards your payment to the publisher. You can choose this setting when you select a CPM payment rule.

- **Price floors based on gross network revenue or publisher revenue**

  You can choose whether bids are compared to your price floor as your network revenue and the publisher's revenue combined, or just the publisher's revenue. You can access these options in the **Default Creatives** pane of the **Inventory Manager** screen.

> [!NOTE]
> You cannot assign default creatives to placements that allow interstitial creatives.
> [!TIP]
> **Network-Level Default Creatives**
>
> If you want to use the same default creatives for all your placements, you can work with your Microsoft Advertising representative to add them at the network-level. If you also add default creatives to a particular placement, the placement-level creatives will be used instead of the network-level creatives.
> [!IMPORTANT]
> **About Flagged Impressions**
>
> In the past, filtered impressions on inventory flagged as violating platform standards would serve blanks. Now, these impressions follow seller preferences for impressions with no demand. As with all impressions that follow this workflow, sellers will be charged the applicable fee.

## Step 1. Select the placement

Under **Publishers** > **Inventory Manager**, select the placement to which you want to add a default creative by clicking anywhere in the row. This displays the placement details and any default creatives already assigned to the placement.

In the **Default Creatives** pane, click **Add**. This opens the **Add Default Creative** dialog.

## Step 2. Select an existing default creative or add a new default creative

If you want to assign an existing default creative (if one is available) to the placement, select the creative from the **Creative** field. If you want to add a new hosted or third-party default creative, do not select a value from the **Creative** field (default value is "Add New...") and follow the directions below.

> [!NOTE]
> If no pre-existing default creatives of an appropriate size are available, the **Creative** field will not be displayed (i.e., size and media type of the default creative must match those of the placement).

## Step 3. Set the reserve price for the default creative

Specify a value in the **Serve the default creative if the maximum eCPM bid is less than $** field. If none of the net bids for this placement are above the net eCPM value you set here, the default creative you have specified will be served.

> [!NOTE]
> The value of the **Serve the default creative if the maximum eCPM bid is less than $** field (i.e., the default creative's reserve price) will override any reserve price that has been set on the placement itself.

## Step 4. Set the remaining values for the default creative

### Hosted default creative

- **Name** - Enter a name for the default creative.
- **Type** - The **Upload a file** radio button is selected by default.
- **File** - Browse for the file to upload. The following file formats are supported: jpg, gif, png, swf.
  
  > [!NOTE]
  > If your account is enabled for video hosting, these additional file formats are supported: flv, mp4, wmv, f4v, avi, m4v, mov, and mpg. It is recommended to set up **House Line Item** before attaching a hosted video creative. See [House Line Item](ad-campaign-house-line-items.md) for more details.

- **Landing Page URL** - Set a landing page for the creative.
- **Flash Click Variable** - If you are uploading a swf file that contains a ClickTag variable for click tracking, enter the exact variable.
- **Media Type** - Select the media type for the creative, for example, Standard Banner, In-Banner Video, Standard Interstitial, etc. Note that this must match the media type and media subtype settings on the placement.
- **Template** - Based on the file format and the media type, the correct rendering template for your creative is selected by default, but you can choose a different template, if available. For more information about rendering templates, see [Creative Templates](creative-templates.md).
- **Template Options** - If the rendering template for the creative requires you to make additional decisions about the creative content, complete the fields in the **Template Options** section.
- **Size** - If the file dimensions are not automatically detected, select the file width and height. If you don't find the dimensions listed, select "custom" and then enter the width and height. Note that the default creative's dimensions must match the size of the placement.

    > [!NOTE]
    > In the event that a placement is sizeless and you have not selected a default creative for all possible sizes, a [Default PSA](default-psas.md) may serve instead of your default creative.

### Third-Party default creative

Configure the third-party default creative by providing the following information:

- **Name** - Enter a name for the default creative.
- **Type** - Select the **Third-party creative** radio button.
- **Creative Format** - Select whether you are adding the creative based on a **Third-party tag** or a **Third-party URL**. This selection determines the next fields that you will complete.
- **Tag** and **Tag Type** - For a third-party tag, enter the HTML or raw JavaScript tag that redirects the browser to the third-party ad server, and select whether the tag is HTML and served in an iFrame or is JavaScript code.
  
  > [!WARNING]
  > **AdSense Tags**
  >
  > When adding an AdSense HTML tag, be sure to uncheck the **Serve in iFrame** box. If this box is checked, AdSense may have difficulty determining the content and location of the tag due to the iFrame, which may result in discrepancies between Microsoft Advertising and AdSense. Microsoft Advertising should automatically populate the domain with the full path. However, if you need to manually add it, include the `${REFERER_URL}` [creative macro](creative-macros.md).

- **URL** and **Output Type** - For a third-party URL, enter the URL pointing to the third-party creative, and select the resource type of the third-party creative.
- **Landing Page** - For a third-party URL, if you selected "Image" or "Flash" as the output type, set a landing page for the creative. If you want to associate the creative with multiple line items that have different landing pages, set the landing page at the line item level. For more details, see [Dynamic Landing Pages](dynamic-landing-pages.md).
- **Flash Click Variable** - For a third-party URL, if you selected "Flash" as the output type, if the file contains a ClickTag variable for click tracking, enter the exact variable.
- **Media Type** - Select the media type for the creative, for example, Standard Banner, In-Banner Video, Standard Interstitial, etc. Note that this must match the media type and media subtype settings on the placement.
- **Template** - Based on the file format and the media type, the correct rendering template for your creative is selected by default, but you can choose a different template, if available. For more information about rendering templates, see [Creative Templates](creative-templates.md).
- **Template Options** - If the rendering template for the creative requires you to make additional decisions about the creative content, complete the fields in the **Template Options** section.
- **Size** - Select the dimensions of the default creative. If you don't find the dimensions listed, select "custom" and then enter the width and height. Note that the default creative's dimensions must match the size of the placement.

  > [!NOTE]
  > In the event that a placement is sizeless and you have not selected a default creative for all possible sizes, a [Default PSAs](default-psas.md) may serve instead of your default creative.

## Step 5. Save the default creative

To finish assigning the default creative to the placement, click the **Save** button. The default creative will be visible in the **Default Creatives** pane for the placement.

## Troubleshooting default creatives

If you have a default creative in place but are still seeing [Default PSAs](default-psas.md), this could be caused by several things:

- The default creative was flagged by our audit and prevented from serving
- The placement is sizeless and there is not a default creative for all needed sizes
- The placement is seeing secure traffic but the default has not been trafficked as secure

> [!NOTE]
> If you receive a message that the default creative is prohibited from serving, the most likely cause is that the creative has been marked as malicious, most likely by Sherlock. The contacts identified as Sherlock notification recipients can review the notifications to determine the reason the creative has been flagged. If you need further assistance, contact Microsoft Advertising support.

See [Serve Default Creatives Instead of PSAs](serve-default-creatives-instead-of-psas.md) for step-by-step instructions on how to remedy several of these issues.

## Related topics

- [Create a Placement](create-a-placement.md)
- [Default PSAs](default-psas.md)
- [Serve Default Creatives Instead of PSAs](serve-default-creatives-instead-of-psas.md)
