---
title: Microsoft Monetize - Set Up Line Item Inventory and Brand Safety
description: Explore line item setup with supply source, content categories, inventory preferences, block/allowlists, brand safety, and ads.txt.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up line item inventory and brand safety

You can use the **Inventory & Brand Safety Targeting** section to specify the type of inventory that you want to buy (supply source), target universal or custom content categories, specify whether to advertise on web or app inventory, create and/or apply blocklists or allowlists, define brand safety settings, and set up ads.txt targeting.

1. Set the **Supply Source** to specify the type of inventory that you want to buy.

    The **Supply Source** that you select will affect the available inventory targeting options in the **Inventory & Brand Safety Targeting** section. In addition, certain buying strategy options cannot be combined or must be selected together.

   | Supply Source | Description |
   |---|---|
   | **Open Exchange** | Real-time bidding in our open exchange (also known as RTB). If you select **Open Exchange**, you can opt to pay per impression or per view. We also recommend that you apply an allowlist or a brand safety segment as well. The **Advanced Targeting** subsection displays within the **Inventory & Brand Safety Targeting** section after selecting the **Open Exchange** checkbox so that you can select specific open exchanges. |
   | **Managed** | Select this option if you have a managed relationship. If you select this option, you must select a **Line Item Priority** from the pull-down menu to rank the line item in the auction.<br>**Note**: The default line item priority is 5. When the line item's priority is ranked above the network's reselling priority, the line item will take precedence over line items with lower priorities, as well as open exchange demand. When the line item's priority is ranked below the network's reselling priority, the line item will compete with open exchange bids.<br>The network's reselling priority gives preference to its own advertisers' campaigns over campaigns run by external buyers. |
   | **Deals** | Select this option if you want to buy deals that publishers have exposed to you. You can choose to target all deals or only specific deals. If you select **Specific Deals**, you can include/exclude deals or deal lists. |

1. Set your **Managed Inventory**.

    This setting controls targeting inventory by universal or custom content categories, as well as how you target direct inventory.

    > [!NOTE]
    > This field will only appear if you have selected **Managed** in the **Supply Source** subsection.

1. Set the **Inventory Type**:
    - **App & Web** - Runs on both inventory types (**default setting**).
    - **App Only** - Runs in applications installed on mobile tablets, phones, and Windows 8 devices.
    - **Web Only** - Runs on standard websites and those optimized for browsers on mobile devices.

    > [!TIP]
    > The inventory type can also be set at the insertion order level.

1. Select a member-level or advertiser-level blocklist or create a blocklist directly from the **Inventory & Brand Safety Targeting** section.

    The inventory that has been included in your blocklists won't be bidded on. By default, the Microsoft Advertising blocklist will always be applied.
  
    > [!NOTE]
    > If the **Require for all Line Items** checkbox has been selected at the Network level for a particular blocklist, it will be applied to all of your line items and can't be removed.

1. Select a member-level or advertiser-level allowlist or create an allowlist directly from the **Inventory & Brand Safety Targeting** section.

    The inventory that has been included in your allowlists will be bidded on.

   > [!NOTE]
   >
   > - If the **Require for all Line Items** checkbox has been selected at the Network level for a particular allowlist, it will be applied to all of your line items and can't be removed.
   > - If you have selected **Open Exchange** as one of your supply sources, you should also select at least one allowlist. If you don't have an allowlist, you can select the Microsoft Advertising Inventory List. This list is a collection of inventory that Microsoft Advertising has selected based on demonstrated demand interest within our marketplace. The Microsoft Advertising Inventory List has been vetted using additional quality controls and platform inventory quality filtering.
   > - If you selected **Open Exchange** or **Managed** as your **Supply Source**, you can only bid on inventory in the allowlist.
   > - You can view or export selected allowlists. Allowlists can also be applied at the insertion order level.

1. Add brand safety segments.

    Brand safety segments are pre-defined by third-party verification vendors. These segments help apply additional quality controls to the inventory that you are targeting such as exclude drugs. They are used to limit the placements/pages you will be able to target as opposed to other kinds of segments that are used to target specific
    groups of users.

    1. Click the pencil icon.
    1. Select the desired third-party verification vendor such as comScore or DoubleVerify. If you have selected **Open Exchange** as one of your supply sources and have not already applied an allowlist, you should select at least one brand safety segment. Once selected, the segments are automatically included or excluded based on their intended use.

       > [!TIP]
       > To view all of your brand safety segment selections, click **Summary**.

    1. Select the checkbox for each segment that you want to apply (charges will apply).

    1. Click **Save**.

       If you select more than one brand safety segment, a segment group will be automatically created for each one (under **Targeting \> segments**)  and they will be ANDed together.

1. Expand the **Advanced Targeting** subsection and make an **Ads.txt** selection. When the **ads.txt** option is selected, the line item will only target web inventory on the open exchange that is authorized in a publisher's `ads.txt` file.

    > [!NOTE]
    > The **ads.txt** targeting parameter only applies to open exchange inventory. It does not affect deal inventory targeting.

1. Apply key/value targeting.

    > [!NOTE]
    > If you have **Open Exchange** selected as your **Supply Source**, you won't be able to apply the necessary key/value targeting.

## Related topics

- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Deal Targeting (ALI)](deal-targeting-ali.md)
- [Managing Your Inventory Reselling Exposure](managing-your-inventory-reselling-exposure.md)
- [Inventory Targeting (ALI)](inventory-targeting-ali.md)
- [Inventory Lists (ALI)](inventory-lists-ali-only.md)
- [Ads.txt/App-Ads.txt FAQ for Buyers](../industry-reference/ads-txt---app-ads-txt-faq-for-buyers.md)
- [Key/Value Targeting](key-value-targeting.md)
