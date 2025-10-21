---
title: Microsoft Monetize - Universal Pixel Rule conditions
description: In this article, find a list of rule condition types and their descriptions for universal pixels.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Universal Pixel rule conditions

This document contains a list of rule condition types and their descriptions along with condition elements, comparisons, and keywords for universal pixels.

## Available conditions

| Condition Type | Condition Elements | Description | Comparisons | Keyword |
|---|---|---|---|---|
| View any page | View any page | Whenever the pixel is loaded this will be true. | n/a | n/a |
| URL | - View a domain <br> - View a path <br> - View a Qstring <br> - View a URL | The referrer URL on the call to universal pixel. | - contains <br> - doesn't contain <br> - equals <br> - doesn't equal | The string that will be matched on the selected URL component with the selected operator. |
| Standard Events | - Page View <br> - Landing page <br> - Item view <br> - Add to cart <br> - Initiate checkout <br> - Add payment info <br> - Purchase <br> - Lead | There can only be a single event per action on universal pixel. You will see no loads if you combine two event conditions with an AND operator. | n/a | n/a |
| Parameters | - Item ID <br> - Item name <br> - Item type |  | - contains <br> - doesn't contain <br> - equals <br> - doesn't equal | The string that will be matched on the selected parameter with the selected operator. |
| Parameters | Event Value |  | - greater than <br> - greater than or equals <br> - less than <br> - less than or equals <br> - equals <br> - doesn't equal | The value parameter will be compared to a single value entered in on the condition |

## Examples

| Include users who | Example URL |
|---|---|
| View a complete URL like "`www.xandr.com`" | `https://www.xandr.com` |
| View a URL with a domain of "`Microsoft Advertising`" | `https://www.xandr.com` and `https://www.xandr.com/careers` |
| View a URL with "`careers`" in the path | `https://www.xandr.com/careers` |
| View a URL with "`software`" in the query string | `https://www.xandr.com/careers?queryString=software` |

## Related topics

- [Set Up Audiences with Universal Pixel](set-up-audiences-with-universal-pixel.md)
- [Set Up Conversions with Universal Pixel](set-up-conversions-with-universal-pixel.md)
