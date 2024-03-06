---
title: Set Up Multi-Buyer Deals
description: Explore setting up deals with multiple buyers across platforms/DSPs, involving all buyers on a specific platform.
ms.date: 10/28/2023
---

# Set up multi-buyer deals

You can set up Multi-Buyer Deals in two different ways:

1. Multi-buyer deals with multiple buyers across various DSPs
1. Bidder-level deals with all buyers on a DSP

From the **Deal** section of the **Basic Setup** section see [Create a Deal Line Item](create-a-deal-line-item.md):

1. Click **Edit** under **Buyers** to open the **Buyer Targeting** screen.

    The **Buyer Targeting** screen has the following tabs:
    - **DSPs** – lists individual DSPs (bidders) that support bidder-wide deals. Click the “**\>**” after the DSP to display the list of buyers on that DSP. You can search for DSPs by name and ID. (**DSP Name** corresponds to Bidder Name. **DSP ID** corresponds to Bidder ID.)
    - **Buyers** – corresponds to members or seats, depending on which the DSP is using (see [Understanding Buyer Seat IDs](understanding-buyer-seat-ids.md)). You can search for buyers by name and ID (for seat buyers, **Buyer Name** corresponds to Seat Name, **Buyer ID** corresponds to Seat Code, and **DSP Name** corresponds to Bidder
      Name)

1. Click either the **DSP**s or **Buyers** tab to enable the following configurations:
  
    1. To set up bidder-level deals with all buyers on a DSP, click the **DSPs** tab to display available DSPs that use their own seat IDs for buying on a deal and click the green check mark to include any.

    1. To set up a multi-buyer deal with multiple buyers across various DSPs, you can either:
     - Click the **Buyers** tab to display available buyers and click the green check mark to include any.
     - Click the **DSP**s tab to display available DSPs, click the “**\>**” after the DSP to display the list of buyers on that DSP, and click the green check mark to include any.

       > [!NOTE]
       > Not all DSPs or buyers will be selectable; DSPs need to be enabled by Microsoft Advertising for multi-buyer deals on an individual basis based on their support for the feature. For any DSP that does not support multi-buyer deals, you can still include one buyer from that DSP on a broader multi-buyer deal. If you think a DSP you’re setting up a deal with should support multi-buyer deals, please contact your account representative.

1. Click **Save**.
