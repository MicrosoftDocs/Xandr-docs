---
title: Native Assembly Object Placeholders
description: Learn adding diverse data, images, and placeholders to HTML text box in Renderer tab for native assemblies in this article.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Native assembly object placeholders

You can add a variety of standard and custom data and image object placeholders to the **HTML** text box within the **Renderer** tab for your native assemblies. Here's a list of available standard and custom data and image object placeholders:

## Standard data object placeholders

| Placeholder | Description |
|---|---|
| [%title%] | Title that will appear when the native creative is rendered. |
| [%body%] | Short description that will provide details about the native creative. |
| [%sponsoredBy%] | Brand name that will be associated with the native creative. |
| [%cta%] | Encourages the user to take the necessary action after viewing the native creative (e.g. signing for the mailing list). |
| [%clickUrl%] | URL to the website that the user will be redirected to when they click the native creative. |
| [%displayUrl%] | Public URL that will be visible to the user when the native creative is rendered. |
| [%clickFallbackUrl%] | Backup URL if the main click URL is not supported. |
| [%price%] | Price for product / app / in-app purchase. The appropriate localized currency symbol should be included. |
| [%salePrice%] | Sale price that can be used together with the price to indicate a discounted price compared to a regular price. The appropriate localized currency symbol should be included. |
| [%rating%] | Rating of the product being offered to the user. For example, an app's rating in an app store from 0-5. |
| [%likes%] | Number of social ratings or "likes" for the product being offered to the user. |
| [%downloads%] | Number downloads/installs of this product. |
| [%phone%] | Phone number that will be visible to the user when the native creative is rendered. The phone number should be formatted according to your locality. For example, your phone number would be formatted as such if you are based in the United States: 800-555-5555. |
| [%address%] | Address that will be visible to the user when the native creative is rendered. |
| [%desc2%] | Detailed version of the native creative's body text. |

### Example HTML - title `[%title%]`

```
<p class='native-title'>[%title%]</p>
            <div class='native-body'>
            <a href='[%clickUrl%]' target='_blank'>Click Here</a>
            
            [%impressionTrackers%]
            [%javascriptTrackers%]
            [%clickTrackers%] 
```

A placeholder has been added (**`[%title%]`** on the first line). You can add **`[%title%]`** to represent where you want to add the Native view, which is located on the left side of the **Setup** and **Renderer** tabs. In the Native view, you can replace **`[%title%]`** with the default "10 Breakfast Foods That Everyone Needs In Their Diet" title or the title from the winning creative.

### Example HTML - Call-to-action `[%cta%]`

```
<p class='native-title'>[%title%]</p>
            <div class='native-body'>
            <a href='[%clickUrl%]' target='_blank'>[%cta%]</a>
            
            [%impressionTrackers%]
            [%javascriptTrackers%]
            [%clickTrackers%] 
```

A placeholder has been added (**`[%cta%]`** on the third line). You can add **`[%cta%]`** to represent where you want to add the Native view, which is located on the left side of the **Setup** and **Renderer** tabs. In the Native view, you can replace **`[%cta%]`** with **Click Here**.

## Standard image object placeholders

All of the standard image object placeholders have a URL, width, and height property, so please add the appropriate property after "image". For example, **`[%image.url%]`**, **`[%image.width%]`**, and **`[%image.height%]`**.

| Placeholder | Description |
|---|---|
| [%image%] | Primary image that will appear when the native creative is rendered. |
| [%icon%] | Primary icon that will appear when the native creative is rendered. |

### Example CSS - Image URL `[%image.url%]`

```
.native-title {
            color: grey;
            }
            .native-body {
            background: url([%image.url%]);
            width: 300px;
            height:350px;
            } 
```

## Custom data object placeholders

Please note that there are five placeholders for each of these custom data object placeholders.

| Placeholder | Description |
|--|--|
| [%customTitle1%] - [%customTitle5%] | Additional titles that will appear when the native creative is rendered. |
| [%customBody1%] - [%customBody5%] | Additional body text that will appear when the native creative is rendered. |
| [%customCTAtext1%] - [%customCTAtext5%] | Additional calls to action that will encourage the user to take the necessary action after viewing the native creative (e.g., signing for the mailing list). |
| [%customSocialUrl1%] - [%customSocialUrl5%] | URLs that will take the user to the corresponding social media platforms. |
| [%customDisplayUrl1%] - [%customDisplayUrl5%] | Additional public URLs that may be visible and/or automatically redirect the user to a web page that is connected to the landing page's domain. |

## Custom image object placeholders

Please note that there are five placeholders for each of these custom image object placeholders. All of the custom image object placeholders have a URL, width, and height property, so please add the appropriate property after "`customImage`#.". For example, **`[%customImage1.url%]`**, **`[%customImage1.width%]`**, and **`[%customImage1.height%]`**.

| Placeholder | Description |
|--|--|
| [%customImage1%] - [%customImage5%] | Additional images that will appear when the native creative is rendered. |
| [%customIcon1%] - [%customIcon5%] | Additional icons that will appear when the native creative is rendered. |
| [%customSocialIcon1%] - [%customSocialIcon5%] | Corresponding social media icons that will appear when native creative is rendered. |

## Tracker object placeholders

| Placeholder | Description |
|---|---|
| [%impressionTrackers%] | Adding this to the HTML code will fire impression trackers when the creative is rendered |
| [%javascriptTrackers%] | Adding this to the HTML code will fire Javascript trackers when the creative is rendered |
| [%clickTrackers%] | Adding this to the HTML code will make all tags in the renderer fire click trackers when clicked |

> [!NOTE]
> The trackers won't be fired in the Native Preview. If you are looking to make every element of the native assembly (e.g., title, image, and call-to-action button) a link to the landing page, please add the following to your Javascript:

```
const container = document.getElementById(targetId);
               container.addEventListener('click', () => {
               window.open(nativeObj.clickUrl, '_blank');
               });
```

### Example HTML `[%click_trackers%]`

```
<a href='[%clickUrl%]' target='_blank'>
            <p class='native-title'>[%title%]</p>
            <div class='native-body'>
            [%cta%]
            
            </a>
            [%impressionTrackers%]
            [%javascriptTrackers%]
            [%clickTrackers%] 
```

## Related topic

[Configuring a Native Assembly](configuring-a-native-assembly.md)
