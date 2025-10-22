---
title: Buy-Side Forecasting Service
description: In this article, find information about the Buy-Side Forecasting Service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Buy-side forecasting service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

A successful campaign requires, among other things, accurate delivery. Delivery can sometimes be difficult to predict. For example, a trader may not know whether lowering a bid will result in under delivery. To help traders better understand the dynamics behind available impressions for a particular campaign, you can create a forecast. These forecasts provide buyers with insight into the number of impressions that could be delivered, given their campaign's targeting choices at various CPM bids. Access to this type of data before the actual campaign runs, helps buyers better plan budgets with their clients.

## REST API

The Buy-Side Forecasting Service supports `GET`, `POST`, and `DELETE` calls. `PUT` calls are not supported.

| HTTP Method | Endpoint | Description |
|---|---|---|
| `POST` | `https://api.appnexus.com/periscope-forecast?member_id=MEMBER_ID` | Add a new forecast |
| `DELETE` | `https://api.appnexus.com/periscope-forecast?id=ID` | Delete a forecast. To delete a forecast, the `forecast_id` number is required |
| `GET` | `https://api.appnexus.com/periscope-forecast?member_id=MEMBER_ID` | View all forecasts |
| `GET` | `https://api.appnexus.com/periscope-forecast?id=ID` | View a specific forecast |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `id` | int | The ID of the forecast. |
| `created_on` | string | The date on which the forecast was created. |
| `deleted` | boolean | - `true` = A forecast that has been deleted. <br> - `false` = A forecast that has not been deleted. |
| `name` | string | Name of the forecast object. |
| `profile_id` | int | The ID number of the profile object. (It is the same object used in the [Profile Service](profile-service.md).) |
| `campaign_id` | int | The ID number of the campaign. |
| `member_id` | int | The ID number of the member. |
| `creative_property_targets` | array of objects | List of attributes that applies to underlying creatives. Each JSON object will match with one creative. |
| `bid_buckets` | array of objects | The results of the forecast, containing the following information: <br> - `bid_bucket_percent`: % of total daily impressions (win rate). <br> - `bid_bucket_price`: The CPM base bid necessary to win that % of daily impressions. <br> - `cumulative_imps_available`: Number of daily impressions that would be won at the CPM bid price. <br> - `cumulate_cost`: Daily budget needed to win those impressions. |

## Examples

### Create a new forecast that targets users in Brazil and Australia, with a display (banner) of 300 x 250 pixels

**API call**:

```
curl -b cookies -c cookies -X POST -d @forecast.json 'https://api.appnexus.com/periscope-forecast?member_id=1234'
```

**JSON**:

```
{
"forecast": {
"name": "My Forecast",
"creative_property_targets": [
{
"media_subtype_id": 1,
"width": 300,
"height": 250,
"brand_id": 350
}
],
"profile": {
"country_targets": [
{
"id": 18,
"code": "AU"
},
{
"id": 34,
"code": "BR"
}
],
"country_action": "include"
}
}
}
```

**Response**:

