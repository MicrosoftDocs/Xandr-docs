---
title: Research Discrepancies
description: In this article, find instructions for researching and resolving discrepancy issues.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Research discrepancies

The following steps will walk you through researching and resolving discrepancy issues. The idea is to get a report from your side and compare it with the report on the Xandr side.

## Before opening a discrepancy case

To open a discrepancy investigation case with the Xandr support team, you must confirm the following:

- Discrepancy level is above 10% (15% for mobile).

  Anything below that threshold is an organic component of doing business in an RTB environment, implying different servers to communicate over a "public" network.

- Discrepancy occurred less than 15 days ago.

> [!IMPORTANT]
> If you have not verified these criteria, Xandr would not investigate on the case.

## Retrieve and review aggregated reports

1. Get the impression and spend figures by Seller, Publisher, Tag ID, Domain, Creative Size, Creative ID, and Geo from the [Xandr reporting UI](https://bidder.xandr.com/admin).

1. Retrieve the same report from your side. Compare the reports. We suggest that you first check the data by days, then by the hours. (Be sure to retrieve all the data based on the same time zone.)

   - Get the discrepancy repartition by seller, publisher, tag ID, domain, creative size, creative ID, and geo.
   - Identify if the discrepancy levels are the same within those features.

If you're able to identify the source of the discrepancy based on your comparison of these reports, depending on the discrepancy level you might want to:

- Exclude from your bidder profiles the inventory source causing the discrepancy.
- Determine why there is such discrepancy on a specific feature and attempt to resolve the issue.

Examples of possible issues discovered in these reports include:

- You see a large discrepancy in a particular geographic area on some creatives because an advertiser uses a "swap" technology on their creatives that swap the creative content with a blank if the creative is outside of the campaign scope.
- You see a large discrepancy with a specific seller because most of their pages are in HTTPS but your counting pixels are in HTTP.

If the discrepancy level is the same over all sellers, publishers, tags, domains, sizes, creatives, and geo, you might need to investigate the user browser and operating system issues.
