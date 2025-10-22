---
title: FAQ - Supply Partner Inventory Relationship
description: This article addresses the frequently asked questions about supply partner inventory relationship.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# FAQ - Supply partner inventory relationship

## What is Inventory Relationship, and why are we doing it?

In an effort to maintain transparency and accountability in the supply sold via, sellers will soon be asked to provide information about their inventory sources. The requested information is basic business information about how the inventory is accessed and will be used to support Xandr inventory quality efforts.

Xandr may verify the publisher information with you or the publisher. Any inaccurate information could result in your termination or suspension.

## What is the motivation behind the changes?

There are talks within online advertising self-regulatory groups to produce similar recommendations for sellers participating in the RTB marketplace. Xandr is embracing this industry push to provide a safer RTB marketplace for buyers. Buyers have long been required to register and audit creatives on Xandr. Inventory Relationship is another step towards accountability on the sell side.

## How should sellers define each Inventory Relationship option?

For a complete list of fields and their usage requirements, refer to the [Publisher Service](../digital-platform-api/publisher-service.md) documentation.

||||Managed|||
|:---|:---|:---|:---|:---|:---|
| |**Relationship undeclared** | **Owned & Operated** | **Single publisher sourced directly from publisher** | **Single publisher sourced indirectly from partner(s)** | **Multiple publishers sourced indirectly from partner(s)** |  |
| Description of Inventory Source | Relationship undeclared means you have not yet disclosed the publisher's details and how the inventory is accessed. | You are a publisher | You are sourcing the inventory from only one publisher directly. | You are sourcing the inventory via an intermediary (such as a network, SSP, or exchange) from only one publisher. | You are sourcing the inventory via an intermediary (such as a network, SSP, or exchange) from multiple publishers . |
| Required Fields | NA | Publisher Business Name<br><br> Publisher Contact<br> - Name<br> - Email<br>- Phone | Publisher Business Name<br><br> Publisher Contact <br> <br> Publisher Address<br> - Name<br>- Email<br> - Phone | Inventory Source Name<br><br> Publisher Business Name<br><br> Publisher Contact Publisher Address<br> - Name<br>- Email<br>- Phone | Xandr's [Best Practices for Selling Inventory](./best-practices.md) guidelines advise that our Supply Partners sell inventory from direct publishers. |

## What happens if a seller does not populate the required fields?

To create or edit publishers in the UI or API, you will have to enter this information where prompted. New publisher objects must have the proper Inventory Relationship declared. Existing objects should be updated with the proper Inventory Relationship. We recommend making these updates via the [Publisher Service](../digital-platform-api/publisher-service.md).

## How do I complete the Inventory Relationship and Publisher Information fields for small publishers without a company?

For publishers operating as sole proprietorships under their personal name, add the payee name in the **Business Name** field.

## What are the language requirements for the Publisher Information fields?

Xandr recommends completing the Publisher Information fields in English. However, if this is not possible, the local language may be used.
