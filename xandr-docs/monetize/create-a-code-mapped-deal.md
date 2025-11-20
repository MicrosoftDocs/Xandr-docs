---
title: Create a code mapped deal
description: In this article, find information on creating a code mapped deal.
ms.date: 11/11/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# Create a New Code-Mapped Deal 


The **Code-mapped deal** workflow is designed for scenarios where publishers need to create deals that include an external code.
This code is passed in the **OpenRTB** request and links the deal created in an external platform to its corresponding **Microsoft Monetize deal ID**.

For this use case, no additional targeting settings are required. All targeting is defined and enforced within the external platform.

> [!NOTE]
> This workflow replaces the legacy deal creation process in Partner Center, which is scheduled for deprecation.
> All deals created using the legacy workflow remain fully backward compatible with the new process.

## Access the workflow

- In Microsoft Monetize, go to **Deals**.

- Select **Create**, then choose **Code-mapped deal** from the dropdown menu.

- You can also create a **Code-mapped deal** from an existing deal by selecting Use as template in the Deals grid.

For detailed steps, see [Create a code-mapped deal from a template](#create-a-code-mapped-deal-from-a-template) section below.

## Create a Code-Mapped Deal from scratch

> [!NOTE]
> Before creating a custom deal, confirm the correct buyer ID with the buyer.
> If you plan to use a buyer seat ID from an external DSP, check the Buyer Seat Migration Status reference table in [External DSPs using Buyer Seat IDs](external-dsps-using-buyer-seat-ids.md).

### Basic settings

- **Deal name (required)**: Enter a clear, descriptive name for the deal.

- **Deal code (required)**: Enter the external deal code that will be passed in the ad request to map the external deal to the Microsoft Advertising deal ID.

    - The code must be unique.

    - It isn’t case-sensitive.

    - It can include letters, numbers, periods (.), underscores (_), or dashes (-).

- **Deal description (optional)**: Enter a short description for the deal. This description is visible to buyers.

## Deal Details

- **Buyer**: Select the buyer for whom you’re creating the deal. Buyers can be identified by a Microsoft Advertising member ID or, for external DSPs, by a buyer seat ID. 

  - For more information, see [Understanding buyer seat IDs](understanding-buyer-seat-ids.md).
  - Some seat IDs are visible but not yet eligible for bidding. Check [External DSPs using buyer seat IDs](external-dsps-using-buyer-seat-ids.md) for the latest eligibility information.

- **Ad type**: Select the creative type eligible to bid on the deal. This value is included in the bid request to DSPs.

    - For more granular control, use the Media type setting in the Deal ad quality section.

    - If no ad type is selected, any creative type can bid on the deal.

- **Deal priority**: Defines the deal’s priority within the auction.

    - **Open auction**: Allows the deal to compete with all RTB bids without preference.

    - **Private auction**: Gives the deal priority over open auction bids while still competing with other private auction deals of the same priority.

    - For more information about auction types, see [Deal auction mechanics](deal-auction-mechanics.md)
.

- **Priority level**: Can be set only for private auction deals. Use this setting to prioritize among private deals.

    - The highest priority always wins the auction.

    - The default priority level is 5.

- **Pricing strategy**: Choose how to define pricing for the deal.

    - **Floor price**: The minimum amount the buyer must bid to compete for the inventory. The buyer pays what they bid, as long as the bid meets or exceeds the floor price.

    - **Fixed price**: The buyer pays a fixed amount regardless of their bid. The bid entered in the auction equals the fixed price.

    - **Market price**: Uses your existing yield management floors or open auction dynamics to determine the price. No deal-specific price is set.

- **Price**: If you select **Floor price** or **Fixed price**, enter the price amount and choose the currency.

    - The default currency is the member’s account currency.

    > [!NOTE]
    > The price you enter represents the gross amount. To estimate your actual earnings, factor in the revenue fee specified in your Microsoft Advertising contract.

- **Start date**: Enter the date when the deal should begin. By default, the start date is set as the time the deal is being created.

- **End date**: (Optional) Enter the deal’s end date. If no end date is set, the deal remains active until you cancel it.

## Deal Ad Quality

Because deals are special agreements, buyers can be allowed to serve creatives that wouldn’t normally be eligible in regular auctions. For example, a deal can override the standard network ad quality settings applied in open auctions.

You can also apply additional restrictions to control which creatives are allowed in the deal. Use the following sections to define ad quality preferences:

- Brand

- Creative category

- Language

- Specific creatives

- Trust level

- Media types

- Technical attributes

Each option lets you refine or expand what types of creatives can serve for the deal, giving you full control over quality and compliance.

For more information, see [Override ad quality settings on a deal](override-ad-quality-settings-on-a-deal.md).

**Creative review**: Turn on or off creative approval for the deal.

  - When enabled, creatives must be manually reviewed and approved before they can serve.

  - When disabled, eligible creatives can serve automatically based on the deal’s ad quality and targeting settings.

**Creative attributes**: Configure which creative attributes are allowed for this deal. You can define restrictions or permissions for the following:

  - [Brand](create-a-custom-deal.md)
  - [Language](create-a-custom-deal.md)
  - [Media type](create-a-custom-deal.md)
  - [Creative category](create-a-custom-deal.md)
  - [Technical attributes](create-a-custom-deal.md)

## Save the deal

1. In the upper-right corner of the screen, select **Save** to create the deal.

1. To quickly create a similar deal, select the dropdown arrow next to **Save**, then choose **Save and duplicate**.

    - This option saves the current deal and opens a new creation form prepopulated with the same details.

> [!NOTE]
> The Deal code field is cleared automatically because each deal must have a unique code.

## Deal summary

The summary panel on the right side of the screen provides a real-time overview of all deal settings.

- **Required fields** are always visible, even if they haven’t been completed yet. This helps you confirm that all mandatory inputs are filled before saving.

- **Optional fields** appear in the summary only when values have been entered.

## Create a code-mapped deal from a template

You can create a new deal using an existing code-mapped deal as a template.

1. Search for the deal you want to use as a template.

    - You can search by name, ID, or code.

1. In the Name column, hover over the deal.

    - Two icons appear.

1. Select the **Use as template** icon.

1. Review the deal settings and summary, and make any necessary updates.

1. Select **Save** to create the new deal.

    - To create multiple similar deals, select Save and duplicate.
    This saves the current deal and opens a new form prepopulated with the same details.

> [!NOTE]
> The **Deal code** field is cleared automatically because each deal must have a unique identifier.
