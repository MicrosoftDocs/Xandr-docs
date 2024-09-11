---
title: Profile Service Overview
description: Explore the Profile service, its JSON fields, REST API, parameters with thorough examples.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Profile service overview

A profile is a set of targeting parameters, such as gender, age, geography, and frequency. It can be applied to several objects in the system, most of which are listed below. The most common use of the profile service is to run a campaign; you create a profile and then associate it with the [Campaign Service](campaign-service.md). The campaign object includes fields such as flight dates and associated creatives.

- Except for segment targeting, parameters are absolute. For example, if the geographical target is set only to the United States, ONLY U.S.-based impressions will receive bids.
- Segment targeting uses and/or Boolean logic.
- Profiles must be associated with either an advertiser or a publisher, in order to be used with several other objects in the system, listed below.

Profiles can be used with several other objects in the system (listed below). Any fields in the profile that do not apply to the associated object will be ignored.

- Advertiser
- Line Item
- Creative
- Campaign
- Payment Rule
- Ad Quality Rule

It is also possible to refer to a profile within a deal object, while it is not necessary for the profile to be associated to an advertiser or publisher.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/profile?advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID](https://api.appnexus.com/profile?advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID)<br>(profile JSON) | Add a new profile. |
| `POST` | [https://api.appnexus.com/profile?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/profile?advertiser_code=ADVERTISER_CODE)<br>(profile JSON) | Add a new profile. |
| `PUT` | [https://api.appnexus.com/profile?id=PROFILE_ID&advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID](https://api.appnexus.com/profile?id=PROFILE_ID&advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID)<br>(profile JSON) | Modify an existing profile. |
| `PUT` | [https://api.appnexus.com/profile?code=PROFILE_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/profile?code=PROFILE_CODE&advertiser_code=ADVERTISER_CODE)<br>(profile JSON) | Modify an existing profile. |
| `GET` | [https://api.appnexus.com/profile?advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID](https://api.appnexus.com/profile?advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID) | View all of the profiles for one of your advertisers. |
| `GET` | [https://api.appnexus.com/profile?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/profile?advertiser_code=ADVERTISER_CODE) | View all of the profiles for one of your advertisers. |
| `GET` | [https://api.appnexus.com/profile?id=PROFILE_ID&advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID](https://api.appnexus.com/profile?id=PROFILE_ID&advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID) | View a specific profile for one of your advertisers. |
| `GET` | [https://api.appnexus.com/profile?code=PROFILE_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/profile?code=PROFILE_CODE&advertiser_code=ADVERTISER_CODE) | View a specific profile for one of your advertisers. |

> [!NOTE]
> `postal_code_action_include` - To use this service for publisher profiles, replace `advertiser_id` with `publisher_id`.

## JSON fields

### General

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the profile.<br>**Required:** `PUT`, in query string. |
| `code` | string | Custom code for the profile. |
| `description` | string | Optional description. |
| `is_template` | Boolean | If `true`, the profile has been saved as a targeting template in. To get profiles that are targeting templates in, pass `is_template=true` in the query string of a `GET` call. For more details about targeting templates in, see "[Managing Targeting Templates](../monetize/managing-targeting-templates.md)" within the app's Help System.<br>**Default:** `false` |
| `last_modified` | timestamp | Time of last modification to this profile. |
| `is_archived` | boolean | **Read-only.** Indicates whether the profile has been automatically archived due to it's parent line item not being used (and therefore, having been archived). Once set as `true`, the value can't be changed and the only calls that can be made on the profile object are `GET` and `DELETE`.<br><br>**Note:** If a profile's parent is automatically archived, the profile will also be archived. In addition, once archived, the profile may not be associated with any line items or campaigns.<br>**Default:** `false` |
| `archived_on` | timestamp | **Read-only.** The date and time on which the profile was archived (i.e., when the `is_archived` field was set to `true`).<br>**Default:** `null` |

### Frequency

For details on Frequency and Recency Targeting and the below fields, see [here](frequency-for-the-api.md).

| Field | Type | Description |
|:---|:---|:---|
| `max_lifetime_imps` | int | The maximum number of impressions per person. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `min_session_imps` | int | The minimum number of impressions per person per session. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `max_session_imps` | int | The maximum number of impressions per person per session. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `max_day_imps` | int | The maximum number of impressions per person per day. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `max_hour_imps` | int | The maximum number of impressions per person per hour. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `max_week_imps` | int | The maximum number of impressions per person per week. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `max_month_imps` | int | The maximum number of impressions per person per month. If set, this value must be between `0` and `255`.<br>**Default:** `null` |
| `min_minutes_per_imp` | int | The minimum number of minutes between impressions per person. This field may not be set to `0`.<br>**Default:** `null` |
| `max_page_imps` | int | The maximum number of impressions per page load (seller's ad request).<br><br>**Note:** Only relevant for multi-tag auctions (For example: /(ss)vmap).<br>**Default:** `null` |
| `require_cookie_for_freq_cap` | Boolean | Indicates whether you'll exclusively serve to users with known identifiers to maintain your frequency cap settings. Setting this field to `true` indicates that you'll only serve ads to users with known identifiers, thereby maintaining your frequency cap settings. Setting this field to `false` indicates that you'll serve to anonymous users as well. If you've set a daily-occurring frequency cap, advanced frequency management will control impressions to anonymous users through modeling. Otherwise, frequency-cap settings won't apply to those users. Because this flag is only enforced when a frequency cap has been set, setting this field to `true` won't require identifiers for an object that has no active frequency-cap settings.<br><br> **Default**: `true`<br> **Note**: Advanced Frequency Management is currently not supported for Monetize users. |

### Targeting

When multiple targets are set, only inventory that satisfies all targeting criteria is eligible. For example, if you target intended audience `general` and inventory sources x, y, and z, then the profile will only target `general` audience inventory from inventory sources x, y, and z.

> [!NOTE]
> You may not specify both the `segment_targets` and `segment_group_targets` fields in any `POST` or `PUT` calls (only one of the two may be specified).
>
> - Be aware that some targets accept an array of **objects** rather than integers or strings. The format can be found in the examples at the bottom of this page.
> - For **Programmatic Guaranteed Buying Line Items**:
>   - You can only target one deal target (see [Deal Targets](#deal-targets) below) and the `allow_unaudited` field must be set to `true`.
>   - **Do not set any other targeting fields**.
> - For [Augmented Line Items](line-item-service.md), it is mandatory to set at least one country as geography targeting (See [Country Targets](#country-targets) below).
> - **Effective August 30, 2021**:
>   - TapAd's Graph will provide global coverage excluding Europe.
>   - Xandr's Graph will provide coverage for Europe and the United States.
>
>     Adjust your code accordingly.

| Field | Type | Description |
|:---|:---|:---|
| `graph_id` | int | - `Null` if the line item is targeting your member seat's default graph selection. <br> - `0` if the line item is targeting no graph. <br> - `3` if the line item is targeting the TapAd Graph.<br>- `4` if the line item is targeting the Xandr Graph. <br> **Note**: For select EMEA Invest member seats included in the default cross-device pilot, there is a change to the `graph_id` field expectations. <br> Passing `graph_id` as `Null` will now correspond to your member seat's default graph selection. For members in our EMEA pilot, this will be `graph_id = 4`. To disable cross-device targeting, these member seats will need to pass `graph_id = 0`.|
| `daypart_timezone` | string | The timezone to be used with the `daypart_targets`. For more details, see [API Timezones](api-timezones.md).<br><br>**Note:** `null` is equivalent to the user's timezone.<br><br>**Default:** `null` |
| `daypart_targets` | array of objects | The day parts during which to serve the campaign. For more details, see [Daypart Targets](#daypart-targets) below. <br><br>**Note:** If you do not set any daypart targets, the campaign will serve on all days of the week at all times. |
| `segment_targets` | array of objects | **Note:** If you use `segment_targets` and edit the associated campaign in our UI, the segments will be converted to a group in the `segment_group_targets` array. Therefore, it's recommended to use `segment_group_targets` when working via the API.<br><br>The segment IDs to target, each of which has an associated action (`include` or `exclude`). You define the Boolean logic between segments with the `segment_boolean_operator` field outside of the array. For more details, see [Segment Targets](#segment-targets) and example below. |
| `segment_group_targets` | array of objects | The segment groups to target. Whereas the `segment_targets` array allows you to define Boolean logic between individual segments, this array allows you to establish groups of segments, defining Boolean logic between the groups as well as between the segments within each group. You define the Boolean logic between groups with the `segment_boolean_operator` field outside of the array; you define the Boolean logic between segments in a group with the `boolean_operator` field within the group object. For more details, see [Segment Group Targets](#segment-group-targets) and an example below.<br><br>**Note:** Null segments cannot be added.<br>You may not add `null` segments to this array using `POST` or `PUT`. |
| `segment_boolean_operator` | enum | If using `segment_targets`, this defines the Boolean logic between the segments specified. If using `segment_group_targets`, this defines the Boolean logic between the segment groups (the Boolean logic between segments in a group is defined directly in the `segment_group_targets` array).<br>Possible values: `and` or `or`.<br>**Default:** `and` |
| `age_targets` | array of objects | The list of age ranges to target for this profile. The `allow_unknown` field is available as a Boolean in order to account for ad calls where the age of the user is not available. For more description and examples, see the [Age Targets](#age-targets) section below. |
| `gender_targets` | object | The gender targeting used for the profile. Possible values for gender are `m` or `f`. The `allow_unknown` field is available as a Boolean in order to account for ad calls where the gender of the user is not available. See the [Gender Targets](#gender-targets) section below. |
| `country_targets` | array of objects | The country IDs to be either excluded or included in a profile, as defined by the `country_action` field. You can use the [Country Service](country-service.md) to retrieve a list of country IDs. For more details and format, see [Country Targets](#country-targets).<br>**Required:** `POST`/`PUT`, when `country_action` is include. |
| `country_action` | enum | Action to be taken on the `country_targets` list. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `region_targets` | array of objects | The region/state IDs to be either excluded or included in a profile, as defined by the `region_action` field. You can use the [Region Service](region-service.md) to retrieve a list of region IDs. For more details and format, see [Region Targets](#region-targets) below.<br>**Required On:** `POST`/`PUT`, when `region_action` is `include`. |
| `require_transparency_and_consent_framework_string` | boolean | - If `true`, only allow associated objects to purchase inventory where valid TCF string is present.<br>- If `false`, allow associated objects to purchase any inventory that falls within pre-defined targeting declarations.<br>- This is only supported on advertiser level as targeting at other levels may lead to undefined behavior.<br><br>**Note:** This parameter is only applicable to the traffic coming from territories where GDPR applies.<br><br>**Default:** `false` |
| `region_action` | enum | Action to be taken on the `region_targets` list.<br>Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `dma_targets` | array of objects | The IDs of designated market areas to be either excluded or included in a profile, as defined by the `dma_action` field. You can use the [Designated Market Area Service](designated-market-area-service.md) to retrieve a list of DMA IDs. See [format example](#dma_targets-format). |
| `dma_action` | enum | Action to be taken on the `dma_targets` list.<br>Possible values: include or exclude.<br>**Default:** `exclude` |
| `city_targets` | array of objects | The IDs of cities to be either included or excluded in a profile, as defined by the `city_action` field. You can use the [City Service](city-service.md) to retrieve a list of city IDs. For more details and format, see [City Targets](#city-targets) below.<br>**Required On:** `POST`/`PUT`, when `city_action` is `include`. |
| `city_action` | enum | Action to be taken on the `city_targets` list. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `domain_targets` | array of objects | List of domains to be either included or excluded in a profile, as defined by the `domain_action` field. For format, see the [example](#domain_targets-format) below. |
| `domain_action` | enum | Action to be taken on the `domain_targets` list. For details on domains, see the [Create a Domain or App List](../monetize/create-a-domain-list-or-app-list.md) in documentation.<br>Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `domain_list_targets` | array of objects | The IDs of domains lists to either include or exclude in a profile, as defined by the `domain_list_action` field. You can use the [Domain List Service](domain-list-service.md) to retrieve domain list IDs. See the example below for format.<br><br>**Note:** You can use no more than 100 domain lists in a single profile. |
| `domain_list_action` | enum | Action to be taken on the `domain_list_targets` list. For details on domains, see [Working with Targeting Lists](../monetize/working-with-targeting-lists.md) in documentation. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `platform_placement_targets` | array of objects | RTB or other Networks' inventory you can target. You can use Inventory Resold or Reporting services to find platform placements. |
| `size_targets` | array of objects | List of eligible sizes to be included in the profile.<br>The sizes are in an array size objects, each object containing the width and height of each target size. See [example](#size_targets-example) below.<br><br>**Note:** When you enable roadblocking on a guaranteed line item, this value is combined with creative sizes on the line item and campaign to produce forecasting. The size with the lowest forecasted number of impressions will be returned as the forecasted capacity. |
| `seller_member_group_targets` | array of objects | The seller member groups to be excluded or included in a profile. To target Xandr's direct supply, see the [format](#seller_member_group_targets-format) below. |
| `member_targets` | array of objects | Seller member IDs to be either excluded or included in a profile. The specific format can be found in the example at the bottom of the page. |
| `member_default_action` | enum | **Deprecated.**<br>**Default:** `null` |
| `video_targets` | object | Video target IDs to be included in a profile. For the specific format, see [Video Targets](#video-targets) below. |
| `engagement_rate_targets` | array of objects | Target specific, highly performant inventory based on historic performance. For details, see [Engagement Rate Targets](#engagement-rate-targets) below.<br>**Default:** `null` |
| `publisher_targets` | array of objects | Managed/direct publisher IDs to be either excluded or included in a profile. |
| `site_targets` | array of objects | The sites IDs to be either excluded or included in a profile. Exclude or include is inherited from the `publisher_targets` field.<br>**Default:** If you do not provide action with `site_targets`, action will default to `NULL` and `profile.inventory_action` will be used. |
| `placement_targets` | array of objects | The placement IDs to be either excluded or included in a profile. Exclude or include is inherited from the `publisher_targets` field.<br><br>**Default:** If you do not provide action with `placement_targets`, action will default to NULL and `profile.inventory_action` will be used. |
| `inventory_action` | enum | Action to be taken on the `inventory_targets`, `publisher_targets`, `site_targets`, and `placement_targets` list. Possible values: `include` or `exclude`. If action is `include`, then any targeted publisher, site, or placement will be included.<br>**Default:** `exclude` |
| `content_category_targets` | object with string and array | The content categories to target for this profile as well as whether to allow unknown categories. For more details and format, see [Content Category Targets](#content-category-targets) below. To retrieve content category IDs, use the [Content Category Service](content-category-service.md). |
| `deal_targets` | array of objects | The deal IDs to be targeted by this profile. A deal is an agreement between a seller and buyer that may provide the buyer preferential pricing, access to exclusive inventory, reduced competition on inventory, or other opportunities. For more details and format, see [Deal Targets](#deal-targets) below.<br>For more information on how the value of this field and the `deal_action_include` field affect targeting results, see [Targeting Results for `deal_action_include` AND `deal_targets`](#targeting-results-for-deal_action_include-and-deal_targets-fields) fields below. |
| `deal_list_targets` | array of objects | The deal list IDs to be targeted by this profile. See [example](#deal_list_targets-example) below.<br>Deal list IDs can be fetched using the [Deal List Service](deal-list-service.md). |
| `platform_publisher_targets` | array of objects | Third party publisher IDs to be either excluded or included in a profile. For a list of IDs the [Inventory Resold Service](inventory-resold-service.md). |
| `platform_content_category_targets` | array of objects | List of network resold content categories to target for this profile. For a list of IDs, see the [Inventory Resold Service](inventory-resold-service.md). |
| `use_inventory_attribute_targets` | Boolean | If `true`, the profile will allow inventory that has the sensitive attributes included in `inventory_attribute_targets`.<br>**Default:** `false` |
| `trust` | enum | Indicates the level of audit which inventory must meet in order to be eligible.<br>Possible values: `appnexus` or `"seller"`. If this field is set to `"appnexus"`, the `allow_unaudited` field must be set to `false`.<br>**Default:** `seller` |
| `allow_unaudited` | Boolean | If `true`, this profile will allow unaudited inventory to pass targeting. If the `trust` field is set to `appnexus`, this must be set to `false`.<br><br>**Note:**<br>- This setting overrides the seller trust settings in the `inventory_trust` object of the [Member Service](member-service.md).<br>- For Programmatic Guaranteed Buying Line Items, `allow_unaudited` must be set to `true`.<br>**Default:** `false` |
| `session_freq_type` | enum | Indicates how the number of impressions seen by the user are counted during the current browsing session. Possible values: `platform` (across all publishers in the current session) or `publisher` (for the specific publisher).<br>**Default:** `platform` |
| `inventory_attribute_targets` | array of objects | The IDs of inventory attributes to target for this profile. You can use the [Inventory Attribute Service](inventory-attribute-service.md) to retrieve a list of IDs. |
| `intended_audience_targets` | array of strings | The intended audience targets. Possible values: `general`, `children`, `young_adult`, or `mature`. <br><br>**Note:** You can only choose to include (not exclude) intended audience targets.<br>See [example](#intended_audience_targets-example).<br><br>**Note:** To use the intended audience targeting, `default_trust` under `inventory_trust` (an attribute under the member) must be set to `seller`. Without this setting, the intended audience targeting will not be applied. |
| `language_targets` | array of objects | The IDs of the browser languages to either include or exclude in the profile, as defined by the `language_action` field. You can use the [Language Service](language-service.md) to retrieve language IDs. |
| `language_action` | enum | Action to be taken on `language_targets`. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `querystring_targets` | array of objects | The query string targets to either `include` or `exclude` in the profile, as defined by the `querystring_action` field. |
| `querystring_action` | enum | Action to be taken on the `querystring_targets`. <br>Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `querystring_boolean_operator` | enum | Boolean logic to be applied to the `querystring_targets`. <br>Possible values: `and` or `or`.<br>**Default:** `and` |
| `postal_code_targets` | array of objects | The postal code IDs to target. See [example](#postal_code_targets-example).<br>IDs can be fetched using the [Postal Code Service](postal-code-service.md). |
| `postal_code_list_targets` | array of objects | The postal code list IDs to target. See [example](#postal_code_list_targets-example).<br>IDs can be fetched using the [Postal Code List Service](postal-code-list-service.md). |
| `postal_code_action_include` | boolean | Whether to include the postal codes defined in `postal_code_targets`, postal code lists defined in `postal_code_list_targets` in your targeting, and political districts defined in `political_district_targets`.<br>**Default:** `true` |
| `zip_targets` | array of objects | **Deprecated.** Use `postal_code_targets` instead. |
| `supply_type_targets` | array of strings | The type(s) of supply to either include in or exclude from targeting, as defined by the `supply_type_action` field. Possible values: `web`, `mobile_web` and `mobile_app`.<br><br>**Note:** The `facebook_sidebar` option has been **deprecated**. |
| `supply_type_action` | enum | Supply types are `web`, `mobile_web`, and `mobile_app`. Possible values: `include` or `exclude`. If this field is set to `include`, only inventory of types included in `supply_type_targets` will be targeted. If `exclude`, only inventory not in `supply_type_targets` will be targeted (except `facebook_sidebar`, which has been **deprecated**).<br>**Default:** `exclude` |
| `user_group_targets` | object | Every user is randomly assigned to 1 of 100 user groups, no group holding any advantage over another. You can use this field to target a specific range of these user groups. Also, you can use the `include_cookieless_users` field to include or exclude users without cookies. For formatting, see the [View a profile](#view-a-profile) example below. <br><br>**Note:** The [User Group Pattern Service](user-group-pattern-service.md) can help you calculate your user group targets.<br>The most common use for user group targets is defining user groups for A/B testing of campaign targeting strategies. Here's how it works: You set test user group targets in one profile and control user group targets in another. Then you apply the user group label to each affected campaign, using the label to identify the user group as test or control (see the `labels` field in the [Campaign Service](campaign-service.md)). Then you run the [Network Analytics](network-analytics.md), [Network Advertiser Analytics](network-advertiser-analytics.md), or [Advertiser Analytics](advertiser-analytics.md) report grouped by `user_group_for_campaign` to rank how campaigns performed by user group. |
| `position_targets` | object | The fold positions to target. For more details, see [Position Targets](#position-targets) below. |
| `browser_targets` | array of objects | The IDs of browsers to either include in or exclude from your targeting, as defined by the `browser_action` field. You can use the [Browser Service](browser-service.md) to retrieve a list of browser IDs. For the format, see the example below. |
| `browser_action` | enum | Action to be taken on the `browser_targets`. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `location_target_latitude` | double | The latitude of the user's location. This must be between -90 and 90, with up to 6 decimal places, where south is negative and north is positive. A profile can be targeted to a specific location when GPS data is available from a mobile device. When lat/long targeting is set, users will only be targeted within the area defined by the center (`location_target_latitude`, `location_target_longitude`) and radius `location_target_radius`. Users will not be targeted when GPS data is not available for the impression. |
| `location_target_longitude` | double | The longitude of the user's location. This must be between -180 and 180, with up to 6 decimal places, where west is negative and east is positive. A profile can be targeted to a specific location when GPS data is available from a mobile device. When lat/long targeting is set, users will only be targeted within the area defined by the center (`location_target_latitude`, `location_target_longitude`) and radius `location_target_radius`. Users will not be targeted when GPS data is not available for the impression. |
| `location_target_radius` | integer length in meters | For more information, see `location_target_latitude`. |
| `device_model_targets` | array of objects | The models of mobile devices (i.e., iPhone) to either include in or exclude from your targeting, as defined by the `device_model_action` field. To retrieve a complete list of device models registered in our system, use the read-only [Device Model Service](device-model-service.md). For more details and format, see [Device Model Targets](#device-model-targets) below. |
| `device_model_action` | enum | Action to be taken on `device_model_targets`. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `device_type_targets` | array of strings | The types of devices to either include in or exclude from your targeting, as defined by the `device_type_action` field.<br>Possible values:<br>- `phone`<br>- `tablet`<br>- `pc`<br>- `tv`<br>- `gameconsole`<br>- `stb`<br>- `mediaplayer`<br><br>For format, see [Device Type Targets](#device-type-targets) below. |
| `device_type_action` | enum | Action to be taken on `device_type_targets`. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `carrier_targets` | array of objects | The mobile carriers to either include in or exclude from your targeting, as defined by the `carrier_action` field. To retrieve a complete list of mobile carriers registered in our system, use the read-only [Carrier Service](carrier-service.md). For more details and format, see [Carrier Targets](#carrier-targets) below. |
| `carrier_action` | enum | Action to be taken on the `carrier_targets`. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `inventory_url_list_targets` | array of objects | Contains a list of inventory list IDs (allowlists and/or blocklists). Used to attach a single allowlist and/or one or more blocklists to the profile.<br>- The allowlist contains a list of domains or apps to be targeted by the line item using the profile. If an allowlist is included, domains and apps not in the allowlist will not be targeted.<br>- Each blocklist contains a list of domains or apps that are to be excluded from targeting by line item that uses the profile.<br><br>For more details, see [Inventory Lists](#inventory-lists) below. |
| `operating_system_family_targets` | array of objects | The operating systems as a whole (e.g., Android, Apple iOS, Windows 7, etc.) to either include in or exclude from your targeting, as defined by the `operating_system_family_action` field. <br><br>**Note:** This field is used to target all versions of operating systems, whereas `operating_system_extended_targets` is used to target specific versions of operating systems. For more details and format, see [Operating System Family Targets](#operating-system-family-targets) below. |
| `operating_system_family_action` | enum | Action to be taken on `operating_system_family_targets`. Possible values: `include` or `exclude`.<br>**Default:** `exclude` |
| `use_operating_system_extended_targeting` | Boolean | **Read-only.** If `true`, the `operating_system_extended_targets` field will be respected.<br>By default, newer profiles will have this field set to `true`. However, older profiles (and any "newer" profiles created by duplicating them) will have this field set to `false` by default.<br>There is no way to update an older profile (or its duplicates) to set this field to `true`. If you want add OS extended targeting to these old profiles (or their duplicates), you must create a new profile and add your targeting settings to the new profile.<br>**Default:** `true` |
| `operating_system_extended_targets` | array of objects | The list of specific operating systems to either include in or exclude from your targeting. <br><br>**Note:** This array is used to target specific operating system versions, whereas `operating_system_family_targets` is used to target all versions of operating systems. For more details and format, see [Operating System Extended Targets](#operating-system-extended-targets) below.<br><br>**Note:** This field will be respected only if `use_operating_system_extended_targeting` is `true`. |
| `operating_system_action` | enum | **Deprecated.** Use `operating_system_extended_targets` instead.<br>**Default:** `exclude` |
| `operating_system_targets` | array of objects | **Deprecated.** Use `operating_system_extended_targets` instead. |
| `mobile_app_instance_targets` | array of objects | A list of mobile app instances that you'd like to include or exclude from targeting. For field definitions, see [Mobile App Instance Targets](#mobile-app-instance-targets) below. For more details about what mobile app instances are and how they work, see the [Mobile App Instance Service](mobile-app-instance-list-service.md). |
| `mobile_app_instance_action_include` | Boolean | Whether to include the mobile app instances defined in `mobile_app_instance_targets` in your campaign targeting.<br>**Default:** `false` |
| `mobile_app_instance_list_targets` | array of objects | This list contains mobile app instance lists (in other words, it's a list of lists). For field definitions, see [Mobile App Instance List Targets](#mobile-app-instance-list-targets) below. For more information about mobile app instance lists are and how they work, see the [Mobile App Instance List Service](mobile-app-instance-list-service.md). |
| `mobile_app_instance_list_action_include` | Boolean | Whether to include the mobile app instance lists defined in `mobile_app_instance_list_targets` in your campaign targeting.<br>**Default:** `false` |
| `deal_action_include` | Boolean | Whether to include or exclude deals defined in `deal_targets` and deal lists defined in `deal_list_targets` in campaign and/or line item targeting. When set to `true`, deals and deal lists will be included.<br><br>**Note:** To target or exclude deals and deal lists, in addition to setting this field to `true` or `false`, you must also:<br>- Provide a list of deals and deal lists to include or exclude in the `deal_targets` and `deal_list_targets` array. An empty list would either target no deals/deal lists (if `deal_action_include` is set to `true`) or target all deals/deal lists (if `deal_action_include` is set to `false`).<br>- (Only when using ALIs) Set the `deals` field to `true` within the `supply_strategies` array of the [Line Item Service](line-item-service.md).<br><br>For more information on how the value of this field and the `deal_targets` field affect targeting results, see Targeting Results for `deal_action_include` AND `deal_targets` fields.<br>**Default:** `true` |
| `ip_range_list_targets` | array of objects | A list of IP address ranges to be included or excluded from campaign targeting. For more information, see [IP Range List Targets](#ip-range-list-targets) below, as well as the documentation for the [IP Range List Service](ip-range-list-service.md). |
| `key_value_targets` | array of objects | A list of custom key/value targets. For details and examples, see [Key value targets](#key-value-targets) below. |
| `ad_slot_position_action_include` | Boolean | Intent to target specific slots in an ad pod. Note that you can target ad slots or ad bumpers, but not both.<br>**Default:** `false` |
| `ad_slot_position_targets` | array of ints | The ad slot positions a buyer wants to serve on. `-1` represents the last position, `0` represents the first. By default when `ad_slot_position_action_include` is set to `false`, an empty array means spending can happen on any position. Set `ad_slot_position_action_include` to `true` first if you want to use `ad_slot_position_targets` to specify positions to target.<br>**Default:** `empty row` |
| `ad_slot_intro_bumper_action_include` | Boolean | This controls if the creative will target video intro positions for VAST video auctions. The default is `true`. To ensure that your creative does not target the intro adpod position, set this field to `false`. <br><br>**Note:** You can target ad slots or ad bumpers, but not both.<br><br>**Default:** `true` |
| `ad_slot_outro_bumper_action_include` | Boolean | This controls if the creative will target video outro positions for VAST video auctions. The default is `true`. To ensure that your creative does not target the outro adpod position, set this field to `false`. <br><br>**Note:** You can target ad slots or ad bumpers, but not both.<br><br>**Default:** `true` |
| `screen_size_action` | string | **Deprecated.**<br>**Default:** `exclude` |
| `screen_size_targets` | array of objects | **Deprecated.** |
| `optimization_zone_action` | string | **Not currently supported.**<br>**Default:** `exclude` |
| `optimization_zone_targets` | array of objects | **Not currently supported.** |
| `created_on` | timestamp | **Read-only.** The date and time when the profile was created. |
| `is_expired` | Boolean | **Read-only.** If `true`, the object associated with the profile is expired. This parameter is only supported for internal purposes.<br>**Default:** `false` |
| `inventory_network_resold_targets` | array of objects | **Deprecated.** |
| `exelate_targets` | array of objects | **Deprecated.** |
| `inventory_url_allowlist_settings` | object | This object contains fields used to determine how allowlists are applied to line item buying. See [Inventory URL Allowlist Settings](#inventory-url-allowlist-settings). |
| `ads_txt_authorized_only` | Boolean | When `true`, the line item will only target web inventory from authorized sellers of domains that have an ads.txt file.<br><br>**Note:** The `ads_txt_authorized_only` targeting parameter only applies to Open Exchange inventory. It does not affect targeting of deal inventory. It also does not apply to app inventory (since use of an `ads.txt` file for app inventory has not yet been adopted by the industry). For more information, see [Ads.txt FAQ for Buyers](../industry-reference/ads-txt---app-ads-txt-faq-for-buyers.md).<br>**Default:** `false` |
| `political_district_targets` | array of objects | The political district IDs to target.<br> See [example](#political_district_targets-example).<br>IDs can be fetched using the [Political District Service](political-district-service.md). |

#### `dma_targets` format

```
{
   "dma_targets":[
      {
         "dma":612
      },
      {
         "dma":622
      }
   ]
}
```

#### `domain_targets` format

```
{
   "domain_targets":[
      {
         "profile_id":128350561,
         "domain":"telenet.be"
      },
      {
         "profile_id":99898705,
         "domain":"cnn.us"
      }
   ]
}
```

#### `size_targets` example

```
{
   "size_targets":[
      {
         "width":190,
         "height":213
      },
      {
         "width":728,
         "height":90
      }
   ]
}
```

#### `seller_member_group_targets` format

```
{
   "seller_member_group_targets":[
      {
         "id":1,
         "action_include":"true/false"
      }
   ]
}
```

#### `deal_list_targets` example

```
{
   "profile":{
      "id":1367515,
      "deal_list_targets":[
         {
            "id":"0101"
         },
         {
            "id":"0102"
         }
      ]
   }
}
```

#### `intended_audience_targets` example

```
{
   "intended_audience_targets":[
      "children",
      "general"
   ]
}
```

#### `postal_code_targets` example

```
{
   "profile":{
      "id":1367515,
      "postal_code_targets":[
         {
            "id":"00135"
         },
         {
            "id":"00136"
         }
      ]
   }
}
```

#### `postal_code_list_targets` example

```
{
   "profile":{
      "id":1367515,
      "postal_code_list_targets":[
         {
            "id":"0099"
         },
         {
            "id":"0100"
         }
      ]
   }
}
```

#### `political_district_targets` example

```
{
   "profile":{
      "id":130465799,
      "political_district_targets":[
         {
            "id":"139897"
         }
      ]
   }
}
```

### Targeting results for `deal_action_include` AND `deal_targets` fields

The following targeting results occur for these values of the `deal_action_include` AND `deal_targets` fields:

| `deal_action_include` | `deal_targets` | Targeting Result |
|:---|:---|:---|
| `true` | `null` | Target no deals |
| `false` | `null` | Target all deals |
| `true` | Contains deal targets | Include these deals in targeting |
| `false` | Contains deal targets | Exclude these deals in targeting |

### Mobile app instance targets

For more information about mobile app instances, including instructions on adding them to your profile, see the [Mobile App Instance Service](mobile-app-instance-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of the mobile app instance. |
| `bundle_id` | string | The bundle ID of this mobile app instance. |
| `os_family_id` | int | The OS family ID associated with this mobile app instance. |

### Mobile app instance list targets

For more information about mobile app instance lists, including instructions on adding them to your profile, see the [Mobile App Instance List Service](mobile-app-instance-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of the mobile app instance list. |
| `name` | string | The name of this mobile app instance list. |
| `description` | string | An optional description of the list's purpose or contents. |

### Daypart targets

Each object in the `daypart_targets` array includes the following fields. For formatting, see the [View a profile](#view-a-profile) example below.

| Field | Type | Description |
|:---|:---|:---|
| `day` | enum | The day of the week. <br>Possible values: `sunday`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, or `all`. <br><br>**Note:** These strings must be in lower case. |
| `start_hour` | int | The start hour for the daypart. This must be an integer between `0` and `23`. The campaign will start serving at the beginning of the hour (`6` is equivalent to `"6:00"` am). |
| `end_hour` | int | The end hour for the daypart. This must be an integer between `0` and `23`. The campaign will stop serving at the end of the hour (`23` is equivalent to `"23:59"`). |

### Segment targets

You define the Boolean logic between segments with `segment_boolean_operator` field outside of the array. If `segment_boolean_operator` is `AND`, then the profile will only target users that satisfy all segment targets. If the `segment_boolean_operator` is `OR`, then the profile will target users that satisfy any of the specified segments. For detailed guidance on Boolean logic for segment targeting, see [Segment Targeting](../monetize/segment-targeting.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the segment.<br>**Required On:** `POST` |
| `code` | string | The custom code for the segment. |
| `action` | enum | Possible values: `include` or `exclude`.<br>**Default:** `include` |
| `start_minutes` | int | The lower bound for the amount of time since a user was added to the segment.<br>**Default:** `0` |
| `expire_minutes` | int | The upper bound for the amount of time since a user was added to the segment.<br>**Default:** `-1` |
| `other_equals` | int | The exact segment value to target.<br><br>**Note:** If you use `other_in_list`, you cannot use this field.<br>**Default:** `null` |
| `other_less` | int | The non-inclusive upper bound for segment value targeting.<br>**Default:** `null` |
| `other_greater` | int | The non-inclusive lower bound for segment value targeting.<br>**Default:** `null` |
| `other_in_list` | array | The list of segment values to target.If you use `other_equals`, you cannot use this field.<br>**Default:** `null` |

> [!NOTE]
> For `other_equals`, `other_less`, `other_greater`, and `other_in_list`, the segment value can be an "other" value passed by the segment pixel or can be related to segment query string values (see the `"querystring_mapped"` field in the [Segment Service](segment-service.md)). For examples of how to target query string values in a segment, see other examples below.

In segment targeting, you need to keep the settings for the Boolean logic consistent, otherwise you would not be able to edit the segments in Microsoft Invest UI. For consistent Boolean logic settings, you need to ensure that:

- `segment_boolean_operator` field is set as either “`and`” or “`or`”.
- The `boolean_operator` field in each object of the segment_group_targets array (See Segment Group Targets) is set as either “`and`” or “`or`”. However this value should be the opposite of what is set in `segment_boolean_operator` above. For example, if the value set in segment_boolean_operator is "`or`", the value of `boolean_operator` for the objects should be "`and`".
- The value of `boolean_operator` field for all objects in the segment_group_targets array needs to be same. In short, you cannot have boolean_operator of one object as "`and`" and other as "`or`" in the same profile. For an example of consistent and inconsistent JSONs, see below.

#### Consistent JSONs

```
{
   "segment_boolean_operator":"and",
   "segment_group_targets":[
      {
         "boolean_operator":"or",
         "segments":[
            {
               "action":"include",
               "code":"1094797",
               "deleted":false,
               "expire_minutes":null,
               "id":19285936,
               "name":"Travel Intender",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"3119772",
               "deleted":false,
               "expire_minutes":null,
               "id":19378950,
               "name":"XAS - US HH Demographic - Online Shopping - Travel",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"6502105",
               "deleted":false,
               "expire_minutes":null,
               "id":19378951,
               "name":"XAS - US HH Demographic - Online Shopping - Electronics and Gadgets",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"3734388",
               "deleted":false,
               "expire_minutes":null,
               "id":19378952,
               "name":"XAS - US HH Demographic - Online Shopping - Apparel",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            }
         ]
      },
      {
         "boolean_operator":"or",
         "segments":[
            {
               "action":"include",
               "code":"2137013",
               "deleted":false,
               "expire_minutes":null,
               "id":19378954,
               "name":"XAS - US HH Demographic - Online Shopping - Buy Online",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"2272811",
               "deleted":false,
               "expire_minutes":null,
               "id":19378955,
               "name":"XAS - US HH Demographic - Online Shopping - Personal Health",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"8578372",
               "deleted":false,
               "expire_minutes":null,
               "id":19378957,
               "name":"XAS - US HH Demographic - Online Shopping - Shoes",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            }
         ]
      },
      {
         "boolean_operator":"or",
         "segments":[
            {
               "action":"include",
               "code":"8578372",
               "deleted":false,
               "expire_minutes":null,
               "id":19378957,
               "name":"XAS - US HH Demographic - Online Shopping - Shoes",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"4608982",
               "deleted":false,
               "expire_minutes":null,
               "id":21015599,
               "name":"Xandr Audiences - Demographic - Occupation - Detail - Attorneys",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"2420395",
               "deleted":false,
               "expire_minutes":null,
               "id":21015602,
               "name":"Xandr Audiences - Demographic - Occupation - Detail - Accountants/CPA",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            }
         ]
      }
   ]
}
```

#### Inconsistent JSONs

```
{
   "segment_boolean_operator":"and",
   "segment_group_targets":[
      {
         "boolean_operator":[
            "and",
            "- - same as segment_boolean_operator + also all other boolean_operators in the rest of the object is set to",
            "or",
            "therefore this is inconsistent behavior"
         ],
         "segments":[
            {
               "action":"include",
               "code":"1094797",
               "deleted":false,
               "expire_minutes":null,
               "id":19285936,
               "name":"Travel Intender",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"3119772",
               "deleted":false,
               "expire_minutes":null,
               "id":19378950,
               "name":"XAS - US HH Demographic - Online Shopping - Travel",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"6502105",
               "deleted":false,
               "expire_minutes":null,
               "id":19378951,
               "name":"XAS - US HH Demographic - Online Shopping - Electronics and Gadgets",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"3734388",
               "deleted":false,
               "expire_minutes":null,
               "id":19378952,
               "name":"XAS - US HH Demographic - Online Shopping - Apparel",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            }
         ]
      },
      {
         "boolean_operator":"or",
         "segments":[
            {
               "action":"include",
               "code":"2137013",
               "deleted":false,
               "expire_minutes":null,
               "id":19378954,
               "name":"XAS - US HH Demographic - Online Shopping - Buy Online",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"2272811",
               "deleted":false,
               "expire_minutes":null,
               "id":19378955,
               "name":"XAS - US HH Demographic - Online Shopping - Personal Health",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"8578372",
               "deleted":false,
               "expire_minutes":null,
               "id":19378957,
               "name":"XAS - US HH Demographic - Online Shopping - Shoes",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            }
         ]
      },
      {
         "boolean_operator":"or",
         "segments":[
            {
               "action":"include",
               "code":"8578372",
               "deleted":false,
               "expire_minutes":null,
               "id":19378957,
               "name":"XAS - US HH Demographic - Online Shopping - Shoes",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"4608982",
               "deleted":false,
               "expire_minutes":null,
               "id":21015599,
               "name":"Xandr Audiences - Demographic - Occupation - Detail - Attorneys",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            },
            {
               "action":"include",
               "code":"2420395",
               "deleted":false,
               "expire_minutes":null,
               "id":21015602,
               "name":"Xandr Audiences - Demographic - Occupation - Detail - Accountants/CPA",
               "other_equals":null,
               "other_greater":null,
               "other_in_list":null,
               "other_less":null,
               "start_minutes":null
            }
         ]
      }
   ]
}
```

#### Segment targets example

In this example, since the `segment_boolean_operator` is `AND`, the profile will target only users that fit in both segment 86 and segment 202.

```
{
   "profile":{
      "segment_boolean_operator":"and",
      "segment_targets":[
         {
            "id":86,
            "code":null,
            "name":"Network segment 1",
            "action":"include",
            "start_minutes":0,
            "expire_minutes":-1,
            "other_less":null,
            "other_greater":null,
            "other_equals":null
         },
         {
            "id":202,
            "code":null,
            "name":"Credit Score segment",
            "action":"include",
            "start_minutes":0,
            "expire_minutes":-1,
            "other_less":null,
            "other_greater":null,
            "other_equals":null
         }
      ]
   }
}
```

### Segment group targets

Each segment group object contains the following fields.

> [!NOTE]
> You define the Boolean logic between groups with the `segment_boolean_operator` field outside of the array, and you define the Boolean logic between segments in a group with the `boolean_operator` field within the group object. See the example below for formatting and for an example of the logic of combining `segment_boolean_operator` and `boolean_operator`. For detailed guidance on Boolean logic for segment targeting, see [Segment Targeting](../monetize/segment-targeting.md).
>
> Null segments cannot be added.
>
> You may not add `null` segments to this array using `POST` or `PUT`.

| Field | Type | Description |
|:---|:---|:---|
| `boolean_operator` | enum | The boolean logic between segments in a segment group. Possible values: `and` or `or`. <br>The value of `boolean_operator` field for all objects in the `segment_group_targets` array needs to be same.<br>In short, you cannot have `boolean_operator` of one object as `"and"` and other as `"or"` in the same profile.<br>**Default:** `or`<br>**Required:** `POST` |
| `id` | int | The ID of the segment.<br>**Required:** `POST` |
| `code` | string | The custom code for the segment. |
| `action` | enum | Possible values: `include` or `exclude`.<br>**Default:** `include` |
| `start_minutes` | int | The lower bound for the amount of time since a user was added to the segment.<br>**Default:** `0` |
| `expire_minutes` | int | The upper bound for the amount of time since a user was added to the segment.<br>**Default:** `-1`  |
| `other_equals` | string | The exact segment value to target.<br><br>**Note:** If you use `other_in_list`, you cannot use this field.<br>**Default:** `null` |
| `other_less` | int | The non-inclusive upper bound for segment value targeting.<br>**Default:** `null` |
| `other_greater` | int | The non-inclusive lower bound for segment value targeting.<br>**Default:** `null` |
| `other_in_list` | array | The list of segment values to target.<br><br>**Note:** If you use `other_equals`, you cannot use this field.<br>**Default:** `null` |

> [!NOTE]
> For `other_equals`, `other_less`, `other_greater`, and `other_in_list`, the segment value can be an `"other"` value passed by the segment pixel or can be related to segment query string values (see the `"querystring_mapped"` field in the [Segment Service](segment-service.md)). For examples of how to target query string values in a segment, see other examples below.

#### Segment group targets example

In this example, since the `segment_boolean_operator` is `OR` and the `boolean_operator` for each group is `AND`, the profile will target only users that fit in both segment 11 and segment 22 or both segment 33 and segment 44.

```
{
   "profile":{
      "segment_boolean_operator":"or",
      "segment_group_targets":[
         {
            "boolean_operator":"and",
            "segments":[
               {
                  "id":11,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_equals":null,
                  "other_less":null,
                  "other_greater":null
               },
               {
                  "id":22,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_equals":null,
                  "other_less":null,
                  "other_greater":null
               }
            ]
         },
         {
            "boolean_operator":"and",
            "segments":[
               {
                  "id":33,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_equals":null,
                  "other_less":null,
                  "other_greater":null
               },
               {
                  "id":44,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_equals":null,
                  "other_less":null,
                  "other_greater":null
               }
            ]
         }
      ]
   }
}
```

### Age targets

| Field | Type | Description |
|:---|:---|:---|
| `allow_unknown` | Boolean | Determines whether to include targets where age is not know.<br>**Default:** `false` |
| `ages` | array of objects | The age ranges targeted in this profile. |

#### `ages` object

| Field | Type | Description |
|:---|:---|:---|
| `low` | int | The lower bound of the age range (min 13). |
| `high` | int | The upper bound of the age range (max 100). |

#### Age targets example

```
{
   "profile":{
      "age_targets":{
         "allow_unknown":false,
         "ages":[
            {
               "low":20,
               "high":35
            }
         ]
      }
   }
}            
            
```

### Gender targets

The `gender_targets` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `gender` | enum | The gender of the user. Possible values: `m` (male), or `f` (female).<br>**Default:** `null`<br>**Required On:** `POST` |
| `allow_unknown` | Boolean | If `true`, target ad calls where the gender of the user is not available.<br>**Default:** `false` |

### Country targets

Each object in the `country_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the country. You can use the [Country Service](country-service.md) to retrieve a complete list of country IDs. |
| `name` | string | **Read-only.** The name of the country. |
| `code` | string | **Read-only.** The code for the country. |

#### Country targets example

```
{
   "profile":{
      "country_action":"include",
      "country_targets":[
         {
            "id":233,
            "name":"United States",
            "code":"US"
         }
      ]
   }
}           
            
```

### Region targets

Each object in the `region_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the region. You can use the [Region Service](region-service.md) to retrieve a list of region IDs. |
| `name` | string | **Read-only.** The name of the region. |
| `code` | string | **Read-only.** The code for the region. |
| `country_name` | string | **Read-only.** The name of the country to which the region belongs. |
| `country_code` | string | **Read-only.** The code for the country to which the region belongs. |

#### Region targets example

```
{
   "profile":{
      "region_action":"include",
      "region_targets":[
         {
            "id":3950,
            "name":"New York",
            "code":"NY",
            "country_name":"United States",
            "country_code":"US"
         }
      ]
   }
}            
            
```

### Require transparency and consent framework string

| Field | Type | Description |
|:---|:---|:---|
| `require_transparency_and_consent_framework_string` | boolean | - If `true`, only allow associated objects to purchase inventory where valid TCF string is present<br>- If `false`, allow associated objects to purchase any inventory that falls within pre-defined targeting declarations. |

> [!NOTE]
> This parameter is only applicable to the traffic coming from territories where GDPR applies.

#### Example

```
{
   "profile":{
      "require_transparency_and_consent_framework_string":"false"
   }
}            
            
```

### City targets

Each object in the `city_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the city to target. You can use the [City Service](city-service.md) to retrieve a list of city IDs. |
| `name` | int | **Read-only.** The name of the city to target. |
| `region_name` | string | **Read-only.** The name of the region to which the city belongs. |
| `region_code` | string | **Read-only.** The code of the region to which the city belongs. |
| `country_name` | enum | **Read-only.** The name of the country to which the region belongs. |
| `country_code` | enum | **Read-only.** The code of the country to which the region belongs. |

#### City targets example

```
{
   "profile":{
      "city_action":"include",
      "city_targets":[
         {
            "id":200942,
            "name":"Portland",
            "region_name":"Oregon",
            "region_code":"OR",
            "country_code":"US",
            "country_name":"United States"
         }
      ]
   }
}            
            
```

### Inventory lists

Each object in the `inventory_url_list_targets` array includes the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `deleted` | Boolean | **Read-only.** Indicates whether the inventory list has been deleted. |
| `id` | int | The ID of the allowlist or blocklist to be applied.<br>- The allowlist contains a list of domains and apps to be targeted by the line item that uses the profile.<br>- Each blocklist contains a list of domains and apps to be excluded from targeting by the line item that uses the profile.<br>**Required On:** `POST`, `PUT` |
| `list_type` | string | **Read-only.** Denotes whether the list is a blocklist or allowlist. Valid values are `allowlist` or `blocklist`.<br><br>**Note:** The `list_type` field (used by the [Inventory List Service](inventory-list-service.md)) is **not** used by the Profile Service for determining whether an inventory list is excluded (`blocklist`) in targeting or included (`allowlist`). For excluding or including an inventory list in targeting, see `exclude` field in this table. |
| `name` | string | **Read-only.** Name of the allowlist or blocklist. |
| `exclude` | Boolean | **Read-only.** If `true`, the inventory list will be excluded from targeting (i.e., treated as a blocklist). If `false`, the inventory list will be included in targeting (i.e., treated as an allowlist). This field is solely dependent on the inventory `list_type` field described above. |

#### Inventory lists example

```
{
   "profile":{
      "id":145,
      "inventory_url_list_targets":[
         {
            "deleted":false,
            "id":51,
            "list_type":"blocklist",
            "name":"Blocklist to exclude medical sites",
            "exclude":true
         },
         {
            "deleted":false,
            "id":53,
            "list_type":"blocklist",
            "name":"Blocklist to exclude military sites",
            "exclude":true
         },
         {
            "deleted":false,
            "id":54,
            "list_type":"blocklist",
            "name":"Line Item - Blocklist - 2017-08-23T21:44:42Z",
            "exclude":true
         },
         {
            "deleted":false,
            "id":66,
            "list_type":"allowlist",
            "name":"Test Allowlist for Targeting",
            "exclude":false
         }
      ]
   }
}            
            
```

### Content category targets

The `content_category_targets` object includes the `allow_unknown` field, which is a Boolean, and the `content_category` array. Each object in the `content_category` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the content category to target.<br>**Default:** `null`<br>**Required On:** `POST` |
| `action` | num | The action to take for this content category.<br>Possible values: `include` or `exclude`.<br>If `include`, then category will be targeted; if `exclude`, the category will explicitly not be targeted.<br>**Default:** `exclude` |

#### Content category targets example

```
{
   "profile":{
      "content_category_targets":{
         "allow_unknown":false,
         "content_categories":[
            {
               "id":3,
               "action":"include"
            }
         ]
      }
   }
}            
            
```

### Video targets

The `video_targets` object contains the `allow_unknown_playback_method`, `allow_unknown_context`, `allow_unknown_player_size` fields and the `playback_methods`, `contexts`, `player_sizes` arrays. For Deals, it also contains the `deal_creative_duration` field and the `video_frameworks` arrays.

| Field | Type | Description |
|:---|:---|:---|
| `allow_unknown_playback_method` | Boolean | Use this field to target inventory where the playback method is unknown. Set this field to `true` when using the fields of the `playback_method` array to target specific playback methods AND when you want to include inventory for which no playback method information has been provided.<br>If you are not targeting specific playback methods, this field will have no effect on targeting.<br>**Default:** `false` |
| `allow_unknown_context` | Boolean | Use this field to target inventory where the context is unknown. Set this field to `true` when using the fields of the `contexts` array to target specific contexts AND when you want to include inventory for which no context information has been provided.<br>If you are not targeting specific contexts, this field will have no effect on targeting.<br>**Default:** `false` |
| `allow_unknown_player_size` | Boolean | Use this field to target inventory where the player size is unknown. Set this field to `true` when using the fields of the `player_sizes` array to target specific player sizes AND when you want to include inventory for which no player size information has been provided.<br>If you are not targeting specific player sizes, this field will have no effect on targeting.<br>**Default:** `false` |

> [!NOTE]
>
> - When you do NOT set any specific video targeting options, you will target all inventory, including undefined inventory.
> - Ensure that you have elected to include or exclude intro and outro creatives by setting them in the `ad_slot_intro_bumper_action_include` and `ad_slot_outro_bumper_action_include` fields.

### Contexts

The default value is an empty array, and will target any roll position. The `contexts` array contains objects with the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the context. Possible values:<br>- `1`: position-pre-roll<br>- `2`: position-mid-roll<br>- `3`: position-post-roll<br>- `4`: outstream |
| `name` | string | **Read-only.** Possible values: `pre-roll`, `mid-roll`, `post-roll`, or `outstream`. |

### Playback methods

The default value is an empty array, and will target any playback method. The `playback_methods` array contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the playback method. Possible values:<br>- `1`: playback-method-auto-play-sound-on<br>- `2`: playback-method-auto-play-sound-off<br>- `3`: playback-method-click-to-play<br>- `4`: playback-method-mouse-over<br>- `5`: playback-method-auto-play-sound-unknown |
| `name` | string | **Read-only.** Possible values: `auto_play_sound_on`, `auto_play_sound_off`, `click_to_play`, `mouse_over`, or `auto_play_sound_unknown`. |

### Player sizes

The default value is an empty array, and will target any player size. The `player_sizes` array contains objects with the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the player size. Possible values:<br>- `1`: player-size-sm <br>- `2`: player-size-med<br>- `3`: player-size-lg |
| `name` | string | **Read-only.** Possible values: `small`, `medium`, or `large`. |
| `min_width` | int | **Read-only.** The minimum width of the player, in pixels. |
| `max_width` | int | **Read-only.** The maximum width of the player, in pixels. |

### Creative duration

The `deal_creative_duration` setting is only used by video deal line items. It lets deals target impressions that allow at least a given creative duration, so creatives of the defined length can successfully serve through a deal without errors. It will aggregate only the impressions with the given setting already in place.

| Field | Type | Description |
|:---|:---|:---|
| `deal_creative_duration` | int | The duration of the video creative in seconds. |

### Video frameworks

The `video_frameworks` array is only used by video deal line items. It lets deals target impressions that allow a given video framework (for example, VPAID) so creatives of this type can successfully serve through a deal without errors. This setting won’t override existing placement settings; it will aggregate only the impressions with the given setting already in place.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The id of the video framework. IDs include:<br>- `VPAID 1.0`<br>- `VPAID 2.0`<br>- `MRAID-1`<br>- `ORMMA`<br>- `MRAID-2` |
| `name` | string | The name of the video framework. <br>Possible values:<br>- `vpaid_1_0`<br>- `vpaid_2_0`<br>- `mraid_1`<br>- `ormma`<br>- `mraid_2` |

#### Video frameworks example

```
{
   "profile":{
      "video_targets":{
         "allow_unknown_playback_method":true,
         "allow_unknown_context":true,
         "allow_unknown_player_size":true,
         "contexts":[
            {
               "id":1,
               "name":"pre-roll"
            },
            {
               "id":2,
               "name":"mid-roll"
            },
            {
               "id":4,
               "name":"outstream"
            }
         ],
         "playback_methods":[
            {
               "id":2,
               "name":"auto_play_sound_off"
            },
            {
               "id":3,
               "name":"click_to_play"
            }
         ],
         "player_sizes":[
            {
               "id":1,
               "name":"small",
               "min_width":0,
               "max_width":300
            }
         ],
         "deal_creative_duration":60,
         "video_frameworks":[
            {
               "id":1,
               "name":"vpaid_1_0"
            },
            {
               "id":2,
               "name":"vpaid_2_0"
            }
         ]
      }
   }
}            
            
```

### Engagement rate targets

The `engagement_rate_targets` array of objects is used to target specific, highly performant inventory based on historic performance. You can use targeting criteria to purchase either video inventory with a high completion rate, or highly viewable inventory, by specifying the desired video completion rate or viewability rate.

| Field | Type | Description |
|:---|:---|:---|
| `engagement_rate_type` | enum | The targeting criteria.<br>Possible values:<br>- `1: video_completion` - Video Completion Rate. A prediction of how likely a video impression is to be fully played (video completes/total impressions).<br>- `2: view` - Predicted IAB Viewability Rate (previously known as  "Estimated IAB Viewthrough Rate"). A prediction of how likely a web display impression is to be viewable (viewed/measured impressions), judged by the IAB standard.<br>- `3: view_over_total` - Predicted IAB Viewability Rate Over Total. A prediction of how likely a web display impression is to be viewable (viewed/total impressions), judged by the IAB standard.<br>- `4: predicted_iab_video_view_rate` - Predicted IAB Video Viewability Rate. A prediction of how likely a web video impression is to be viewable (viewed/measured impressions), judged by the IAB standard.<br>- `5: predicted_iab_video_view_rate_over_total` - Predicted IAB Video Viewability Rate Over Total A prediction of how likely a web video impression is to be viewable (viewed/total impressions), judged by the IAB standard.<br>- `6: predicted_100pv50pd_video_view_rate` - Predicted Video Viewability Rate (100% View, 50% Duration, Sound On). A prediction of how likely a web video impression is to be viewable (viewed/measured impressions), judged by this custom standard (100% viewable, 50% duration, sound on).<br>- `7: predicted_100pv50pd_video_view_rate_over_total` - Predicted Video Viewability Rate Over Total (100% View, 50% Duration, Sound On). A prediction of how likely a web video impression is to be viewable (viewed/total impressions), judged by this custom standard (100% viewable, 50% duration, sound on).<br>- `8: predicted_100pv1s_display_view_rate` - Predicted Viewability Rate (100% View). A prediction of how likely a web display impression is to be viewable (viewed/measured impressions), judged by this custom standard (100% viewable, 1 second).<br>- `9: predicted_100pv1s_display_view_rate_over_total` - Predicted Viewability Rate Over Total (100% View). A prediction of how likely a web display impression is to be viewable (viewed/total impressions), judged by this custom standard (100% viewable, 1 second). |
| `engagement_rate_pct` | int | Possible values: `1` - `100`. |

### Deal targets

Each object in the `deal_targets` array contains the following fields.

> [!NOTE]
> To target or exclude deals, in addition to setting the fields within this array as needed, you must also:
>
> - Set the `deal_action_include` field to `true` or `false` (depending on inclusion or exclusion).
> - When using ALIs, set the `deals` field to `true` within the `supply_strategies` array of the [Line Item Service](line-item-service.md).
> - Programmatic Guaranteed Buying Line Items can only have one deal target in the `deal_targets` array.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the deal. To retrieve the IDs of your deals, use the [Deal Buyer Access Service](deal-buyer-access-service.md). |
| `name` | string | **Read-only.** The name of the deal. |
| `code` | string | **Read-only.** The custom code for the deal. For deals with external supply partners, this is generally the string that you will use to identify the deal. |

#### Deal targets example

```
{
   "profile":{
      "deal_targets":[
         {
            "id":44,
            "name":"Deal with external supply partner",
            "code":"APN-1234-2200f"
         },
         {
            "id":45,
            "name":"Deal with UI seller",
            "code":null
         }
      ]
   }
}            
            
```

### Position targets

The `position_targets` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `allow_unknown` | Boolean | If `true`, the profile will target placements for which the fold position is not known.<br>**Default:** `false` |
| `positions` | array of objects | The fold positions to target. Possible values: `"above"` or `"below"`. |

#### Position targets example

```
{
   "profile":{
      "position_targets":{
         "allow_unknown":false,
         "positions":[
            {
               "position":"above"
            }
         ]
      }
   }
}            
            
```

### Device model targets

Each object in the `device_model_targets` array contains the following fields.

> [!TIP]
> To retrieve the IDs of device models registered in our system, use the [Device Model Service](device-model-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the device model. |
| `name` | string | **Read-only.** The name of the device model, i.e., `Onetab XST2`, `PAD7`, `A101`, etc. |

#### Device model targets example

```
{
   "profile":{
      "device_model_action":"include",
      "device_model_targets":[
         {
            "id":1,
            "name":"Onetab XST2"
         },
         {
            "id":2,
            "name":"PAD7"
         },
         {
            "id":3,
            "name":"A101"
         }
      ]
   }
}            
            
```

### Device type targets

The `device_type_targets` array can contain one or more of the following strings:

- `phone`
- `tablet`
- `pc`
- `tv`
- `gameconsole`
- `stb`
- `mediaplayer`

#### Device type targets example

```
{
   "profile":{
      "device_type_action":"include",
      "device_type_targets":[
         "phone",
         "tablet"
      ]
   }
}            
            
```

### Carrier targets

Each object in the `carrier_targets` array contains the following fields.

> [!NOTE]
>
> - To retrieve the IDs of mobile carriers registered in our system, use the [Carrier Service](carrier-service.md).
> - The ability to target by carrier refers to the fact that you can target devices currently using that carrier's network. You are not able to target subscribers of the network.
>
>   For example, a Verizon iPhone using a 4G network can be targeted as Verizon when on 4G, but not when the user is connected to their home wifi.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the mobile carrier. |
| `name` | string | **Read-only.** The name of the mobile carrier. |
| `country` | enum | **Read-only.** The ISO code for the country in which the carrier operates. |

#### Carrier targets example

```
{
   "profile":{
      "carrier_action":"include",
      "carrier_targets":[
         {
            "id":14,
            "name":"Verizon - US",
            "country":"US"
         },
         {
            "id":26,
            "name":"Sprint - US",
            "country":"US"
         },
         {
            "id":32,
            "name":"Orange - US",
            "country":"US"
         }
      ]
   }
}            
            
```

### IP range list targets

For more information about IP range lists, see the [IP Range List Service](ip-range-list-service.md).

Per profile, you can target up to 10 `"include"` IP range lists (`include` set to `true` in the IP range list) and no more than 1 `"exclude"` IP range list (`include` set to `false` in the IP range list). The excluded IP ranges must be a subset of the included IP ranges.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of this IP range list. |
| `name` | string | **Read-only.** The name of this IP range list. |
| `include` | Boolean | **Read-only.** Whether to include or exclude the IP ranges in the IP range list. This is defined in the IP range list itself, not in the profile |
| `description` | string | **Read-only.** An optional description of the list's purpose or contents. |

### Operating system extended targets

The `operating_system_extended_targets` array specifies operating system versions (e.g., Android 3.x, Apple iOS 6, etc.) to either include in or exclude from your targeting.

> [!NOTE]
> `operating_system_extended_targets` array is used to target specific operating system versions, whereas `operating_system_family_targets` is used to target all versions of operating systems.
>
> - **OS family targets and OS extended targets work together**
>
>   The OS Family and OS Extended Targets are most effective when used together. For examples of how to use their combined targeting
>   capabilities, see the [Use OS Family Targets and OS Extended Targets together](#use-os-family-targets-and-os-extended-targets-together) example below.
>
> - To use `operating_system_extended_targets`, you must set `use_operating_system_extended_targeting` to `true`. Once a profile is created using the `operating_system_extended_targets`, you will not be allowed to set `use_operating_system_extended_targeting` to `false` or populate the `operating_system_targets` fields on `PUT`.

Each object in the `operating_system_extended_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the operating system version. To retrieve the IDs of operating system versions registered in our system, use the [Operating System Extended Service](operating-system-extended-service.md). |
| `name` | string | **Read-only.** The name of the operating system version, e.g., `Android 3.x`, `Apple iOS 5`, etc. |
| `action` | enum | Action to be taken on `id`.<br>Possible values: `include` or `exclude`. |

#### Operating system extended targets example

```
{
   "profile":{
      "use_operating_system_extended_targeting":true,
      "operating_system_extended_targets":[
         {
            "id":2,
            "name":"Android 2.1",
            "action":"exclude"
         },
         {
            "id":3,
            "name":"Android 2.2",
            "action":"include"
         }
      ]
   }
}
            
```

### Operating system family targets

The `operating_system_family_targets` array specifies the operating systems as a whole (e.g., Android, Apple iOS, Windows 7, Windows 11 etc.) to either include in or exclude from your targeting, as defined by the `operating_system_family_action` field.

> [!NOTE]
> `operating_system_family_action` field is used to target all versions of operating systems, whereas `operating_system_targets` is used to target specific versions of operating systems.
>
> **OS Family Targets and OS Extended Targets Work Together**
>
> The OS Family and OS Extended Targets are most effective when used together. For examples of how to use their combined targeting capabilities, see the [Use OS Family Targets and OS Extended Targets together](#use-os-family-targets-and-os-extended-targets-together) example below.

Each object in the `operating_system_family_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the operating system family. To retrieve the IDs of operating system families registered in our system, use the [Operating System Family Service](operating-system-family-service.md). |
| `name` | string | **Read-only.** The name of the operating system family, i.e., `Microsoft Windows`, `Android`, `Apple iOS`, etc. |

#### Operating system family targets example

```
{
   "profile":{
      "operating_system_family_action":"exclude",
      "operating_system_family_targets":[
         {
            "id":2,
            "name":"Android"
         },
         {
            "id":3,
            "name":"Apple iOS"
         }
      ]
   }
}            
            
```

### Key value targets

The `key_value_targets` field defines the combination of custom keys and values that are targeted in this profile. The field is a parsed version of a logical expression.

You can find more information on how key value targeting works and details on how to parse out expressions for the profile service at [Custom Key Value Targeting](custom-key-value-targeting.md).

#### `key_value_targets` object

| Field | Type | Description |
|:---|:---|:---|
| `kv_expression` | object | This is a wrapper object that contains all the key/value targeting objects, including the `header` and `exp` objects. |

| Field | Type | Description |
|:---|:---|:---|
| `header` | object | Versioning information used to evaluate the expression. |
| `exp` | object | The regular expression that defines the combination of key/values. |

#### `header` object

| Field | Type | Value | Description |
|:---|:---|:---|:---|
| `an_version` | string | `1.0` | The version of the back-end engine evaluating the expression.<br>Current version is `1.0`. This field is required on `PUT` and `POST`. |
| `client_version` | string | `1.0` | The version of the client-facing implementation of the expression (the format shown in the example below). Current version is `1.0`. This field is required on `PUT` and `POST`. |

#### `exp` object

| Field | Type | Description |
|:---|:---|:---|
| `typ` | string | The operators used in the expression. Possible values include:<br>- `and`<br>- `or`<br>- `not`<br>- `in`<br>- `eq` (equal to)<br>- `gt` (greater than)<br>- `lt` (less than)<br>- `gte` (greater than or equal to)<br>- `lte` (less than or equal to)<br>- `neq` (not equal to)<br><br>The operators `and`, `or`, and `not` can be used only with sub-expressions.<br>The operators `gt`, `lt`, `gte` and `lte` can be used only with numeric values.<br>All operators must be lowercase. |
| `sbe` | exp object | An object containing the sub-expression (the elements of the expression). |
| `key` | string | The name of the targeting key. |
| `vtp` | type | This field identifies the data type of the expression value. The value you enter in this field must match the field and type of the corresponding value field. The following values are valid:<br>- `num`: *numeric*; a value must be provided in the `vnm` field.<br>- `str`: *string*; a value must be provided in the `vst` field.<br>- `nma`: *numeric array*; a value must be provided in the `vna` field.<br>- `sta`: *string array*; a value must be provided in the `vsa` field. |
| `vnm` | numeric value | The value as a 32-bit signed float (for example, 25.3). Numbers can be up to 13 digits (with a maximum of six digits to the right of the decimal point). |
| `vst` | string | The value as a string. |
| `vna` | array of numeric values | A set of values as an array of floats. |
| `vsa` | array of strings | A set of values as an array of strings. |

#### Key value targets example

```
{
   "profile":{
      "key_value_targets":{
         "kv_expression":{
            "header":{
               "an_version":"1.0",
               "client_version":"1.0"
            },
            "exp":{
               "typ":"and",
               "sbe":[
                  {
                     "exp":{
                        "typ":"eq",
                        "key":"fruit",
                        "vtp":"str",
                        "vst":"apple"
                     }
                  },
                  {
                     "exp":{
                        "typ":"eq",
                        "key":"city",
                        "vtp":"str",
                        "vst":"NY"
                     }
                  }
               ]
            }
         }
      }
   }
}            
            
```

### Inventory URL allowlist settings

The fields in this object are used to set how allowlists attached to a line item will be applied. All allowlists will be applied to RTB buying by default. You can additionally choose to apply the allowlists to Managed buying as well.

| Field | Type | Description |
|:---|:---|:---|
| `apply_to_managed` | boolean | Designates whether the allowlist is to be applied to managed buying. If set to `true`, any allowlists associated with the line item will be applied to managed buying.<br><br>**Note:** Set this field to `true` if the line item associated with this profile has its `inventory_type` field set to `direct`.<br>**Default:** `false` |
| `apply_to_rtb` | boolean | **Read-only.** All allowlists associated with the line item will be applied to RTB buying.<br>**Default:** `false` |

#### Inventory URL allowlist settings example

```
{
   "inventory_url_allowlist_settings":{
      "apply_to_managed":true,
      "apply_to_rtb":true
   }
}            
            
```

## Examples

### View a profile

This is an example of a profile service.

> [!NOTE]
> For the sake of demonstration, this profile has an unrealistic targeting strategy.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/profile?id=439&advertiser_id=8&member_id=123'

{
   "response":{
      "status":"OK",
      "count":1,
      "start_element":0,
      "num_elements":100,
      "profile":{
         "id":37291837,
         "code":null,
         "description":null,
         "country_action":"include",
         "region_action":"exclude",
         "city_action":"exclude",
         "browser_action":"exclude",
         "ads_txt_authorized_only":false,
         "use_inventory_attribute_targets":true,
         "last_modified":"2015-07-17 20:01:56",
         "daypart_timezone":null,
         "dma_action":"exclude",
         "domain_action":"exclude",
         "domain_list_action":"include",
         "inventory_action":"exclude",
         "language_action":"include",
         "segment_boolean_operator":"or",
         "min_session_imps":null,
         "session_freq_type":"platform",
         "carrier_action":"exclude",
         "supply_type_action":"exclude",
         "device_type_action":"exclude",
         "screen_size_action":"exclude",
         "device_model_action":"exclude",
         "location_target_radius":null,
         "location_target_latitude":null,
         "location_target_longitude":null,
         "querystring_action":"exclude",
         "querystring_boolean_operator":"and",
         "is_expired":false,
         "non_audited_url_action":"include",
         "daypart_bitmap":"000000000000000000000000111111111111111111111000111111111111111111111000111111111111111111111000111111111111111111111000111111111111111111111000000000000000000000000000",
         "optimization_zone_action":"exclude",
         "advertiser_id":16401,
         "publisher_id":null,
         "max_session_imps":null,
         "max_day_imps":null,
         "max_lifetime_imps":100,
         "max_page_imps":null,
         "min_minutes_per_imp":30,
         "venue_action":"exclude",
         "operating_system_action":"exclude",
         "require_cookie_for_freq_cap":true,
         "trust":"seller",
         "allow_unaudited":false,
         "is_template":false,
         "created_on":"2015-07-17 20:01:56",
         "operating_system_family_action":"exclude",
         "use_operating_system_extended_targeting":true,
         "mobile_app_instance_action_include":false,
         "mobile_app_instance_list_action_include":true,
         "user_group_targets":{
            "include_cookieless_users":false,
            "groups":[
               {
                  "low":0,
                  "high":49
               }
            ]
         },
         "country_targets":[
            {
               "id":233,
               "name":"United States",
               "code":"US"
            }
         ],
         "region_targets":[
            {
               "id":3950,
               "name":"New York",
               "code":"NY",
               "country_name":"United States",
               "country_code":"US"
            }
         ],
         "city_targets":null,
         "inv_class_targets":null,
         "inventory_attribute_targets":[
            {
               "id":2,
               "name":"Political",
               "deleted":false
            },
            {
               "id":4,
               "name":"Social media",
               "deleted":false
            },
            {
               "id":6,
               "name":"Photo and video sharing",
               "deleted":false
            },
            {
               "id":8,
               "name":"Forums (moderated)",
               "deleted":false
            },
            {
               "id":10,
               "name":"Forums (unmoderated)",
               "deleted":false
            },
            {
               "id":12,
               "name":"Incentivized clicks",
               "deleted":false
            },
            {
               "id":14,
               "name":"Non-english languages",
               "deleted":false
            },
            {
               "id":16,
               "name":"Streaming media",
               "deleted":false
            },
            {
               "id":17,
               "name":"Toolbars, plugins, or extensions",
               "deleted":false
            },
            {
               "id":29,
               "name":"Contextual Nudity",
               "deleted":false
            }
         ],
         "age_targets":{
            "allow_unknown":false,
            "ages":[
               {
                  "low":18,
                  "high":24
               },
               {
                  "low":25,
                  "high":34
               },
               {
                  "low":35,
                  "high":44
               }
            ]
         },
         "daypart_targets":[
            {
               "day":"monday",
               "start_hour":0,
               "end_hour":20
            },
            {
               "day":"tuesday",
               "start_hour":0,
               "end_hour":20
            },
            {
               "day":"wednesday",
               "start_hour":0,
               "end_hour":20
            },
            {
               "day":"thursday",
               "start_hour":0,
               "end_hour":20
            },
            {
               "day":"friday",
               "start_hour":0,
               "end_hour":20
            }
         ],
         "browser_targets":[
            {
               "id":4,
               "name":"Internet Explorer (other versions)",
               "deleted":false
            },
            {
               "id":11,
               "name":"Opera (all versions)",
               "deleted":false
            }
         ],
         "dma_targets":null,
         "domain_targets":[
            {
               "profile_id":37291837,
               "domain":"test.com"
            }
         ],
         "domain_list_targets":[
            {
               "id":3905,
               "name":"Test Domain List 1",
               "description":"",
               "type":"white",
               "deleted":false
            }
         ],
         "language_targets":[
            {
               "id":1,
               "name":"English",
               "code":"EN",
               "deleted":false
            }
         ],
         "size_targets":null,
         "zip_targets":null,
         "member_targets":[
            {
               "id":1185,
               "action":"include",
               "third_party_auditor_id":null,
               "billing_name":"AppNexus Demo"
            }
         ],
         "video_targets":null,
         "segment_group_targets":[
            {
               "boolean_operator":"and",
               "segments":[
                  {
                     "id":465381,
                     "action":"include",
                     "start_minutes":null,
                     "expire_minutes":null,
                     "other_less":null,
                     "other_greater":null,
                     "other_equals":null,
                     "code":null,
                     "name":null,
                     "deleted":false,
                     "other_in_list":null
                  },
                  {
                     "id":465382,
                     "action":"include",
                     "start_minutes":null,
                     "expire_minutes":null,
                     "other_less":null,
                     "other_greater":null,
                     "other_equals":null,
                     "code":null,
                     "name":null,
                     "deleted":false,
                     "other_in_list":null
                  }
               ]
            },
            {
               "boolean_operator":"and",
               "segments":[
                  {
                     "id":514839,
                     "action":"exclude",
                     "start_minutes":null,
                     "expire_minutes":null,
                     "other_less":null,
                     "other_greater":null,
                     "other_equals":null,
                     "code":null,
                     "name":null,
                     "deleted":false,
                     "other_in_list":null
                  },
                  {
                     "id":523129,
                     "action":"include",
                     "start_minutes":null,
                     "expire_minutes":null,
                     "other_less":null,
                     "other_greater":null,
                     "other_equals":null,
                     "code":null,
                     "name":null,
                     "deleted":false,
                     "other_in_list":null
                  }
               ]
            }
         ],
         "carrier_targets":null,
         "supply_type_targets":null,
         "device_type_targets":null,
         "screen_size_targets":null,
         "device_model_targets":null,
         "querystring_targets":null,
         "gender_targets":null,
         "intended_audience_targets":[
            "general",
            "children",
            "young_adult"
         ],
         "inventory_network_resold_targets":null,
         "operating_system_targets":null,
         "operating_system_family_targets":[
            {
               "id":6,
               "name":"BlackBerry OS"
            },
            {
               "id":8,
               "name":"Linux"
            }
         ],
         "position_targets":{
            "allow_unknown":true,
            "positions":null
         },
         "site_targets":null,
         "venue_targets":null,
         "operating_system_extended_targets":null,
         "mobile_app_instance_targets":null,
         "mobile_app_instance_list_targets":[
            {
               "id":3,
               "name":"Mopub iOS Apps 1-100",
               "description":"",
               "deleted":false
            }
         ],
         "optimization_zone_targets":null,
         "content_category_targets":{
            "allow_unknown":false,
            "content_categories":[
               {
                  "id":7,
                  "action":"exclude",
                  "name":"Beauty and Personal Care",
                  "is_system":true,
                  "deleted":false
               },
               {
                  "id":10,
                  "action":"include",
                  "name":"Arts and Entertainment",
                  "is_system":true,
                  "deleted":false
               },
               {
                  "id":20344,
                  "action":"exclude",
                  "name":"",
                  "is_system":false,
                  "deleted":false
               },
               {
                  "id":22224,
                  "action":"include",
                  "name":"",
                  "is_system":false,
                  "deleted":false
               }
            ]
         },
         "deal_targets":null,
         "placement_targets":null,
         "platform_content_category_targets":null,
         "platform_placement_targets":null,
         "platform_publisher_targets":[
            {
               "id":500070,
               "action":"exclude",
               "name":"Mediaset",
               "deleted":false
            }
         ],
         "publisher_targets":null,
         "segment_targets":null,
         "exelate_targets":null,
         "ip_range_list_targets":null
      }
   }
}
```

### Target a range of query string values

Scenario: Two auto publishers told you to expect `"car year"` data in the query strings of their placements. The first passes the year with the `"car_year"` parameter, and the second passes the year with the `"car_YYYY"` parameter. In order to target this information in your campaign, you added the `"car_year"` parameter to segment 25 and the `"car_YYYY"` parameter to segment 26. Now you want to update the campaign's profile to target placements that include either parameter when the parameter passes any year between `"car_year=2009"` and `"car_year=2012"`, so you create the following JSON and make a `PUT` call to update the profile.

```
$ cat profile_update

{
   "profile":{
      "segment_group_targets":[
         {
            "boolean_operator":"or",
            "segments":[
               {
                  "id":25,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_less":2012,
                  "other_greater":2009
               },
               {
                  "id":26,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_less":2012,
                  "other_greater":2009
               }
            ]
         }
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @profile_update 'https://api.appnexus.com/profile?id=9&advertiser_id=210&member_id=123'

{
   "response":{
      "status":"OK",
      "count":1,
      "id":9
   }
}
```

### Target a list of query string values

Scenario: An auto publisher told you to expect any of the following key-values in the query strings of their placements: `"car_make=ford"`, `"car_make=honda"`, or `"car_make=toyota"`. In order to target such information, you added the parameter and values to segment 12. Now you want to update the campaign's profile to target those values, so you create the following JSON and make a `PUT` call to update the profile.

```
$ cat profile_update

{
   "profile":{
      "segment_group_targets":[
         {
            "segments":[
               {
                  "id":12,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_in_list":[
                     "ford",
                     "honda",
                     "toyota"
                  ]
               }
            ]
         }
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @profile_update 'https://api..com/profile?id=10&advertiser_id=210&member_id=123'

{
   "response":{
      "status":"OK",
      "count":1,
      "id":10
   }
}
```

### Target an exact query string value

Scenario: An auto publisher told you to expect the following key-values in the query strings of their placements: `car_color=red`, `car_color=blue`, or `car_color=black`. In order to target such information, you added the parameter and values to segment 15. Now you want to update the campaign's profile to target a specific query string value, `black`, so you create the following JSON and make a `PUT` call to update the profile.

```
$ cat profile_update

{
   "profile":{
      "segment_group_targets":[
         {
            "segments":[
               {
                  "id":15,
                  "code":null,
                  "action":"include",
                  "start_minutes":0,
                  "expire_minutes":-1,
                  "other_equals":"black"
               }
            ]
         }
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @profile_update 'https://api..com/profile?id=10&advertiser_id=210&member_id=123'

{
   "response":{
      "status":"OK",
      "count":1,
      "id":10
   }
}
```

### Target specific countries

Scenario: You want to target your profile to the United States and Canada. This requires setting `country_action` to `include` and `country_targets` to `US` and `CA`, so you create the following JSON and make a `PUT` call to update the profile.

```
$ cat profile_update

{
   "profile":{
      "country_action":"include",
      "country_targets":[
         {
            "id":233
         },
         {
            "id":39
         }
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @profile_update 'https://api..com/profile?id=10&advertiser_id=210&member_id=123'

{
   "response":{
      "status":"OK",
      "count":1,
      "id":10
   }
}
```

### Target a specific state but exclude a DMA

Scenario: You want to target your profile to the state of New York, excluding the New York City area. This requires setting `region_action` to `include`, `region_targets` to `US:NY`, `dma_action` to `exclude`, and `dma_targets` to `501`, which is the DMA code for New York City. You therefore create the following JSON and make a `PUT` call to update the profile.

```
$ cat profile_update

{
   "profile":{
      "region_action":"include",
      "region_targets":[
         {
            "id":1
         }
      ],
      "dma_action":"exclude",
      "dma_targets":[
         {
            "dma":501
         }
      ]
   }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @profile_update 'https://api..com/profile?id=10&advertiser_id=210&member_id=123'

{
   "response":{
      "status":"OK",
      "count":1,
      "id":10
   }
}
```

### Target a deal

Scenario: You have negotiated a deal with a seller that grants you access to inventory that is not available to other buyers (i.e., a private auction). To take advantage of this deal, you need to use the Deal Buyer Access Service to find the deal ID and then update the `deal_targets` array of your profile to target that ID.

1. To find the ID for your deal, you make a `GET` call to the [Deal Buyer Access Service](deal-buyer-access-service.md) and identify the right deal. Alternately, if you know the member ID of the seller, you can pass it in the query string to retrieve only deals you have with that seller, as shown below.

    ```
    $ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-access?seller_member_id=814'
     
    {
       "response":{
          "status":"OK",
          "count":1,
          "start_element":0,
          "num_elements":100,
          "deals":[
             {
                "id":65,
                "code":null,
                "name":"Private deal for buyer 1085 with floor of 2.5",
                "description":null,
                "active":true,
                "seller_member_id":814,
                "start_date":"2013-12-01 00:00:00",
                "end_date":"2013-12-31 23:59:59",
                "profile_id":null,
                "floor_price":2.5,
                "currency":"USD",
                "use_deal_floor":true,
                "last_modified":"2013-12-04 22:37:49",
                "buyer":{
                   "id":1085,
                   "bidder_id":2
                },
                "type":{
                   "id":2,
                   "name":"Private Auction"
                },
                "brands":[
                   {
                      "id":1
                   }
                ]
             }
          ]
       }
    }
    ```

1. You then create the JSON file with `deal_targets` set to the ID of the deal.

    ```
    $ cat profile_update

    {
       "profile":{
          "deal_targets":[
             {
                "id":65
             }
          ]
       }
    }
    ```

1. Finally, you make a `PUT` call to update the profile.

    ```
    $ curl -b cookies -c cookies -X PUT -d @profile_update 'https://api.appnexus.com/profile?id=22&advertiser_id=210&member_id=123'

    {
       "response":{
          "status":"OK",
          "count":1,
          "id":22
       }
    }
    ```

### Use OS family targets and OS extended targets together

The OS extended and OS family targets work in tandem to allow different targeting scenarios for specific operating system families. This functionality is best represented by usage examples. This section contains the following examples (scroll down or search to view them).

- Target iOS 7.0 devices; all other OS families and other iOS versions will not serve.
- Target all iOS devices regardless of version; all other OS families will not serve.
- Target all OSes that are not Unknown, Linux, or Symbian.
- Target all Android devices, along with iOS 7.0.
- Target all Android and all iOS and all Windows Mobile.
- Target Mac OS 10.8 (Mountain Lion) and MS Windows 8.0.
- Target Mac OS X 10.8 (Mountain Lion) and all Windows Desktop except XP and 2000.
- Target all iOS operating systems except 2.0 and 2.1.
- Invalid configuration: Cannot include an OS family and exclude its members.
- Invalid configuration: Cannot include and exclude members of the same OS family.
- Invalid configuration: Cannot include members of an excluded OS family.

### Target iOS 7.0 devices; all other OS families and other iOS versions will not serve

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":{
         
      },
      "operating_system_extended_targets":{
         "id":80,
         "name":"iOS 7.0",
         "action":"include"
      }
   }
}            
            
```

### Target all iOS devices regardless of version; all other OS families will not serve

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":{
         "id":3,
         "name":"Apple iOS"
      }
   },
   "operating_system_extended_targets":{
      
   }
}            
            
```

### Target all OS that are not Unknown, Linux, or Symbian

In other words, serve on any Android, iOS, MacOS, Windows, Blackberry, or Windows Mobile device.

```
{
   "profile":{
      "operating_system_family_action":"exclude",
      "operating_system_family_targets":[
         {
            "id":0,
            "name":"Unknown"
         },
         {
            "id":8,
            "name":"Linux"
         },
         {
            "id":9,
            "name":"Symbian OS"
         }
      ]
   }
}            
            
```

### Target all Android devices, along with iOS 7.0

All other iOS versions will not serve, and all non-Android devices will not serve.

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":{
         "id":2,
         "name":"Android"
      }
   },
   "operating_system_extended_targets":[
      {
         "id":80,
         "name":"iOS 7.0",
         "action":"include"
      }
   ]
}            
            
```

### Target all Android and all iOS and all Windows mobile

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":[
         {
            "id":2,
            "name":"Android"
         },
         {
            "id":3,
            "name":"Apple iOS"
         },
         {
            "id":7,
            "name":"Microsoft Mobile"
         }
      ],
      "operating_system_extended_targets":{
         
      }
   }
}            
            
```

### Target Mac OS 10.8 (Mountain Lion) and MS Windows 8.0

This example combines OS Extended Targets from different OS families.

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":{
         
      },
      "operating_system_extended_targets":[
         {
            "id":81,
            "name":"10.8 Mountain Lion",
            "action":"include"
         },
         {
            "id":93,
            "name":"Windows 8",
            "action":"include"
         }
      ]
   }
}            
            
```

### Target Mac OS X 10.8 (Mountain Lion) and all Windows Desktop except XP and 2000

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":{
         
      },
      "operating_system_extended_targets":[
         {
            "id":80,
            "name":"10.8 Mountain Lion",
            "action":"include"
         },
         {
            "id":89,
            "name":"Windows 2000",
            "action":"exclude"
         },
         {
            "id":90,
            "name":"Windows XP",
            "action":"exclude"
         }
      ]
   }
}            
            
```

### Target all iOS operating systems except 2.0 and 2.1

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":[
         {
            "id":3,
            "name":"Apple iOS"
         }
      ],
      "operating_system_extended_targets":[
         {
            "id":47,
            "action":"include",
            "name":"iOS 2.0"
         },
         {
            "id":48,
            "action":"include",
            "name":"iOS 2.1"
         }
      ]
   }
}            
            
```

The following profile targeting configurations are invalid and may result in unexpected behavior.

### Invalid configuration: Cannot include an OS family and exclude its members

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":[
         {
            "id":3,
            "name":"Apple iOS"
         }
      ],
      "operating_system_extended_targets":[
         {
            "id":47,
            "action":"include",
            "name":"iOS 2.0"
         },
         {
            "id":48,
            "action":"include",
            "name":"iOS 2.1"
         }
      ]
   }
}            
            
```

### Invalid configuration: Cannot include and exclude members of the same OS family

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":{
         
      },
      "operating_system_extended_targets":[
         {
            "id":47,
            "name":"iOS 2.0",
            "action":"include"
         },
         {
            "id":48,
            "name":"iOS 2.1",
            "action":"exclude"
         }
      ]
   }
}            
            
```

### Invalid configuration: Cannot include members of an excluded OS family

```
{
   "profile":{
      "operating_system_family_action":"include",
      "operating_system_family_targets":[
         {
            "id":3,
            "name":"Apple iOS"
         }
      ],
      "operating_system_extended_targets":[
         {
            "id":47,
            "action":"include",
            "name":"iOS 2.0"
         },
         {
            "id":48,
            "action":"include",
            "name":"iOS 2.1"
         }
      ]
   }
}            
            
```

### Target ad pod positions

#### Target specific ad slot positions (last, first, third)

```
{
   "profile":{
      "ad_slot_intro_bumper_action_include":false,
      "ad_slot_outro_bumper_action_include":false,
      "ad_slot_position_action_include":true,
      "ad_slot_position_targets":[
         -1,
         0,
         2
      ]
   }
}            
            
```

#### Target only bumper positions (intro and outro)

```
{
   "profile":{
      "ad_slot_position_action_include":true,
      "ad_slot_position_targets":[],
      "ad_slot_intro_bumper_action_include":true,
      "ad_slot_outro_bumper_action_include":true
   }
}            
            
```

#### Target any ad pod slot

```
{
   "profile":{
      "ad_slot_position_action_include":false,
      "ad_slot_position_targets":[],
      "ad_slot_intro_bumper_action_include":false,
      "ad_slot_outro_bumper_action_include":false
   }
}            
            
```

#### Exclude all ad pod slots and bumpers

This behavior is not something you will want to replicate; you will not serve on anything.

```
{
   "profile":{
      "ad_slot_position_action_include":true,
      "ad_slot_position_targets":[],
      "ad_slot_intro_bumper_action_include":false,
      "ad_slot_outro_bumper_action_include":false
   }
}            
            
```

#### Target only the intro bumper

```
{
   "profile":{
      "ad_slot_position_action_include":true,
      "ad_slot_position_targets":[],
      "ad_slot_intro_bumper_action_include":true,
      "ad_slot_outro_bumper_action_include":false
   }
}            
            
```

The following profile targeting configurations are invalid and may result in unexpected behavior.

#### Invalid configuration: Cannot target all ad slots and all bumper positions

```
{
   "profile":{
      "ad_slot_position_action_include":false,
      "ad_slot_position_targets":[],
      "ad_slot_intro_bumper_action_include":true,
      "ad_slot_outro_bumper_action_include":true
   }
}            
            
```

### Target a Programmatic Guaranteed deal

Scenario: You have negotiated a Programmatic Guaranteed deal (PG deal) with a seller and would like to target this deal with a PG buying line item. You'll need to create a PG deal profile using the PG deal ID. You then must associate this profile with a PG buying line item to target the deal (see the Create a PG buying line item example in [Line Item ALI Service](line-item-service---ali.md)).

1. Create a PG deal profile JSON that includes the deal target ID.
    > [!NOTE]
    > For PG buying line items, you can only have one deal target in the `deal_targets` array.

    ```
    $ cat pg_deal_profile

    {
       "profile":{
          "deal_targets":[
             {
                "id":456
             }
          ],
          "allow_unaudited":true
       }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/profile` endpoint with this PG deal profile JSON and an appropriate `advertiser_id`.

    ```
    $ curl -b cookies -c cookies -X POST -d @pg_deal_profile 'https://api.appnexus.com/profile?advertiser_id=123'
     
    {
       "response":{
          "status":"OK",
          "count":1,
          "id":123456,
          "start_element":0,
          "num_elements":100,
          "profile":{
             "id":123456,
             "code":null,
             "description":null,
             "country_action":"exclude",
             "region_action":"exclude",
             "city_action":"exclude",
             "browser_action":"exclude",
             "use_inventory_attribute_targets":false,
             "last_modified":"2019-08-07 19:43:12",
             "daypart_timezone":null,
             "dma_action":"exclude",
             "domain_action":"exclude",
             "domain_list_action":"exclude",
             "inventory_action":"exclude",
             "language_action":"exclude",
             "segment_boolean_operator":"and",
             "min_session_imps":null,
             "session_freq_type":"platform",
             "carrier_action":"exclude",
             "supply_type_action":"exclude",
             "device_type_action":"exclude",
             "screen_size_action":"exclude",
             "device_model_action":"exclude",
             "location_target_radius":null,
             "location_target_latitude":null,
             "location_target_longitude":null,
             "querystring_action":"exclude",
             "querystring_boolean_operator":"and",
             "is_expired":false,
             "non_audited_url_action":"include",
             "daypart_bitmap":null,
             "is_archived":false,
             "archived_on":null,
             "advertiser_id":123,
             "publisher_id":null,
             "max_session_imps":null,
             "max_day_imps":null,
             "max_lifetime_imps":null,
             "max_page_imps":null,
             "min_minutes_per_imp":null,
             "venue_action":"exclude",
             "operating_system_action":"exclude",
             "require_cookie_for_freq_cap":true,
             "trust":"seller",
             "allow_unaudited":true,
             "is_template":false,
             "created_on":"2019-08-07 19:43:12",
             "operating_system_family_action":"exclude",
             "use_operating_system_extended_targeting":true,
             "mobile_app_instance_action_include":false,
             "mobile_app_instance_list_action_include":false,
             "inventory_prefer_direct":false,
             "deal_action_include":true,
             "exclude_unknown_seller_member_group":false,
             "ad_slot_position_action_include":false,
             "ad_slot_intro_bumper_action_include":true,
             "ad_slot_outro_bumper_action_include":true,
             "graph_id":null,
             "media_subtype_action_include":false,
             "ads_txt_authorized_only":false,
             "inventory_url_allowlist_settings":{
                "apply_to_rtb":true,
                "apply_to_managed":true
             },
             "user_group_targets":null,
             "country_targets":null,
             "region_targets":null,
             "city_targets":null,
             "inventory_attribute_targets":null,
             "placement_type_targets":null,
             "age_targets":null,
             "daypart_targets":null,
             "browser_targets":null,
             "dma_targets":null,
             "domain_targets":null,
             "domain_list_targets":null,
             "language_targets":null,
             "size_targets":null,
             "zip_targets":null,
             "member_targets":null,
             "video_targets":{
                "allow_unknown_playback_method":false,
                "allow_unknown_context":false,
                "allow_unknown_player_size":false
             },
             "engagement_rate_targets":null,
             "segment_group_targets":null,
             "carrier_targets":null,
             "supply_type_targets":null,
             "device_type_targets":null,
             "screen_size_targets":null,
             "device_model_targets":null,
             "querystring_targets":null,
             "gender_targets":null,
             "intended_audience_targets":null,
             "inventory_network_resold_targets":null,
             "operating_system_targets":null,
             "operating_system_family_targets":null,
             "position_targets":null,
             "site_targets":null,
             "venue_targets":null,
             "operating_system_extended_targets":null,
             "postal_code_targets":null,
             "seller_member_group_targets":null,
             "cross_device":null,
             "key_value_targets":null,
             "media_subtype_targets":null,
             "content_category_targets":null,
             "deal_targets":[
                {
                   "id":456,
                   "name":"PG Deal 123",
                   "code":"PGD_123",
                   "deleted":false
                }
             ],
             "placement_targets":null,
             "platform_content_category_targets":null,
             "platform_placement_targets":null,
             "platform_publisher_targets":null,
             "publisher_targets":null,
             "ip_range_list_targets":null,
             "mobile_app_instance_targets":null,
             "mobile_app_instance_list_targets":null,
             "ad_slot_position_targets":null,
             "inventory_url_list_targets":null,
             "max_hour_imps":null,
             "max_week_imps":null,
             "max_month_imps":null
          },
          "dbg_info":{
             "warnings":[
                
             ],
             "version":"1.18.1247",
             "output_term":"profile"
          }
       }
    }
    ```

1. Create a PG buying line item and associate it with the ID of the newly created PG deal profile (see the Create a PG buying line item example in [Line Item ALI Service](line-item-service---ali.md)).

    **Target a specific political district**

    ```
    {
       "profile":{
          "political_district_targets":[
             {
                "id":"139897"
             }
          ]
       }
    }                        
                            
    ```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Political District Service](political-district-service.md)
