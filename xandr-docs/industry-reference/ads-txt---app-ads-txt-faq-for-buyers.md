---
title: Ads.txt/App-Ads.txt Buyer FAQ
description: In this article, explore answers to frequently asked questions (FAQs) about Ads.txt/App-Ads.txt for buyers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Ads.txt/App-Ads.txt buyer FAQ

## What are ads.txt and app-ads.txt?

Ads.txt and App-Ads.txt are IAB initiatives aimed to help prevent unauthorized inventory sales. Publishers can drop these text files on their web servers to list all of the resellers that are authorized to sell the publishers’ inventory. Similarly, programmatic platforms also integrate ads.txt and app-ads.txt files to confirm which publishers’ inventory they are authorized to sell. This allows buyers to check the validity of the inventory they purchase.

Ads.txt files are used to declare authorized sellers of display inventory on domains. App-Ads.txt files are used to declare authorized sellers of application inventory.

To learn more about what problems these two standards are meant to solve, read the IAB Tech Lab blog on the topic: [https://iabtechlab.com/ads-txt-about/](https://iabtechlab.com/ads-txt-about/).

## Why did the the IAB implement ads.txt and app-ads.txt?

Unauthorized reselling is a major concern in programmatic advertising, and unless buyers contacted publishers directly, they would have had no way of knowing which SSPs are authorized to sell a particular publisher’s inventory. With Ads.txt and App-Ads.txt, the industry has created a quick, easy way for buyers to know which programmatic firms have legitimate access to the inventory they want to buy.

## How is Xandr approaching ads.txt and app-ads.txt implementations?

Xandr uses ads.txt and app-ads.txt files as the source of truth for who is authorized to sell inventory on a given domain or application. We work closely with our publisher partners to ensure their files are accurate and up-to-date, and subsequently block unauthorized resale on our platform.

## How easy are ads.txt and app-ads.txt for a publisher to implement?

Very easy. It is as simple as posting a text file to a publisher's domain similar to what virtually every website already does today with their robots.txt file. Additionally, there are many free resources on the internet to help validate ads.txt and app-ads.txt files, via a cursory internet search. These resources can help digital publishers ensure their ads.txt and app-ads.txt files are free of errors.

## What percent of publishers and top publishers have implemented ads.txt and app-ads.txt already? Where can I get an up-to-date list?

Since the launch of the ads.txt in the Winter of 2018, adoption rose quickly, with over 90 percent of our top 1,000 domains having adopted ads.txt already. This figure is likely to continue increasing, along with the app-ads.txt standard, which launched in the Spring of 2019. Because ads.txt and app-ads.txt have been developed and publicized by the IAB, Xandr expects and encourages all publishers and exchanges to adopt this standard, as it is in publishers' best interests to do so.

## Does Xandr enforce direct versus reseller declarations?

No. Publishers control the content of their own files. They are responsible for their accuracy.

## How often does Xandr's crawler update?

Daily for Ads.txt. Weekly for App-Ads.txt.

## What if I buy external from Xandr? Does a publisher have to list Rubicon's Xandr seat for it to be an authorized path?  

No, as long as Rubicon is an authorized path, we will note an implied relationship for Rubicon's APN seat for Monetize buyers.

## Are publishers who have ads.txt and app-ads.txt files posted more legitimate or trustworthy than those that do not?

No, not really, but ads.txt and app-ads.txt use is strongly encouraged. Publishers are free to decide when and if they post an ads.txt file and those that have posted them reflect a wide range of web content.

## When are ads.txt and app-ads.txt being enforced by Xandr?

Support for these two standards was rolled out to production by Xandr. Winter 2018 for Ads.txt, and Summer 2019 for app-ads.txt. For those publishers that have ads.txt and app-ads.txt implemented, Xandr only buys from authorized monetization partners.

## Will Xandr's adoption of ads.txt/app-ads.txt impact Deals or external demand?

No.

## What does that mean for me as a buyer? Do I have to do anything?

No. Buyers don't have to do anything. Publishers only list sellers in their ads.txt / app-ads.txt file and do not need to list any sort of buyer ID from any platform, including ours. APP automatically uses ads.txt / app-ads.txt to filter out Publisher who are not authorized to sell a domain, and if a publisher does not have ads.txt / app-ads.txt implemented, we will not do anything.

## If I buy, am I only buying on Ads.txt enabled domains or App-Ads.txt enabled applications?

If a publisher has an ads.txt or app-ads.txt file, we thoroughly enforce it and only purchase from authorized monetization partners. If they don't, we won't exclude them from being purchased but continue to recommend that all publishers adopt ads.txt and app-ads.txt at the earliest opportunity.

## Related topics

- [Ads.txt/App-Ads.txt FAQ for Sellers](ads-txt---app-ads-txt-faq-for-sellers.md)
- [Xandr Support for Ads.txt and App-Ads.txt](xandr-support-for-ads-txt-and-app-ads-txt.md)
