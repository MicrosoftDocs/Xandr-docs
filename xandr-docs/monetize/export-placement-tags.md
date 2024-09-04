---
title: Export Placement Tags
description: Explore cookie-free Microsoft Ads, ensuring data-consent-free experience with advantages like relevant calls, avoiding extra cookies.
ms.date: 10/28/2023
---

# Export placement tags

> [!NOTE]
> Microsoft Advertising now supports a domain, `adnxs-simple.com`, which does not send or read browser cookies on requests. Clients can leverage this cookie-free domain when there is no consent to use personal data. Relevant calls initiated by Microsoft Advertising will automatically use this domain when there is no consent or when cookies are not required for the function. For more information, see [Part of Service Policies](../policies-regulations/index.yml).

Once you've finished setting up placements, you can export the tags and give them to your publishers for inclusion on pages.

## How to export placement tags 
The following steps will guide you through exporting placement tags.

## Step 1. Select the placements to export

**For Publisher clients:** Navigate to **Partners** >  **Placements** and select a publisher. Check the boxes next to placements that you want to export, click **More Actions**, then select **Export Tags**. This displays the **Export Placement Tags** dialog.

**For all other clients:** Navigate to **Publisher** >  **Inventory Manager**, check the boxes next to placements that you want to export, click **More Actions**, then select **Export Tags**. This displays the **Export Placement Tags** dialog.

## Step 2. Modify the tag options

In the **Modify Tags** section, set the format and type for the tags:

- **Format** - This field is set to "JavaScript" by default. If necessary, you can change the format using the dropdown menu.
  
  > [!IMPORTANT]
  > For placements that allow VAST video creatives, the **Format** option is not relevant. Tags for these placements will always be URL.  

- **Type** - This field is set to "Standard" by default. If necessary, change the type using the dropdown menu.
  
   > [!NOTE]
   > **Secure Tags**:
   >
   > To obtain a secure tag, it is not sufficient to simply export a standard tag and change "http" to "https" in the tag URL. Instead, to make sure the tag gets formatted properly as secure, it's important to select "Secure" as the tag **Type**.

You can also add additional parameters to the tags:

- **Use cachebuster** - If the publisher uses a macro to dynamically ensure that the user's browser does not cache the placement URL, select this option and enter the cachebuster macro.
- **Enable click-tracking** - If the publisher provided you with a third-party click tracking URL to include in the ad call, select this option and enter the URL (not applicable to video).
- **Age** - If your publisher uses a macro to dynamically add the age of the user to the ad call, select this option and enter the age macro.
- **Gender** - If your publisher uses a macro to dynamically add the gender of the user to the ad call, select this option and enter the gender macro. Note that we only evaluate the first letter of the value (m or f).
- **Allowed size** - This option is mandatory for sizeless placements. You must enter the creative dimensions that the placement allows. Be sure to enter the dimensions without brackets, for example, `300x250` instead of `[300x250]`.
- **Allow additional sizes** - If you want the placement to allow creatives of additional sizes, select this option and enter the dimensions. Be sure to enter the dimensions without brackets and separated by commas, for example,
  `300x250,180x150` instead of `[300x250],[180x150]`.

## Step 3. Generate the tags

Click the **Get Tags** button. The dialog refreshes to show the tags as well as your delivery options. Also, a preview displays below each tag that has default creatives.

## Tag format

Except for placements that allow VAST video creatives, all tags are generated in the format selected in step 2 (IFrame or JavaScript). For placements that allow VAST video creatives, the tags are generated as URLs. In the URLs, we have automatically changed "/ttj" to "/ptv" to ensure ad calls will return the XML required by your publisher's video
player.

> [!NOTE]
> **Secure Tags**:
>
> To obtain a secure tag, it is not sufficient to simply export a standard tag and change "http" to "https" in the tag URL. Instead, to make sure the tag gets formatted properly as secure, it's important to select "Secure" as the tag **Type** (see step 2).

## Delivery options

You have three delivery options: You can either copy the tags manually, download the tags as an HTML file, or email the tags to up to 10 recipients.

 **VAST Tags**

> [!TIP]
>
> - Be sure to tell your publisher to copy the URL into the video player rather than placing it directly on the page.
> - If you have whitelabeled Monetize and your domain appears within the generated tag, you must replace your domain with
> "ib.adnxs.com" in the tag before sending the tag to your publisher. Otherwise, the whitelabeled VAST tag will redirect
> to the Microsoft Advertising domain, which the Flash-based player will not accept; for security purposes, Flash-based players will not retrieve content when redirected to a different domain.
>
:::image type="content" source="media/generated-tags.png" alt-text="Screenshot that explains the export placement tags.":::

## Related topics

- [Create a Placement](create-a-placement.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)
- [Placement Tag Parameters](placement-tag-parameters.md)
