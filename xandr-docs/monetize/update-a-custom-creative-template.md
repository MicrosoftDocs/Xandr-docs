---
title: Microsoft Monetize - Update a Custom Creative Template
description: In this article, find instructions for how to modify the code and macros in a custom creative template.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Update a custom creative template

Although you cannot modify the standard Microsoft Advertising creative templates, you can modify the rendering code and macros in your own custom templates.

> [!WARNING]
> Your changes immediately affect any creatives that are already using the template. If your changes cause these creatives to stop rendering properly, their audit status will be changed to "**rejected**" and they will stop serving on most third-party inventory.

1. Navigate to the **Creative Templates** screen by clicking **Network** > **Creative Templates**.

1. From the grid, click the custom template that needs to be updated.

    The **Creative Template Details** pane displays.

1. Click **Edit**.

1. Update any of the following fields:
    1. **Name**: The name of the creative template, which helps buyers identify the creative template when uploading creatives that match this template's media type and format.

        > [!TIP]
        > Be sure to use a name that buyers will easily recognize.

    1. **Media Type**: Defines the display style of the creatives that can use the template, such as banner.
    1. **Creative Format**: Defines the creative resource type that can use this template such as Flash, iframe, or External File.
    1. **Template Code**: Specifies how the creative should be rendered.

        > [!NOTE]
        > If you include custom macros in the template code, they must begin with the `#` symbol. If you include standard macros in the template code, they must begin with the `$` symbol. Be sure to replace any hard-coded `adnxs.com` references within the **Template Code** field with the `${XANDR_DOMAIN}` macro to ensure that the appropriate domain adnxs.com or adnxs-simple.com will be used when the auction takes place.

1. Expand the **Custom macros** section if necessary.

1. If no custom macros exist in the **Custom macros** section, or if you want to add more custom macros, click **Add Macros** and do the following:

    > [!NOTE]
    > You can add up to 20 custom macros. If the template is being used by any active creatives, you cannot add additional custom macros.

    1. Enter a name for this macro in the **Name** field that buyers will see when they upload creatives that use this template.

        The **Name** field is limited to a maximum of 50 characters.

    1. Select a macro type from the **Type** pull-down menu such as **String** and **True / False**.

        For example, if you select **True / False**, buyers will see the macro name followed by a checkbox.

    1. If you selected **Select from List**, enter a value for **Option 1**.

        To add more options, click **Add another option** and enter the corresponding value.

    1. If you want to require buyers to complete the macro when uploading new creatives that use this template, click the **Required** checkbox.

    1. If you do not want the macro to be required, enter the **Default Value** that will be used when buyers do not complete the macro during creative uploads.

1. Repeat **Step 6** to add each individual custom macro.

1. Update the details for any of the existing custom macros if necessary.

1. Click **Save**.

## Related topics

- [Creative Templates](creative-templates.md)
- [Managing Creative Templates](managing-creative-templates.md)
