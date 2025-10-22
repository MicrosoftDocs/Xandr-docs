---
title: Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles
description: Explore organized seller groups, target supply, and overview FAQs on Enhanced Bidder profiles for efficient engagement.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Frequently asked questions (FAQ) for enhanced Bidder profiles

## How do I know which bidder profile version I am using?

Your account manager and services partner should have already discussed this with you.

## Can I use legacy bidder profiles and enhanced bidder Profiles at the same time?

No, a bidder can only be on one version of the bidder profile. This prevents conflicting logic and confusion.<br><br>If you are a bidder on legacy bidder profiles, the profiles listed in `bidder.child_profiles` and `bidder.parent_profile_id` will be used on your bidder object.<br><br>If you are a bidder on Enhanced Bidder Profiles, your profiles with active set to `true` in the `/bidder-profile` API service are in effect.

## What changes happened between the legacy and enhanced bidder Profiles?

All changes have been documented here: [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md).

## What fields in the bidder object changed?

All changes have been documented here: [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md).

## Where can I contribute feedback about enhanced bidder Profiles?

Reach out to your account manager or services partner with any feedback.

## What fields are you keeping vs removing?

You can see a list of all fields in Enhanced Bidder Profiles here: [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md).

## Why can't I target Microsoft in the included members array?

All members that belong to the Direct Exchange (Exchange 1) are on a blocklist only. This means that you can not add those members in the `excluded_members` array on the new bidder profiles. You can see more information about Exchanges here: [Exchange Service](exchange-service.md).

## Is a bidder profile active as soon as I POST it?

No, new profiles that are added are inactive by default (active: `false`). You will have to set active to `true` in order to activate it.

## Do the `{$MATCHED_PROFILE_CODE}` and `{$MATCHED_PROFILE_ID}` macros work with the new profiles?

Yes, we will still populate both those macros. However, we will only populate with one ID/code if several profiles match.

## How can I access my profile in?

You can access your profile in our new Bidder Platform UI: [Xandr Bidder Login](https://bidder.appnexus.com/login).

## How can I switch from the legacy bidder profiles to Enhanced Bidder Profiles?

Review the steps here: [Bidder Profile Migration Guide](bidder-profile-migration-guide.md).

## Related topics

- [Enhanced Bidder Profiles](enhanced-bidder-profiles.md)
- [Exchange Service](exchange-service.md)
- [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)
- [API Use Cases for Enhanced Bidder Profiles](api-use-cases-for-enhanced-bidder-profiles.md)
- [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md)