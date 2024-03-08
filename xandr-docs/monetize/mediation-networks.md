---
title: Mediation Networks
description: Our mediation tools let you allocate inventory to networks that are not directly integrated with our platform. This page is a step-by-step guide to add a network.
ms.date: 10/28/2023
---


# Mediation networks

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

Our mediation tools let you allocate inventory to networks that are not directly integrated with our platform yet. To sell to these networks, you'll need to set them up in our system. We already support a number of popular demand sources, including Amazon, Facebook, Google, and Millennial Media.

To add a network:

1. Select **Mediation** \> **Networks** from the navigation menu. This will take you to the **Ad Networks Overview** screen.
1. Click **+ New** to open the **Add a Network** dialog. Most users will want a network we already support. You also have the ability to set up a custom network integration.
1. To select a supported network, choose one from the dropdown. Networks that have already been added are shown in gray and can't be added again For a list of supported networks, see [Mediation FAQs](mediation-faqs.md).
1. If you want to integrate a mobile or web network that is not currently supported, select **Custom Mobile Network**, **Custom Web Network**, or **Custom Video Network**. Type a **Network Name** before saving. When you create a bid for this network, you will have to enter additional information about the custom network's ad placement ID and mobile advertising SDK (for a custom mobile network).

   > [!NOTE]
   > To change a custom network name, hover over a network in the **Network Name** list to make the **Edit** button appear. Click the button to display the Edit dialog box, then type the new name and click **Save**.

## Third-party reporting

If you see the **Enable Report Sync** checkbox, it means we can pull reporting data from that network's servers. This data is used to create daily reports and monitor trends directly from the UI.

For report sync, there are two things to keep in mind:

1. It is not available for all networks.
1. Data from third-party servers may be 1-2 days behind since we refresh this data once per day

## Related topics

- [How Auctions Work for Sellers](mediation-how-auctions-work-for-sellers.md)
- [Mediation Bids](mediation-bids.md)