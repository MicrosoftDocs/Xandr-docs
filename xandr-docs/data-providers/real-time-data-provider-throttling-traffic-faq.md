---
title: Real Time Data Provider Throttling Traffic FAQ
description: In this article, explore answers to frequently asked questions (FAQS) about real time data provider throttling traffic.
ms.custom: data-providers
ms.date: 10/28/2023
---

# Real time data provider throttling traffic FAQ

## How should I set up my bidder profile?

There's no single right way to set up your bidder profile ([Legacy Bidder Profile Service](../bidders/legacy-bidder-profile-service.md)), but see below for best practices about the fields to use for filtering:

- **Filtering by selling member**
  - The `member_targets` array should be populated depending on how you'd like to buy.
    - Buying only a select set of sellers:

      `"member_targets": [{"id": "100","action": "include"},{"id": "101","action": "include"},{"id": "102","action": "include"}]`

    - Excluding a select group of sellers:

      `"member_targets": [{"id": "100","action": "exclude"},{"id": "101","action": "exclude"}]`
- **Filtering by country**
  - Set up a global `"include"` or `"exclude"` using the `"country_action"` parameter.
  - Add the countries or regions that you would like to include or exclude to the `"country_targets"` array as objects.
    - `"country_targets": [{"country": "GB"},{"country": "US"},{"country": "DE"}]`
- **Filtering by size**
  - Include the list of creative sizes for which your bidder has creatives. This list should be exhaustive if you choose to filter by creative size.
    - `"size_targets":[{"width": "100","height": "200"},{"width": "100","height": "200"}]`
- **Filtering by domain list**
  - Include or exclude lists of domains. These are created using the [Domain List Service](../bidders/domain-list-service.md).
    - `"domain_list_target":[{"id":1}, {"id":2}]`
    - `"domain_list_action":"include"`
- **Filtering by seller classified inventory attributes**
  - This option allows you to opt-in to inventory that has been classified with a sensitive attribute. When `"use_inventory_attribute_targets"` is set to `true`, your bidder will receive traffic from inventory classified with the inventory attributes listed in the `inventory_attribute_targets` array and all unclassified inventory.

  - For example, if you wanted to receive bid requests from all inventory except that inventory classified as Toolbar, you should adjust your bidder profile to contain the following information:

    ```
    "use_inventory_attribute_targets": true,
    "inventory_attribute_targets": [
                {
                    "id": 2,
                    "name": "Political"
                },
                {
                    "id": 4,
                    "name": "Social media"
                },
                {
                    "id": 6,
                    "name": "Photo & video sharing"
                },
                {
                    "id": 8,
                    "name": "Forums (moderated)"
                },
                {
                    "id": 10,
                    "name": "Forums (unmoderated)"
                },
                {
                    "id": 12,
                    "name": "Incentivized clicks"
                },
                {
                    "id": 14,
                    "name": "Non-english languages"
                },
                {
                    "id": 16,
                    "name": "Streaming media"
                }
            ]
    ```

- **General notes**
  - Once you have included any item in any array, you don't need to exclude items you don't want to see, as only those that are explicitly included will be sent.
  - Do not set the action to be "include" if you haven't set any targets to include. For example, `country_action` should not be include if `country_targets` has no elements.

## How can I find a certain seller's member ID?

You can get all publicly available seller member IDs through the [Platform Member Service](../bidders/platform-member-service.md).

## How can I make changes to my bidder profile?

You can update your bidder profile by making a `PUT` call to the [Legacy Bidder Profile Service](../bidders/legacy-bidder-profile-service.md). The `PUT` call must include only:

1. The ID of the profile.
1. The field that you want to change.

You must include the value that you'd like the changed field(s) to be. If you are changing an array, this means that every value of the array after the change must be sent in the `PUT`.

## Can I associate child profiles with my real time data provider?

No, data provider bidders may only be associated with a parent profile.

## Can I have different throttling levels for different geographies in the same datacenter?

Unfortunately this is not possible for real time data providers as they cannot have child profiles under their parent profile.

## How can I set different throttling settings for each datacenter?

You may only have one profile. You may attempt to set different throttling levels for datacenters by blocking IP addresses through your bidder's ACL settings. For example, if you want to listen to 80% of traffic in NY and 60% of traffic in AMS then you should progressively inch the filter percentage of your bidder up to 80% as well as block IPs in the AMS datacenter so that traffic from AMS is only at 60%. To determine what IP addresses to block, contact your Xandr Account Manager. You may block them through the Rule Builder in the Network section of the Xandr Portal.

## What is dynamic throttling?

For traffic that is not throttled through a data providers bidder profile, bid requests will under-go dynamic bidder throttling if the bidder has dynamic throttling enabled (which all data provider bidders do). Dynamic bidder throttling only impacts bid requests (e.g. it does not affect ready requests) and is driven by a 100 request sliding window average of timeout percentages. For example, if 50% of the last 100 bid requests timed out, then there is a 50% probability that the next request will be sent to the bidder (and a 50% probability that it will not be sent out).

## How do I enable/disable dynamic throttling for a real time data provider?

By default, dynamic throttling is initially enabled for all data providers. [Submit a Support Request](https://help.xandr.com/s/login/) to request enabling/disabling the feature for your data provider bidder.

## Does dynamic throttling always affect incoming bid requests?

No, very high and very low timeout rates are handled as special cases. If a bidder's timeout percentage falls below 5%, then none of the bid requests sent are dynamically throttled. On the other hand, if a bidder's timeout percentage goes above 90%, then we will send a minimum 10% of traffic regardless of how high the timeout rate becomes until the timeout rate dips below 90% (when we will reengage dynamic throttling).

## I wish to listen for a particular supply type (e.g. web or mobile-app), how should I proceed?

The best way to proceed is to exclude undesirable supply types through the `"supply_type_action"` and `"supply_type_targets"` parameters through [Legacy Bidder Profile Service](../bidders/legacy-bidder-profile-service.md). However, keep in mind that since there is supply (mostly `"web"`) that is of unmarked supply type, when you will include this supply type you will miss on this unmarked supply.

## Can RTDPs listen to Facebook traffic?

Real-time Data Providers by default cannot listen to traffic incoming from Facebook.
