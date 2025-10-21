---
title: Update Campaigns
description: Learn to update, activate/deactivate, duplicate and edit campaigns in this page.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Update campaigns

You can take several actions on campaigns to update them, including editing, delete, duplicating, and activating.

## Editing a campaign

You can edit a campaign directly from the **Campaigns** screen. Hover over the row for the campaign you want to edit and then click the pencil icon that appears in the row.

In addition, you can click the row of the campaign you want to edit to expose the **Campaign Summary** pane. From there, you can edit targeting and creatives, or click the pencil icon next to the campaign name to be taken to the full **Edit Campaign** screen.

## Editing lifetime and daily budgets

You can edit both lifetime and daily budgets for one or more campaigns directly from the **Campaigns** screen. Click the pencil and paper icon at the top of either the **Lifetime Budget** or **Daily Budget** column to expose the column editing options.

> [!NOTE]
> The bulk edit option is currently not available through Microsoft Internet Explorer. If you would like to access this feature, please use another browser.

This exposes the **Edit Daily Budget** or **Edit Lifetime Budget** column, where you can modify budgets and save your changes.

## Bulk editing flight dates

You can edit the flight dates of one or more campaigns directly from the **Campaigns** screen. Check the checkbox for each campaign whose flight dates you wish to edit then click **Actions** \> **Change Flight Dates**. You can edit both start and/or end dates for all the campaigns selected in the **Bulk Change Flight Dates** dialog that appears.

## Activating/Deactivating campaigns

You can activate or deactivate one or more campaigns directly from the **Campaigns** screen. Check the checkbox for each campaign that you want to activate or deactivate and click **Actions** \> **Activate** or **Actions** \> **Deactivate**.

A confirmation dialog lists the campaign(s) to be activated or deactivated. Click **OK** to complete the action.

When you deactivate a campaign, the campaign will typically stop serving within 10 - 15 seconds, with a maximum wait time of approximately 60 seconds.

## Duplicating campaigns

You can duplicate campaigns directly from the [Explore Campaigns](explore-campaigns.md). Each new campaign will be assigned a unique ID, will not inherit the original campaign's External Code, and will default to the Inactive state, but will otherwise have the exact same settings as the original, including budgets, flight dates, buying strategies, and targeting.

> [!IMPORTANT]
> When you duplicate a campaign that uses a buying strategy involving optimization, the optimization data (impressions, clicks, conversion, etc.) of the original campaign is not available to the new campaign. This means that the new campaign must go through its own "learning" process. For more details, see [Targeted Learn](targeted-learn.md).

1. On the **Campaigns** screen, check the box next to each campaign that you want to duplicate.
1. Click **Actions** \> **Duplicate**.
1. In the confirmation dialog, decide whether you want to create each new campaign under the original's parent line item or select a different line item under which all copies should be created.

    > [!IMPORTANT]
    > CPA campaigns use conversion pixels associated with their parent line item. Therefore, such campaigns can be copied to a different line item only if the relevant conversion pixels are also associated with that line item.

1. By default, the new campaigns have the same names as the original campaigns but with "Copy" as a prefix. If necessary, update the names for the new campaigns.
1. Review your choices and then click **Duplicate** to confirm the duplication. The new campaigns will then appear on the [Explore Campaigns](explore-campaigns.md).

## Deleting campaigns

You can delete campaigns directly from the **Campaigns** screen. This is particularly useful when you are approaching your object limit for campaigns, or when you want to get rid of unnecessary or accidentally created campaigns for a particular advertiser. For more information about object limits, see [Viewing Your Object Limits](viewing-your-object-limits.md).

> [!WARNING]
> Deleting campaigns is permanent and cannot be reverted. Also, although deleted campaigns continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., budget and targeting).

1. On the **Campaigns** screen, check the box next to each campaign that you want to delete.
1. Click **Actions** \> **Delete**.
1. A confirmation dialog lists the campaigns that you selected for deletion. Review the list carefully and then click **Confirm** to permanently delete the campaigns from the system.

## Edit multiple campaigns with power uploader

> [!IMPORTANT]
> This offering is currently in Open Beta. It is available to all clients, but subject to change or downtime without notice.

Power Uploader enables you to edit multiple campaigns in one easy process by updating and uploading an Excel spreadsheet, instead of [creating a new campaign](create-a-campaign.md) or using the [Campaign Service](../digital-platform-api/campaign-service.md).

## Spreadsheet fields

The Beta version of Power Uploader currently supports updates to the following fields:

| Spreadsheet Field | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Basics |  |  |  |
| ID | **ID** | Required. The ID of the campaign. | Campaign / `id` |
| Name | **Name** | Required. The name of the campaign. | Campaign / `name` |
| Status | **Status** | Required. The state of the campaign. Valid values: Active or Inactive | Campaign / `state` |

