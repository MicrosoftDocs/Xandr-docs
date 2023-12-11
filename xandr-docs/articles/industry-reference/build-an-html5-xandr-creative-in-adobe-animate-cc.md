---
title: Industry Reference - Build an HTML5 Xandr Creative in Adobe Animate CC
description: In this article, learn step-by-step instructions about how to build an HTML5 Xandr creative in Adobe Animate CC.
ms.date: 10/28/2023
ms.custom: industry-reference
---

# Industry Reference - Build an HTML5 Xandr creative in Adobe Animate CC

This guide explains how to use Adobe Animate CC to build HTML5 creatives that will properly track clicks in Xandr. It assumes that you are familiar using Adobe Animate CC to build creatives.

## With Xandr HTML5 library

1. From within Adobe Animate CC, select the element you want to make clickable.

1. Open the **Actions** window.

    :::image type="content" source="media/actions-window.png" alt-text="Screenshot of the Actions window.":::

1. Select **Code Snippets** in Actions toolbar.  

   :::image type="content" source="media/code-snippet-in-actions.png" alt-text="Screenshot of Code Snippets in Actions toolbar.":::

1. Click **HTML Canvas**, then **Event Handlers**, and then select **Mouse Click** and click **OK** if you receive a warning.  

    :::image type="content" source="media/click-html-canvas.png" alt-text="Screenshot of the HTML Canvas screen.":::

1. You will see a text editor pre-populated with code. Replace the “`alert("Mouse clicked");`” with:

    ``` 
    function getParameterByName(name) {
      var match = RegExp('[?&]' + name + '=([^&]*)').exec(window.location.search);
      return match && decodeURIComponent(match[1].replace(/\+/g, ' '));
    }
    window.open(getParameterByName('clickTag'), '_blank');
    ```

    :::image type="content" source="media/mouse-clicked.png" alt-text="Screenshot of text editor pre-populated with code.":::

1. Save and **Publish** your work. Open the project's `.html` file in your web browser. Add `?clickTag=http://www.appnexus.com` at the end of the URL in the address bar.

    :::image type="content" source="media/save-and-published.png" alt-text="Screenshot of the address bar.":::

    Refresh the page and click on the ad. A new window with Xandr's website should open in your browser. When the ad is served Xandr sets the value of clickTag to Xandr's click tracker and a redirect to the landing page URL provided for the creative in Console.

## Related topic

[Use IAB's HTML5 clickTag Standard on Xandr](use-iab-s-html5-clicktag-standard-on-xandr.md)
