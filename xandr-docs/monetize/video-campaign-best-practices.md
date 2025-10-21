---
title: Video Campaign Best Practices
description: This page provides you with a list of best practices to ensure maximum delivery and success for your video campaigns on the Microsoft Advertising platform. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Video campaign best practices

This page provides you with a list of best practices in a question-answer format to ensure maximum delivery and success for your video campaigns on the Microsoft Advertising platform.

## Are you following general delivery best practices?

Check the following settings to make sure you are not limiting your delivery:

- Is the budget set restrictively low?
- is the budget conflicting with the minimum bid price?
- Are you capping advertising frequency?
- Are you pacing effectively?

Check your campaign parameters to ensure that they are accurate for a video campaign.

## Have you reviewed available domains and available impressions by geography?

Review all available domains and monthly available impressions, segregated by geography, from each Microsoft Advertising supply partner.

It is best to ensure that any specific inventory you are looking for will be available before you kick off a campaign.

## Are you bidding an aggressive base price?

CPMs are higher for video creatives than they are for normal creatives (approximately $6-$13). Ensure your base bid is aggressive enough to cover the higher CPMs.

## Is your campaign targeting video sellers?

If so, the following external supply partners represent the greatest reach for video campaigns:

- SpotXchange
- Rubicon
- Google Ad Exchange
- LiveRail
- StickyAds
- Adap.TV
- AerServ
- Optimatic
- Falk Technologies or Fyber

## Have you checked seller eligibility in Partner Center?

Sellers must be classified as 'eligible' for seller targeting to work. Ensure that you are not blocking any video sellers.

## Are you targeting the right supply + device types?

Mobile web and in-app video inventory is available. However, if your VAST contains VPAID, you should be aware that some mobile devices will not support all implementations of VPAID.

## Is your video parameter targeting too restrictive?

Setting any of the three video targeting parameters - Playback Method, Player Size, or Position - may limit your delivery, as not all suppliers pass in these parameter. It is recommended to include "No Playback Method/Player Size/Position Provided" as well to account for these instances.

## Have you selected 'Auto-play, Sound Unknown' or 'Mouse Over' in the video targeting section?

When targeting these dimensions, your campaign will not deliver.

## Are you eligible to serve on all video inventory?

Some sellers only allow known partners to buy their inventory. In order to gain access, please reach out to your Microsoft Advertising representative.

## Are you using multiple video formats in the same campaign?

Avoid using both VAST creatives and in-banner or interstitial video creatives within the same video campaign.

An in-banner or interstitial video creative will not serve when you target by position: Pre-Roll, Mid-Roll, or Post-Roll.
