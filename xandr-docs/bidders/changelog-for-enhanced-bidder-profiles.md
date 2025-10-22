---
title: Changelog for Enhanced Bidder Profiles
description: This page covers changes in Legacy Bidder Profile Behavior and Enhanced Bidder Profile Behavior in tabular form.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Changelog for Enhanced Bidder Profiles

Document to cover all changes between legacy bidder profiles and Enhanced Bidder Profiles.

## Changes in targeting

| Category | Legacy Bidder Profile Behavior | Enhanced Bidder Profile Behavior | More information |
|--|--|--|--|
| # of Fields | 30+ targetable fields | 11 targetable fields | [Enhanced Bidder Profiles](enhanced-bidder-profiles.md) |
| Ad Type Targeting | - No explicit way to target or block ad types <br> - User could target the 1x1 size for native/video creatives | - Explicit ad type targeting field <br> - User must explicitly exclude an ad type in the bidder profile to not receive that type of traffic | [Hierarchy and Ad Type Targeting](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md) |
| Country Targeting | Can include/exclude a list of countries or regions | Behavior remains the same as legacy profile behavior |  |
| Domain List Targeting | Can include/exclude domain lists | Behavior remains the same as legacy profile |  |
| Inventory Attributes Targeting | Can include/exclude inventory attributes | Behavior remains the same as legacy profile |  |
| Nonaudited Url Action | If this is set to "exclude", all inventory that has not been audited by Xandr will be excluded. Otherwise, all inventory will be included. | Behavior remains the same as legacy profile |  |
| Passthrough Percent | The percent (50 = 50%) of bid requests which satisfy your profile targeting that you receive, set in increments of 0.1. Requests sent are randomly chosen, although you can choose to always receive requests for users in segments of members associated with your bidder. If set to 0, you will only receive requests for users in your members' segments. | Not available. Bidder should use QPS caps instead. | [Bidder Instance Service](bidder-instance-service.md) |
| Segment Targeting | - Could either AND or OR across targeted segments <br> - Could either include/exclude on individual segments | Not available. |  |
| Seller Targeting | Can include/exclude individual seller members | - Can target "Exchanges" <br> - Can still include/exclude certain members <br> - Can not individually include members who belong to the Direct Exchange (ID 1) | [Exchange Service](exchange-service.md) |  |
| Size Targeting | Size targets apply to all ad types | - Size targets are specific to banner and video <br> - Size targets for banner/video are set separately <br> - User can not target size 1x1 or 0x0. | [Hierarchy and Ad Type Targeting](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md) |  |
| Supply Types Targeting | Can include/exclude supply Types | Behavior remains the same as legacy profile |

## Change in logic

| Category | Legacy Bidder Profile Behavior | Enhanced Bidder Profile Behavior | More information |
|--|--|--|--|
| Hierarchy | - Uses a parent/child hierarchy <br> - The parent profile must be met along with one of the child profiles in order to send impression | - Flat structure <br> - Impression must meet requirements of a single profile | [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md) |

## Changes in Bidder object

The bidder object in reference is documented here: [Bidder Service](bidder-service.md)

| Category | Legacy Bidder Profile Behavior | Enhanced Bidder Profile Behavior |
|--|--|--|
| Activating Profile | Profile must be attached to the bidder object in either the parent or child profiles field | Set active=1 on the profile in order to activate it. No modification is needed to the bidder object. |
| always_send_owned_segments | - Overrides the passthrough percent on the bidder profile <br> - Bidder will always receive traffic with a user in an owned or shared segment | - Field is moved over to the profile: "user_not_in_segment_action" <br> &nbsp;&nbsp;&nbsp;- If include: Send the impression regardless of whether the user exists in a segment owned by or shared with the bidder. All other fields in the bidder profile should be taken into account. <br><br> &nbsp;&nbsp;&nbsp;- If exclude: Only send impressions where the user exists in a segment owned by or shared with the bidder. QPS restrictions should apply to this field. The bidder doesn't have to explicitly state the segment in the segment actions. Impressions where the user does not exist in a segment owned by or shared with the bidder should not be sent. All other fields on the bidder profile will be taken into account. <br><br> - The "always_send_owned_segments" field in the bidder object will be ignored. |
| override_for_deals | Determines whether or not to use the bidder profile to determine if a bid request should be sent. Deals are usually negotiated directly between sellers and buyers and are generally not subject to bidder profile restrictions. <br> - `true`: Ignore the bidder profile and send bid request regardless of bidder profile <br> - `false` (default): Use bidder profile to determine whether the bid request should be sent | No change; behavior is the same as in legacy profile |

## Related topics

- [Enhanced Bidder Profiles](enhanced-bidder-profiles.md)
- [Exchange Service](exchange-service.md)
- [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)
- [API Use Cases for Enhanced Bidder Profiles](api-use-cases-for-enhanced-bidder-profiles.md)
- [Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles](frequently-asked-questions-faq-for-enhanced-bidder-profiles.md)
