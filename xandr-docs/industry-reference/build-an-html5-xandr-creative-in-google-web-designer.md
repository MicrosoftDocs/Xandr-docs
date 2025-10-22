---
title: Build an HTML5 Xandr Creative in Google Web Designer  
description: In this article, learn step-by-step instructions about how to build an HTML5 Xandr creative in Google Web Designer.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Build an HTML5 Xandr creative in Google Web Designer

This page explains how to use Google Web Designer to build HTML5 creatives that will properly track clicks in Xandr.

1. Open Google Web Designer.
1. Click **CREATE NEW FILE**. The *Create New Blank File* pop-up displays.
1. Click **HTML** from the **Others** menu.
1. Enter a **Name** and **Title** for the creative.
1. Select a **Location** and **Animation Mode**.
1. Click **OK**. The *Create New Blank File* pop-up closes.
1. Click the **+** button in the lower left of Google Web Designer under the **Events** tab to add a new event.

   :::image type="content" source="media/google-web-designer.png" alt-text="Screenshot of the Events tab.":::

    A pop-up displays.
1. Select a target.  

    :::image type="content" source="media/target.png" alt-text="Screenshot that shows Target been selected.":::

    This will be the element of the ad that will be clickable.
1. Select an event.
1. Select one of the available options that display for the event.  

    :::image type="content" source="media/event.png" alt-text="Screenshot of the available event options.":::

1. Select **Custom** under the **action** menu.
1. Select **Add custom action**.  

   :::image type="content" source="media/custom-action.png" alt-text="Screenshot of the Add custom action option.":::

1. Type a unique name in the text field that displays next to "*gwd*." (e.g., *XandrClick*).
1. Paste the code below into the text box provided (this is your `clickTag` code).

    ```
    function getParameterByName(name) {
      var match = RegExp('[?&]' + name + '=([^&]*)').exec(window.location.search);
      return match && decodeURIComponent(match[1].replace(/\+/g, ' '));
    }
    window.open(getParameterByName('clickTag'), '_blank');
    ```

    :::image type="content" source="media/click-tag.png" alt-text="Screenshot of the custom code.":::

    > [!NOTE]
    > Since Google Web Designer has a [known issue](https://stackoverflow.com/questions/30221826/how-do-you-copy-paste-html-code-in-google-web-designer) related to key commands, you must paste the code using your computer's menu bar paste option.

1. Click **OK**.
1. Test the creative by performing the following if necessary:
    1. Click **Preview** in the upper-right of Google Web Designer to open the creative in your browser.

       :::image type="content" source="media/preview.png" alt-text="Screenshot of the preview screen.":::

    1. Add "`?clickTag=https://yoururlhere.com`" in the address bar at the end of the landing page URL that you want to test.
    1. Refresh the page and click on the creative.

        A new window with the landing page that you entered should open in your browser. When the creative is served, Xandr sets a value of `clickTag` to Xandr' click tracker along with a redirect to the landing page URL provided in Microsoft Monetize.
