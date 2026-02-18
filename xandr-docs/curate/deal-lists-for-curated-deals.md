---
title: Deal Lists for Curated Deals
description: This article provides details on the deal lists for curated deals. A deal list is a group of deal IDs categorized for targeting across curated deal line items.
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Deal lists for curated deals

A deal is an agreement between a buyer, curator or seller that provides special access to inventory and/or data. Deals are primarily used to access preferred premium inventory, negotiated inventory or unique audiences.

A deal list is a group of deals IDs categorized under a single heading for targeting across curated deal line items. Deal lists allow curators to pre-define lists of seller deals for their operations team and streamline their workflows, making it easy to target the same group of seller deals across curated deal line items. If deal grouping requirements change, you can make the changes in the deal list and all curated deal line items will be updated accordingly.

## Manage deal lists

You can create and manage Deal Lists at the Member and Advertiser level. A deal list may contain one or more deal IDs and a deal ID can be added to multiple deal lists. However, a deal ID can be added only once to a single deal list. While adding or removing deals in a deal list, you can find the deals by deal ID, deal name or deal alias. Additionally, deal IDs can be added to a list in bulk.

### Create a new deal list

1. In the **Inventory** menu select **Deal Lists** from the dropdown.
1. Select **New** on the **Deal List** page and provide the following details on the **Create a New Deal List** page:
    1. **Name**: Enter the name of the deal list.
    1. **Description**: Enter a description for the deal list which can offer a brief definition for it. For example, Deal list for Ford USA advertisers.
    1. **Available to**: *(Optional)* Select whether the deal list is specific to particular advertisers, or if it is available to all advertisers under the current member. If the deal list is available only to particular advertisers, enter the advertiser details by searching for the name or ID of the advertisers. You can add one or more advertisers in this field.
    1. **Deals**: Add deals to the deal list. There are multiple options for adding deals to the list:
        1. **Search and Add**: Search deals by ID, name or alias. Post selection of a deal, it displays the particulars about the deal such as **Name**, **ID**, **Buyer Deal Status (Active/Inactive)** and **Seller member**. You can also select the **eye** button to view further details about the deal such as **Currency**, **Type**, **Sizes**, **Brands**, **Media Types**, **Start** and **End dates**, etc. You can add multiple deals using this search option.
        1. **Import**: Allows you to bulk import a list of deals from a CSV file to a deal list.
        1. **Paste Deal IDs**: Add the Deal IDs by entering them manually, each ID separated by a comma or hard return.

        > [!NOTE]
        > Deals with pending, active, or null deal acceptance status can be added to a deal list. Inactive or Declined deals are ineligible deals which cannot be added to a deal list.

1. Once all deal IDs are added, select **Save** to complete the setup.

### Edit a deal list

1. Select the name of the deal list on the **Deal List** page. This will display the details of the deal list with the deals it contains.
1. Select **Add** to include more deals to the deal list. To add deals to the deal list, follow the instructions in the **Create a New Deal List** section above.
1. To remove an existing deal from the deal list, select the checkbox next to the deal and then select **Remove**. A confirmation window will be displayed. Select **Save** to delete the deal from the list.

## Target deal lists

After creating a deal list you can target it on the curated deal line item setup screen. In the **Basic Setup** section, select the **Deals** option under **Supply Strategy**. You’ll then be able to target either individual deals or deal lists.

### Target all available deals

Select **All Deals**.

### Target specific available deals

> [!IMPORTANT]
> Curated Deal line items should not target other curated deals. Ensure that the deal list does not include curated deals.

1. Select **Specific Deals**.
1. A pull-down menu displays with **Deals** selected by default.
1. To target specific deals, select one of the following targeting options and complete the corresponding steps:

    | Menu Option | Steps |
    |:---|:---|
    | **Deals** | a. Search for available deals by name, alias, ID, or code to target.<br>b. Include deals by selecting the :::image type="icon" source="./media/check-edited.png":::.<br><br> **Tip**: You can also select the **eye** button to view additional details about the deal such as **Currency**, **Type**, **Sizes**, **Brands**, **Media Types**, **Start Date**, and **End Date**. |
    | **Deal Lists** | a. Search for available deal lists by ID or name to target.<br> b. Include deals by selecting the :::image type="icon" source="./media/check-edited.png":::. |

   > [!NOTE]
   > You may only include deals and deal lists in your targeting. It is not possible to exclude deals or deal lists. You can include a mix of deals and deal lists in your targeting.
1. Select **Save** to complete the setup.
