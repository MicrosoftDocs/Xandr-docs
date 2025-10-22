---
title: Digital Platform API - Selecting the Correct Template for Your Creative
description: This article guides you to select the correct template for your creative.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Selecting the correct template for your creative

Use the guide below in determining which template to use for your creatives.

> [!TIP]
> A creative's `media_url` / `content`value is plugged into the the creative template to form the code that is delivered to the user's browser. Therefore, it is essential to choose the appropriate template ID when submitting a creative. For more information about creatives, see the [Creative Service](./creative-service.md).
> [!NOTE]
> Get more information about template IDs.
>
> For more information about creative templates (and template IDs), see the [Creative Template Service](./creative-template-service.md).

## ID: 1

This template is used if your creative is a single URL that points to a piece of html code.

You will need to pass the URL in the `media_url` field and set an `id` of `1` in the template object.

### Template

```
    <iframe frameborder="0" width="${CREATIVE_WIDTH}" height="${CREATIVE_HEIGHT}" marginheight="0" marginwidth="0" target="_blank" scrolling="no" src="${MEDIA_URL}"></iframe>  
            
```

#### ID: 1 Example

**Creative**

```
{
    "creative": {
        "width": 320,
        "height": 50,
        "media_url": "http://test.com/piece_of_html",
        "template": {
            "id": 1
        }
    }
}
```

The following will be sent to the user's browser.

```
<iframe frameborder="0" width="320" height="50" marginheight="0" marginwidth="0" target="_blank" scrolling="no" src="http://test.com/piece_of_html"></iframe>
```

## ID: 2

This template is used if your creative is a single URL that points to a piece of Javascript code.

You will need to pass the URL in the `media_url` field and set an `id` of `2` in the template object.

### Template

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript" src="${MEDIA_URL}"></script></body></html>
      
```

#### ID: 2 Example

**Creative**

```
{
    "creative": {
        "width": 320,
        "height": 50,
        "media_url": "http://test.com/piece_of_js",
        "template": {
            "id": 2
        }
    }
}
```

The following will be sent to the user's browser.

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript" src="http://test.com/piece_of_js"></script></body></html>
```

## ID: 5

This template is used if your creative starts and ends with Javascript components, even if the Javascript code writes HTML.

You will need to pass the Javascript code in the `content` field and set an `id` of `5` in the template object.

### Template

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript">${CONTENT}</script></body></html>
      
```

#### ID: 5 Example

**Creative**

```
{
    "creative": {
        "width": 320,
        "height": 50,
        "content": "var source = "http://test.com/test.img; var cw = 320; var ch = 50; ",
        "template": {
            "id": 5
        }
    }
}
```

The following will be sent to the user's browser.

```
<html><body style="margin-left: 0%; margin-right: 0%; margin-top: 0%; margin-bottom: 0%"><script type="text/javascript">var source = "http://test.com/test.img"; var cw = 320; var ch = 50</script></body></html>
```

## ID: 6

This template is used if your creative starts and ends with HTML components, even if these HTML components are `<script>` tags.

You will need to pass the html code in the `content` field and set an `id` of `6` in the template object.

### Template

```
      ${CONTENT}
      
```

#### ID: 6 Example

**Creative**

```
 {
    "creative": {
        "width": 320,
        "height": 50,
        "content": "<script type="text/javascript">var hostname = "http://hostname.com";</script><noscript>var hostname = "http://hostname.com";</noscript>",
        "template": {
            "id": 7
        }
    }
}
 
```

The following will be sent to the user's browser.

```
<script type="text/javascript">var hostname = "http://hostname.com";</script><noscript>var hostname = "http://hostname.com";</noscript>
```

## Related topics

- [Creative Template Service](./creative-template-service.md)
- [Creative Service](./creative-service.md)
- [Creative Search Service](./creative-search-service.md)
- [Creative Macro Check Service](./creative-macro-check-service.md)
- [Creative Troubleshooting FAQ](../bidders/creative-troubleshooting-faq.md)
