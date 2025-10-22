---
title: Bidder Profile - FAQ
description: In this article, explore answers to frequently asked questions about bidder profile, enhancing your understanding of the bidder's profiles.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder profile - FAQ

## Configuration

### How can I find a certain seller's member ID?

You can get all publicly available seller member IDs through the [Platform Member Service](platform-member-service.md).

### How should I set up my bidder profile?

There's no single right way to set up your bidder profile ([Legacy Bidder Profile Service](legacy-bidder-profile-service.md)), but see below for best practices about the fields to use for filtering. Note that these can be used at either the parent or child levels:

- **Filtering by selling member**
  - The `member_targets` array should be populated depending on how you'd like to buy.
    - Buying only a select set of sellers:
      - `"member_targets": [{"id": "100","action": "include"},{"id": "101","action": "include"},{"id": "102","action": "include"}]`
    - Excluding a select group of sellers:
      - `"member_targets": [{"id": "100","action": "exclude"},{"id": "101","action": "exclude"}]`
- **Filtering by country**
  - Set up a global "include" or "exclude" using the `"country_action"` parameter.
  - Add the countries or regions that you would like to include or exclude to the `"country_targets"` array as objects.
    - `"country_targets": [{"country": "GB"},{"country": "US"},{"country": "DE"}]`
- **Filtering by segment**
  - Set the `"segment_boolean_operator"` parameter to either "and or "or".
  - Add the segment(s) that you want to use as filters to the `segment_targets` parameter.
    - `"segment_targets": [{"id": "100","action": "include"},{"id": "101","action": "include"}]`
- **Filtering by size**
  - Include the list of creative sizes for which your bidder has creatives. This list should be exhaustive if you choose to filter by creative size.
    - `"size_targets":[{"width": "100","height": "200"},{"width": "100","height": "200"}]`
- **Filtering by domain list**
  - Include or exclude lists of domains. These are created using the [Domain List Service](domain-list-service.md).
    - `"domain_list_target":[{"id":1}, {"id":2}]`
    - `"domain_list_action":"include"`
- **Filtering by seller classified inventory attributes**
  - This option allows you to opt-in to inventory that has been classified with a sensitive attribute. When `"use_inventory_attribute_targets"` is set to `true`, your bidder will receive traffic from inventory classified with the inventory attributes listed in the `inventory_attribute_targets` array and all unclassified inventory.

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

## Parent and child profiles

You can only have one parent profile and five child profiles assigned to your bidder at any one time.

### Are child profiles required?

No. If there are no child profiles, all impressions that match the parent profile will be sent to your bidder.

### Are parent profiles required?

No. If there is no parent profile, all impressions that match any of the child profiles will be sent to your bidder. If you have no parent profile and no child profiles, all impressions will be sent to your bidder.

> [!NOTE]
> If there is no parent profile in place, the bidder configuration element, `bid_percent`, will be ignored.

### How can I set up my parent and child profiles?

There are a few steps in this process. The first would be deciding on what logic you'd like to use. Read the rest of this FAQ and reach out to your account representatives if you have any questions about best practice. This example will use one parent profile and two child profiles. The parent profile will filter on a segment, and each of the child profiles will have a seller member and geo combination.

The first step is creating the profiles themselves. A profile is an object on the Xandr platform that can be created using the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). The sample below can be used in a `POST` to create the profile.

```
{"profile":{
 "segment_targets": [{"id":"12345","action":"include"}]}}
```

This will return the profile ID in Xandr. We will assume that this profile has ID 100. We will now need to make the child profiles. The following two code samples can be used in POSTs to the bidder profile service.

```
{"profile":{
 "country_action":"include",
 "country_targets": [{"country":"US"},{"country":"CA"}],
 "member_targets": [{"id":1000, "action":"include}]}}
```

and

```
{"profile":{
 "country_action":"include",
 "country_targets": [{"country":"US"}],
 "member_targets": [{"id":2000, "action":"include}]}}
```

We will assume that these two profiles are created and given IDs of 101 and 102, respective. If you are bidder 15, you will need to update your bidder using the [Bidder Service](bidder-service.md). Using the following in a `PUT`, you can update your bidder to have a parent profile with profile 100 and child profiles of profiles 101 and 102 with the following:

```
{"bidder":{
 "id":15,
 "parent_profile_id":100,
 "child_profiles":[{"id":101},{"id":102}]
}}
```

### How do I set child profiles?

Create the profiles that you want to be your child profiles using the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). Each profile will have an ID. Update the `child_profiles` in the [Bidder Service](bidder-service.md) to have the full array of objects specifying all of the child profiles - e.g. `[{"id":123},{"id":456},{"id":789}]`. You must specify the full list of ids that you want to be child profiles in every update to the `child_profiles` in the bidder service.

### How do I set my parent profile?

Create the profile that you want to be your parent profile using the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). This will return the ID of that particular profile. Update the `parent_profile_id` in the [Bidder Service](bidder-service.md) to use the ID of the profile you created.

### How should I set up my parent and child profiles?

This depends on your business logic. Common examples include:

- Setup 1 - Filter on segments and countries or regions at parent level, include seller-specific restrictions at child levels.
  - Parent profile: Include segment 1 and segment 2; include countries or regions A, B, C and D.
  - Child profile 1: Include seller E; include domain list F; include countries or regions  B and C.
  - Child profile 2: Include sellers F, G, exclude domain list H; allow all countries or regions.
  - Child Profile 3: Include sellers I, J, K; include countries or regions A and D, include domain list L.
- Setup 2 - Filter on countries or regions, exclude sellers at the parent level.
  - Parent profile: Include countries or regions A, B, C; exclude sellers D and E.
  - No child profiles.
- Setup 3 - Filter on domain list only.
  - Parent profile: Include domain list A.
- Setup 4 - User must be in either segment 1 or segment 2. There is also an exlcusion segment 3 (e.g. user's who have previously converted) - user must not be in that segment.
  - Parent profile: Segment boolean operator, OR. Include segment 1, include segment 2.
  - Child profile: Exclude segment 3.

### What's the relationship between parent and child profiles?

If an impression passes the parent profile, it will be sent to the bidder if:

1. There are no child profiles.
1. Or, at least one of the child profiles allows the impression to be sent.

If the impression is blocked by the parent profile, it will not be sent to the bidder - even if it is explicitly allowed by a child profile. This relationship can be summed up with the following boolean logic: Parent AND (Child-1 OR Child-2 OR ... OR Child-n)

## Updating a bidder profile

### How can I make a change to my bidder profile?

You can update your bidder profile by making a `PUT` call to the bidder profile service. The `PUT` call must include only:

1. The ID of the profile.
1. And, the field that you want to change. You must include the value that you'd like the changed field(s) to be. If you are changing an array, this means that every value of the array after the change must be sent in the `PUT`.
