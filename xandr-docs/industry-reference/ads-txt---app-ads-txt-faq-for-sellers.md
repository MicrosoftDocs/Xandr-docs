---
title: Ads.txt/App-Ads.txt Seller FAQ
description: In this article, explore answers to frequently asked questions (FAQs) about Ads.txt/App-Ads.txt for sellers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Ads.txt/App-Ads.txt seller FAQ

## What is ads.txt and app-ads.txt?

The goal of Ads.txt and App-Ads.txt is to give publishers a way to list ALL their approved SSP, ad network, and exchange partners (both direct and resellers). Theoretically, the publisher’s inventory should not be found via other partners.

Technically, Ads.txt and App-Ads.txt are files the publisher places on their domain (`website.com/ads.txt`, or `website.com/app-ads.txt`). Ads.txt is a file used to declare authorized sellers of display inventory on the web, whereas app-ads.txt is a file used to declare authorized sellers of application inventory. Within the respective files each approved partner is listed with their tech platform (Xandr, Google, Rubicon, etc.), account detail, and the relationship. DSPs & SSPs will regularly crawl these files to discover the approved inventory sources.

You can read more about what problems these standards are meant to solve on the IAB Tech Lab blog: [https://iabtechlab.com/ads-txt-about/](https://iabtechlab.com/ads-txt-about/).

## How is Xandr as a DSP going to use ads.txt and app-ads.txt files?

Xandr uses Ads.txt and App-Ads.txt information as a way to strengthen our existing inventory quality programs.

## How should publishers or networks incorporate their Xandr accounts into their ads.txt file?

For more information on how publishers and networks should use ads.txt and app-ads.txt, see [Xandr Support for Ads.txt](xandr-support-for-ads-txt-and-app-ads-txt.md).

## Does Xandr recommend that all publishers and networks implement ads.txt?

Yes. The Ads.txt standard was launched in early 2018, and has gained significant traction in the industry. Some buyers will exclusively purchase content that is considered "authorized" by Ads.txt. App-Ads.txt formally launched in the Spring of 2019, and is also quickly gaining traction.  

## Where can I find an example ads.txt file?

There are some samples of what ads.txt files should look like in [Xandr Support for Ads.txt](xandr-support-for-ads-txt-and-app-ads-txt.md).

## What percentage of Xandr publisher clients are ads.txt compliant?

Over 90% of our top 1000 publishers are compliant and have ads.txt files on their domains.

## How often does Xandr's crawler update?

Daily for Ads.txt. Weekly for App-Ads.txt.

## How is ads.txt used by Xandr buyer clients?

Buyers (both Xandr UI and API users as well as external bidder clients) benefit from Xandr's daily ads.txt file crawling and enforcement because, by default, they only buy from compliant sellers if a domain has an ads.txt file associated to it. Buyers do not have the option to target any differently because Xandr simply suspends supply paths in violation of information found in sellers' ads.txt files.

## What percentage of buyers are actively crawling publishers' files currently? At what cadence? Is this number expected to rise in the near future?

We have no way to know which bidders are crawling and which are not. Some buyers have publicly said that they both crawl for ads.txt and app-ads.txt files, and enforce inventory standards on the basis of these results. Xandr performs scanning and enforcement on a daily basis for display inventory, and a weekly basis for application inventory.

## Can publishers be blocked by buyers because they do not support ads.txt or app-ads.txt, or because their files are incorrect?

If a publisher has a file in error (meaning they don't include all their sellers that are authorized), then that has the potential impact them. If a file is found that appears unintentionally broken or corrupted in some way, Xandr will check with publishers rather than immediately disable buying from parties whose information is not found in the file.

## Does Xandr enforce ads.txt compliance for external bidder demand?

We are not enforcing ads.txt compliance for external bidders because we anticipate that many of our external bidder partners will be rolling out ads.txt detection and enforcement mechanisms within their own systems, and wanted to avoid duplication of logic.

For bidders who are buying external SSP demand via Xandr and are building out their own ads.txt compliance mechanisms, we recommend they implement enforcement mechanisms in a similar fashion to Xandr - If the SSP is listed in the file, then treat them as an authorized relationship via Xandr.

## Related topics

- [Ads.txt/App-Ads.txt FAQ for Buyers](ads-txt---app-ads-txt-faq-for-buyers.md)
- [Xandr Support for Ads.txt/App-Ads.txt](xandr-support-for-ads-txt-and-app-ads-txt.md)
