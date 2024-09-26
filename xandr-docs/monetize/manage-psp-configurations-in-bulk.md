---
title: Manage PSP Configurations in Bulk
description: In this page, learn to create new PSP configurations in bulk and adding Demand Partners to existing configurations in bulk.
ms.date: 10/28/2023
---

# Manage PSP configurations in bulk

Bulk upload allows a user to manage multiple configurations via bulk template rather than creating configurations individually in the UI.

## Create new PSP configurations in bulk

Follow these steps to create new PSP configurations in bulk:

1. In the Monetize UI, go to the **Publishers** menu and click **Prebid Server Premium**. This loads the default **Demand Partner Configurations**.
1. In the left navigation pane, click **Bulk Upload New Configurations**.

**Configuration filters**

These optional configuration settings may also be included:

| Options | Settings |
|--|--|
| **Operating System (OS)** | To set the operating system for the configuration, click in the **Search OS** text field and select an OS, or type in the field to see filtered options. This will ensure the PSP configuration is utilized (PSP demand partners are sent ad requests) only when Microsoft Advertising detects the corresponding OS from the user's device in the auction. For more information, see the [Operating System-Families API Service](../digital-platform-api/operating-system-families-service.md). |
| **Ad Size Selection** | To specify which ad sizes will be allowed for this configuration, click in the **Ad Size Selection** field and select some ad sizes, or type in the field to see filtered options. This will ensure the PSP configuration is utilized (PSP demand partners are sent ad requests) only when the auction includes one of the selected ad sizes. The **Ad Size Selection** menu includes all standard sizes as well as any custom sizes saved to the Monetize member seat.<br>Follow these steps to add new custom sizes:<br>- Select **Network** > **Tools** > **General** from the top menu. This will display the **Tools: General** page.<br> - Select **Custom Sizes** from the horizontal sub-menu.<br> - Click the **New custom size** button. This will display the **Custom Size Details** popover.<br> - Enter values for **Width** and **Height** text fields, and select the check box to mark this as a standard size.<br> - Click the **Save** button. |

If these optional settings are left blank, then any auction for the selected Placement/Placement Group/Publisher ID will trigger the corresponding PSP configuration to be used in the auction and enable PSP to call the associated Demand Partners.

**Add a demand partner**

1. Type to search or **select a demand partner** from the **Select a Demand Partner** dropdown.

    > [!NOTE]
    > Follow below tips if the desired Demand Partner is not included in the list:
    > - Ensure the proper media type(s) are selected.
    > - Ensure the **Demand Partner** is enabled in the Global Settings page as described in [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md).
    > - Check that the partner shows up as `Enabled` in that list.
    > A full list of Demand Partners is available [here](prebid-server-premium-demand-partner-integrations.md).

1. Once a **Demand Partner** is selected from the dropdown, new input fields will appear representing the parameters, both required and optional, that each demand partner's adapter accepts.
      1. Required parameters will automatically be checked and cannot be excluded from the spreadsheet.
      1. Required parameters that stipulate that "one of" a set of values is required will note "Select at least one of...".
      1. Check boxes will also be displayed by optional parameters. If the check box is checked, then the parameter will be included in the spreadsheet.
1. To add additional Demand Partners, click the **Add a Demand Partner** button.
1. Click **Download Bulk Spreadsheet**.
1. Enter the number of data rows. These represent the number of configurations to Monetize entities (placements, placement groups, publishers) that will be mapped to external demand partners.
1. Optionally, rename the file.
1. Click **Download**.

**Populate template**

1. Open the template and populate each row, representing one configuration, with the information requested for each column.
1. Configuration Mapping Object ID is the ID of the placement, placement group, or publisher to be mapped to the demand partner in each row. Each mapping object ID can only be associated with one PSP configuration.
1. Each demand partner and its selected (required + any optional chosen) parameters are represented as an additional section of columns to the right.
1. Each demand partner and its parameter columns can only appear once per row. Additional values for the same demand partner must be applied on a separate row which represents a separate PSP configuration.

    > [!WARNING]
    > Do not edit any of the pre-populated cells except for the "data.demand_partner_config_params\[X\].enabled", which toggles the partner as active or inactive within that configuration (row).

1. Save changes to the template.

**Send template**

Submit the complete template to Microsoft Advertising for processing, unless instructed otherwise.

## Add demand partners to existing configurations in bulk

Follow below steps to add demand partners to PSP configurations in bulk:

