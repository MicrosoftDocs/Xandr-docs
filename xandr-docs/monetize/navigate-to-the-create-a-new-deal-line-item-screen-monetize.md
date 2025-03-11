---
title: Navigate to the Create New PG Deal Screen
description: Explore creating a programmatic guaranteed deal, choose pacing, and proceed on the Create New PG Deal screen for effective implementation.
ms.date: 10/28/2023
---

# Navigate to new PG Deal screen

To create a new programmatic guaranteed (PG) deal, start by pre-selecting a pacing option for your guaranteed deal. The creation process begins in **Seller Monitoring Workflow (SMW)**.

1. Access the SMW Line Items screen:

- Navigate to **Advertisers** > **Line Items** from the main menu.
- The **SMW Line Items** screen opens, displaying existing line items.

1. Click **+New** \> **Line Item**.

1. Search for and select an advertiser from the **Advertiser** text field.

   (Optional) Select the *Make Default Advertiser* checkbox to set this advertiser as the default for future PG deals.

1. Search and select an insertion order from the **Insertion Order** text field.

    (Optional), select the ***Make Default Insertion Order*** checkbox to make this insertion order your default insertion order for future PG deals.
1. Select a **Pacing** option:

   | Choice | Description |
   |---|---|
   | **Pacing in Microsoft Advertising** | If you choose this pacing option, pacing and other configurations such as targeting, frequency/recency caps, and deal creative criteria will be handled within Microsoft Advertising Monetize.<br>**Note**: **Pacing in Microsoft Advertising** is a **beta** feature that isn't available to all clients. If you'd like access to this feature, please contact your Microsoft Advertising account representative. |
   | **Pacing in Ad Server of Record** | If you choose this pacing option, a third-party ad server will handle pacing and other configurations. |

1. Click **Next**.

    - If you selected **Pacing in Microsoft Advertising**, the **Create New Line Item** screen appears.
    - If you selected **Pacing in Ad Server of Record**, the **Create New Programmatic Guaranteed Deal** screen appears.

For instructions on creating a programmatic guaranteed deal with your pacing selection, see

- [Create a Programmatic Guaranteed Deal](create-a-programmatic-guaranteed-selling-line-item.md)(if you chose **Pacing in Microsoft Advertising**)
- [Create a Programmatic Guaranteed Deal that Uses Third-Party Ad Server Pacing, Tag Integration](create-a-programmatic-guaranteed-selling-line-item-ssp.md)(if you chose **Pacing in Ad Server of Record**)
