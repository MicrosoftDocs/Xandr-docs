---
title: Understanding Yield Management
description: In this article, learn what yield management, floor rule, and bias rules are and how they work.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Understanding yield management

> [!IMPORTANT]
> This feature is not available by default. If you are interested in gaining access or discussing potential use cases that may apply to your business, reach out to your Microsoft Advertising representative.

Networks can use yield management (YM) tools to set floor (minimum bid price) and bias (bid modifying) rules, thereby exerting more control over impression pricing in order to:

- Serve creatives with the highest yields for publishers
- Allow publishers to express preferences for creatives from certain buyers over others
- Avoid channel conflict with directly negotiated deals

YM rules are set up per publisher and can apply to various impression properties including:

- The specific audience the network is trying to reach, based on geographic region or marketing segment
- The type of creatives that are most desired, e.g., those that synchronize with the publisher's content
- Whether the creatives involved would create channel conflict

This page will explain floor and bias rules, and how they work.

For instructions on creating floor and bias rules, see [Create a Floor Rule](create-a-floor-rule.md) and [Create a Bias Rule](create-a-bias-rule.md).

## Floors overview

A floor is the preferred bid amount a network would like to receive for an impression. The network's preferred bid amount may vary depending upon one or more factors, such as the type of creative involved. Put another way, a floor can be thought of as the minimum price the network would like to receive for an impression. There are two types of floors; hard floors and soft floors.

- **Hard Floor:** The minimum amount the network will accept as a net bid. If the hard floor price is not met, then no bids are accepted and the auction ends without a winner, or a default creative is served. A bid will be considered only if it is equal to or greater than the hard floor.

    > [!NOTE]
    >
    > - Net bids are inclusive of any biases set in the seller's yield management rules. In the event that a bias pushes a net bid above the minimum set by the hard floor, the seller may receive less revenue than is specified by this minimum.
    > - Where there is only one bid that exceeds the hard floor and wins the auction, that bid is reduced to the value of the hard floor, assuming there is no soft floor.

- **Soft Floor:** More subtle than a hard floor, the soft floor is the lowest price the network will price-reduce a bid down to. Put another way, a soft floor enables the network to alter the mechanics of the standard second-price auction. In a second-price auction, the winning bidder pays $0.01 more than the amount of the second bidder's bid. However, when a soft floor is set, the winning bidder pays the greater of the two between the soft floor price or the second bidder's bid. If the soft floor is above the winner's bid, the winner simply pays the price they've bid.

> [!NOTE]
> The soft floor can not be set to a value below the hard floor.

### Soft floor examples

The soft floor for an auction has been set at $1.25. The two highest bids are $1.50 and $1.00. Normally the $1.50 bidder wins and pays $1.01. However, with the soft floor setting, the winner pay $1.25 instead.

In another auction, where the same $1.25 soft floor applies, the highest bid you receive is $1.00. The soft floor of $1.25 means that the winning bidder pays their actual bid of $1.00, since it is closest to the soft floor.

### Visualize hard and soft floors

Read through the slides below to visualize the effects of hard and soft floor settings.

## Biases overview

A bias is a way of modifying certain bids to appear higher or lower than they actually are in order to prefer or deter the bid. This setting affects the way that bids are ranked but does not affect the value of each bid when it comes time to determine the winning price. It is possible to have a winning bid with a value less than another bid. In this case, the higher bid acts as a soft floor to the winning bid, so the winning bid is not price reduced.

Biases can be set for a certain buyer, group of buyers, or on certain types of inventory. Put another way, networks can set a positive bias to favor bids from specific buyers or groups of buyers, or set a negative bias for less preferred buyers.

### Bias examples

Buyer A has bid $1.50 and Buyer B has bid $1.30 in an auction. The network has set a +20% bias for Buyer B, making Buyer B's bid appears to be higher than $1.50 (around $1.56). Therefore, Buyer B wins the auction but only pays $1.30.

In another auction Buyer C has bid $1.50 and Buyer D has bid $1.40. The network has set a -10% bias for Buyer C, making Buyer C's bid appear to be $1.35. Therefore, Buyer D wins the auction.

## How YM rules are applied

You may have multiple floor and bias rules set up that apply to the same inventory or buyer. The system will follow these steps to gather, prioritize, and apply YM rules.

1. When an auction occurs, the system checks if there is a publisher-level YM profile. If yes, the system proceeds to #2. If no, the system proceeds to #5.
1. All YM rules within the profile are gathered and listed from highest to lowest priority. As a priority 1 rule, the base rule is at the bottom of the list.
1. Starting with the first rule in the list, the impression is checked to see if it matches the rule's criteria. If yes, the system proceeds to #4. If no, the system repeats this step until a matching rule is found then proceeds to #4. The base rule is the lowest priority and applies to all of the publisher's inventory (has no matching criteria). If the impression does not match any of the higher priority (conditional) rules, the base rule will be applied. If the list of rules is exhausted without finding a match, and you have not set up a base rule, the system proceeds to #5.
1. The matching YM rule is applied.
1. An auction winner is selected.

> [!IMPORTANT]
> A single rule applies in an auction. The highest priority rule that has matching targeting criteria will apply. In the case where more than one rule of the same priority passes targeting, we will randomly choose which rule to apply.

## Related topics

- [Create a Floor Rule](create-a-floor-rule.md)
- [Update Floor Rules](update-floor-rules.md)
- [Create a Bias Rule](create-a-bias-rule.md)
- [Update Bias Rules](update-bias-rules.md)
