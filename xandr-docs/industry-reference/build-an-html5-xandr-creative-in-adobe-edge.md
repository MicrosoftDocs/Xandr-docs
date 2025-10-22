---
title: Build an HTML5 Xandr Creative in Adobe Edge
description: In this article, learn step-by-step instructions about how to build an HTML5 Xandr creative in Adobe Edge.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Build an HTML5 Xandr creative in Adobe Edge

This guide explains how to use Adobe Edge to build HTML5 creatives that will properly track clicks in Xandr. It assumes that you are familiar using Adobe Edge to build creatives.

## With Xandr HTML5 library

1. From within Adobe Edge, select the element you want to make clickable from the **Elements** panel. (Naming the element "clickable" is not required.)

    :::image type="content" source="media/clickable-element.png" alt-text="Screenshot of the Elements panel.":::

1. Open **Actions** for the selected element. The Actions panel will pop-up with a dropdown menu. Then select **click** in the dropdown menu.

   :::image type="content" source="media/click-menu.png" alt-text="Screenshot of the Actions panel.":::

1. Select **Links** and **Link in New Window** from the **Pick an Action** area.

    :::image type="content" source="media/pick-an-action.png" alt-text="Screenshot of the Pick an Action screen.":::

1. You will see code that looks like this.

   :::image type="content" source="media/function.png" alt-text="Screenshot of the code screen that show function's properties.":::

1. Replace the “[https://www.adobe.com](https://www.adobe.com)” with **`APPNEXUS.getClickTag()`**. Make sure to remove the quotations.

    :::image type="content" source="media/function-properties.png" alt-text="Screenshot that shows the function properties screen with the target attribute replaced.":::

1. From the **Library** panel, in the **Scripts** drop-down, click **Add JS File from URL..**. Paste [https://acdn.adnxs.com/html5-lib/1.3.0/appnexus-html5-lib.min.js](https://acdn.adnxs.com/html5-lib/1.3.0/appnexus-html5-lib.min.js) into the field and click **OK**.

    :::image type="content" source="media/library-panel.png" alt-text="Screenshot of the Library panel.":::

    > [!TIP]
    > Use https to ensure the creative can serve on secure inventory.

1. Click **Preview in Browser** to open the ad in your browser. Add `?clickTag=http://YOUR-URL-HERE.com` at the end of the URL in the address bar with the landing page you want to test. Refresh the page and click on the ad. A new window with the landing page you entered should open in your browser. When the creative is served, Xandr sets the value of `clickTag` to Xandr's click tracker and sets a redirect to the landing page URL provided in Microsoft Monetize.

## Without Xandr HTML5 library

1. From within Adobe Edge, select the element you want to make clickable from the **Elements** panel. (Naming the element "clickable" is not required).

    :::image type="content" source="media/clickable-element.png" alt-text="Screenshot that shows the Elements panel.":::

1. Open **Actions** for the selected element. The **Actions** panel will pop-up with a dropdown menu. Then select **click** in the dropdown menu.

    :::image type="content" source="media/click-menu.png" alt-text="Screenshot of the Actions panel with Click option selected.":::

1. Paste the code below into the text box provided (this is your `clickTag` code).

    ```
    function getParameterByName(name) {
      var match = RegExp('[?&]' + name + '=([^&]*)').exec(window.location.search);
      return match && decodeURIComponent(match[1].replace(/\+/g, ' '));
    }
    window.open(getParameterByName('clickTag'), '_blank');
    ```

    :::image type="content" source="media/click-tag-code.png" alt-text="Screenshot of the Click Tag Code.":::

1. Click **Preview in Browser** to open the ad in your browser. Add `?clickTag=http://YOUR-URL-HERE.com` at the end of the URL in the address bar with the landing page you want to test. Refresh the page and click on the creative. A new window with the landing page you entered should open in your browser. When the creative is served, Xandr sets the value of `clickTag` to Xandr's click tracker and sets a redirect to the landing page URL provided in Microsoft Monetize.

## Related topic

[Build an HTML5 Xandr Creative in Google Web Designer](build-an-html5-xandr-creative-in-google-web-designer.md)