1. In the Monetize UI, go to the **Publishers** menu and click **Prebid Server Premium**. This loads the default **Demand Partner Configurations** screen.
1. Use the multi-select checkboxes to choose the configurations to which the demand partner will be added.

    > [!NOTE]
    > The partner must be new to all of the configurations selected. If the demand partner is already included in any of the configurations processing of the bulk template will fail.

1. Select the **Actions** menu \> **Bulk Add Demand Partner to Configurations**.

**Configuration filters**

These optional configuration settings may also be included:

| Options | Settings |
|--|--|
| **Operating System (OS)** | To set the operating system for the configuration, click in the **Search OS** text field and select an OS, or type in the field to see filtered options. This will ensure the PSP configuration is utilized (PSP demand partners are sent ad requests) only when Microsoft Advertising detects the corresponding OS from the user's device in the auction. For more information, see the [Operating System-Families API Service](../digital-platform-api/operating-system-families-service.md). |
| **Ad Size Selection** | To specify which ad sizes will be allowed for this configuration, click in the **Ad Size Selection** field and select some ad sizes, or type in the field to see filtered options. This will ensure the PSP configuration is utilized (PSP demand partners are sent ad requests) only when the auction includes one of the selected ad sizes. The **Ad Size Selection** menu includes all standard sizes and any custom sizes saved to the Monetize member seat.<br>Follow these steps to add new custom sizes:<br> - Select **Network** > **Tools** > **General** from the top menu. This will display the **Tools: General** page.<br> - Select **Custom Sizes** from the horizontal sub-menu.<br> - Click the **New custom size** button. This will display the **Custom Size Details** popover.<br> - Enter values for **Width** and **Height** text fields and click the check box to make this a standard size.<br> - Click the **Save** button. |

If these optional settings are left blank, then any auction for the selected Placement/Placement Group/Publisher ID will trigger the corresponding PSP configuration to be used in the auction and enable PSP to call the associated Demand Partners.

**Add a demand partner**

1. Type to search or select a demand partner from the **Select a Demand Partner** dropdown.

    > [!NOTE]
    > Follow below tips if the desired Demand Partner is not included in the list:
    > - Ensure the proper media type(s) are selected.
    > - Ensure the Demand Partner is enabled in the Global Settings page as described in [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md).
    > - Check that the partner shows up as `Enabled` in that list. A full list of Demand Partners is available  [here](prebid-server-premium-demand-partner-integrations.md).

1. Once a **Demand Partner** has been selected from the dropdown, new input fields will appear representing the parameters, both required and optional, that each demand partner's adapter accepts.
    1. Required parameters will automatically be checked and cannot be excluded from the spreadsheet.
    1. Required parameters that stipulate that "one of" a set of values is required will note "Select at least one of...".
    1. Check boxes will also be displayed by optional parameters. If the check box is checked, then the parameter will be included in the spreadsheet.
1. Click **Download Bulk Spreadsheet**.
1. Enter the number of data rows. These represent the number of configurations to Monetize entities (placements, placement groups, publishers) that will be mapped to external demand partners.
1. Optionally, rename the file.
1. Click **Download**.

**Populate template**

1. Open the template and populate each row, representing one configuration, with the information requested for each column.
1. Configuration Mapping Object ID is the ID of the placement, placement group, or publisher to be mapped to the demand partner in each row. Each mapping object ID can only be associated with one PSP configuration.
1. The demand partner and its selected (required + any optional chosen) parameters are represented as an additional section of columns to the right.
1. Each demand partner and its parameter columns can only appear once per row. Additional values for the same demand partner must be applied on a separate row which represents a separate PSP configuration.

    > [!WARNING]
    > Do not edit any of the pre-populated cells except for the "data.demand_partner_config_params[X].enabled, which toggle the partner as active or inactive within that configuration (row).

1. Save changes to the template.

**Send template**

Submit the complete template to Microsoft Advertising for processing, unless instructed otherwise.

 > [!NOTE]
 > The bulk template cannot yet be used to edit configuration-level details (i.e. media type, size(s), OS family(ies)) or demand partner details (which parameters to utilize or their values). Those capabilities will be added in the future, as well as self-service processing and upload of the templates.

## Related topics

- [Create a New PSP Configuration](create-a-psp-configuration.md)
- [Manage a PSP Configuration](manage-a-psp-configuration.md)
- [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Config Service](../digital-platform-api/config-service.md)