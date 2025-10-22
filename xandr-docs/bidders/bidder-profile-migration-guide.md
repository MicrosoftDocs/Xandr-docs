---
title: Bidder Profile Migration Guide
description: In this article, explore step-by-step guidance for the Bidder profile migration process, ensuring a seamless transition for optimal performance.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder profile migration guide

Bidder Profiles (both the legacy Profile Service and Enhanced Bidder Profiles) allow you to filter traffic you receive from Xandr. This profile migration guide helps you migrate your setup from the legacy Bidder Profiles over to Enhanced Bidder Profiles.

> [!NOTE]
> **Step 4** on this page is only relevant if you received a Breaking Change email communication about the profile migration. If you did not, contact your account manager instead.
>
> Breaking Change Notice: If You Don't Complete the Migration:
>
> On October 4th, 2019, we will enable your bidder for Enhanced Bidder Profiles, at which point your new profile(s) will control how you receive traffic, and your legacy profiles will be deprecated. If you do not update your Enhanced Bidder Profiles before this date, by default your bidder will have no inventory restrictions configured.

## Migration process overview

1. Get the current state through legacy Profile Service API (recommended) or legacy Bidder UI. (0.25~0.5 hours)
1. Understand the changes and re-evaluate the filters based on your business needs. (0.5~1 hours)
1. Set up Enhanced Bidder Profiles in new Bidder Platform UI (recommended) or via new Bidder Profile Service. (0.5~1 hours)
1. Contact Support to flip the switch from using legacy Profiles to Enhanced Bidder Profiles. (~1 business day)

Your new Enhanced Bidder Profile configuration in or API does NOT impact the traffic flow until you complete the Step 4 before May 21st, 2019.

## Migration process

### Step 1: Get the Current State (0.25~0.5 hours)

There are two ways to check the current state. We recommend the API method since the legacy UI may not show all of your targeting parameters.

> [!TIP]
> Understanding the Relationship Between Parent & Child Profile in Legacy Bidder Profile
>
> In legacy Bidder Profiles, there are parent profile and (optional) child profile(s). All incoming traffic from Xandr must meet the conditions in the parent profile first. In addition, the traffic must pass one of the child profiles if your bidder has active child profiles. To summarize, traffic is sent when it meets the criteria in
> `(Parent Profile) AND (Child Profile 1 OR Child Profile 2 OR ... OR Child Profile N)`.
>
> Example:
>
> If you include the United States in your parent profile, include the Mobile App supply type in your child profile 1, and include the Mobile Web supply type in your child profile 2, your bidder will receive both US mobile app traffic (through child profile 1) and US mobile web traffic (through child profile 2). Your bidder will not receive any US Desktop traffic or any non-US traffic.
>
> For more information, refer to the Legacy [Bidder Profile FAQ](bidder-profile---faq.md).

#### Method 1: Using API (Recommended)

##### Overview

- Get the active profile objects through Bidder Service API: `GET` bidder/\[bidder id\].
- For all active profile objects, `GET` profile/\[profile id\] through legacy Bidder Profile Service API.
- Summarize the results.

##### Step 1.1: Get the active profile objects through Bidder Service API: `GET` bidder/\[bidder id\]

Active parent profile id is in the `parent_profile_id` field, and active child profile ids are in the `child_profiles` array.

Reference: [Authentication Service](authentication-service.md) and [Bidder Service](bidder-service.md).

###### Example

```
-> curl -b cookie -c cookie -s "https://api.adnxs.com/bidder/129" # 129 is a sample bidder ID.
{
    "response": {
        "bidder": {
            ...
            "parent_profile_id": 12345,
            "child_profiles": [
                {
                    "id": 34567
                },
                {
                    "id": 56789
                }
            ],
            ...
        }
    }
}
```

##### Step 1.2: For all active profile objects, `GET` profile/\[profile id\] through legacy Bidder Profile Service API

Each profile has an allowlist and/or blocklist of items. There are usually “action” and “targets” per member, country or region, etc.