```
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 50,
"dbg_info": {
"instance": "03.forecast-api.prod.0002",
"db": "",
"warnings": [

],
"start_microtime": 1463161332.731,
"time": 4,
"version": "",
"output_term": "forecast"
},
"forecast": [
{
"id": 179,
"created_on": "2016-05-13 17:42:12",
"deleted": false,
"name": "My Forecast",
"profile_id": 57167266,
"campaign_id": 13100202,
"member_id": 1234,
"creative_property_targets": [
{
"id": 562,
"forecast_id": 179,
"media_subtype_id": 1,
"width": 300,
"height": 250,
"is_skippable": null,
"duration_ms": null
}
],
"bid_buckets": [

],
"profile": {
"id": 57167266,
"code": null,
"description": "PERISCOPE_HOLD_PROFILE_DESC",
"country_action": "include",
"region_action": "exclude",
"city_action": "exclude",
"browser_action": "exclude",
"use_inventory_attribute_targets": false,
"last_modified": "2016-05-13 17:42:11",
"daypart_timezone": null,
"dma_action": "exclude",
"domain_action": "exclude",
"domain_list_action": "exclude",
"inventory_action": "exclude",
"language_action": "exclude",
"segment_boolean_operator": "and",
"min_session_imps": null,
"session_freq_type": "platform",
"carrier_action": "exclude",
"supply_type_action": "exclude",
"device_type_action": "exclude",
"screen_size_action": "exclude",
"device_model_action": "exclude",
"location_target_radius": null,
"location_target_latitude": null,
"location_target_longitude": null,
"querystring_action": "exclude",
"querystring_boolean_operator": "and",
"is_expired": false,
"non_audited_url_action": "include",
"daypart_bitmap": null,
"optimization_zone_action": "exclude",
"advertiser_id": 945485,
"publisher_id": null,
"max_session_imps": null,
"max_day_imps": null,
"max_lifetime_imps": null,
"max_page_imps": null,
"min_minutes_per_imp": null,
"venue_action": "exclude",
"operating_system_action": "exclude",
"require_cookie_for_freq_cap": true,
"trust": "seller",
"allow_unaudited": false,
"is_template": false,
"created_on": "2016-05-13 17:42:11",
"operating_system_family_action": "exclude",
"use_operating_system_extended_targeting": false,
"mobile_app_instance_action_include": false,
"mobile_app_instance_list_action_include": false,
"certified_supply": false,
"user_group_targets": null,
"country_targets": [
{
"id": 18,
"name": "Australia",
"code": "AU"
},
{
"id": 34,
"name": "Brazil",
"code": "BR"
}
],
"region_targets": null,
"city_targets": null,
"inventory_attribute_targets": null,
"age_targets": null,
"daypart_targets": null,
"browser_targets": null,
"dma_targets": null,
"domain_targets": null,
"domain_list_targets": null,
"language_targets": null,
"size_targets": null,
"zip_targets": null,
"member_targets": null,
"video_targets": {
"allow_unknown_playback_method": false,
"allow_unknown_context": false,
"allow_unknown_player_size": false
},
"engagement_rate_targets": null,
"segment_group_targets": null,
"carrier_targets": null,
"supply_type_targets": null,
"device_type_targets": null,
"screen_size_targets": null,
"device_model_targets": null,
"querystring_targets": null,
"gender_targets": null,
"intended_audience_targets": null,
"inventory_network_resold_targets": null,
"operating_system_targets": null,
"operating_system_family_targets": null,
"position_targets": null,
"site_targets": null,
"venue_targets": null,
"operating_system_extended_targets": null,
"optimization_zone_targets": null,
"postal_code_targets": null,
"seller_member_group_targets": null,
"cross_device": null,
"content_category_targets": null,
"deal_targets": null,
"placement_targets": null,
"platform_content_category_targets": null,
"platform_placement_targets": null,
"platform_publisher_targets": null,
"publisher_targets": null,
"segment_targets": null,
"exelate_targets": null,
"ip_range_list_targets": null,
"mobile_app_instance_targets": null,
"mobile_app_instance_list_targets": null
}
}
]
}
}
```

### Create a forecast that targets video inventory with creative property targets

**API call**:

```
curl -b cookies -c cookies -X POST -d @forecast2.json 'https://api.appnexus.com/periscope-forecast?member_id=1234'
```

**JSON**:

```
{ "forecast": {
"name": "My Second Forecast",
"creative_property_targets": [
{
"media_subtype_id": 64,
"width": 1,
"height": 1,
"brand_id": 96,
"is_skippable": true,
"duration_ms": 30000
}
],
"profile": {
"video_targets": {
"allow_unknown_playback_method": true,
"allow_unknown_context": true,
"allow_unknown_player_size": true
},
"device_type_action": "include",
"device_type_targets": [
"phone",
"tablet"
]
}
}
}
```

**Response**:

