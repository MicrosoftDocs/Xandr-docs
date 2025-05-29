---
title: Managing Targeting Templates
description: Learn how you can use the Targeting Templates screen to view the details of each template and choose one template to act as the default for all new campaigns. 
ms.date: 10/28/2023
---


# Managing targeting templates

Targeting templates allow users to apply pre-established inventory and user targeting settings to campaigns. These templates can be saved and applied when creating or editing a campaign; however, the **Targeting Templates** screen is the only place where you can view the details of each template and choose one template to act as the default for all new campaigns.

For details on applying a specific template to a new campaign, see [Apply a Targeting Template](apply-a-targeting-template.md).

## Accessing the targeting templates screen

Navigate to **Network** > **General** from the left vertical navigation menu and then select the **Targeting Templates** tab from the top navigation menu.

## Viewing template details

To see the details of a template, highlight the row in the **Targeting Templates** section at the top of the screen.

> [!NOTE]
> Do not click the check box to the left of the template name. This does not show the template details; instead, it selects the template for bulk editing.

You can only see the settings for one template at a time. The following information is displayed in the **Template Details** section (these topics may have multiple settings):

- **ID**
- **Name**
- **Inventory Type Targeting**
- **Inventory Targeting**
- **Geography Targeting**
- **Segment Targeting**
- **System Targeting**

<!--
- **ID**
- **Name**
- **Supply types**
- **Quality**
- **Categories**
- **Sources**
- **Domains**
- **User Frequency**
- **Geography**
- **Daypart**
- **Segment**
- **Demographics**
- **System (OS and Browsers)**
-->

## Specifying a default template

You can designate one template to act as the default template and apply to all new campaigns when they are created (you will retain the option to update these settings for each campaign separately before it is saved). When you highlight a template to see its information in the **Template Details**, one of two statements are visible above the settings:

1. **This is not your default template. To apply these settings to all new campaigns - make this template default.**
1. **This is your default template. To STOP applying these settings to all new campaigns - remove global default.**

If Statement 1 is visible, the selected template is not the default template. It can either be another template, or you may not have one defined. You can click on the green text (**make this template default**) to designate this template as the default.

If Statement 2 is visible, the selected template is your default template. The word **DEFAULT** appears in red to the right of the template ID. You can have only one default template at a time. You can click on the green text (**remove global default**) to remove the default setting from this template.

## Deleting one or more templates

Check the box to the left of each template that you want to delete, and then click **More Actions** \> **Delete**.

> [!IMPORTANT]
> When you delete a template, users can no longer select it when creating a campaign. Campaigns that currently exist with this template will not be affected.

## Related topics

- [Create a Campaign](create-a-campaign.md)
- [Buy-Side Targeting](buy-side-targeting.md)