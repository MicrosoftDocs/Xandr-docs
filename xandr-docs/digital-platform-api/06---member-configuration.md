---
title: Member Configuration
description: In this article, learn about member configuration and explore detailed information about the various parameters configured at the member level.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member configuration

Prior to creating any objects via the API, it is best practice to fully configure the member first. The reason for this is that there are defaults that can be specified on a member level which cascade to child objects under the member.

There are a number of different parameters which can be configured at the member level:

## No reselling priority

This setting, stored in the `"no_reselling_priority"` parameter, specifies the priority at which managed impressions will never be resold. Put another way, if there is a campaign at or above this priority which is eligible to serve, it will always serve above any RTB campaigns from other buyers. Among managed campaigns of the same priority, the usual auction mechanics still apply. The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "no_reselling_priority": 5
  }
}
```

## Content categories

This parameter, stored in the `"content_categories"` parameter, defines the list of custom content categories that can be used to categorize managed inventory.

> [!NOTE]
> These categories will not be targeted by other buyers.

The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "content_categories": [
      {"id":"2950","name":"Animals"},
      {"id":"2951","name":"Arts & Humanities"},
      ... ,
      {"id":"2977","name":"Travel"}
    ]
  }
  }
```

## Standard sizes

This setting, stored in the `"standard_sizes"` parameter, specifies the creative and placement sizes which are shown in. The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "standard_sizes": [
      {"width": "120", "height": "600", "is_standard": true},
      {"width": "160", "height": "600", "is_standard": true},
      ... ,
      {"width": "728", "height": "90", "is_standard": true},
      {"width": "800", "height": "60", "is_standard": false}
    ]
  }
  }
```

## Timezone

This parameter, stored in the `"timezone"` field, defines the default timezone that will be applied to newly created objects unless otherwise specified at the time of their creation. For a list of valid timezone values, see [API Timezones](api-timezones.md). The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "timezone": "EST5EDT"
  }
  }
```

## Dongle

The dongle is used as a password for debugging auctions. This password is used on a placement call on the querystring prompting our platform to simulate an auction and display how we are bidding on that tag. It is useful for determining why a campaign is not bidding on certain inventory. The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "dongle": "keepitsecret"
  }
  }
```

## Platform exposure

The platform exposure setting determines how your account is displayed to other members on the platform. There are three values which result in slightly different behaviors as outlined below:

| Platform Exposure Value | Behavior |
|:---|:---|
| public | Member is displayed using the billing name. |
| private | Member is displayed as "Member 123" where 123 is the member ID. |
| hidden | Member is not displayed. |

The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "platform_exposure": "public"
  }
}
```

## Default currency

The default currency, like the timezone, is applied to advertisers and line items unless otherwise specified when creating those objects. The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "default_currency": "USD"
  }
  }
```

## Use Insertion Orders

This setting, stored in the `"use_insertion_orders"` parameter, specifies whether or not insertion orders should be used on all advertisers within the account. This setting is also available on an advertiser-by-advertiser basis. The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "use_insertion_orders": false
  }
  }
```

## Summary example

Below is a summary of the JSON samples above into a single member object. For this example, the member specification is in a text file.

```
$cat member
{
  "member": {
    "no_reselling_priority": 5,
    "content_categories": [
      {"id":"2950","name":"Animals"},
      {"id":"2951","name":"Arts & Humanities"},
      ... ,
      {"id":"2977","name":"Travel"}
    ],
    "standard_sizes": [
      {"width": "120", "height": "600", "is_standard": true},
      {"width": "160", "height": "600", "is_standard": true},
      ... ,
      {"width": "728", "height": "90", "is_standard": true},
      {"width": "800", "height": "60", "is_standard": false}
    ],
    "timezone": "EST5EDT",
    "dongle": "keepitsecret",
    "platform_exposure": "public",
    "default_currency": "USD",
    "use_insertion_orders": false
  }
}
```

In order to make the modifications, you should `PUT` the member specification to the API.

```
$ curl -b cookies -c cookies -X PUT --data-binary @member 'https://api.appnexus.com/member?id=123'
{
   "response":{
      "status": "OK",
      "id": 1234
   }
}
```

To verify that the changes were made, you can pull down the member from the API using a `GET` request.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/member?id=123'
{
  "response": {
    "status": "OK",
    "member": {
      "id": 123,
      "name": "Member",
      "whitelabel_support_email": null,
      "reselling_description": null,
      "state": "active",
      "expose_ixi_support": false,
      "enable_advertisers": true,
      "no_reselling_priority": 5,
      "entity_type": "reseller",
      "expose_global_inventory_sources": true,
      "buyer_clearing_fee_pct": null,
      "default_placement_id": null,
      "default_buyer_group_id": 0,
      "max_daily_credit_pct": 0,
      "interface_domain": null,
      "interface_domain_beta": null,
      "content_categories": [
        {"id":"2950","name":"Animals"},
        {"id":"2951","name":"Arts & Humanities"},
        ... ,
        {"id":"2977","name":"Travel"}
      ],
      "dw_member": true,
      "contracts": [
        {
          "id": 75,
          "start_date": "2010-01-01 00:00:00",
          "end_date": null,
          ...
        }
      ],
      "default_inv_source_id": null,
      "default_ad_profile_id": null,
      "email_code": null,
      "serving_domain": null,
      "contract_approved": true,
      "reselling_exposure": "public",
      "reselling_exposed_on": "0000-00-00 00:00:00",
      "last_modified": "2011-07-13 16:00:43",
      "standard_sizes": [
        {"width": "120", "height": "600", "is_standard": true},
        {"width": "160", "height": "600", "is_standard": true},
        ... ,
        {"width": "728", "height": "90", "is_standard": true},
        {"width": "800", "height": "60", "is_standard": false}
      ],
      "buyer_credit_limit": 1000000,
      "timezone": "EST5EDT",
      "seller_revshare_pct": 95,
      "is_billable": true,
      "note": null,
      "default_country": null,
      "dongle": "keepitsecret",
      "primary_type": "buyer",
      "platform_exposure": "public",
      "contact_email": null,
      "allow_ad_profile_override": true,
      "account_owner_user": null,
      "default_currency": "USD",
      "use_insertion_orders": false,
      "expose_optimization_levers": false,
      "pops_enabled_UI": false,
      "default_accept_supply_partner_usersync": true,
      "default_accept_data_provider_usersync": true,
      "default_accept_demand_partner_usersync": true,
      "short_name": "",
      "expose_eap_ecp_placement_settings": false,
      "daily_imps_verified": null,
      "daily_imps_self_audited": null,
      "daily_imps_unaudited": null,
      "is_iash_compliant": false,
      "deal_types": null,
      "allow_non_cpm_payment": true,
      "default_allow_cpc": true,
      "default_allow_cpa": true,
      "visibility_profile_id": 15,
      "inventory_trust": {
        "default_trust": "appnexus",
        "default_allow_unaudited": false,
        "default_is_banned": false,
        "members": [...]
      },
      "default_campaign_trust": "appnexus",
      "default_campaign_allow_unaudited": false,
      "contract_allows_unaudited": true,
      "enable_budget_check": false,
      "active_contract": {
        "auditing_fee_per_creative": 1,
        "creative_priority_fee_1": 25,
        "creative_priority_fee_2": 25
      },
      "allow_priority_audit": false,
      "enable_mobile_ui": false,
      "audit_notify_email": null,
      "default_external_audit": false,
      "contact_info": null
    },
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "dbg_info": {
      ...
    }
  }
}
```