- "...\_action" can be set to “include” or “exclude”.
- "...\_targets" can have a list of IDs for seller member, country or region, etc.

Reference: [Legacy Bidder Profile Service](legacy-bidder-profile-service.md)

###### Step 1.2: Example

```
-> curl -b cookie -c cookie -s "https://api.adnxs.com/profile/129/12345" # 129 is a sample bidder id and 12345 is a sample bider profile ID.
{
    "response": {
        "profile": {
            "country_action": "include",
            "country_targets": [
                {
                    "active": true,
                    "code": "US",
                    "id": 233,
                    "name": "United States"
                }
            ],
            ...
        }
    }
}
```

##### Step 1.3: Summarize the results

Remember to evaluate the parent & child profile logic: traffic is sent when it meets the criteria in `(Parent Profile) AND (Child Profile 1 OR Chile Profile 2 OR ... OR Child Profile N)`.

There are multiple deprecated fields in the legacy Profile API service. We recommend you only focus on these targetable fields below. There is a guide to which exact fields to look at in the Mapping of Legacy To Enhanced Bidder Profile Fields section on this page.

To make it easier to set up the new Enhanced Bidder Profiles, for each of these fields, list included/excluded attributes:

- Seller Members
- Countries/Regions
- Domain Lists
- Sizes
- Supply Types
- Inventory Attributes
- Known Users Only
  > [!NOTE]
  > If you're listening to known users only, you have a 0% passthrough rate in your bidder profile.
- Non-Audited URL Action

> [!TIP]
> What is AppNexus Direct?
>
> Depending on your legacy profile setup, Xandr's direct supply may be included in your profile object, in addition to your included seller members. For more information, see: [Microsoft Monetize Supply for External Demand Partners](xandr-monetize-supply-for-external-demand-partners.md).
>
> In the new Bidder Platform UI, you will be able to see which seller members belong to Xandr's "direct" exchange group.
>
> How to pull the domains in your domain list?
>
> If you would like to review the domains in your domain list, you can get or edit the list via the domain-list API service:
> [Domain List Service](domain-list-service.md).

#### Method 2: Using the legacy bidder UI

##### Overview (Method 2)

- See the current filters in each bidder profile.
- Summarize the results.

##### Step 1.1: See the current filters in each bidder profile

