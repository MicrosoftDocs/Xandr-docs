---
title: Use IAB's HTML5 clickTag Standard on Xandr
description: Implement IAB's clickTag in HTML5 for ad click tracking, linking the landing page to a specified URL.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Use IAB's HTML5 `clickTag` standard on Xandr

Follow these instructions to use the IAB's `clickTag` standard in HTML5 creatives hosted with Xandr. This allows
Xandr to track clicks and set the ad's landing page to the URL provided in.

## Prerequisites

You will require a text editor to complete the procedure below. If you do not have one, we recommend [Sublime Text](http://www.sublimetext.com/2).

> [!NOTE]
> Do not hardcode landing page URLs for your creative. This will be set in when the assets are uploaded.

## Step 1: Add the Xandr HTML5 library

Add the Xandr HTML5 Library inside the `<head>` tag in the **`index.html`** file, by adding the following `<script>` tag:

`<script type="text/javascript" src="https://acdn.adnxs.com/html5-lib/1.4.1/appnexus-html5-lib.min.js"></script>`

> [!TIP]
> Use https to ensure the creative can serve on secure inventory.

## Step 2: Add `APPNEXUS.getClickTag()` to a clickable element

Wrap the banner markup in an HTML element that opens a new window and uses the `APPNEXUS.getClickTag()` function. This will retrieve the value of the `clickTag` parameter set in the ad URL. The example below uses the \<a\> anchor element with the `href` attribute set to `javascript:void(0)` and an `onClick` attribute set to `window.open(APPNEXUS.getClickTag(), '_blank');`.

Open `<a href="javascript:void(0)" onClick="window.open(APPNEXUS.getClickTag(), '_blank');">` immediately
after `<body>` and be sure to close it with `</a>` immediately before `</body>`. The banner markup should go
between `<a href="javascript:void(0)" onClick="window.open(APPNEXUS.getClickTag(), '_blank');">` and `</a>`.

```
<body>
        <a href="javascript:void(0)" onClick="window.open(APPNEXUS.getClickTag(), '_blank');">
                <!-- Your banner markup goes here. -->
        </a>
</body>
```

## Step 3: Test

Save your work. Open the **`index.html`** file in your web browser. Add `?clickTag=http://www.xandr.com` at the end of the URL in the address bar.

`file:///Users/username/Desktop/ad.html?clickTag=http://www.xandr.com`

Refresh the page and click on the ad. A new window with Xandr' website should open in your browser. When
the ad is served Xandr sets the value of `clickTag` to Xandr' click tracker and a redirect to the landing page URL provided for the creative in.

Save your work again.

## Step 4. Zip creative contents

Select all of the contents. Compress the contents into a `.zip` file.

:::image type="content" source="media/zip-creatives.png" alt-text="Screenshot that explains how you can select all of the contents and compress the contents into a .zip file.":::

You are now ready to upload your HTML5 creative onto the Xandr platform.

## Additional option

Xandr follows [IAB HTML5 guidance](http://www.iab.com/guidelines/html5-for-digital-advertising-guidance-for-ad-designers-creative-technologists/) for `clickTag` (Section 3.10.1). The ad URL returned to a publisher's page includes a `clickTag` parameter in the query string. Ad developers who prefer not to use Xandr' `getClickTag()` convenience can access the `clickTag` parameter's value with their own Javascript. In this case, the ad does not need to load the Xandr HTML5 Library.

**Example Ad URL with `clickTag` parameter**
`https://vcdn.``adnxs``.com/.../index.html?clickTag=http%3A%2F%2Fnym1-ib.``adnxs``.com%2Fclick%3FAA...gwJUgAAAAA.%2Fbn%3D0%2Fclickenc%3Dhttp%253A%252F%252Fwww.``appnexus``.com%252F`

## Related topics

- [Build an HTML5 Xandr Creative in Google Web Designer](build-an-html5-xandr-creative-in-google-web-designer.md)
- [Build an HTML5 Xandr Creative in Adobe Edge](build-an-html5-xandr-creative-in-adobe-edge.md)
- [Integrate the Xandr HTML5 Library with Ads Created in Adobe Edge](integrating-the-xandr-html5-library-with-ads-created-in-adobe-edge.md)
- [Integrating the Xandr HTML5 Library with Ads Created in Google Web Designer](integrating-the-xandr-html5-library-with-ads-created-in-google-web-designer.md)
