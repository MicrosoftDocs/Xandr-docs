---
title: Create a Placement
description: In this article, find information on how to create and set up a placement.
ms.date: 10/28/2023
---

# Create a placement

> [!NOTE]
> Microsoft Advertising now supports a domain, `adnxs-simple.com`, which does not send or read browser cookies on requests. Clients can leverage this cookie-free domain when there is no consent to use personal data. Relevant calls initiated by Microsoft Advertising will automatically use this domain when there is no consent or when cookies are not required for the function. For more information, see [Part of Service Policies]([../policies-regulations/index.yml](https://learn.microsoft.com/en-us/xandr/policies-regulations/)).

A placement is the object in our system that represents (and is used to generate) the tag that is placed on a publisher's page.

When you create a placement, follow these steps:

- Select the types of creatives that can serve on the placement.
- Configure settings that may impact monetization, such as size, video requirements, and reserve price
- Self-classify the placement with categories and sensitive attributes for line item targeting and reporting

## Step 1. Get started

Depending on which version of Monetize you use, you can access the **Inventory Manager** screen by doing one of the following:

- From the **Publishers** tab, navigate to **Publishers** > **Inventory Manager**.
- From the **Inventory** tab, navigate to **Partners** > **Placement**.

If prompted, select a publisher. Click the **Create New** button, and then select **Placement**.

## Step 2. Define the basic settings

Select the placement group the placement will be associated with.

Enter a **Name** for the placement and do any of the following:

- If you want to assign your own custom codes to the placement, expand the **Enable Code** field and enter your codes.
- If you do not want the placement to be active once it's saved, select **Inactive**. Otherwise, the **State** field is set to **Active** by default.

    > [!NOTE]
    > If you try to serve an impression on an inactive placement, the impression will be blank and Microsoft Advertising will not redirect it.

- Enable Rewarded Content if the user receives a reward (such as in-app currency or in-game powerups) after viewing an ad.

> [!NOTE]
> The **Enable this placement for reselling to other platform members** checkbox has been removed from placement-level settings.
>
> If you want to make a placement's inventory available for resale to other members, you must set the **RTB Marketplace** option to "**Participate**" on the placement group that contains the placement. Since placement group settings apply to all placements within a placement group, it is important to ensure that placement groups which are to be resold only contain placements that you want enabled for reselling. See [Create a Placement Group](create-a-placement-group.md) for a description of this new setting and how it works.

## Step 3. Limit the type and size of creatives that can serve

In the **Allowed Media** section, you can limit the creative media types and sizes that can serve on the placement.

### Media types and subtypes

The Microsoft Advertising platform categorizes creatives by media type and media subtype. Media type defines the general display style of creatives such as Banner and Skin, and media subtype defines the specific display style of creatives such as Standard Banner, In-Banner Video, IAB skin, and Custom skin.

- **Type and Subtype Combinations:** At least one allowed media must be selected, but Placements can also be configured to support multi-format. For example, you can enable "Banner" and "Native" media types such that creatives with either media type designation would be eligible to bid on this placement, potentially increasing available demand. There are limitations on the combination of media types allowed; media types will be greyed out when they are ineligible based on your current selection. This limitation ensures that only appropriate creatives are served on a placement. For example, a placement that allows creatives of the "Video" media type is intended to be fed to a video player; it would not make sense to allow creatives of any other media type, such as "Interstitial," to serve on the placement.
- **Expandable Placements:** You can set a placement to allow the "Expandable" media type or any of its subtypes for direct (not resellable) inventory only.

    > [!NOTE]
    > If you select this option, an error message appears if you try to save the placement with this media type for resellable inventory. If you want to support expandable creatives for placements associated with placement groups that have been made available for reselling to other platform members, the placement ID and URL must be provided to [support](https://support.ads.microsoft.com) for verification.
    When exporting and placing an expandable tag on your publisher's page, declare a size in the `size=` parameter as you would in a standard banner tag. When an expandable creative is served to the tag, it will expand outside of the designated size.

- **Private Media Types:** Private media types and subtypes can serve only for custom deals or packages. When checked, the **Private** checkbox allows the media type or subtype to serve on custom deals and packages you set up.

### Sizes

Sizes are only relevant for Display ads. By default, the creative size for the placement is **Sizeless**, which means that creatives of any size will be allowed to serve. If you want to restrict the placement to creatives of a specific size, select the size from the **Creative Sizes** field.

If your placement uses a friendly iFrame and you want the placement to resize to fit smaller or larger creatives, you can select the **Resize placement if creative size is different...** checkbox.

> [!NOTE]
> This option should only be used with MegaTag, because the resizing depends on JavaScript with variables and methods that are only defined in megatag.js.

### Private sizes

Private sizes are additional placement sizes that can serve for custom deals, packages and managed campaigns. If you want to allow private sizes, select the sizes you want from the **Private Sizes** list, or add a new size below the list.

To use these sizes in a deal, check the **Allow deal to include private sizes** checkbox in the [Create a Custom Deal](create-a-custom-deal.md).

> [!TIP]
> You can also set private sizes when you export the placement tag using the `private_sizes` query string. See [Placement Tag Parameters](placement-tag-parameters.md) for more information.

## Step 4. Choose the appropriate video settings (video placements only)

If you are creating a video placement, the **Video Settings** and **Advanced Video Settings** sections appear when you select a Video media type under Allowed Media.

In the **Video Settings** tab, enter details about the video position and ad pod configuration (in-stream only), player size, ad duration, and skipability.

> [!NOTE]
> If you are working with ad pods (linear groupings of more than one ad designed to fill a single placement), the max duration you select is the maximum duration for the total number of ads in the ad pod. Buyers will be able to target placements that allow ads that fit into the max duration specified for the ad pod, and they can specify the order in the ad pod where they would like their ads to appear.

### Skippable

When a video placement is set to **Skippable**, a new **Skip Offset** (skipoffsetseconds) field is displayed. A publisher can specify how many seconds pass until the ad can be skipped. When the VAST file gets rendered for the placement, the skipoffsetseconds value from the placement is inserted into the VAST file. This will apply to that placement every single time a creative is served. However, when you traffic a creative, we are giving users the option of setting a skipoffset_seconds value that would override the default that is on the placement. This occurs in the publisher ad server use case, where an ad server is running their own creative in a placement. You now have the ability to override the value on an individual ad.

> [!NOTE]
> The value provided in the creative will override the value defined in the placement. It should also be noted that this will only apply to placements that are in your member.

The Advanced Video Settings section enables additional video configurations such as VAST versions, supported frameworks and mime types, and player settings, where relevant.

## VAST version

The creative's VAST version must be compatible with the VAST player it is served to. Otherwise, errors may occur, causing the publisher to lose revenue. For example, if the publisher's VAST 3.0 player validates a creative with a VAST version of 3.0 but instead we serve a creative with a VAST version of 2.0 to that VAST player, an error will be generated. Select the appropriate VAST version from the Player VAST version menu to avoid errors.

To add the VAST player version when creating a new placement:

1. Click the **Create New** button from the **Inventory Manager** screen.
1. Select **Placement**.
1. Search for an existing placement group and select from the list of results.
1. Scroll down to the **Allowed Media** section and select a media type under the **Video** section.
1. Expand the **Advanced Video Settings** section that displays.
1. Select the appropriate **Player VAST version** from the menu.
1. Click the **Save and close** button.

To add the VAST player version for an existing placement:

1. Select the appropriate placement from the **Inventory Manager** screen.
1. Expand the **Advanced Video Settings** section.
1. Select the appropriate **Player VAST version** from the menu.
1. Click the **Save and close** button.

### Mixed media and mime type options

> [!NOTE]
> If a creative's VAST contains both VPAID and inline video files, it will be assigned the VPAID frameworks when it's uploaded in Microsoft Advertising. Therefore, certain placements that permit multiple creative types may be blocked in auction. To ensure accurate creative matching, you should follow the steps outlined below.

To set mime type options (recommended), select the **Show Mime Type Options** checkbox. This opens the **Mime Type Options** section. From there, you will need to set two distinct fields: **Handles Mixed Media** and **Video Mime Types**.

### Handles mixed media

This checkbox is used to denote if your player can successfully parse a creative and identify the correct media files if the creative has media files with varying mime types.

- If checked (default), Microsoft Advertising will serve a creative as long as it has one media file you do support.
- If not checked, Microsoft Advertising will not serve a creative unless it only has the media files you do support.

> [!NOTE]
> Unchecking the handles mixed media option may have meaningful monetization implications from programmatic demand sources. It is recommended that if your video player supports it, that this option remains checked.

### Video mime types

These checkboxes allow you to identify the format of the file. For instance, **video/mp4** is a mime type that tells Microsoft Advertising the file is a video and the type of video file is mp4. All mime types are selected by default.

- To ensure we are only serving creatives with media files that your player can play, select the mime types that you know your player supports by checking the appropriate boxes.
- If your player does not support VPAID, do not select application/javascript or application/x-shockwave-flash.

## Step 5. Apply content categories to the placement (optional)

In the **Categories and auditing** section, you can apply **universal** and **custom** categories to the placement.

### Universal categories

You can apply up to 20 categories from the Microsoft Advertising universal list of content categories. Your managed advertisers and other buyers who trust your self-categorization can target these categories through their campaigns.

### Custom categories

You can apply your own custom categories to sites or placements to create particular slices of inventory. Your managed advertisers can target these categories through their campaigns. You can enable buyers to target only those custom categories you specify in your buyer eligibility settings.

You can create a new custom category by navigating to the **Network** tab > General > Content Categories, and selecting **New content category**. See [Manage Custom Content Categories](manage-custom-content-categories.md) for more details.

Once a custom category has at least one placement associated to it, buyers can select it when targeting a campaign if they have been given access via your buyer eligibility settings.

## Step 6. Self-audit the placement for sensitive categories

In the **Categories and auditing** section, you can self-classify the placement for sensitive attributes and intended audience. Your advertisers and buyers who trust your self-audit can target these settings in their campaigns. Microsoft Advertising may review this inventory if it exceeds a certain volume threshold.

> [!WARNING]
> You will be notified of undeclared and improperly declared toolbar inventory on a weekly basis. Microsoft Advertising will flag this inventory and declare/properly declare it within 72 hours of notification.
> [!NOTE]
> For compliance with the Children's Online Privacy Protection Act (COPPA), designating your placement as intended for children will indicate to our system to apply special COPPA rules, including that user information will not be collected. Campaigns requiring user information for frequency capping or other targeting purposes will not serve on this placement.

## Step 7. Apply advanced settings to your placement (optional)

### Apply pricing rules

If you want to override publisher-level payment rules, select the Use placement-level pricing checkbox and then enter the CPM amount that the publisher should receive.
If you'd like to set a reserve price on this placement, select the Set a placement reserve price checkbox and enter a CPM price into the text area. Note that any reserve price you enter here will be applied to all demand for this placement. However, you can change this setting later by editing Reserve Price Setting. For more information, see [Update a Placement](update-a-placement.md).

If you use placement-level pricing, impressions governed by this pricing will appear in reporting under default payment rules even when these rules were not applied to impressions. This is because every managed or resold impression currently must be associated with a payment rule in reports.

### Limit the advertisers and line items that can serve

In the Advertiser Filtering section, you can include or exclude specific managed advertisers, line items, and campaigns from serving on the placement.

> [!NOTE]
> Including or excluding specific advertisers will not prevent RTB Marketplace buyers from serving on this placement. To do this you must use [Working with Ad Quality](working-with-publisher-ad-quality.md) or ensure that the placement's parent [Create a Placement Group](create-a-placement-group.md) is not participating (reselling) in the RTB Marketplace.

## Step 8. Add a piggyback pixel (optional)

If you want a piggyback pixel to fire when a creative serves on the placement, enter the pixel's URL or secure URL on the **Piggyback Pixel** tab and specify whether the pixel is a 1x1 image or JavaScript. A piggyback pixel can be an [Impression and Click Tracker](working-with-impression-and-click-trackers.md), a beacon, or any other JavaScript that the publisher needs loaded alongside an ad.

> [!NOTE]
> Piggyback pixels are currently unsupported for `/ptv` video tags due to how VAST payloads are structured.

## Step 9. Save the placement

To finish adding the placement to the Microsoft Advertising platform, click the **Save** button. The placement is then added to the **Placement List** in the **Inventory Manager**.