Go to [https://bidder.adnxs.net/](https://bidder.adnxs.net/) and log in with your bidder user credentials. If you cannot log in, check with your company's integrations team first and contact Xandr Support.

Navigate to the Profiles tab on the left. You can see the parent profile setup.

Non-italic child profiles are currently active. If you click on a child profile, you can see the profile setup.

##### Step 1.2: Summarize the results

Remember to evaluate the parent & child profile logic: All incoming traffic from Xandr must meet the conditions in the parent profile first; in addition, the traffic must pass one of the child profiles if you have child profiles set up.

To make it easier to set up the new Enhanced Bidder Profiles, for each of these fields, list included/excluded attributes:

- Seller Members
- Countries/Regions
- Domain Lists
- Sizes
- Supply Types
- Inventory Attributes
- Known Users Only
  > [!NOTE]
  > If you're listening to known users only, you have a 0% passthrough rate in your bidder profile.
- Non-Audited URL Action

> [!TIP]
> What is AppNexus Direct?
>
> You may not see it in the legacy Bidder UI, but in addition to the seller member targeting in a profile, seller members from Xandr's direct supply are included in a profile. For more information, see: [Microsoft Monetize Supply for External Demand Partners](xandr-monetize-supply-for-external-demand-partners.md).
>
> In the new Bidder Platform UI, you will be able to see which seller members belong to Xandr's "direct" exchange group.
>
> How to pull the domains in your domain list?
>
> If you would like to review the domains in your domain list, you can get or edit the list via the domain-list API service:
> [Domain List Service](domain-list-service.md).

### Step 2: Understand the changes and re-evaluate the filters (0.5~1 hours)

Enhanced Bidder Profiles offers the following benefits:

- Flat Hierarchy: The parent and child profile model has been removed.
- Ad Types: You can now easily target the four main ad types you wish to receive: Banner, Video, Native, and Audio.
- Exchanges: We have grouped seller members into Exchanges for easier targeting.
- Simplified Profile: We have narrowed down the profile to only relevant fields for your business.
- New Bidder Platform UI: We have built a new UI for you to manage and maintain your profiles. Additional capabilities will be added to this UI throughout 2019.

Review these pages first: [Change Log for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md) and [Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles](frequently-asked-questions-faq-for-enhanced-bidder-profiles.md).

### Step 3: Set Up Enhanced Bidder Profiles (0.5~1 hours)

> [!NOTE]
> Enhanced Bidder Profile setup in new Bidder Profile Service API or new Bidder Platform UI does NOT affect the traffic flow from Xandr until you complete Step 4: Contact Xandr Support and we flip the switch in the backend before May 21st, 2019.

There are two ways to set up Enhanced Bidder Profiles. We recommend using the new Bidder Platform UI over API.

- Bidder Platform User Interface (Recommended): [https://bidder.appnexus.com/login](https://bidder.appnexus.com/login)
  - [Bidder Platform User Interface](bidder-platform-user-interface.md)
  - [Profiles Screen](profiles-screen.md)
- New [Bidder Profile Service API](enhanced-bidder-profiles.md)

### Using multiple profiles in enhanced bidder profile

Impression must meet requirements of a single profile to be sent to your bidder. If you create multiple profiles, the logic between the profiles is OR. In other words, impression is sent when it meets the criteria in `(Profile 1 OR Profile 2 OR ... Profile N).`

### Mapping of legacy to enhanced bidder profile fields

| Targeting | Legacy Bidder Profile API fields | Enhanced Bidder Profile UI & API fields |
|:---|:---|:---|
| Seller Members/Groups | `member_targets` and `seller_member_group_targets` fields in API | Exchanges and Members tab in. All seller members belong to one of the three Exchanges, and you can see which seller members belong to each Exchange in.<br>`exchanges` field in API (For member-level control, use `excluded_members` and `included_members` arrays under exchanges). |
| Countries | `country_action` field has `include` or `exclude`.<br>`country_targets` array has a list of countries or regions. | Countries tab in.<br>`countries` field in API. (Use `action` and `targets` under `countries`. For targets, use ids retrieved from [Country Service](country-service.md).) |
| Domain Lists | `domain_list_action` field has `include` or `exclude`.<br>`domain_list_targets` array has a list of domain list. Use [Domain List Service](domain-list-service.md) to create, view, or edit domains. | Domain Lists tab in (To edit domains, use [Domain List Service](domain-list-service.md)).<br>`domain_lists` field in API. (Use `action` and `targets` under `domain_lists`. For targets, use ids retrieved from [Domain List Service](domain-list-service.md).) |
| Sizes (and Ad Types) | `size_targets` array (include only). | Ad Types tab in. You can first select Ad Types to include. If you include Banner ad type, you can select sizes to include.<br>`ad_types` field in API. For each ad type, set `action` to `include` or `exclude`. For `banner` ad type, you can include sizes in the `sizes` array. |
| Supply Types | `supply_type_action` field has `include` or `exclude`.<br>`supply_type_targets` array has web, mobile web, or mobile app. | Supply Types tab in .<br>`supply_types` field in API. (Use `action` and `targets` under `supply_types`. For targets, possible values are `web`, `mobile_web`, and `mobile_app`.) |
| Inventory Attributes | `use_inventory_attribute_targets` has true or false.<br>`inventory_attribute_targets` array has a list of inventory attributes (include only). | Sensitive Attributes tab in .<br>`inventory_attributes` field in API. (Action is include only. For targets, use ids retrieved from [Inventory Attribute Service](inventory-attribute-service.md).) |
| Receiving Known Users Only | If `passthrough_percent` field has 0 and your Bidder object has `always_send_owned_segments` set to true, you're listening to known users only.<br>Alternatively, your bidder profile may include a segment id to target known users only. | **Note:** To use this feature, you must be using/setuid url with Xandr for user matching.<br><br>Unknown Users toggle in. Set `Allow Unknown Users` to excluded.<br>`user_not_in_segment_action` field in API. Set to `exclude` to listen to known users only. |
| Non-Audited URL Action | `non_audited_url_action` field in API. | `non_audited_url_action` field in API. |

### Adjusting traffic volume: Passthrough percent alternative

In legacy Bidder Profile, some clients used `passthrough_percent` to control traffic volume or bid request QPS (query per second). Enhanced Bidder Profile does not have a volume control feature; instead, use the **`qps_limit`** field in [Bidder Instance](bidder-instance-service.md) to set up a QPS safety cap per datacenter. To see your current traffic volume, see the Metrics tab in the legacy bidder UI: [https://bidder.adnxs.net/metrics](https://bidder.adnxs.net/metrics).

If you have QPS safety caps in all bidder instances, you have an option to enable the Optimized Bid Stream feature. All traffic is sent until your QPS cap is met; when there is more available traffic than your QPS cap, instead of cutting off the traffic volume randomly to meet your QPS cap, low priority traffic based on your buying behavior that exceeds your QPS cap will be cut. For more information, see [Optimized Bid Stream FAQ](optimized-bid-stream-faq.md). If you're interested in the feature, contact your account manager or Xandr Support.

### Activating a new bidder profile

To activate a new Bidder Profile in API, set the **active** field to `true`. You no longer need to set a profile id in [Bidder Service](bidder-service.md) API to activate a profile. Once the step 4 below is complete, `parent_profile_id` and `child_profiles` in Bidder API object will be ignored.

You need to click on the Activate button in the profile screen to activate the profile. Non-italic profiles are active.

Activate your new Bidder Profiles before moving onto step 4. Your Enhanced Bidder Profile setup does not impact the traffic flow until the backend switch is flipped by Xandr Support in Step 4 before May 21st, 2019.

### Step 4: Contact Xandr support to complete the migration (~1 business day)

> [!NOTE]
> This section is only relevant if you received a Breaking Change email communication about profile migration. Do not follow this step if you did not. Instead, contact your account manager.
> [!WARNING]
> Your new Enhanced Bidder Profile setup does not impact the traffic flow until you complete this step before May 21st, 2019.

Open a support ticket. When entering information:

- Category: Select Product Support
- What Can We Help With?: Select External Bidder Integration

#### Use this template for your support ticket

I have reviewed and configured Enhanced Bidder Profiles. Migrate my profile setup.

1. Bidder ID and bidder name:
1. Did you configure using new Bidder Platform UI or API?:
1. Provide a brief explanation of the changes from the current profile setup (if no change, write "N/A"):

#### What will happen next?

Our support specialists will review the legacy and Enhanced Bidder Profile setup first. If they look good, support specialists will flip the switch in the backend and send a confirmation note to you. When this happens, your new Enhanced Bidder Profile configuration will start taking affect on the traffic flow, and the legacy bidder profile setup will be ignored.

Monitor your traffic flow using the Metrics tab in the legacy bidder UI: [https://bidder.adnxs.net/metrics](https://bidder.adnxs.net/metrics). If there is any problem, support specialists can switch back to the legacy profile setup immediately (which will take effect on the traffic flow in 5-10 minutes), and you can work on troubleshooting the Enhanced Bidder Profile setup.

If there's no problem on the traffic flow for a day, your migration is complete, and the support ticket will be closed.

> [!TIP]
> Legacy bidder profiles will still be shown as active in API and in the legacy Bidder UI after the migration is complete. As long as it's migrated in the backend, the legacy profile setup is ignored and does not impact the traffic flow.

#### If you do not complete Step 4

On May 21st, 2019, we will enable your bidder for Enhanced Bidder Profiles, at which point your new profile(s) will control how you receive traffic, and your legacy profiles will be deprecated. If you do not update your Enhanced Bidder Profiles before this date, by default your bidder will have no inventory restrictions configured.
