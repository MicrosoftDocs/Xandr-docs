---
title: Bidders - Selecting the Correct Template for Your Creative
description: In this article, find information on how to determine which template to use for your creative.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Selecting the correct template for your creative

Please use the guide below in determining which template to use for your creative.

> [!TIP]
> A creative's `media_url` / `content` value is plugged into the creative template to form the code that is delivered to the user's browser. Therefore, it is essential to choose the appropriate template ID when submitting a creative. For more information about creatives, see [Creative Service](creative-service.md).
> [!NOTE]
> For more information about creative templates (and template IDs), see the [Creative Template Service](creative-template-service.md).

## ID: 1

This template is used if your creative is a single URL that **points to a piece of html code.**

You will need to pass the URL in the `media_url` field and set an `id` of 1 in the template object.

### Template

```
<iframe frameborder="0" width="${CREATIVE_WIDTH}" height="${CREATIVE_HEIGHT}" marginheight="0" marginwidth="0" target="_blank" scrolling="no" src="${MEDIA_URL}"></iframe>  
```

### Example

Creative:

```
{
    "creative": {
                "width": 320,
                "height": 50,
        "media_url": "https://test.com/piece_of_html",
        "template": {
            "id": 1
        }
    }
}
```

The following will be sent to the user's browser.

```
<iframe frameborder="0" width="320" height="50" marginheight="0" marginwidth="0" target="_blank" scrolling="no" src="https://test.com/piece_of_html"></iframe>
```

## ID: 2

This template is used if your creative is a single URL that **points to a piece of Javascript code.**

You will need to pass the URL in the `media_url` field and set an `id` of 2 in the template object.

### Template

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript" src="${MEDIA_URL}"></script></body></html>
```

### Example

Creative:

```
{
    "creative": {
                "width": 320,
                "height": 50,
        "media_url": "https://test.com/piece_of_js",
        "template": {
            "id": 2
        }
    }
}
```

The following will be sent to the user's browser.

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript" src="https://test.com/piece_of_js"></script></body></html>
```

## ID: 5

This template is used if your creative **starts and ends with Javascript components, even if the Javascript code writes HTML.**

You will need to pass the Javascript code in the content field and set an id of 5 in the template object.

### Template

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript">${CONTENT}</script></body></html> 
```

### Example

Creative:

```
{
    "creative": {
                "width": 320,
                "height": 50,
        "content": "var source = "https://test.com/test.img; var cw = 320; var ch = 50; ",
        "template": {
            "id": 5
        }
    }
}
```

The following will be sent to the user's browser.

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript">var source = "https://test.com/test.img"; var cw = 320; var ch = 50</script></body></html>
```

## ID: 6

The `"content"` and `"original_content"` fields are mandatory.

**Clicks:** The **track** and **landing page** should be in the `"content"` code.

### Template

```
 ${CONTENT}
```

### Example

```
{
    "creative": {
    "content": "document.write('<scr' + 'ipt type=\\'text/javascript\\' language=\\'javascript\\'>if (${IS_PREVIEW}){document.write(\\'<a href=\\\"https://www.attenir.co.jp/pub/dress_2/sp/dre05/index.md\\\" target=\\\"_blank\\\"><img src=\\\"https://ad.appier.net/77b44196-e6db-43b3-8676-f59f02cdad4f/vOJY8am_1477927440458_0.jpeg\\\"></a>\\');}else{document.write(\\'<a href=\\\"${Appier_macro1}${Appier_macro2}${Appier_macro3}${Appier_macro4}\\\"target = \\\"_blank\\\"><img src=\\\"${Appier_macro5}${Appier_macro6}${Appier_macro7}${Appier_macro8}\\\" > < /a>\\');} </scr' + 'ipt >');",
    "original_content": "<script type='text/javascript' language='javascript'>if (${IS_PREVIEW}){document.write('<a href=\"https://www.attenir.co.jp/pub/dress_2/sp/dre05/index.md\" target=\"_blank\"><img src=\"https://ad.appier.net/77b44196-e6db-43b3-8676-f59f02cdad4f/vOJY8am_1477927440458_0.jpeg\"></a>');}else{document.write('<a href=\"${Appier_macro1}${Appier_macro2}${Appier_macro3}${Appier_macro4}\"target = \"_blank\"><img src=\"${Appier_macro5}${Appier_macro6}${Appier_macro7}${Appier_macro8}\" > < /a>');} </script >",
        "template": {
            "id": 6
        }    
    }
} 
```

**Content field:** When using a "raw-html" format template (HTML that will not be served in an iFrame), everything in the content field must be escaped (quotes and slashes) and wrapped in a `document.write();` statement. This is necessary to deliver the content to the page.

## ID: 7

This template is used if your creative **starts and ends with HTML components, even if these HTML components are `<script>` tags.**

You will need to pass the html code in the `content` field and set an id of `7` in the template object.

### Template

```
${CONTENT}
```

### Example

Creative:

```
{
    "creative": {
                "width": 320,
                "height": 50,
        "content": "<script type="text/javascript">var hostname = "https://hostname.com";</script><noscript>var hostname = "https://hostname.com";</noscript>",
        "template": {
            "id": 7
        }
    }
}
```

The following will be sent to the user's browser.

```
<script type="text/javascript">var hostname = "https://hostname.com";</script><noscript>var hostname = "https://hostname.com";</noscript>
```

## Related topics

- [Creative Template Service](creative-template-service.md)
- [Creative Service](creative-service.md)
- [Creative Search Service](creative-search-service.md)
- [Creative Macro Check Service](creative-macro-check-service.md)
- [Creative Troubleshooting FAQ](creative-troubleshooting-faq.md)
