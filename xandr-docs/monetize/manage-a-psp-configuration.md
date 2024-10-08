---
title: Manage a PSP Configuration
description: In this article, find instructions for how to edit, enable, disable, or delete a PSP configuration.
ms.date: 10/28/2023
---

# Manage a PSP configuration

## Edit a PSP configuration

To edit a PSP configuration, follow the steps below:

1. Within the **Publishers** menu, select **Prebid Server Premium**, which loads the default **Demand Partner Configurations** tab.
1. In the search box in the upper right corner, configurations can be filtered by configuration name, targeting (placement, placement group, or publisher) ID, or configuration ID.
1. Click the **All Statuses** menu to filter visible configurations by status to limit them to either **Enabled** or **Disabled**.

    > [!NOTE]
    > This does not change the status of configurations, only which ones are visible.

1. Click on the name or row of the configuration to be edited.
1. Click the **Edit** button in the upper right of the configuration panel.
1. Optionally, edit the name, status (**Enabled**/**Disabled**), or demand partners associated with the configuration.

    > [!NOTE]
    > Partners can be removed from configurations entirely by clicking the X icon to the right of their name.

1. To add a new demand partner, click **Add Another Demand Partner**. If the partner does not appear in this list, you must first [Enable them within Global Settings](add-or-edit-a-demand-partner.md).
1. Click **Save**.

## Enable, disable, or delete configurations

To enable, disable, or delete a configuration, select the corresponding checkboxes next to the configurations, then select the desired option from the **Actions** drop-down menu.

## Related topics

- [Create a New PSP Configuration](create-a-psp-configuration.md)
- [Manage PSP Configurations in Bulk](manage-psp-configurations-in-bulk.md)
- [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Config Service](../digital-platform-api/config-service.md)
