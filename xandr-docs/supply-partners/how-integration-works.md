---
title: How Integration Works
description: This article explains the outcome of receiving an ad call by an integrated supply partner.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# How integration works

Here's a diagram and description of what happens when a supply partner that has integrated with Xandr's platform receives an ad call:

:::image type="content" source="./media/c.png" alt-text="Diagram explaining the outcome of receiving an ad call by an integrated supply partner.":::
  
1. A user views a web page that contains an ad tag belonging to the supply partner. The ad tag calls the supply partner.
1. The supply partner starts an auction for the inventory and sends a bid request to Xandr.
1. Xandr offers the bid request to our demand partners, who have a certain number of milliseconds in which to respond with a bid.
1. Xandr holds an auction to choose a winning bid based on the data in the bid request and the publisher's ad quality preferences (ad profile).
1. Xandr passes the bid and a Xandr ad tag to the supply partner. The supply partner includes the Xandr bid in its own auction.
1. If the Xandr bid wins the action, the supply partner drops our ad tag on the web page.
1. The ad tag notifies Xandr that the bid won, sends the bid clearing price and identifies the location of the ad to serve.
1. Xandr serves the ad.
