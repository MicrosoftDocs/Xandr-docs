---
title: Best Practices
description: In this article, explore the essential best practices that Supply Partners must adhere to in order to maintain good standing and gain access to the open exchange.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Best practices

Below are a set of best practices Xandr requires Supply Partners to abide by to be in good standing and to have access to the open exchange. Xandr reserves the right to disable Supply Partners in whole or in part, including shutting off access to the open exchange, if they do not abide by these best practices.

## Integration health

To access the RTB exchange, Supply Partners must:

- Integrate with the latest version of OpenRTB (currently 2.4 or higher) as implemented by Xandr.
- Abide by Xandr's requirements for specific devices & formats across channels.

## Inventory standards

To sell inventory on the open exchange, Supply Partners must provide information that validates that they are approved to monetize a Publisher's inventory. By cooperating with this validation, Xandr and our Supply Partners are taking a stand against the arbitrage of Publisher inventory, building trust through transparency with buyers and sellers alike.

To this end, the following best practices must be followed to sell Publisher inventory as a Xandr Supply Partner:

- Maintain direct relationships with the owner of the inventory's underlying domain or app. No third party or network traffic should be uploaded.
- Create a properly labeled, separate Publisher object for each Publisher. Each Publisher object should represent the business entity with whom the Supply Partner holds the end financial relationship.
- Disclose Publisher details in keeping with Xandr Inventory Relationship Declaration requirements.
- Ensure that domains with `ads.txt` files, or applications with `app-ads.txt` files associated, list you as an authorized reseller. Guidance for how Supply Partners can work with their partners to declare their Xandr members in `ads.txt/app-ads.txt` files can be found in [Support for Ads.txt and App-Ads.txt](../industry-reference/xandr-support-for-ads-txt-and-app-ads-txt.md).

## Transparent auctions

Supply Partners must hold a fair and transparent auction in which auction manipulation is prohibited, which includes but is not limited to non-transparent fees and dynamic flooring.

## Build to our APIs

To access Xandr's platform, Supply Partners must use our APIs. All system objects should be created and managed via APIs. Any Supply Partner who wishes to sell Deals must do so via the [Deal Service](../digital-platform-api/deal-service.md).

## More best practices

- [Understanding the Sell-Side Object Hierarchy](understanding-the-sell-side-object-hierarchy.md)
  
  An overview of publishers and placements and how to work with them.
- [Synchronize Your Inventory Structure](synchronize-your-inventory-structure.md)
  
  Guidance on using  or API to map your supply to Xandr.
- [Define Ad Quality Rules](define-ad-quality-rules.md)  
  
  Determine which creatives can serve on your inventory.
- [RTB Eligibility Requirements](rtb-eligibility-requirements.md)  
  
  Requirements for transacting on the open exchange.
- [Inventory Relationship FAQ](inventory-relationship-faq.md)  
  
  Details on our efforts to maintain transparency and accountability through Inventory Relationship.
