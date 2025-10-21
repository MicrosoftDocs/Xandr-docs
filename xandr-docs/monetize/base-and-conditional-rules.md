---
title:  Microsoft Monetize - Base and Conditional Rules
description: Learn what are Conditional rules and how you can establish priority settings for each of your onditional rules. This page also talks about Base rule to which Monetize defaults to in case none of the conditions of the impression meet the criteria of any conditional rules for a publisher. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Base and conditional rules

There are two different scenarios in which base and conditional rules are applied:

1. **Publisher ad quality**: Publisher base and conditional ad quality rules give you the ability to determine which collection of ad quality settings you would like to apply to a particular impression based on attributes such as creative size, placement, or user frequency. The base rule, synonymous with the default rule, is used when no conditional rules exist, or when the existing conditional rules' targeting requirements are not met by an impression. At most, only two ad quality rules can apply. One of those two is the network rule, which always applies, and the other will be either the base or conditional rule. See [Working with Ad Quality](working-with-publisher-ad-quality.md) for details.
1. **Publisher payment rules**: Payment rules represent a financial agreement between a network and a publisher. Publisher base and conditional payment rules are used by publishers to set this agreement at the impression level. See [Create Payment Rules](create-payment-rules.md) for details on setting up publisher payment rules.

## Conditional rules

A conditional rule has specific targeted settings (frequency, geography, size, placements) that are used as requirements. If an impression does not meet all of the specified requirements of the rule, that rule will not be considered when determining how to pay the publisher.

You can establish priority settings for each of your conditional rules. Priorities run from 1 (lowest priority) to 10 (highest priority).

Priority settings determine the order in which rules are reviewed and eventually applied to impressions. For example, assume that you have an impression that was served in South Carolina. The conditions of the impression will be reviewed against the conditions of the rules, starting with the highest priority.

| Conditional Rule | Priority | Geotargeting Requirement | Match All Targeting Criteria? | Apply Rule? |
|--|--|--|--|--|
| Conditional Rule 1 | 9 | Florida | No | No |
| Conditional Rule 2 | 8 | Georgia | No | No |
| Conditional Rule 3 | 6 | South Carolina | YES | YES |
| Conditional Rule 4 | 5 | North Carolina | Not checked | N/A |
| Conditional Rule 5 | 2 | Virginia | Not checked | N/A |

The impression is checked against the criteria of **Conditional Rule 1** (highest priority) and finds that it does not match, so it goes to **Conditional Rule 2** (next by priority). That is not a match, so the check proceeds to **Conditional Rule 3**, which matches, so that rule is applied.

> [!IMPORTANT]
> Only one rule can apply to a served impression. The highest priority conditional rule that matches the targeting of the impression will apply. All conditional rules with the same priority are reviewed; when multiple rules with the same priority all meet the impression conditions, a selection as to which rule will be used is made at random.

As a general guideline, rules with a higher number of conditions should be assigned a higher priority, especially if there are matching conditions in multiple rules, to ensure that the most detailed rule is applied to the impression. Assume you have an impression that was served in South Carolina, was seen 12 times on that platform, and is 120x600 in size.

| Conditional Rule | Priority | Geotargeting Requirement | Frequency | Match All Targeting Criteria? | Apply Rule? |
|--|--|--|--|--|--|
| Conditional Rule 6 | 9 | South Carolina | None | **YES** | **YES** |
| Conditional Rule 7 | 8 | Georgia | 10-15 times | No | No |
| Conditional Rule 8 | 6 | South Carolina | 10-15 times | **Not Checked** | **Not Checked** |

In this situation, two rules (**Conditional Rule 6** and **Conditional Rule 8**) match the impression. However, because **Conditional Rule 6** has a higher priority, any impression served in South Carolina will follow this rule, regardless of the frequency or dimension values.

See [Create Payment Rules](create-payment-rules.md) for more information.

## Base rules

It is possible that none of the conditions of the impression meet the criteria of any conditional rules for a publisher. In that case, Monetize defaults to the base rule. For example, assume that you have an impression that was served in Utah.

| Conditional Rule | Priority | Geotargeting Requirement | Match All Targeting Criteria? | Apply Rule? |
|--|--|--|--|--|
| Base Rule | 1 (default) | (No Criteria) | (No Comparison) | **YES** |
| Conditional Rule 10 | 8 | Georgia | No | No |
| Conditional Rule 11 | 6 | South Carolina | No | No |
| Conditional Rule 12 | 5 | North Carolina | No | No |
| Conditional Rule 13 | 2 | Virginia | No | No |
| Conditional Rule 9 | 9 | Florida | No | No |

In this situation, Monetize was unable to match the impression criteria to any existing conditional rules, so the base rule (which has no conditions) is applied.

> [!IMPORTANT]
> The use of geo targeting by state is only one condition used as an example. You could substitute placement, size, or frequency conditions and get the same result.

## Related topics

- [Working with Payment Rules](working-with-payment-rules.md)
- [Create Payment Rules](create-payment-rules.md)
- [Working with Ad Quality](working-with-publisher-ad-quality.md)