| Spreadsheet Field for Budget | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Enable Daily Pacing | **Budget > Media Cost / Impression > Impression** | If TRUE, the campaign's daily budgeted spend is spread out evenly throughout each day. You must also provide either a Daily Monetary Budget or Daily Impression budget. Daily Budget Pacing OR Lifetime Budget Pacing may be enabled, but not both.<br>For more details about even daily pacing, see [Daily Pacing](daily-pacing.md). | Campaign / `enable_pacing` |
| Daily Monetary Budget | **Budget > Media Cost > Daily** | The daily budget in media cost. The currency symbol can be omitted and the default currency will be used. Enter unlimited to represent unlimited budget. | Campaign / `daily_budget` |
| Daily Impression Budget | **Budget > Impression > Daily** | The daily budget in impressions. Enter unlimited to represent unlimited budget. | Campaign / `daily_budget_imps` |
| Enable Lifetime Pacing | **Budget>Media Cost/ Impression>Lifetime** | If TRUE, the campaign's overall lifetime budget is spread out evenly over the campaign billing period. Daily Budget Pacing OR Lifetime Budget Pacing may be enabled, but not both.<br>For more details about lifetime pacing, see [Lifetime Pacing](lifetime-pacing.md). | Campaign / `lifetime_pacing` |
| Lifetime Monetary Budget | **Budget > Media Cost > Lifetime** | The lifetime budget in dollars (media cost). The currency symbol can be omitted and the default currency will be used. Enter unlimited to represent unlimited budget.<br>**Warning**: If Campaign, Line Item, and Insertion Order Lifetime Budgets are all set to unlimited, severe overspend can occur. | Campaign / `lifetime_budget` |
| Lifetime Impression Budget | **Budget > Impression > Lifetime** | The lifetime budget in impressions. Enter unlimited to represent unlimited budget. | Campaign / `lifetime_budget_imps` |

| Buying Strategies | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Buy Direct Inventory | **Buying Strategies > Direct Inventory** | The type of inventory targeted by this campaign. If TRUE, you will target inventory managed by your network. | Campaign / `inventory_type` |
| Campaign Priority | **Buying Strategies > Buy Direct Inventory > Campaign Priority** | For a campaign targeting direct inventory, there is no need to input a buying strategy since you have already paid for inventory. However, you can set the campaign's priority to weight the campaign against other direct campaigns within your account. The campaign with the highest priority will always win, even if a lower priority campaign bids more. For more information about managing priority, see [Bidding Priority](bidding-priority.md). | Campaign / `priority` |
| Buy Third Party Inventory | **Buying Strategies > Buy Third-Party Inventory** | The type of inventory targeted by this campaign. If TRUE, you will target all third-party inventory not managed by your network that has been enabled for reselling (including external supply partners such as Microsoft Advertising Exchange and Google Ad Manager).<br>**Warning**: Entering TRUE and a base CPM bid may overwrite existing third-party buying strategies without notice. | Campaign / `inventory_type` |
| CPM Bid | **Buying Strategies > Buy Third-Party Inventory > Pay on a Per-Impression (CPM) basis > Bid a Media Cost CPM** | Use this strategy to bid a fixed dollar amount per thousand impressions. | Campaign / `cpm_bid_type` |

| Spreadsheet Field for Targeting | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Target Desktops & Laptops | **Device and Supply Type** | By default, your campaign will target all physical device types ( Desktops & Laptops , Tablets , and Phones ). To restrict the device types you are targeting, enter FALSE. | Profile / `device_type_targets` |
| Target Tablets | **Device and Supply Type** | By default, your campaign will target all physical device types (Desktops & Laptops, Tablets, and Phones). To restrict the device types you are targeting, enter FALSE. | Profile / `device_type_targets` |
| Target Phones | **Device and Supply Type** | By default, your campaign will target all physical device types (Desktops & Laptops, Tablets, and Phones). To restrict the device types you are targeting, enter FALSE. | Profile / `device_type_targets` |
| Target Deal IDs | **Deals > Deals** | The deal IDs to be targeted by this campaign. A deal is an agreement between a seller and buyer that may provide the buyer preferential pricing, access to exclusive inventory, reduced competition on inventory, or other opportunities.<br>This is a comma separated list with quotations around each deal ID. For example: "ABC123", "DEF456", "GHI789" | Profile / `deal_targets` |