```
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 50,
"dbg_info": {
"instance": "02.forecast-api.prod.0002",
"db": "",
"warnings": [
],
"start_microtime": 1463162647.753,
"time": 6,
"version": "",
"output_term": "forecast"
},
"forecast": [
{
"id": 181,
"created_on": "2016-05-13 18:04:07",
"deleted": false,
"name": "My Second Forecast",
"profile_id": 57167512,
"campaign_id": 13100348,
"member_id": 958,
"creative_property_targets": [
{
"id": 564,
"forecast_id": 181,
"media_subtype_id": 64,
"width": 1,
"height": 1,
"is_skippable": true,
"duration_ms": 30000
}
],
"bid_buckets": [
],
"profile": {
"id": 57167512,
"code": null,
"description": "PERISCOPE_HOLD_PROFILE_DESC",
"country_action": "exclude",
"region_action": "exclude",
"city_action": "exclude",
"browser_action": "exclude",
"use_inventory_attribute_targets": false,
"last_modified": "2016-05-13 18:04:06",
"daypart_timezone": null,
"dma_action": "exclude",
"domain_action": "exclude",
"domain_list_action": "exclude",
"inventory_action": "exclude",
"language_action": "exclude",
"segment_boolean_operator": "and",
"min_session_imps": null,
"session_freq_type": "platform",
"carrier_action": "exclude",
"supply_type_action": "exclude",
"device_type_action": "include",
"screen_size_action": "exclude",
"device_model_action": "exclude",
"location_target_radius": null,
"location_target_latitude": null,
"location_target_longitude": null,
"querystring_action": "exclude",
"querystring_boolean_operator": "and",
"is_expired": false,
"non_audited_url_action": "include",
"daypart_bitmap": null,
"optimization_zone_action": "exclude",
"advertiser_id": 945485,
"publisher_id": null,
"max_session_imps": null,
"max_day_imps": null,
"max_lifetime_imps": null,
"max_page_imps": null,
"min_minutes_per_imp": null,
"venue_action": "exclude",
"operating_system_action": "exclude",
"require_cookie_for_freq_cap": true,
"trust": "seller",
"allow_unaudited": false,
"is_template": false,
"created_on": "2016-05-13 18:04:06",
"operating_system_family_action": "exclude",
"use_operating_system_extended_targeting": false,
"mobile_app_instance_action_include": false,
"mobile_app_instance_list_action_include": false,
"certified_supply": false,
"user_group_targets": null,
"country_targets": null,
"region_targets": null,
"city_targets": null,
"inventory_attribute_targets": null,
"age_targets": null,
"daypart_targets": null,
"browser_targets": null,
"dma_targets": null,
"domain_targets": null,
"domain_list_targets": null,
"language_targets": null,
"size_targets": null,
"zip_targets": null,
"member_targets": null,
"video_targets": {
"allow_unknown_playback_method": true,
"allow_unknown_context": true,
"allow_unknown_player_size": true
},
"engagement_rate_targets": null,
"segment_group_targets": null,
"carrier_targets": null,
"supply_type_targets": null,
"device_type_targets": [
"phone",
"tablet"
],
"screen_size_targets": null,
"device_model_targets": null,
"querystring_targets": null,
"gender_targets": null,
"intended_audience_targets": null,
"inventory_network_resold_targets": null,
"operating_system_targets": null,
"operating_system_family_targets": null,
"position_targets": null,
"site_targets": null,
"venue_targets": null,
"operating_system_extended_targets": null,
"optimization_zone_targets": null,
"postal_code_targets": null,
"seller_member_group_targets": null,
"cross_device": null,
"content_category_targets": null,
"deal_targets": null,
"placement_targets": null,
"platform_content_category_targets": null,
"platform_placement_targets": null,
"platform_publisher_targets": null,
"publisher_targets": null,
"segment_targets": null,
"exelate_targets": null,
"ip_range_list_targets": null,
"mobile_app_instance_targets": null,
"mobile_app_instance_list_targets": null
}
}
]
}
}
```

### Get all forecasts for a member

**API call**:

```
curl -b cookies -c cookies -X GET 'https://api.appnexus.com/periscope-forecast?member_id=1234'
```

**Response**:

```
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 50,
"dbg_info": {
"instance": "03.forecast-api.prod.0002",
"db": "",
"warnings": [
],
"start_microtime": 1466438990.442,
"time": 5,
"version": "",
"output_term": "forecast"
},
"forecast": [
{
"id": 198,
"created_on": "2016-05-18 21:20:49",
"deleted": false,
"name": "AngPlayerSizeAny",
"profile_id": 57471324,
"campaign_id": 13147960,
"member_id": 1370,
"creative_property_targets": [
{
"id": 595,
"forecast_id": 198,
"media_subtype_id": 64,
"width": 1,
"height": 1,
"is_skippable": false,
"duration_ms": 90000
}
],
"bid_buckets": [
]
}
]
}
```
