---
title: Mediation Networks
description: Our mediation tools let you allocate inventory to networks that are not directly integrated with our platform. This page is a step-by-step guide to add a network.
ms.date: 10/28/2023
---


# Mediation networks

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

Microsoft Monetize Ad Server mediation allows demand from sources not integrated into the Monetize Exchange or [Prebid Server Premium](prebid-server-premium.md) to compete for publisher inventory. Both known partners, such as Google, as well as custom networks are supported.

To call each partner for demand, they must first be created as networks within the Monetize account.

To create a network:

1. From the Monetize navigation menu, select **Mediation > Networks**. This will load the **Ad Networks Overview** screen.
2. Click the **New** button to open the **Add a Network** dialog.
3. Select a predefined partner, such as **Google Ad Exchange**, or choose a custom option (**Custom Web/Mobile/Video Network**) to integrate a partner not yet built into Monetize mediation. **Custom networks** require additional information during Bid setup, such as an ad placement ID and, for mobile, the advertising SDK.
4. Select the appropriate currency for the partner.
5. Enter a name for the network. A mediated network is created as a managed advertiser. If you try to use the same name as an existing advertiser, an error will occur. You must rename the original advertiser or choose a different name for the network.
6. Click **Save** to return to the list of networks, or click **Save and Create Bid** to move directly to creating the first bid for the network.
7. After saving, click the edit (pencil) icon to change the name of the network if needed.

   > [!TIP]
   > It is recommended to use no more than 3 or 4 networks in the waterfall for a given impression. Using more networks increases ad serving latency and adversely impacts user experience.

## Network platform setup

Setup is also required in each network’s platform, as covered in Integrating for Mediation.

### Reporting

In Monetize reports, mediated networks appear as advertisers, and bids are displayed as line items (both as filters and dimensions).

## Related topics

- [Selling Your Inventory through Mediation](mediation-selling-your-inventory-through-mediation.md)
- [Integrating for Mediation](mediation-integrating-for-mediation.md)
- [Mediation Bids](mediation-bids.md)
- [Mediated Network Service](../digital-platform-api/mediated-network-service.md)
  