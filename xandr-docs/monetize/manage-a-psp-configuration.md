---
title: Manage a PSP Configuration
description: In this article, find instructions for how to edit, enable, disable, or delete a PSP configuration.
ms.date: 10/28/2023
---

# Manage a PSP configuration

Prebid Server Premium (PSP) configurations can be edited at any time. For more context on what configurations are for and the various settings and targeting options available, see [Create a New PSP Configuration](create-a-psp-configuration.md).

## Edit a PSP configuration

To edit a PSP configuration, follow these steps:

1. In the **Monetize** navigation bar, select the **Publishers** menu, and then click **Prebid Server Premium**.  
   The **Demand Partner Configurations** screen appears.

1. (Optional) Click the **All Statuses** menu to filter visible configurations by **Enabled** or **Disabled**.  
   This does not change the status of configurations; it only filters which ones are visible in the table.

1. Use the search box in the upper-right corner to filter configurations by:
   1. Configuration name
   1. Configuration ID
   1. Targeting ID

1. Click the name or row of the configuration to edit.  
   The side preview panel opens, showing targeting and demand partners applied to the configuration.

1. To view and edit all options available during configuration setup, click the **Edit** icon in the upper-right corner of the side panel.

   1. Alternatively, click the **Edit** (pencil) icon next to **Configuration Details** to quickly edit the name or **Enabled/Disabled** status.

   1. To quickly edit a demand partner’s parameters:
      1. Expand the partner in the side panel.
      1. Click the **Edit** (pencil) icon.

1. To add a new demand partner:
    1. Click **Add Demand Partner**.
    1. In the selection box, view the list of demand partners enabled in **PSP Global Settings**, or type to search by name.
    1. Select a demand partner. Required and optional parameters appear. Partner parameters are also available in the [Demand Partner Schema API Service](../digital-platform-api/demand-partner-schema-service.md) and on the [Prebid](https://docs.prebid.org/dev-docs/pbs-bidders.html) site.
    1. Referencing identifiers and values from the partner’s platform, fill out the required and optional parameters.

1. After editing the desired settings, click **Save**.

## Enable, disable, or delete configurations

Disabling a configuration stops bid requests for the applied inventory and demand partners. To resume bid requests, toggle the configuration back to **Enabled** and save.

1. In the **Monetize** navigation bar, select the **Publishers** menu, and then click **Prebid Server Premium**.  
   The **Demand Partner Configurations** screen appears.

1. (Optional) Click the **All Statuses** menu to filter visible configurations by **Enabled** or **Disabled**.  
   This does not change the status of configurations; it only filters which ones are visible in the table.

1. Use the search box in the upper-right corner to filter configurations by:
   1. Configuration name  
   1. Configuration ID  
   1. Targeting ID  

1. Select the corresponding checkboxes next to the configurations, and then choose the desired option from the **Actions** drop-down menu:
   1. **Enable**  
   1. **Disable**  
   1. **Delete**  

Alternatively, to delete an individual configuration from the configuration side preview panel, click Delete in the upper right corner.

## Pause or remove a demand partner  

To temporarily or permanently stop bid requests from being sent to a demand partner without removing them from individual configurations, disable the partner in [PSP Global Settings](add-or-edit-a-demand-partner.md).

To permanently remove the partner from all current configurations, delete the partner in [PSP Global Settings](add-or-edit-a-demand-partner.md). Please note that this action cannot be undone.

If a demand partner will not be used again on a specific configuration and needs to be removed, follow these steps:  

1. In the **Monetize** navigation bar, select the **Publishers** menu, and then click **Prebid Server Premium**.  
   The **Demand Partner Configurations** screen appears.  

1. (Optional) Click the **All Statuses** menu to filter visible configurations by **Enabled** or **Disabled**.  
   This does not change the status of configurations; it only filters which ones are visible in the table.  

1. Use the search box in the upper-right corner to filter configurations by:
    a. Configuration name  
    b. Configuration ID  
    c. Targeting ID  

1. Click on the name or row of the configuration to be edited.  
   The side preview panel appears, showing the targeting and demand partners applied to the configuration.  
1. Click **Edit** in the upper-right corner of the side panel.  
1. In the **Demand Partners** section, hover over the row of the partner to be removed.  
1. Click **Delete Demand Partner**.  
1. Click **Delete** to confirm.  
1. Click **Save** to save the configuration.  

## Related topics

- [Create a New PSP Configuration](create-a-psp-configuration.md)
- [Manage PSP Configurations in Bulk](manage-psp-configurations-in-bulk.md)
- [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md)
- [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Config Service](../digital-platform-api/config-service.md)
- PSP Campaign Objects Service ([temporary Sharepoint link](https://microsoftapc.sharepoint.com/:u:/r/teams/TechComm/SitePages/Prebid-Server-Premium-(PSP)---Flexible-Configurations---PSP-campaign-objects-service.aspx?csf=1&web=1&share=EYGZNmETFyZMvtU0ojz-_6gBQJRs4otnzWsolwOuCQ4GPg&e=ZGrmhU). Learn link TBD)
- [Common Issues and Best Practices](psp-common-issues-and-best-practices.md)