---
title: Microsoft Monetize - Pass Custom Macros to a Split
description: In this article, find instructions on how to add custom macros to a split.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Pass custom macros to a split

The split custom macro is used to pass any value to a creative landing page URL where the split will serve.

> [!IMPORTANT]
> Split custom macros are not supported by Guaranteed Delivery ALIs.

For example, suppose you set a custom macro for a split by defining the key as "color" and the value as "red". If you have a macro called `${color}` within the creative's landing page URL, Microsoft Advertising will replace it with a "red" value. Before you begin passing custom macros, you need to first add custom macro keys to your creatives' landing page URLs when editing a creative or line item.

1. Select the **Use Custom Macros** checkbox.
1. Click the pencil icon in the **Creatives** > **Custom Macro** column for the corresponding split.
1. In the **Edit Split** pane, click the **Setup** tab.
1. Under **Pass Custom Macros**, enter the macro name as the key and enter the value that you want to serve on this split.
1. Click **Add Another** to add another custom macro or click **Apply** to save your changes.
