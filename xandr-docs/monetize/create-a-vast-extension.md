---
title: Create a VAST Extension
description: In this article, find step-by-step instructions on how to create and set up VAST extensions.
ms.date: 10/28/2023
---

# Create a VAST extension

To avoid having to create VAST extensions for each video creative, you can create one VAST extension that can be associated with multiple video creatives.

VAST extensions are custom XML snippets that video players render.

1. From the **Network** menu, select **VAST Extensions**.

    The **Template Manager: VAST Extensions** screen displays.

1. Click the **New Extension** or **Create New Extension** button.

1. Enter a new and unique **Name** for your custom extension.

1. Enter the XML for the extension in the **Content** text field using creative or custom macro elements.

    > [!NOTE]
    > Custom and impbus macros are supported. You must define all the custom macros that are listed in the **Content** text field.

1. Click the **Add macro** button and do the following:
    1. Enter the **Macro name** using the XML code provided in the **Content** text field.
    1. Enter the **Code** for the macro.
    1. Click the **Required** toggle if this macro is required.
    1. Select a macro **Type**.

1. Click **Save**.

    The extension now displays on the **Template Manager: VAST Extensions** screen. You can associate the extension with your video creatives using the **VAST Features** section of the **Create New** or **Edit** screens. For more information, see [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

## Related topics

- [Working with Creatives](working-with-creatives.md)
- [Video Creatives](video-creatives.md)
