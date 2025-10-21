---
title: Curation Optimization
description: In this article, learn about the Curation optimization process in detail.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Curation optimization

With the growth of the programmatic industry, systems must process a greater volume of auctions with more and more information. For example, there are now industry IDs, schains, and, in recent years, curated deals incorporated into the auction.

In programmatic auctions, each participating system has a fixed amount of time (a few milliseconds) to process the auction and respond. Therefore, each system must ensure it processes auctions as efficiently as possible, and deprioritizing unnecessary information is one way to drive efficiency.

As part of the curation process, we can deprioritize unnecessary information by predicting which curated deals will drive spend in a given auction. For example, we can sample curated deals that a buyer has stopped bidding on and unsample them if the buyer starts bidding again.

This ensures that each auction focuses on processing the most valuable curated deals. In this way, buyers, curators, and sellers will achieve better results.

## Curator's role

Curators don’t need to take additional actions to benefit from Curation Optimization. Curators should be aware that if there is a lack of bidding activity or low levels of spend on a curated deal, both you and the buyer may observe a decrease in impressions matched and bid requests over time. This isn't due to the available supply but rather the sampling applied to the deal.

### Best practices to follow

- If your buyer has provided their campaign’s flight dates and you’re creating a curated deal for them in advance, use the Flights setting so that it launches at the same time as their campaign.

- If a deal is not needed for a prolonged period, deactivate it and reactivate it later, such as with seasonal deals. Alternatively, if a deal is no longer needed, delete it. Reports can still be generated for deleted deals.
