---
title: Microsoft Monetize - Create a Custom Creative Template
description: Explore creating a new custom creative template anytime by crafting from scratch or duplicating existing ones for modification.
ms.date: 10/28/2023
---

# Microsoft Monetize - Create a custom creative template

You can create a new custom creative template from scratch at any time.

You can also duplicate an existing template and then modify it. For more information, see [Duplicate an Existing Custom Creative Template](duplicate-an-existing-custom-creative-template.md).

1. Navigate to the **Creative Templates** screen by clicking **Network** > **Creative Templates**.
1. Click **New**.
1. Provide the following information:

   1. **Name**: The name of the creative template, which helps buyers identify the creative template when uploading creatives that match this template's media type and format.

       > [!TIP]
       > Be sure to use a name that buyers will easily recognize.

   1. **Media Type**: Defines the display style of the creatives that can use the template, such as banner.
   1. **Creative Format**: Defines the creative resource type that can use this template such as Flash, iframe, or External File.
   1. **Template Code**: Specifies how the creative should be rendered.

      > [!NOTE]
      > If you include custom macros in the template code, they must begin with the `#` symbol. If you include standard macros in the template code, they must begin with the `$` symbol. Be sure to replace any hard-coded `adnxs.com` references within the Template Code field with the `${XANDR_DOMAIN}` macro to ensure that the appropriate domain `adnxs.com` on or `adnxs-simple.com` will be used when the auction takes place.

1. To add custom macros, expand the **Custom macros** section if necessary, click **Add Macros**, and do the following.

    > [!NOTE]
    >
    > You can add up to 20 custom macros. If the template is being used by any
    > active creatives, you cannot add additional custom macros.

   1. Enter a name for this macro in the **Name** field that buyers will see when they upload creatives that use this template.
   1. The **Name** field is limited to a maximum of 50 characters.=
   1. Select a macro type from the **Type** pull-down menu such as **String** and **True / False**.
   1. For example, if you select **True / False**, buyers will see the macro name followed by a checkbox.
   1. If you selected **Select from List**, enter a value for **Option 1**.
   1. To add more options, click **Add another option** and enter the corresponding value.
   1. If you want to require buyers to complete the macro when uploading new creatives that use this template, click the **Required** checkbox.
   1. If you do not want the macro to be required, enter the **Default Value** that will be used when buyers do not complete the macro during creative uploads.

1. Repeat step 4 to add each individual custom macro.
1. Click **Save**.

   The new creative template is active by default and can be applied to new creatives.

## Related topics

- [Creative Templates](creative-templates.md)
- [Managing Creative Templates](managing-creative-templates.md)
