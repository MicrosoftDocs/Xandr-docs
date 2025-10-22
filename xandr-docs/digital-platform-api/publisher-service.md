---
title: Publisher Service
description: Explore the Publisher Service to create and update your managed publishers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Publisher service

The Publisher Service is used to create and update your managed publishers.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/publisher](https://api.appnexus.com/publisher)<br>(publisher JSON) | Add a new publisher (with a default site and placement). |
| `POST` | [https://api.appnexus.com/publisher?create_default_placement=false](https://api.appnexus.com/publisher?create_default_placement=false)<br>(publisher JSON) | Add a new publisher (without a default site and placement). |
| `PUT` | [https://api.appnexus.com/publisher?id=PUBLISHER_ID](https://api.appnexus.com/publisher?id=PUBLISHER_ID)<br>(publisher JSON) | Update an existing publisher. |
| `GET` | [https://api.appnexus.com/publisher](https://api.appnexus.com/publisher) | View all publishers. |
| `GET` | [https://api.appnexus.com/publisher?id=PUBLISHER_ID](https://api.appnexus.com/publisher?id=PUBLISHER_ID) | View a specific publisher. |
| `GET` | [https://api.appnexus.com/publisher?id=1,2,3](https://api.appnexus.com/publisher?id=1,2,3) | View multiple publishers by ID using a comma-separated list. |
| `DELETE` | [https://api.appnexus.com/publisher?id=PUBLISHER_ID](https://api.appnexus.com/publisher?id=PUBLISHER_ID) | Delete a publisher.<br><br>**Caution:** Deleting a publisher deletes all of its child objects as well, including sites, placements, payment rules, and publisher-level ad quality profiles. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings. |
| `GET` | https://api.appnexus.com/publisher/meta | Find out which fields you can filter and sort by. |

If your API call returns an error with "**Request failed due to timeout or memory issue**", you can append `add_mappings=false` to your query parameters. Adding this parameter will only return the top-level API objects, but not their nested children.

For example:

```
curl -b cookies -c cookies "https://api.appnexus.com/publisher?id=2,3,5,8,13,21&add_mappings=false"
```

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the publisher.<br>**Default:** Auto-incremented number (i.e. 123) |
| `code` | string (100) | The custom code for the publisher. |
| `name` | string (255) | The name of the publisher.<br>**Required On:** `POST`/`PUT` |
| `state` | enum | The state of the publisher. Possible values: `"active"` or `"inactive"`.<br>**Default:** `"inactive"` |
| `expose_domains` | boolean | If `true`, domains associated with the publisher are exposed to other members of the platform.<br>**Default:** `true` |
| `enable_cookie_tracking_default` | boolean | If `true`, users visiting this publisher's inventory will be tracked via our cookies.<br>**Default:** `true` |
| `reselling_exposure` | enum | The publisher's exposure for reselling to other members of the platform. Possible values: `"public"` or `"private"`.<br>**Default:** `"private"` |
| `reselling_exposed_on` | timestamp | The date and time when the publisher was exposed for reselling.<br>**Default:** `"0000-00-00 00:00:00"` |
| `reselling_name` | string (255) | The name that appears in the inventory manager to other members of the platform, if `reselling_exposure` is `true`. If this field is empty, the value in the name field is used. |
| `description` | string (255) | The description that appears in the inventory manager to other members of the platform, if `reselling_exposure` is `true`. If this field is empty, no description is shown. |
| `is_rtb` | boolean | All networks have one publisher object that serves as a so-called "plumbing link" to real-time inventory. This mock publisher has no ad profile, no ad quality rules, no visibility profiles, or any of the other trappings of an actual publisher. All other publishers have `is_rtb` set to `false` by default.<br>**Default:** `false` |
| `timezone` | enum | The timezone for this publisher. For details and accepted values, see [API Timezones](api-timezones.md).<br>**Default:** `"EST5EDT"` or the member's timezone. |
| `last_modified` | timestamp | **Read-only.** The date and time when the publisher was last updated in the our system. |
| `stats` | array | The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `max_learn_pct` | int | The maximum % of the publisher's daily volume that can be used for learn.<br><br>**Tip:** If you want us to automatically allocate an optimal percent of impressions to learn to keep introducing new offers as older offers become less profitable, set this field to `null`.<br><br>**Default:** `0` |
| `learn_bypass_cpm` | int | If an impression selected for learn receives a bid higher than this value from an external buyer, the bid will be accepted and the impression will not be used for learn.<br>**Default:** `5` |
| `ad_quality_advanced_mode_enabled` | boolean | If `true`, multiple ad quality rules can be created for the publisher in the UI.<br>**Default:** `true` |
| `allow_report_on_default_imps` | boolean | If `true`, publisher users can report on detailed impression and revenue metrics in the UI, such as imps filled, imps defaulted, total revenue, total revenue eCPM, filled revenue, filled revenue eCPM, defaulted revenue, and defaulted revenue eCPM.<br>**Default:** `false` |
| `default_site_id` | int | The ID of the publisher's default site. The site is created automatically when the publisher is added.<br><br>**Caution:** When adding a publisher, you can prevent a default site from being created by passing `"create_default_placement=false"` in the query string of the `POST` request.<br><br>**Default:** Auto-incremented number (i.e. 123). |
| `default_ad_profile_id` | int | Most publishers should use the base ad quality rule associated with the `base_ad_quality_rule_id`. Ad quality rules provide more control over what is allowed to serve on a publisher's inventory. If there is no base ad quality rule, the system will use the ad profile associated with the `default_ad_profile_id`. For more information, see the [Ad Profile Service](ad-profile-service.md).<br>**Default:** The member's default ad profile ID. |
| `billing_dba` | string (100) | The "Doing Business As" name to use for billing purposes.<br>**Required On:** `POST`/`PUT` |
| `billing_address1` | string (100) | The street information of the billing address.<br>**Required On:** `POST`/`PUT`, if `inventory_relationship` is set to `direct`. |
| `billing_address2` | string (100) | The street information of the billing address (cont.). |
| `billing_city` | string (100) | The city of the billing address.<br>**Required On:** `POST`/`PUT`, if `inventory_relationship` is set to `direct`. |
| `billing_state` | string (100) | The state of the billing address.<br>**Required On:** `POST`/`PUT`, if `inventory_relationship` is set to `direct`. |
| `billing_zip` | string (100) | The zip code of the billing address.<br>**Required On:** `POST`/`PUT`, if `inventory_relationship` is set to `direct`. |
| `billing_country` | string (100) | The country/region of the billing address.<br>**Required On:** `POST`/`PUT`, if `inventory_relationship` is set to `direct`. |
| `accept_supply_partner_usersync` | boolean | If `true`, the publisher accepts usersync pixels from platform supply partners. (Recommended) |
| `accept_demand_partner_usersync` | boolean | If `true`, the publisher accepts usersync pixels from platform demand partners. (Recommended) |
| `accept_data_provider_usersync` | boolean | If `true`, the publisher accepts usersync pixels from platform data providers. (Recommended) |
| `ym_profile_id` | int | The unique identifier for the yield management profile applied to the publisher. |
| `allow_cpm_managed` | boolean | If you allow your managed advertisers' campaigns with a CPM bidding strategy to serve on this publisher.<br>**Default:** `true` |
| `allow_cpm_external` | boolean | If you allow demand partners to purchase inventory on a CPM basis on this publisher.<br>**Default:** `true` |
| `allow_cpa_managed` | boolean | If you allow your managed advertisers' campaigns with a cpa bidding strategy to buy inventory from this publisher.<br>**Default:** `true` |
| `allow_cpa_external` | boolean | If you allow your demand partners to purchase inventory on a CPA basis.<br>**Default:** `false` |
| `allow_cpc_managed` | boolean | If you allow your managed advertisers' campaigns with a cpc bidding strategy.<br>**Default:** `true` |
| `allow_cpc_external` | boolean | If you allow your demand partners to purchase inventory on a CPC basis.<br>**Default:** `false` |
| `managed_cpc_bias_pct` | int | Risk Premium: What percent you will bias a CPC bid by when comparing it to a CPM bid from managed advertisers. This field is the inverse of the value displayed in the UI, e.g., 20 in the UI is represented as 100 - 20 = 80 in the API.<br>**Default:** `100` |
| `managed_cpa_bias_pct` | int | Risk Premium: What percent you will bias a CPA bid by when comparing it to a CPM bid from managed advertisers. This field is the inverse of the value displayed in the UI, e.g., 20 in the UI is represented as 100 - 20 = 80 in the API.<br>**Default:** `100` |
| `external_cpc_bias_pct` | int | Risk Premium: What percent you will bias a CPC bid by when comparing it to a CPM bid from a buyer. This field is the inverse of the value displayed in the UI, e.g., 20 in the UI is represented as 100 - 20 = 80 in the API.<br>**Default:** `100` |
| `external_cpa_bias_pct` | int | Risk Premium: What percent you will bias a CPA bid by when comparing it to a CPM bid from a buyer. This field is the inverse of the value displayed in the UI, e.g., 20 in the UI is represented as 100 - 20 = 80 in the API.<br>**Default:** `100` |
| `is_oo` | boolean | If `true`, the publisher is owned and operated by the network, meaning the network gets 100% of the revenue.<br>**Default:** false |
| `base_payment_rule_id` | int | The unique identifier for the publisher's catch-all payment rule. Use the [Payment Rule Service](./payment-rule-service.md) to find the ID for the publisher's payment rule you desire.<br>**Default:** Auto-incremented number (i.e. 123). |
| `base_ad_quality_rule_id` | int | The unique identifier for the publisher's base ad quality rule. This acts as a "catch-all" ad quality rule in two cases:<br>- There are no conditional ad quality rules that match the current impression.<br>There are no conditional ad quality rules defined.<br>- If the `base_ad_quality_rule_id` is not defined, the system will use the ad profile associated with the `default_ad_profile_id` (defined above). For more information, see the [Ad Quality Rule Service](ad-quality-rule-service.md). |
| `currency` | enum | The publisher's currency.<br><br>**Warning:** This field can be set on `POST`, but it cannot be updated on `PUT`.<br><br>**Tip:** As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience.<br><br>**Default:** Member's default currency or USD. |
| `visibility_profile_id` | int | The ID of the visibility profile assigned directly to the publisher. For more details about visibility profiles, see the [Visibility Profile Service](visibility-profile-service.md). |
| `billing_internal_user` | int |  |
| `labels` | array of objects | The optional labels assigned to the publisher. Currently, two labels are available: `"Salesperson"` and `"Account Manager"`. For more details, see [Labels](#labels) below.<br><br>**Note:**<br>You can report on publisher labels with the [Network Analytics](network-analytics.md) report. For example, if you use the `"Salesperson"` label to specify the name of the salesperson responsible for each publisher, you could run the Network Analytics report filtered by `"salesperson_for_publisher"` to focus on the publishers that a particular salesperson is responsible for, or grouped by `"salesperson_for_publisher"` to rank the performance of your salespeople. |
| `placements` | array of objects | The placements associated with the publisher, including the default placement that is created with the publisher. When you create additional placements, or publisher tags, with the [Placement Service](placement-service.md), you associate them with a publisher. For more details, see [Placements](#placements) below. |
| `external_inv_codes` | array of objects | Some sellers use their own codes to break out their inventory more granularly than by Publisher > Site > Placement. This is done via the External Inventory Code Service. This field shows the external inventory codes associated with the publisher. |
| `cpm_reselling_disabled` | boolean | **Read-only.** If `true`, we have detected impression issues on this publisher's inventory and has therefore set `"allow_cpm_external"` to `false`, preventing the reselling of the publisher's inventory on a CPM basis.<br>**Default:** `false` |
| `cpc_reselling_disabled` | boolean | **Read-only.** If `true`, we have detected click issues on this publisher's inventory and has therefore set `"allow_cpc_external"` to `false`, preventing the reselling of the publisher's inventory on a CPC basis.<br>**Default:** `false` |
| `platform_ops_notes` | string | **Read-only.** Notes about the disabling of CPM/CPC reselling. |
| `pitbull_segment_id` | int | **Warning:** This field has been **deprecated**. |
| `pitbull_segment_value` | int | **Warning:** This field has been **deprecated**. |
| `publisher_brand_exceptions` | array of objects | An array of brand IDs. Creatives associated with these brand IDs will be allowed to serve on this publisher's page more than once per `/mtj` call. The brands that you add to this array will be appended to the array of brands in the `member_brand_exceptions` field of the [Member Service](member-service.md). For internal field definitions, see [Publisher Brand Exceptions](#publisher-brand-exceptions) below.<br>**Required On:** `n/a` |
| `seller_page_cap_enabled` | boolean | This field **must** be set in order to be able to enable page caps for this publisher. Page caps keep creatives associated with a given brand from serving more than once per page load, except for those brand IDs added to the `publisher_brand_exceptions` array on this service or the `member_brand_exceptions` array on the [Member Service](member-service.md).<br><br>**Note:** This setting activates the function but does not make the setting on the UI visible. To see this setting in the UI, contact your representative.<br><br>**Required On:** `n/a` |
| `inventory_relationship` | enum | The relationship of the inventory to the publisher. Possible values:<br>- `unknown`<br>- `owned_operated`<br>- `direct`<br>- `indirect_single_publisher`<br>- `indirect_multiple_publishers`<br><br>**Note:**<br>If both `is_oo` and `inventory_relationship` are specified, `inventory_relationship` will overwrite `is_oo` with the appropriate value based on the relationship.<br><br>**Required On:** `POST`/`PUT` |
| `inventory_source` | enum | The source of the inventory. Possible values:<br>- `other`<br>- `rubicon`<br>- `openx`<br>- `pubmatic`<br>- `aol`<br><br>If `inventory_source` is set to `other`, then `inventory_source_name` must be completed. |
| `inventory_source_name` | string | Publisher (source) name for `indirect_single_publisher`.<br>**Required On:** `POST`/`PUT` for publishers whose `inventory_relationship` is set to `indirect_single_publisher`. |
| `contact` | object | An array of objects containing contact information for this publisher.<br>**Required On:** `POST`/`PUT` |
| `use_anx_auction_logic` | boolean | Determines whether ANX Auction Logic will be enabled for the publisher. When set to `True`, we will automatically handle all floors and price reductions.<br>**Default:** `False` |

### Contact

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | The name of the point of contact for this publisher. |
| `phone` | string | The phone number for the above point of contact. |
| `email` | string | The email of the publisher. |

### Labels

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the label. Possible values: `2` (Salesperson) or `4` (Account Manager). |
| `name` | enum | **Read-only.** The name of the label. Possible values: `"Salesperson"` or `"Account Manager"`. |
| `value` | string (100) | The value assigned to the label. For example, for the `"Salesperson"` label, this could be a name such as `"Michael Sellers"`. |

### Placements

> [!NOTE]
> When you add a publisher, a default placement is created automatically and included in this array. You can prevent a default placement from being created automatically by passing `"create_default_placement=false"` in the query string of the `POST` request.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the placement. |
| `code` | string (100) | The custom code for the placement. |

### Publisher brand exceptions

| Field | Type | Description |
|:---|:---|:---|
| `brand_id` | int | The ID of the brand whose associated creatives you would like to allow to serve more than once per page load on this publisher's inventory. This setting will only take effect if you toggle the `seller_page_cap_enabled` field on this service. For more information about brands, see the [Brand Service](brand-service.md). |

### Stats

The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.

## Examples

### Add a new publisher

Create a JSON file with the required fields for a publisher.

> [!NOTE]
>
> - Replace the placeholders (e.g., "PUBLISHER_NAME") in the below JSON example with your own values.
> - When you create a new publisher, a publisher id (`"id"` in the `"publisher"` object), `"default_site_id"`, default placement id (`"id"` in the `"placements"` array), and `"base_payment_rule_id"` are automatically generated.

Since the `inventory_relationship` field is required, we’ve set it to `“direct”`, (but it can be set to other values). We’ve also set `state` to `“inactive”` for now. Since we don’t provide the other publisher fields in our request, they will be set to their default values and display in the response body. For more information, see [Sell-Side Setup](sell-side-setup.md).

```
$ cat publisher

{
    "publisher": {
            "name": "PUBLISHER_NAME",
            "inventory_relationship": "direct",
            "billing_dba": "PUBLISHER_DBA",
            "billing_address1": "PUBLISHER_ADDRESS",
            "billing_city": "PUBLISHER_CITY",
            "billing_state": "PUBLISHER_STATE",
            "billing_zip": "PUBLISHER_ZIP",
            "billing_country": "PUBLISHER_COUNTRY",
            "contact": {
                    "phone": "CONTACT_PHONE",
                    "email": "CONTACT_EMAIL",
                    "name": "CONTACT_NAME"
                }
        }
}

$ curl -b cookies -c cookies -X POST -d @publisher 'https://api.appnexus.com/publisher'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 233,
        "start_element": 0,
        "num_elements": 100,
        "publisher": {
            "id": 233,
            "code": null,
            "reselling_name": null,
            "expose_domains": true,
            "is_rtb": false,
            "reselling_exposure": "private",
            "reselling_exposed_on": "1970-01-01 00:00:01",
            "timezone": "EST5EDT",
            "last_modified": "2015-05-12 23:58:20",
            "max_learn_pct": 0,
            "accept_demand_partner_usersync": null,
            "learn_bypass_cpm": 5,
            "ad_quality_advanced_mode_enabled": true,
            "allow_report_on_default_imps": false,
            "name": "New Publisher",
            "description": "",
            "state": "active",
            "default_site_id": 229,
            "default_ad_profile_id": null,
            "billing_dba": null,
            "billing_address1": null,
            "billing_address2": null,
            "billing_city": null,
            "billing_state": null,
            "billing_zip": null,
            "billing_country": null,
            "accept_supply_partner_usersync": null,
            "accept_data_provider_usersync": null,
            "ym_profile_id": null,
            "allow_cpm_managed": true,
            "allow_cpm_external": true,
            "allow_cpa_managed": true,
            "allow_cpa_external": false,
            "allow_cpc_managed": true,
            "allow_cpc_external": false,
            "managed_cpc_bias_pct": 100,
            "managed_cpa_bias_pct": 100,
            "external_cpc_bias_pct": 100,
            "external_cpa_bias_pct": 100,
            "is_oo": false,
            "base_payment_rule_id": 161,
            "base_ad_quality_rule_id": null,
            "currency": "USD",
            "visibility_profile_id": null,
            "cpm_reselling_disabled": false,
            "cpc_reselling_disabled": false,
            "platform_ops_notes": null,
            "enable_cookie_tracking_default": true,
            "seller_page_cap_enabled": false,
            "billing_internal_user": null,
            "labels": null,
            "placements": [
                {
                    "id": 232,
                    "code": null
                }
            ],
            "external_inv_codes": null,
            "contact_info": null,
            "publisher_brand_exceptions": null
        }
    }
}
```

### View information about publisher 10

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/publisher?id=10'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "publisher": {
            "id": 10,
            "code": null,
            "reselling_name": null,
            "expose_domains": false,
            "state": "inactive",
            "is_rtb": false,
            "reselling_exposure": "private",
            "reselling_exposed_on": "2011-05-04 21:37:52",
            "timezone": "EST5EDT",
            "last_modified": "2011-08-31 15:11:08",
            "max_learn_pct": 5,
            "accept_demand_partner_usersync": null,
            "learn_bypass_cpm": 5,
            "ad_quality_advanced_mode_enabled": true,
            "member_id": 95,
            "name": "test",
            "description": "test",
            "default_site_id": 137,
            "default_ad_profile_id": 256,
            "billing_dba": null,
            "billing_address1": null,
            "billing_address2": null,
            "billing_city": null,
            "billing_state": null,
            "billing_zip": null,
            "billing_country": null,
            "accept_supply_partner_usersync": null,
            "accept_data_provider_usersync": null,
            "ym_profile_id": null,
            "allow_cpm_managed": true,
            "allow_cpm_external": true,
            "allow_cpa_managed": true,
            "allow_cpa_external": false,
            "allow_cpc_managed": true,
            "allow_cpc_external": false,
            "managed_cpc_bias_pct": 100,
            "managed_cpa_bias_pct": 100,
            "external_cpc_bias_pct": 100,
            "external_cpa_bias_pct": 100,
            "is_oo": false,
            "base_payment_rule_id": null,
            "base_ad_quality_rule_id": 1,
            "currency": "USD",
            "redirect_to_rm": true,
            "billing_internal_user": null,
            "labels" [
                {
                    "value: "First Contact",
                    "id": 2,
                    "name": "Salesperson"
                },
                {
                    "value: "Second Contact",
                    "id": 4,
                    "name": "Account Manager"
                },
            "placements": [
                {
                    "id": 1234,
                    "code": null
                },
                {
                    "id": 5678,
                    "code": null
                }
            ]
        }
}
```

### Update a publisher

Update the `base_ad_quality_rule_id` field of a publisher:

```
$ cat PublisherBaseAdQualityRuleUpdate.json

{
         "publisher" :  {
            "base_ad_quality_rule_id" : 632112
         }
}

$ curl -b cookies -X PUT -d @PublisherBaseAdQualityRuleUpdate.json 'https://api.appnexus.com/publisher?id=100'

{
   "response" : {
      "count" : 1,
      "status" : "OK",
      "start_element" : 0,
      "id" : "100",
      "publisher" : {
         "billing_address1" : "BILLING_ADDRESS",
         "managed_cpa_bias_pct" : 100,
         "inventory_source" : null,
         "external_cpc_bias_pct" : 100,
         "ym_profile_id" : null,
         "currency" : "USD",
         "allow_cpa_managed" : true,
         "inventory_source_name" : null,
         "use_anx_auction_logic" : false,
         "learn_bypass_cpm" : 5,
         "platform_ops_notes" : null,
         "contact" : {
            "phone" : "555-555-1212",
            "email" : "CONTACT_EMAIL@EMAIL.COM",
            "id" : CONTACT_ID,
            "name" : "CONTACT_NAME"
         },
         "allow_cpc_managed" : true,
         "is_rtb" : false,
         "disclosure_status" : "disclosed_pending",
         "visibility_profile_id" : null,
         "billing_dba" : "BILLING_DBA",
         "reselling_exposure" : "private",
         "managed_cpc_bias_pct" : 100,
         "default_placement_id" : 13741957,
         "labels" : null,
         "accept_supply_partner_usersync" : null,
         "expose_domains" : true,
         "reselling_name" : null,
         "billing_internal_user" : null,
         "placements" : [
            {
               "id" : 13741957,
               "code" : null
            },
            {
               "id" : 13847262,
               "code" : null
            }
         ],
         "enable_cookie_tracking_default" : true,
         "external_inv_codes" : null,
         "inventory_relationship" : "direct",
         "pitbull_segment_value" : 0,
         "default_site_id" : 3731466,
         "publisher_brand_exceptions" : null,
         "billing_address2" : null,
         "timezone" : "CET",
         "contact_info" : null,
         "last_modified" : "2018-08-26 22:33:13",
         "code" : null,
         "billing_zip" : "BILLING_ZIP",
         "billing_country" : "US",
         "reselling_exposed_on" : "1970-01-01 00:00:01",
         "is_oo" : false,
         "billing_state" : "BILLING_STATE",
         "ad_quality_advanced_mode_enabled" : true,
         "allow_cpm_external" : true,
         "pitbull_segment_id" : 0,
         "base_ad_quality_rule_id" : 632112,
         "default_ad_profile_id" : null,
         "seller_page_cap_enabled" : false,
         "description" : "",
         "allow_cpa_external" : false,
         "id" : 100,
         "state" : "inactive",
         "billing_city" : "Portland",
         "max_learn_pct" : 0,
         "cpc_reselling_disabled" : false,
         "allow_report_on_default_imps" : false,
         "cpm_reselling_disabled" : false,
         "base_payment_rule_id" : 1570229,
         "name" : "PUBLISHER_NAME",
         "allow_cpm_managed" : true,
         "accept_demand_partner_usersync" : null,
         "accept_data_provider_usersync" : null,
         "external_cpa_bias_pct" : 100,
         "allow_cpc_external" : false
      },
      "num_elements" : 100
   }
}
```
