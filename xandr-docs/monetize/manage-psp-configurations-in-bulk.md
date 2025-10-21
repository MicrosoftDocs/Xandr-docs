---
title: Manage PSP Configurations in Bulk
description: In this page, learn to create new PSP configurations in bulk and adding Demand Partners to existing configurations in bulk.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Manage PSP configurations in bulk

Bulk upload allows a user to manage multiple configurations via bulk template rather than creating configurations individually in the UI.

## Create new PSP configurations in bulk

Follow these steps to create new PSP configurations in bulk:

1. In the Monetize UI, go to the **Publishers** menu and click **Prebid Server Premium**. This loads the default **Demand Partner Configurations**.
1. In the left navigation pane, click **Bulk Upload New Configurations**.

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
1. The Configuration Targeting ID is the line item ID in the response from the PSP [campaign objects service](../digital-platform-api/campaign-object-service.md). The targeting of this PSP line item determines which bid requests trigger the PSP configuration and call the associated demand partners in this row. Each Targeting ID can be associated with one configuration.
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
1. The Configuration Targeting ID is the line item ID in the response from the PSP [campaign objects service](../digital-platform-api/campaign-object-service.md). The targeting of this PSP line item determines which bid requests trigger the PSP configuration and call the associated demand partners in this row. Each Targeting ID can be associated with only configuration.
1. The demand partner and its selected (required + any optional chosen) parameters are represented as an additional section of columns to the right.
1. Each demand partner and its parameter columns can only appear once per row. Additional values for the same demand partner must be applied on a separate row which represents a separate PSP configuration.

    > [!WARNING]
    > Do not edit any of the pre-populated cells except for the "data.demand_partner_config_params[X].enabled, which toggle the partner as active or inactive within that configuration (row).

1. Save changes to the template.

**Send template**

Submit the complete template to Microsoft Advertising for processing, unless instructed otherwise.

 > [!NOTE]
 > The bulk template does not yet support editing configuration-level details (such as media type) or demand partner details (such as which parameters to use or their values). These capabilities will be added in the future, along with self-service processing and template uploads.

## Related topics

- [Create a New PSP Configuration](create-a-psp-configuration.md)
- [Manage a PSP Configuration](manage-a-psp-configuration.md)
- [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Config Service](../digital-platform-api/config-service.md)