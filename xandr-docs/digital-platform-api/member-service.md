---
title: Digital Platform API - Member Service
description: This article provides information on Member service. Each member has multiple users with their own UI and API credentials managed by the User Service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Member service

A member is any entity that has a financial relationship with Xandr, and each client is a single member. Members are registered with the Member Service by Xandr personnel, and all API activity must be associated with a member. Note that the Member Service does not grant API or UI access. Each member has multiple users who have their own UI and API credentials, and are managed by the [User Service](./user-service.md).

## Members and Contracts

Before they can buy or sell ads, a member needs a contract with Xandr. This contract will establish financial terms and credit facilities (if applicable), and bind the member to the terms and conditions of Xandr, such as content quality and use of personally identifiable information.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/member` | View your member |
| `GET` |`https://api.appnexus.com/member?id=MEMBER_ID` | View a particular member, if you have multiple |
| `GET` | `https://api.appnexus.com/member/meta` | Find out which fields you can filter and sort by |
| `PUT` | `https://api.appnexus.com/member?id=MEMBER_ID` | Modify an existing member |
| `POST` | `https://api.appnexus.com/member` | Add a new member (**Admin-only**) |

## JSON fields

| Field | Type | Description |  |  |  |  |  |  |  |  |  |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| `allow_ad_profile_override` | Boolean | If `true`, the ad quality restrictions in `default_ad_profile_id` will take precedence over ad quality restrictions defined at the placement level. For example, if you restrict Advertiser X in the default ad quality profile at the network level, but do not restrict Advertiser X at the placement level, Advertiser X will still be restricted. If you set this to `false` , settings at the placement level will take precedence.<br><br>**Note**: If you set this to `true`, you must set the `default_ad_profile_id` as well.<br><br>**Default**: `true` |  |  |  |  |  |  |  |  |  |
| `allow_non_cpm_payment` | Boolean | **Default**: `true` |  |  |  |  |  |  |  |  |  |
| `app_contract_accepted` | Boolean | **Not yet supported**. Indicates whether the member has agreed to the Xandr terms of service contract for Xandr's exchange. Non-admin users can only change this field from `False` to `True`. In order to set it from `True` to `False`, contact your Xandr representative.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `audit_notify_email` | string | Each time Xandr audits a creative belonging to this member, a detailed response is sent to this email address. The response includes the creative's audit status and any reasons why the creative has not passed audit. This field supports multiple comma-separated email addresses. Could also be used for domain audit notification ( see `domain_blocklist_email` below). |  |  |  |  |  |  |  |  |  |
| `buyer_clearing_fee_pct` | double | **Admin-only**. The percent of the CPM paid for inventory charged as a fee in certain cases. See your contract for more information. |  |  |  |  |  |  |  |  |  |
| `buyer_credit_limit` | double | **Admin-only**. The credit limit with Xandr taken into consideration when the member is buying inventory. |  |  |  |  |  |  |  |  |  |
| `contact_email` | string | The email contact for this member. |  |  |  |  |  |  |  |  |  |
| `content_categories` | array of objects | A list of available categories that you can apply to publishers, sites, and placements. Can be customized by the member. [The array is of this format](#content_categories-array-format). |  |  |  |  |  |  |  |  |  |
| `contract_allows_unaudited` | Boolean | **Admin-only**. See `default_campaign_trust` and `default_campaign_allow_unaudited` for information about Xandr-reviewed inventory. If your contract does not allow you to run on non-Xandr-reviewed inventory for some reason, this will be `false`.<br><br>**Default**: `true` |  |  |  |  |  |  |  |  |  |
| `creative_size_fee_per_gb` | float | **Read-only**. The fee that is charged per GB for a creative that exceeds the `creative_size_minimum_bytes`. |  |  |  |  |  |  |  |  |  |
| `creative_size_minimum_bytes` | int | **Read-only**. The size above which a creative is considered over-sized. The member is charged a creative overage fee for serving an over-sized creative. |  |  |  |  |  |  |  |  |  |
| `daily_budget` | money | The safety budget for your member, in U.S. dollars. The safety budget establishes a member-wide cap for your daily CPM media cost on third-party inventory. This helps limit the risk of unintentional overspend due to trafficking and campaign setup errors. Your safety budget always operates on the `timezone` of your member and resets each day at 12am.<br><br>To control who receives email notifications when your safety budget is approached, use the `send_safety_budget_notifications` field on the [User Service](./user-service.md).<br><br>**Default**: `null` |  |  |  |  |  |  |  |  |  |
| `daily_budget_imps` | int | The safety budget for your member, in impressions. See `daily_budget` above for more details.<br><br>**Default**: `null` |  |  |  |  |  |  |  |  |  |
| `daily_imps_self_audited` | int |  |  |  |  |  |  |  |  |  |  |
| `daily_imps_unaudited` | int |  |  |  |  |  |  |  |  |  |  |
| `daily_imps_verified` | int |  |  |  |  |  |  |  |  |  |  |
| `deal_types` | array of objects | **Default**: `null` |  |  |  |  |  |  |  |  |  |
| `default_accept_data_provider_usersync` | Boolean | See `default_accept_supply_partner_usersync`.<br><br>**Default**: `true` |  |  |  |  |  |  |  |  |  |
| `default_accept_deals` | Boolean | If `true`, the `acceptance_status` field of the [Deal Buyer Setting Service](./deal-buyer-setting-service.md) defaults to `active`, if `false`, the `acceptance_status` defaults to `pending`.<br><br>**Default**: `true` |  |  |  |  |  |  |  |  |  |
| `default_accept_demand_partner_usersync` | Boolean | See `default_accept_supply_partner_usersync`.<br><br>**Default**: `true` |  |  |  |  |  |  |  |  |  |
| `default_accept_supply_partner_usersync` | Boolean | We use pixels to sync user IDs between Xandr and our major non-platform supply partners, such as Google, and third party data providers. This increases our ability to apply frequency and recency caps and segment data across the Internet. You can opt not to participate in user syncing; however this reduces our ability to apply the right information to your campaigns.<br><br>**Default**: `true` |  |  |  |  |  |  |  |  |  |
| `default_ad_profile_id` | int | The ID of the default [Ad Profile](./ad-profile-service.md) to use. This is required when `allow_ad_profile_override` is `true`. |  |  |  |  |  |  |  |  |  |
| `default_allow_cpa` | Boolean | **Default**: `true` |  |  |  |  |  |  |  |  |  |
| `default_allow_cpc` | Boolean | **Default**: `true` |  |  |  |  |  |  |  |  |  |
| `default_buyer_group_id` | int | Currently used for an alpha feature. |  |  |  |  |  |  |  |  |  |
| `default_campaign_allow_unaudited` | Boolean | You can choose to apply Inventory Quality criteria to your campaigns (sensitive attributes, intended audience, etc.). If this field is `false`, then certain inventory quality criteria will be applied by default to each campaign. You can override it at any time in the Campaign Manager or through the campaign's [profile](./profile-service.md). If `true`, no inventory quality criteria will be applied to your campaigns unless you manually apply it.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `default_campaign_trust` | enum | Xandr reviews a significant portion of inventory and applies quality attributes, and also encourages members who sell on our platform to review their inventory in the same manner. If you would like campaigns to by default run only on Xandr-reviewed inventory, then set this field to `"appnexus"`. If you want to default to your seller trust settings, which may include seller-reviewed and unreviewed inventory, set this field to `"seller"`. You can override this with the campaign's [profile](./profile-service.md).<br>Possible values:<br> - `seller`<br> - `appnexus`<br><br>**Default**: `appnexus` |  |  |  |  |  |  |  |  |  |
| `default_content_retrieval_timeout_ms` | int | The default timeout, specified in milliseconds, for all placements created by this member. The default value of `0` will mean that mediated content will not be served.<br><br>**Note**: This setting can still be overridden by the `content_retrieval_timeout_ms` field on the placement itself.<br><br>**Default**: `0` |  |  |  |  |  |  |  |  |  |
| `default_country` | array of objects | The objects are:<br> - `"country_id"`<br>- `"country_name"`<br> - `"country_code"`<br><br>**Default**: `null` |  |  |  |  |  |  |  |  |  |
| `default_currency` | string | The default currency for this member. Can be overridden at more granular levels. For possible currency values, use the [Currency Service](./currency-service.md).<br><br>**Default**: `USD` |  |  |  |  |  |  |  |  |  |
| `default_enable_for_mediation` | Boolean | Whether placements created by this member are enabled to serve mediation creatives by default. Even if this field is set to `false`, the `enable_for_mediation` field on the placement itself can still override the behavior defined here.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `default_placement_id` | int | The placement ID to be used as a default when an inactive or nonexistent seller tag is called. |  |  |  |  |  |  |  |  |  |
| `developer_id` | int | **Read-only**. The ID of the developer, if the member is developing on Xandr's platform (e.g., for the Apps Marketplace). |  |  |  |  |  |  |  |  |  |
| `domain_blocklist_email` | string | When Xandr finds domains belonging to this member to be in violation of its standards and auditing policies, the domains are put into a blocklist, and an email is sent to this email address. The email identifies the domain URL, average daily impressions, and blocklist reason(s) for each domain that averaged at least 10,000 daily impressions over the last 7 days. Blocked domains that averaged less than 10,000 daily impressions over the last 7 days are not included in the email.<br><br>**Note**: If no email address is provided here, the email address in the `audit_notify_email` is used instead. |  |  |  |  |  |  |  |  |  |
| `dongle` | string | A code that is used as a password for a member's debug output. |  |  |  |  |  |  |  |  |  |
| `email_code` | string(50) | Email code is a unique value used when placements are processed via our email tag processing tool. Must be an alphanumeric value. |  |  |  |  |  |  |  |  |  |
| `enable_click_and_imp_trackers` | Boolean | **Admin-only**. If `true`, external click and impression trackers can be created in.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `entity_type` | enum | **Admin-only**. A legacy field that may be used in the future. Possible values: `"reseller"` or `"direct"` (deprecated).<br><br>**Default**: `"reseller"` |  |  |  |  |  |  |  |  |  |
| `expose_eap_ecp_placement_settings` | Boolean | **Deprecated as of March 2011**. |  |  |  |  |  |  |  |  |  |
| `expose_optimization_levers` | Boolean | **Admin-only**. If `true`, optimization levers are shown in.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `floor_optimization` | array of objects | **Read-only**. Indicates if floor optimization is enabled for this member and provides the bidder ID of a real-time price provider. See [Floor Optimization](#floor-optimization) below for the definitions of the objects in this array. May also be set to `null` to disable the feature. |  |  |  |  |  |  |  |  |  |
| `id` | int | The ID of the member.<br><br>**Required on**: `PUT` |  |  |  |  |  |  |  |  |  |
| `interface_domain` | string(100) | **This field is being deprecated**. |  |  |  |  |  |  |  |  |  |
| `interface_domain_beta` | string(100) | **This field is being deprecated**. |  |  |  |  |  |  |  |  |  |
| `inventory_trust` | array of objects | This controls who you buy from and whether Xandr will use their quality and category information for targeting. See [Inventory Trust](#inventory-trust) below for more details. |  |  |  |  |  |  |  |  |  |
| `is_iash_compliant` | Boolean | **Admin-only**. If a selling member is IASH compliant, a logo will be placed next to the member's name in Partner Center.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `last_modified` | timestamp | The timestamp of last modification to this member. |  |  |  |  |  |  |  |  |  |
| `max_hosted_video_size` | int | **Admin-only**. The maximum file size for hosted in-stream video creatives. In addition to limiting file size, setting this field enables the member to host videos with Xandr. |  |  |  |  |  |  |  |  |  |
| `mediation` | array of objects | **Read-only**. Indicates whether automatic bid adjustments and reporting sync are enabled for this member. See [Mediation](#mediation) below for the definitions of the objects in this array. |  |  |  |  |  |  |  |  |  |
| `member_brand_exceptions` | array of objects | An array of brand IDs. Creatives associated with these brands will be allowed to serve more than once per page load on your publishers' pages (4 on those publishers' pages who have enabled sell-side page caps via the `seller_page_cap_enabled` field of the [Publisher Service](./publisher-service.md)). You can also add per-publisher brand exceptions using the `publisher_brand_exceptions` field of the [Publisher Service](./publisher-service.md). See [Member Brand Exceptions](#member-brand-exceptions) for the definitions of the objects stored in this array.<br><br>**Default**: n/a |  |  |  |  |  |  |  |  |  |
| `name` | string | The name of the member.<br><br>**Required on**: `POST` |  |  |  |  |  |  |  |  |  |
| `native_custom_keys` | array of objects | Some sellers of native advertising require buyers to use `"custom keys"` to target their inventory. These keys will vary from member to member. This field allows sellers to define what custom values they'd like buyers to pass in via a native creative. For more information, see [Native Custom Keys](#native-custom-keys) below.<br><br>**Note**: You can obtain a list of native custom keys using the read-only [Native Custom Keys](#native-custom-keys).<br><br>**Default**: `null` |  |  |  |  |  |  |  |  |  |
| `no_reselling_priority` | int | This value is used to determine whether RTB bids are allowed to compete with your managed campaigns. In order for an RTB bid to be able to compete with a managed bid for an impression, this field's value must be greater than the priority of the managed bid.<br><br>For example, let's say you have the following [auction and settings](#auction-and-settings-for-no_reselling_priority). In this example, the RTB bid will not compete, even though its bid price is higher. In order for RTB to compete on this impression, `no_reselling_priority` would have to be 9 or higher.<br><br>In addition, when reselling is allowed for an impression, the highest priority standard managed demand will be allowed to compete with the highest priority guaranteed demand (as well as with RTB). |
| `pitbull_segment_id` | int | **Note**: This field has been deprecated. |  |  |  |  |  |  |  |  |  |
| `pitbull_segment_value` | int | **Note**: This field has been deprecated. |  |  |  |  |  |  |  |  |  |
| `platform_exposure` | enum | This determines whether and how your member appears in the **Buyers** tab of the Ad Quality Manager in and in the [Platform Member](./platform-member-service.md) service. Possible values:<br> - `"public"` = Your member name is shown.<br> - `"private"` = Your member ID is shown.<br> - `"hidden"` = Your member does not appear.<br><br>**Note**:<br> - Setting `platform_exposure` to `"hidden"` will hide your member `"name"` and `"domain"` fields in our [sellers.json](https://acdn.adnxs.com/sellers/1d/appnexus/sellers.json) file and list your member seat as `"is_confidential": 1`. See [example](#setting-platform_exposure-to-hidden). <br>This can limit the monetization of your inventory as some DSPs may not choose to buy impressions from sellers who are not transparent in the `"schain"` object.<br><br> - Setting `platform_exposure` to `"public"` will display your member `"name"` and `"domain"` fields in our [sellers.json](https://acdn.adnxs.com/sellers/1d/appnexus/sellers.json) file. See [example](#setting-platform_exposure-to-public).<br><br> - `primary_type` must be either `"buyer"` or `"network"` in order for it to appear in the **Buyers** tab of the Ad Quality Manager in.<br><br>**Default**: `"public"` |  |  |  |  |  |  |  |  |  |
| `plugins` | array | The plugins that users see on the Apps tab in. See [Plugins](#plugins) below for more details. |  |  |  |  |  |  |  |  |  |
| `plugins_enabled` | Boolean | **Admin-only**. If `true`, the **Apps** tab is shown in.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `pops_enabled_UI` | Boolean | **Admin-only**. If `true`, pop ad support is shown in.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `prioritize_margin` | Boolean | If set to `true` Xandr will perform a bid/no bid check for managed campaigns based on line item minimum margin settings. If set to `false` Xandr will not not perform any bid/no bid check for managed campaigns based on the line item minimum.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `reporting_decimal_type` | enum | The decimal mark used in reporting. This setting can be overridden at the user and report levels (see `"reporting_decimal_type"` in the [User Service](./user-service.md) and [Report Service](./report-service.md)). Possible values:<br> - `"comma"`<br> - `"decimal"` (period)<br><br>**Default**: `"decimal"` |  |  |  |  |  |  |  |  |  |
| `reselling_description` | string | This description is not currently used in. |  |  |  |  |  |  |  |  |  |
| `reselling_exposure` | enum | Whether or not to expose the member's inventory to the platform for reselling in the real-time marketplace. Possible values: `"public"` or `"private"`.<br><br>**Default**: `"private"`  |  |  |  |  |  |  |  |  |  |
| `reselling_exposed_on` | string | The date and time at which `reselling_exposure` was changed to `"public"` |  |  |  |  |  |  |  |  |  |
| `seller_member_groups` | array of objects | **Admin-only**. Specifies information about the groups of sellers to which this member belongs. See [Seller Member Group](#seller-member-group) below for more information. |  |  |  |  |  |  |  |  |  |
| `seller_revshare_pct` | int |**Admin-only**. If this member is a seller and has a revenue sharing agreement with Xandr, the Xandr portion of the revenue sharing is indicated here. |  |  |  |  |  |  |  |  |  |
| `serving_domain` | object | **Admin-only**. The domain through which advertisements are served. The format of the object is `{"cname":"ad.domain.com","type":null}` |  |  |  |  |  |  |  |  |  |
| `sherlock_notify_email` | string | Each time Sherlock scans a creative belonging to this member, a response is sent to this email address. The response includes the creative's audit status and any reasons why the creative has not passed audit. This email address will also receive [object limit notifications](../bidders/object-limits---faq.md), sent when you reach 85, 95, and 100 percent of your limit for an object. This field supports multiple comma-separated email addresses. |  |  |  |  |  |  |  |  |  |
| `short_name` | string | URL-friendly name to be used as needed. |  |  |  |  |  |  |  |  |  |
| `standard_sizes` | array | The list of sizes which are included in the standard sizes dropdown in when creating creatives. The array is of the following format:<br> `[{"width":"120","height":"600","is_standard":true},{"width":"160","height":"600","is_standard":true}, ... ,{"width":"728","height":"90","is_standard":true},{"width":"800","height":"60","is_standard":false}]` |  |  |  |  |  |  |  |  |  |
| `state` | enum | The state of the member. Possible values: `"active"` or `"inactive"`. |  |  |  |  |  |  |  |  |  |
| `thirdparty_pixels` | array | **Read-only**. An array of third-party pixels associated with the member. You can automatically attach these pixels to all creatives owned by this member using the [Third-party Pixel service](./third-party-pixel-service.md) or attach them individually at the creative level using the [Creative Service](./creative-service.md).<br><br>**Default**: `null` |  |  |  |  |  |  |  |  |  |
| `timezone` | enum | The timezone of the member. See [API Timezones](./api-timezones.md) for details and accepted values. To change the default timezone of an individual advertiser, use the [Advertiser Service](./advertiser-service.md). If no timezone is specified in the Advertiser Service, advertisers inherit the member's timezone.<br><br>**Default**: `"EST5EDT"` |  |  |  |  |  |  |  |  |  |
| `use_insertion_orders` | Boolean | If `true`, use insertion orders (an organizational level above line items) for this member.<br><br>**Default**: `false` |  |  |  |  |  |  |  |  |  |
| `visibility_profile_id` | int | The ID of the optional visibility profile attached to the member. See the [Visibility Profile Service](./visibility-profile-service.md) for more details.<br><br>**Default**: `null` |  |  |  |  |  |  |  |  |  |
| `website_url` | string | The company website for this member. This is used in a number of areas where contact details are displayed. |  |  |  |  |  |  |  |  |  |

### `Content_categories` array format

```
[{"id":"2950","name":"Animals"},{"id":"2951","name":"Arts
& Humanities"}, ...
,{"id":"2977","name":"Travel"}]
```

### Auction and settings for `no_reselling_priority`

| Bid Type | Bid Price | Priority |
|:---|:---|:---|
| RTB | $5 | 8 (`no_reselling_priority`) |
| Managed | $3 | 8 ( priority) |

### Setting `platform_exposure` to `hidden`

```
{
"seller_id": "7694",
"seller_type": "INTERMEDIARY",
"domain": "groupm.com",
"name": "Xaxis – Slovakia Marketplace"
}
```

### Setting `platform_exposure` to `public`

```
{
"seller_id": "8253",
"is_confidential": 1,
"seller_type": "PUBLISHER"
}
```

### Server of record

> [!NOTE]
> Server of record applies only to Publisher Ad Server clients.

| Field | Type | Description |
|:---|:---|:---|
| `server_of_record` | object | For some line items, the most important performance indicator is that the line item delivers its budget in full and evenly across its flight dates. This object is used to hold configuration details related to these line items. <br><br>**Default**: `null` |
| `enforce_true_priority_tiers` | Boolean | **Deprecated**.<br>For more information about Guaranteed Delivery line items, see the `delivery_goal` array on the [Line Item Service](./line-item-service.md).<br><br>**Default**: `false` |
| `guaranteed_delivery_enabled` | Boolean | If `true`, this member has access to guaranteed delivery features.<br><br>**Default**: `false` |
| `guaranteed_delivery_version` | int | This temporary flag denotes the version of the Guaranteed Delivery pacing algorithm being used. It can be set at either the member or [line item](./line-item-service.md) level. The flag will be removed when the new version (2) of the algorithm is released platform-wide. Allowed values:<br>`1`<br>`2`<br><br>**Default**: `null` |

### Native custom keys

| Field | Type | Description |
|:---|:---|:---|
| `custom_key` | string | A seller-defined key that defines what information the seller would like the buyer to pass in via a native creative. |

### Third-party pixels

The `thirdparty_pixels` array contains the fields in the table below. These fields are read-only. To update or create third-party pixels and/or attach third-party pixels to all creatives owned by the member, use the [Third-party Pixel service](./third-party-pixel-service.md). To attach third-party pixels to individual creatives, use the [Creative Service](./creative-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `active` | Boolean | **Read-only**. The current status of the pixel (`true = active`). |
| `audit_status` | string | **Read-only**. Audit status of the pixel. |
| `id` | int | **Read-only**. The pixel's ID. |
| `name` | string | **Read-only**. The full name of the pixel. |

### Inventory trust

| Field | Type | Description |
|:---|:---|:---|
| `default_allow_unaudited` | Boolean | If `true`, campaigns using inventory quality filtering will allow unaudited inventory from sellers unless overridden in the `members` array. |
| `default_trust` | enum | Possible values:<br> - `appnexus`: Campaigns using inventory quality filtering will only buy Xandr-audited inventory from sellers unless overridden in the members array.<br> - `seller`: Inventory quality filtering will allow inventory that has been audited by the selling member in Xandr. |
| `members` | array | For each selling member, controls banned/eligible for selling to you, whether you trust their inventory audit, and whether you allow unaudited inventory from them. |

### Seller member group

All fields in the `seller_member_group` object can be written by admins only.

| Field | Type | Description |
|:---|:---|:---|
| `created_on` | date | Timestamp that indicates when this seller member group was created. |
| `description` | string | Specifies a description of this seller member group. |
| `display_order` | int | Specifies the order in which this seller member group will be displayed in . Default is `5`. |
| `id` | int | Specifies the unique ID of this seller member group. |
| `last_modified` | date | Timestamp that indicates when this seller member group was last modified. |
| `name` | string | Specifies the name of this seller member group. |

### Plugins

| Field | Type | Description | Required On |
|:---|:---|:---|:---|
| `id` | int | The ID of the plugin. |  |
| `status` | enum | The state of the plugin. If `"available"` the user has not yet installed the plugin; if `"installed"`, the user has installed the plugin; if `"accept_permissions"`, the user has installed the plugin, but changes to the plugin require the user to explicitly accept the changes before continuing to use it. Possible values:<br> - `"available"`<br> - `"installed"`<br> - `"accept_permissions"` |  |

### Member brand exceptions

| Field | Type | Description | Required On |
|:---|:---|:---|:---|
| `brand_id` | int | The ID of the brand whose associated creatives you would like to allow to serve more than once per page load on page-cap-enabled publishers' inventory. This setting will only take effect on those publishers which you've enable for page capping by setting the `seller_page_cap_enabled` field to `true` on the [Publisher Service](./publisher-service.md). For more information about brands, see the [Brand Service](./brand-service.md). |  |

### Floor optimization

| Field | Type | Description | Required On |
|:---|:---|:---|:---|
| `active` | Boolean | If `true`, this member has floor optimization enabled. |  |
| `bidder_id` | integer | The ID of an internal real-time price provider that performs the floor optimization. |  |

### Mediation

| Field | Type | Description | Required On |
|:---|:---|:---|:---|
| `auto_bid_adjustment_enabled` | Boolean | If `true`, this member can use the automatic bid adjustment feature, in which Xandr suggests a bid based on an estimate what the network will pay and automatically updates the bid as conditions change. |  |
| `reporting_sync_enabled` | Boolean | If `true`, this member can use the reporting sync feature, in which reporting data from third-party networks can be pulled from that network's servers. This data is used to create daily reports and monitor trends directly from within Xandr. |  |

## Examples

### View your member

```
$ curl - b cookies 'https://api.appnexus.com/member'
{
    "response": {
        "status": "OK",
        "member": {
            "id": 186,
            "name": "My Network",
            "whitelabel_support_email": null,
            "reselling_description": null,
            "state": "active",
            "no_reselling_priority": 6,
            "entity_type": "reseller",
            "buyer_clearing_fee_pct": null,
            "default_placement_id": null,
            "default_buyer_group_id": null,
            "thirdparty_pixels": [{
                "id": 656,
                "name": "sample pixel",
                "audit_status": "pending",
                "active": true
            }, {
                "id": 311,
                "name": "another sample pixel",
                "audit_status": "pending",
                "active": true
            }],
            "interface_domain": null,
            "interface_domain_beta": null,
            "content_categories": [{
                "id": "10432",
                "name": "Pets & Animals"
            }, {
                "id": "10433",
                "name": "Fun & Trivia"
            }, {
                "id": "10434",
                "name": "Autos & Vehicles"
            }, {
                "id": "10435",
                "name": "Beauty & Personal Care"
            }, {
                "id": "10436",
                "name": "Business & Industry"
            }, {
                "id": "10437",
                "name": "Computers & Electronics"
            }, {
                "id": "10438",
                "name": "Arts & Entertainment"
            }, {
                "id": "10439",
                "name": "Finance"
            }, {
                "id": "10440",
                "name": "Food & Drink"
            }, {
                "id": "10441",
                "name": "Games"
            }, {
                "id": "10442",
                "name": "Health"
            }, {
                "id": "10443",
                "name": "Home & Garden"
            }, {
                "id": "10444",
                "name": "Internet & Telecom"
            }, {
                "id": "10445",
                "name": "Lifestyles"
            }, {
                "id": "10446",
                "name": "Local News"
            }, {
                "id": "10447",
                "name": "News"
            }, {
                "id": "10448",
                "name": "Online Communities"
            }, {
                "id": "10449",
                "name": "Photo & Video Sharing"
            }, {
                "id": "10450",
                "name": "Real Estate"
            }, {
                "id": "10451",
                "name": "Recreation"
            }, {
                "id": "10452",
                "name": "Reference & Language"
            }, {
                "id": "10453",
                "name": "Science"
            }, {
                "id": "10454",
                "name": "Shopping"
            }, {
                "id": "10455",
                "name": "Sports"
            }, {
                "id": "10456",
                "name": "Consumer Electronics"
            }, {
                "id": "10457",
                "name": "Travel"
            }, {
                "id": "16040",
                "name": "test"
            }],
            "default_ad_profile_id": 19040,
            "email_code": null,
            "serving_domain": {
                "cname": null,
                "type": null
            },
            "reselling_exposure": "public",
            "reselling_exposed_on": "2011-07-15 20:35:17",
            "last_modified": "2011-11-16 20:51:33",
            "standard_sizes": [{
                "width": "120",
                "height": "600",
                "is_standard": true
            }, {
                "width": "160",
                "height": "600",
                "is_standard": true
            }, {
                "width": "300",
                "height": "250",
                "is_standard": true
            }, {
                "width": "468",
                "height": "60",
                "is_standard": true
            }, {
                "width": "728",
                "height": "90",
                "is_standard": true
            }, {
                "width": "180",
                "height": "150",
                "is_standard": false
            }, {
                "width": "234",
                "height": "600",
                "is_standard": false
            }, {
                "width": "430",
                "height": "600",
                "is_standard": false
            }],
            "buyer_credit_limit": 2000,
            "timezone": "EST5EDT",
            "seller_revshare_pct": null,
            "default_country": null,
            "dongle": "DONGLE",
            "platform_exposure": "hidden",
            "contact_email": null,
            "allow_ad_profile_override": true,
            "default_currency": "USD",
            "use_insertion_orders": false,
            "expose_optimization_levers": true,
            "pops_enabled_UI": true,
            "default_accept_supply_partner_usersync": true,
            "default_accept_data_provider_usersync": true,
            "default_accept_demand_partner_usersync": true,
            "short_name": "ANU",
            "expose_eap_ecp_placement_settings": true,
            "daily_imps_verified": null,
            "daily_imps_self_audited": null,
            "daily_imps_unaudited": null,
            "is_iash_compliant": false,
            "deal_types": null,
            "allow_non_cpm_payment": true,
            "default_allow_cpc": true,
            "default_allow_cpa": true,
            "visibility_profile_id": 8,
            "inventory_trust": {
                "default_trust": "appnexus",
                "default_allow_unaudited": false,
                "default_is_banned": false,
                "members": [{
                    "seller_member_id": "181",
                    "trust": "appnexus",
                    "allow_unaudited": false,
                    "is_banned": false
                }, {
                    "seller_member_id": "459",
                    "trust": "appnexus",
                    "allow_unaudited": false,
                    "is_banned": false
                }]
            },
            "seller_member_groups": [{
                "display_order": 1,
                "id": 2,
                "last_modified": "2016-01-26 18:23:38",
                "created_on": "2016-01-26 18:23:38",
                "name": "My Seller Group"
            }],
            "default_campaign_trust": "appnexus",
            "default_campaign_allow_unaudited": false,
            "contract_allows_unaudited": true,
            "active_contract": {
                "auditing_fee_per_creative": 0,
                "creative_priority_fee_1": 25,
                "creative_priority_fee_2": 25
            },
            "allow_priority_audit": true,
            "enable_mobile_ui": true,
            "contact_info": null,
            "audit_notify_email": null,
            "default_external_audit": false,
            "reporting_decimal_type": "decimal",
            "daily_budget": 500,
            "enable_click_and_imp_trackers": true,
            "plugins_enabled": true,
            "plugins": [{
                "id": "1",
                "status": "installed"
            }, {
                "id": "2",
                "status": "installed"
            }, {
                "id": "3",
                "status": "installed"
            }, {
                "id": "5",
                "status": "installed"
            }, {
                "id": "6",
                "status": "installed"
            }, {
                "id": "7",
                "status": "installed"
            }, {
                "id": "8",
                "status": "installed"
            }, {
                "id": "9",
                "status": "installed"
            }, {
                "id": "10",
                "status": "installed"
            }, {
                "id": "11",
                "status": "installed"
            }, {
                "id": "12",
                "status": "accept_permissions"
            }]
        },
        "count": 1,
        "start_element": 0,
        "num_elements": 100
    }
}
```

### Update your member

```
$ cat member_mod
{
    "member": {
        "id": 185,
        "reselling_exposure": "public"
    }
}
$ curl -b cookies -X PUT -d @member_mod 'https://api.appnexus.com/member?id=185'
{
    "response": {
        "status":"OK"
    }
}
```

## Related topics

- [Reference](./reference.md)
- [API Semantics](./api-semantics.md)