| Spreadsheet Field | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Include or Exclude Direct Publishers | **Inventory > Direct Inventory > Publishers** | Valid value is Include or Exclude. You can only use one value or the other. | Profile / `inventory_action` |
| Direct Publisher IDs | **Inventory > Direct Inventory > Publishers** | Managed/direct publisher IDs to be either excluded or included in targeting.<br>This is a comma separated list. For example: 123, 456, 789 | Profile / `publisher_targets` |
| Include or Exclude Direct Placement Groups | **Inventory > Direct Inventory > Placement Groups** | Valid value is Include or Exclude. You can only use one value or the other. | Profile / `inventory_action` |
| Direct Placement Group IDs | **Inventory > Direct Inventory > Placement Groups** | The sites IDs to be either excluded or included in targeting.<br>This is a comma separated list. For example: 123, 456, 789 | Profile / `site_targets` |
| Include or Exclude Direct Placements | **Inventory > Direct Inventory > Placements** | Valid value is Include or Exclude. You can only use one value or the other. | Profile / `inventory_action` |
| Direct Placement IDs | **Inventory > Direct Inventory > Placements** | The placement IDs to be either excluded or included in targeting.<br>This is a comma separated list. For example: 123, 456, 789 | Profile / `placement_targets` |
| Include or Exclude Third-Party Sellers | I**nventory > 3rd Party Inventory > Sellers** | Valid value is Include or Exclude. You can only use one value or the other. | Profile / `member_default_action` |
| Third-Party Seller IDs | **Inventory > 3rd Party Inventory > Sellers** | Seller member IDs to be either excluded or included in targeting.<br>This is a comma separated list. For example: 123, 456, 789 | Profile / `member_targets` |
| Include or Exclude Third-Party Publishers | **Inventory > 3rd Party Inventory > Publishers & Categories** | Valid value is Include or Exclude. You can only use one value or the other. | Profile / `platform_publisher_targets`<br>Profile / `platform_content_category_targets` |
| Third-Party Publisher IDs | **Inventory > 3rd Party Inventory > Publishers & Categories** | The third-party publisher and content category IDs to be either excluded or included in targeting.<br>This is a comma separated list. For example: 123, 456, 789 | Profile / `platform_publisher_targets`<br>Profile / `platform_content_category_targets` |

| Spreadsheet Field | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Include or Exclude Third-Party Placements |  |  |  |
| Third-Party Placement IDs |  |  |  |
| # of Imps over lifetime | **Frequency** | The maximum number of impressions per user. | Profile / `max_lifetime_imps` |
| # of Imps per user per day | **Frequency** | The maximum number of impressions per user per day. | Profile / `max_day_imps` |

| Spreadsheet Field for Creatives | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Associated Creatives IDs | **Associated Creatives** | The list of creative IDs or codes associated to the campaign.<br>This is a comma separated list. For example: 123, 456, 789 | Campaign / `creatives` |
| Landing Page URL | **Landing Page URL** | The optional landing page URL for non-3rd party image and flash creatives. | Campaign / `click_url` |

| Spreadsheet Field | Campaign Screen Field | Description | API Service / Field |
|--|--|--|--|
| Comments | **Comments** | Comments about the campaign. | Campaign / `comments` |

## Export a spreadsheet

While this step is not required, it is recommended that you export the Excel spreadsheet from Monetize to use as a template and prevent errors.

1. On the **Campaigns** screen, select the campaigns to edit.
1. Select Edit in **Excel** \> **Export selected to Excel** or **Export all to Excel**.
1. In the **Download Spreadsheet** window, select the columns you want to show and/or edit in the spreadsheet.

    > [!NOTE]
    > ID, Name, and Status will download by default.

1. Click **Download**. The campaigns are downloaded into an editable Excel spreadsheet. The default spreadsheet name is `campaigns.xlsx`.

## Edit the spreadsheet

> [!TIP]
> While you can use your own spreadsheet containing matching column names, a spreadsheet downloaded from Monetize will include the correct column names. It is suggested to start with this downloaded spreadsheet to avoid errors.

Name and Status are required for each campaign. When you're editing existing campaigns, treat ID as read-only so that you don't accidentally update the wrong campaign.

To create new campaigns, leave the ID field blank.

## Import a spreadsheet

1. When you have edited and saved the spreadsheet, select **Edit in Excel** \> **Import from Excel**.
1. In the **Upload Spreadsheet** window, click **Browse**....
1. Select your edited spreadsheet. If the upload is successful, a confirmation message will display. If the spreadsheet is improperly formatted, an error message will display. Click **Select another file** to select a different spreadsheet.
1. Click **Next**. The **Upload Spreadsheet** window will display the changes for you to review before applying them.
1. Click **Apply Settings**. The changes will be applied.
1. If the changes are applied successfully, a confirmation message will display. Proceed to step 9.
1. If the changes are unsuccessful, an error message will list all the campaigns that could not be updated. Click on a red X for more details about the error for that campaign, or click **Download Errors** to download a spreadsheet containing all the rows that failed to update.
1. Correct the errors on the spreadsheet and return to step 1.
1. If there are no errors or you want to bypass editing errors, click **Go to Campaigns** to navigate back to the **Campaigns** screen.

## Related topics

- [Working with Campaigns](working-with-campaigns.md)
- [Create a Campaign](create-a-campaign.md)
- [Explore Campaigns](explore-campaigns.md)