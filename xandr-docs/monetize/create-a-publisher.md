---
title: Create a Publisher
description: In this article, find step-by-step instructions on how to create and set up a publisher.
ms.date: 10/28/2023
---

# Create a publisher

When you create a publisher, you can enter key publisher information, define your financial and business relationship with that publisher, specify how you would like to sell the publisher's inventory to your Microsoft Advertising partners, and set the appropriate types of payments, payment terms, and ad quality settings.

## Get started

To add a new publisher user, go to **Publishers** > **All Publishers** and click on **+New** button it opens the **Create New Publisher** dialog.

## Step 1. Define publisher details

In the **Publisher Details** section, enter the following basic information about the publisher:

- **Name**: Enter the publisher name.
- **Status**: Select from **Active** or **Inactive**. The best practice is to set the state to **Inactive** on initial setup. Set the status to **Active** when the publisher is ready.
- **Currency**: Select the currency for the publisher.

## Step 2. Define the inventory relationship

Here, you will select your relationship to the publisher and their inventory.

- **Relationship undeclared**: means you have not yet disclosed the publisher's details and how the inventory is accessed.
- **Managed - single publisher sourced directly**: means you are sourcing the inventory from only one publisher directly.
- **Managed - single publisher sourced indirectly**: means you are sourcing the inventory via an intermediary (such as a network, SSP, or exchange) from only one publisher.
- **Managed - multiple publishers sourced indirectly**: means you are sourcing the inventory via an intermediary (such as a network, SSP, or exchange) from multiple publishers.
- **Owned & Operated**: means you are the publisher.

## Step 3. Set the payment terms

- **Revenue Share**: Enter the percentage revenue share in the field provided.
- **CPM**: Enter the CPM and choose whether to pay when a default served.

## Step 4. Complete the publisher information

Depending on the **Inventory Relationship** setting you selected, you will be asked to enter specific information about the publisher. Enter the requested information into the fields provided, then check **I confirm the inventory relationship and publisher information provided is accurate**.

## Step 5. Define the allowed payment types

In the **Allowed Payment** section, select whether or not you will accept CPA or CPC deals from your managed advertisers as well as other trusted partners on the platform.

- **Allow CPA/CPC payment from direct buyers**: These options are selected by default. You must leave them selected if you want your managed CPA and CPC campaigns to serve on the publisher's inventory.
- **Allow CPA/CPC payment from trusted partners**: Select these options if you want to allow your trusted partners to pay you per action (conversion or click). You and the publisher will only be paid when a user clicks or converts on an ad served on the publisher. Enter the risk premium for the payment option.

> [!NOTE]
> CPM deals are allowed by default.

## Step 6. Determine the publisher's ad quality settings

**Ad Quality Settings** limit the creative attributes allowed to serve on this publisher. The network profile is always applied, but if you'd like to select additional settings you may do that here. Choose an ad quality profile to control which creatives can appear on your publisher's inventory. If you do not apply a **Publisher Template** or create a **Custom Profile**, the publisher's ad quality settings will default to your **Network Profile**.

- **None**: Select this option to use only the network profile
- **Use a template**: Select this option if you want to apply a template to determine ad quality settings. Note that if the template is updated, the ad quality settings will change accordingly.
- **Create a rule from a template**: Select this option if you want to copy a template profile into a new rule. Note that if the template is updated, the ad quality settings will not change.
- **Create a blank rule**: Select this option if you want to create a new blank rule and fill in the details on the **Ad Quality** screen.

## Step 7. Choose the exposure settings

The exposure settings allow you to choose how much information you want to show buyers about publishers, including names and how well they are performing.

- **Show Performance & Volumes in Reporting**: This will show buyers publisher performance in the **Site Domain Report** and available impressions in the **Inventory Manager**.
- **Show Publisher Name in Reporting**: This will show the publisher name in reporting, rather than just the ID.

## Step 8. Set the advanced options (optional)

In the **Advanced Options** section, you can set a publisher code, a max learn percent, user ID syncing settings, and you can enable Publisher Users to report on advanced metrics.

- **Code**: Assign a code to a publisher as your own unique identifier.
- **Override Dynamic Learn**: The optimization system automatically allocates a certain percentage of auctions to prefer learn bids over other types (i.e., optimized bids or base bids). However, you can override this percentage by entering a value in the **% learn auctions** field. This number indicates the percentage of auctions that will first attempt to find and use bids that are in the learning stage if they are available (including CPC and CPA bids from trusted partners). We recommend that you allow the system to maintain this percentage.
- **User ID Syncing**: In order to increase the Microsoft Advertising pool of cookied users, we apply user syncing pixels to allow partners to map our IDs to their IDs. You can choose which partners use them. The options for this setting, which effect the partners you can select, are **Use default settings** or **Override default settings**.
  - **Allow supply partner syncing**: Select this option to allow supply partners to utilize user syncing pixels. This option is selected (and locked) by default. To deselect it, set the **User ID syncing** field to **Override default settings**.
  - **Allow data provider syncing**: Select this option to allow data provider partners to utilize user syncing pixels. This option is selected (and locked) by default. To deselect it, set the **User ID syncing** field to **Override default settings**.
  - **Allow demand partner syncing**: Select this option to allow demand partners to utilize user syncing pixels. This option is selected (and locked) by default. To deselect it, set the **User ID syncing** field to **Override default settings**.
- **Report on Defaulted Imps**: Select this option to see data about default impressions in reports, such as imps filled, imps defaulted, total revenue, filled revenue, and defaulted revenue. This option is available regardless of the **User ID Syncing** setting (in **User ID Syncing**).
- **Enable Sell-side Page Capping**: Use this setting to limit the number of impressions that an individual brand can serve on a page in multi-tag auctions using **Sell-Side Page Caps**.

    > [!IMPORTANT]
    > This feature is not available to clients by default; for more information, please speak with your Microsoft Advertising representative.

- **Reporting Labels**: Enter the name of an internal **Salesperson** or an **Account Manager** (or both) responsible for the publisher in order to report on performance in **Network Reporting**.

## Related topics

- [Create a User](create-a-user.md)
- [CPC and CPA Payment Types](cpc-and-cpa-payment-types.md)
- [Advertiser and Publisher User Reporting](advertiser-and-publisher-user-reporting.md)
