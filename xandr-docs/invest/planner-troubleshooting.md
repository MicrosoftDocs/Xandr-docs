---
title: Microsoft Invest - Planner Troubleshooting
description: Learn about different possibilities and estimates in a planner and what you can infer from that. 
ms.date: 10/28/2023
---


# Microsoft Invest - Planner troubleshooting

## Estimated Reach = 0

If you don't see any estimated reach, it means that no auctions or users in the daily or weekly sample matched the targeting parameters you set. Make sure you haven't set parameters that conflict with each other. You can reference the targeting breakdown visualization to understand where drop-off is occurring.

If you don't find conflicting parameters, it's likely that your targeting parameters are too restrictive.

## Failed to fetch error

The "failed to fetch" error occurs when there is a timeout on the API. Typically, this happens when several updates were made consecutively, resulting in multiple API calls. Try refreshing the plan and waiting for the plan to load after each update.

## Numbers in planner don't match delivered impressions

You may find that the estimates in Planner don't match your recent results. For example, you may see delivered impressions in past data that aren't reflected in Planner's projections. Because the data is projected from a limited sample of historical data, estimates are not guaranteed to match existing campaign data.

## User count is greater than impression count

Because we sample auction and user data separately, user and impression data don't always align. We sample 10 million auctions and 10 million users daily. However, because multiple auctions can be associated with each user, each user may have more targeting attributes associated than each individual auction. As a result, the extent to which auctions associated with users overlap with the auction data used for impression counts is unknown.
