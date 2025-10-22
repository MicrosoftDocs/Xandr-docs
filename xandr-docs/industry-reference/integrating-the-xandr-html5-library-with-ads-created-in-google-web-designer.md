---
title: Integrating the Xandr HTML5 Library with Google Web Designer Ads
description: In this article, find instructions on how to modify an ad created in Google Web Designer to work with the Xandr HTML5 Library. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Integrating the Xandr HTML5 Library with Google Web Designer ads

Follow these instructions to modify an ad created in Google Web Designer such that it works seamlessly with the Xandr HTML5 Library. This is required to properly track clicks.

## Banner ads

### Prerequisites

You will require a text editor to complete the procedure below. If you do not have one, we recommend [Sublime Text](http://www.sublimetext.com/2).

### Step 1: Locate the `index.html` file

Before you begin, locate the folder containing the ad created in Google Web Designer. If the ad is located in a `.zip` file, you must unzip the file to reveal a folder containing its various assets.

Then, locate and open the file named `index.html`. This file is where you will make all of the necessary changes in the steps below.

### Step 2: Add the Xandr HTML5 Library

Ensure that the actual Xandr HTML5 Library is linked to inside `index.html`.

Link the library inside the `<head>` tag in the `index.html` file, by adding the following `<script>` tag:

```
<script type="text/javascript" src="https://acdn..com/html5-lib/1.3.0/-html5-lib.min.js"></script>
```

> [!TIP]
> Use `https` to ensure the creative can serve on secure inventory.

### Step 3: Replace hard-coded URL with `APPNEXUS.getClickTag()`

You could have an ad created in Google Web Designer that has a hard-coded URL embedded.

Search for `gwd-events="handlers"` in the `index.html` file to find hard-coded URLs. If they are present, you will find a block of code that looks like this:

```
<script type="text/javascript" gwd-events="handlers">
        gwd.auto_BodyClick = function(event) {
                // GWD Predefined Function
    gwd.actions.gwdGenericad.exit('gwd-ad', 'https://appnexus.com', true);
  };
</script>
```

> [!NOTE]
> The hardcoded URL (in this case, `https://xandr.com/`) will vary based on the specific ad you are working with.

Replace `"https://xandr.com"` (including the quotation marks) with `APPNEXUS.getClickTag().` The function should look something like this:

```
<script type="text/javascript" gwd-events="handlers">
        gwd.auto_BodyClick = function(event) {
                // GWD Predefined Function
    gwd.actions.gwdGenericad.exit('gwd-ad', APPNEXUS.getClickTag(), true);
  };
</script>
```

### Step 4. Save changes

Save the changes.

### Step 5. Re-zip creative contents

Select all of the contents within the folder created when you unzipped the file. Compress the contents into a new `.zip` file.

:::image type="content" source="media/rezip-creatives.png" alt-text="A screenshot that shows how to compress files.":::

You are now ready to upload your HTML5 creative onto the Xandr platform.

> [!NOTE]
> For information on using Google Web Designer to build HTML5 creative that will properly track clicks in Xandr, go to: [Build an HTML5 Xandr Creative in Google Web Designer](build-an-html5-xandr-creative-in-google-web-designer.md).
>
> If you are facing any build related issue, you can raise a ticket on the [Xandr Customer Support Portal](https://help.xandr.com/s/login/) or get in touch with your Xandr Account Representative.

### IAB validator (optional)

If you would like to verify how this creative measures up to IAB guidelines, you can do so using the [HTML5 Ad Validator](https://www.iab.com/news/iab-tech-lab-releases-html5-ad-validator/) tool.

## Related topics

- [Integrating the Xandr HTML5 Library with Ads Created in Adobe Edge](integrating-the-xandr-html5-library-with-ads-created-in-adobe-edge.md)
- [Integrating the AppNexus HTML5 Library with Manually Created HTML5 Ads](https://github.com/appnexus/appnexus-html5-lib/blob/master/docs/Walkthrough-For-Manually-Created-Ads.md)
- [Use IAB's HTML5 clickTag Standard on Xandr](use-iab-s-html5-clicktag-standard-on-xandr.md)
