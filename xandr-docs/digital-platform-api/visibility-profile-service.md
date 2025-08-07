---
title: Visibility Profile Service
description: Explore the Visibility Profile service, enabling you to control the level of detail you pass to buyers in your bid requests.
ms.date: 08/07/2025
ms.custom: digital-platform-api
---

# Visibility Profile service

If you resell your inventory, the Visibility Profile Service enables you to control the level of detail you pass to buyers in your bid requests. Specifically, you can expose or hide publisher IDs and names, placement IDs and names, publisher-provided age and gender data, the universal and custom categorization of your inventory, inventory URLs, location information, and more.

The default settings in your profile (i.e., `expose_age_default`, `expose_gender_default`, and so on) apply to all platform buyers and external bidders, but you can override the default settings for specific platform buyers and external bidders using the `buyer_members` and `bidders` arrays. For example, you might hide inventory data by default and then expose data only to specific buying members with whom you have a special business relationship. Alternately, you might expose inventory data to everyone except specific buying members whom you deem to be competitors.

In addition to affecting the data that buyers see in your bid requests, visibility settings affect the data that buyers see when they report on impressions bought from you. For example, if you hide publisher IDs and names from a buyer, that buyer won't see your publisher IDs and names in reporting.

> [!NOTE]
> Although you can create multiple visibility profiles, you can attach only one to your member (see the `visibility_profile_id` field in the [Member Service](member-service.md)). If you are interested in attaching visibility profiles directly to publishers, contact your Account Representative.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/visibility-profile](https://api.appnexus.com/visibility-profile)<br>(`visibility_profile` JSON) | Add a visibility profile. |
| `PUT` | [https://api.appnexus.com/visibility-profile?id=VISIBILITY_PROFILE_ID](https://api.appnexus.com/visibility-profile?id=VISIBILITY_PROFILE_ID)<br>(`visibility_profile` JSON) | Modify a visibility profile. |
| `DELETE` | [https://api.appnexus.com/visibility-profile?id=VISIBILITY_PROFILE_ID](https://api.appnexus.com/visibility-profile?id=VISIBILITY_PROFILE_ID) | Delete a visibility profile. |
| `GET` | [https://api.appnexus.com/visibility-profile](https://api.appnexus.com/visibility-profile) | View all of your visibility profiles. |
| `GET` | [https://api.appnexus.com/visibility-profile?id=VISIBILITY_PROFILE_ID](https://api.appnexus.com/visibility-profile?id=VISIBILITY_PROFILE_ID) | View a specific visibility profile. |
| `GET` | [https://api.appnexus.com/visibility-profile?id=1,2,3](https://api.appnexus.com/visibility-profile?id=1,2,3) | View multiple visibility profiles by ID using a comma-separated list. |
| `GET` | [https://api.appnexus.com/visibility-profile/meta](https://api.appnexus.com/visibility-profile/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `id` | int | **Read-only.** The ID of the visibility profile.<br>**Default:** Auto-generated number (i.e., 123).<br>**Required On:** `PUT`, in query string. |
| `member_id` | int | **Read-only.** The ID of the member that owns the visibility profile. |
| `name` | string | The name of the visibility profile.<br>**Required On:** `POST` |
| `notes` | string | Additional information about the visibility profile. |
| `expose_publishers_default` | Boolean | **Do Not Use.**<br>*Not available to all clients.* If `true`, publisher IDs are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_tags_default` | Boolean | **Do Not Use.**<br>*Not available to all clients.* If `true`, placement IDs are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_age_default` | Boolean | If `true`, publisher-provided age data is passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_gender_default` | Boolean | If `true`, publisher-provided gender data is passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_universal_categories_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_custom_categories_default` | enum | The visibility of your custom content categories in your bid requests. <br>Possible values:<br>- `none`: No custom categories are passed in your bid requests.<br>- `all`: All custom categories are passed in your bid requests.<br>- `list`: The custom categories listed in the `custom_categories` array are passed in your bid requests.<br>**Default:** `none` |
| `url_exposure_default` | enum | The visibility of inventory URLs in your bid requests. <br>Possible values:<br>- `full`: Full URLs are passed in your bid requests.<br>- `domain`: Only domains of URLs are passed in your bid requests.<br>- `hidden`: URLs are not passed in your bid requests.<br>**Default:** `full` |
| `expose_bid_requests_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_auction_id_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_locale_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_ecp_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_reserve_price_default` | Boolean | If `true`, the publisher-provided reserve prices are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_user_id_default` | Boolean | If `true`, publisher-provided user IDs are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_ip_default` | Boolean | If `true`, publisher-provided IP addresses are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_venue_id_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_user_agent_default` | Boolean | If `true`, publisher-provided user agents are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_city_default` | Boolean | If `true`, publisher-provided cities are available for targeting and reporting for buyers using Microsoft Invest. This applies to all Microsoft Invest members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target cities. For more details, see the [Deal Service](deal-service.md).<br>Buyers on external DSPs can target and report on cities regardless of this setting.<br>**Default:** `true` |
| `expose_state_default` | Boolean | If `true`, publisher-provided states are available for targeting and reporting for buyers using Microsoft Invest. This applies to all Microsoft Invest members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target states. For more details, see the [Deal Service](deal-service.md).<br>Buyers on external DSPs can target and report on states regardless of this setting.<br>**Default:** `true` |
| `expose_dma_default` | Boolean | If `true`, publisher-provided DMAs are available for targeting and reporting for buyers using Microsoft Invest. This applies to all Microsoft Invest members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target DMAs. For more details, see the [Deal Service](deal-service.md).<br>Buyers on external DSPs can target and report on DMAs regardless of this setting.<br>**Default:** `true` |
| `expose_postal_code_default` | Boolean | If `true`, publisher-provided postal codes are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_geo_lat_lon_default` | Boolean | If `true`, publisher-provided latitude and longitude information is passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_device_id_default` | Boolean | If `true`, publisher-provided device IDs are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_device_model_id_default` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_querystring_default` | Boolean | If `true`, publisher-provided query strings are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_application_id_default` | Boolean | If `true`, publisher-provided Android or iOS mobile application IDs are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_site_id_default` | Boolean | If `true`, publisher-provided placement group (site) IDs are passed in your bid requests. This applies to all platform members and bidders not set separately in the `buyer_members` and `bidders` arrays below.<br>**Default:** `true` |
| `expose_datetime_default` | Boolean | **Do Not Use.** This field is ignored. |
| `expose_multiformat_banner_default` | Boolean | If true, multiformat oRTB bid requests will expose banner `media_type` to buyers, if banner `media_type` is part of the bid request. Note that multiformat bid requests have to be enabled for this fields to be applicable. However, before requesting to enable multiformat, review [seller best practices](../industry-reference/seller-best-practices.md) and discuss with your account manager. This applies to all platform members, bidders amd are not set separately in the `buyer_members` and `bidders` arrays below. <br>**Default:** `true` |
| `expose_multiformat_video_default` | Boolean | If true, multiformat oRTB bid requests will expose video `media_type` to buyers, if video `media_type` is part of the bid request. Note that multiformat bid requests have to be enabled for this fields to be applicable.However, before requesting to enable multiformat, review [seller best practices](../industry-reference/seller-best-practices.md)and discuss with your account manager). This applies to all platform members, bidders amd are not set separately in the `buyer_members` and `bidders` arrays below. <br>**Default:** `true` |
| `expose_multiformat_audio_default` | Boolean | If true, multiformat oRTB bid requests will expose audio `media_type` to buyers, if native `media_type` is part of the bid request. Note that multiformat bid requests have to be enabled for this fields to be applicable.However, before requesting to enable multiformat, review [seller best practices](../industry-reference/seller-best-practices.md)and discuss with your account manager). This applies to all platform members, bidders amd are not set separately in the `buyer_members` and `bidders` arrays below. <br>**Default:** `true` |
| `expose_multiformat_native_default` | Boolean | If true, multiformat oRTB bid requests will expose native `media_type` to buyers, if native `media_type` is part of the bid request. Note that multiformat bid requests have to be enabled for this fields to be applicable.However, before requesting to enable multiformat, review [seller best practices](../industry-reference/seller-best-practices.md)and discuss with your account manager). This applies to all platform members, bidders amd are not set separately in the `buyer_members` and `bidders` arrays below. <br>**Default:** `true` |
| `buyer_members` | array of objects | The visibility rules for specific Xandr platform members. For more details, see [Buyer Members](#buyer-members) below.<br>**Default:** `true` |
| `bidders` | array of objects | The visibility rules for specific external bidders and/or contextual data providers. For more details, see [Bidders](#bidders) below. |
| `custom_categories` | array of objects | The custom content categories that are passed in your bid requests. For more details, see [Custom Categories](#custom-categories) below.<br>**Required On:** `POST`, if `expose_custom_categories_default` is `list`. |
| `last_modified` | timestamp | **Read-only.** The date and time when the visibility profile was last modified. |
| `expose_device_type_targets` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target device types. For more details, see the [Deal Service](deal-service.md). |
| `expose_segment_groups_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target segments. For more details, see the [Deal Service](deal-service.md). |
| `expose_video_context_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video contexts (e.g. pre-roll). For more details, see the [Deal Service](deal-service.md). |
| `expose_video_content_genres_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video content genres (e.g. comedy). For more details, see the [Deal Service](deal-service.md). |
| `expose_video_program_types_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video program types (e.g. series). For more details, see the [Deal Service](deal-service.md). |
| `expose_video_content_ratings_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video content ratings. For more details, see the [Deal Service](deal-service.md). |
| `expose_video_content_duration_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video content durations (e.g. short-form). For more details, see the [Deal Service](deal-service.md). |
| `expose_video_content_networks_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video content networks. For more details, see the [Deal Service](deal-service.md). |
| `expose_video_delivery_types_default` | Boolean | If `true` and this visibility profile is associated with a deal using [Seller Restricted Targeting](./deal-service.md#seller-restricted-targeting), Microsoft Invest buyers targeting the deal will be unable to target video delivery types (e.g. VOD). For more details, see the [Deal Service](deal-service.md). |

### Custom categories

If `expose_custom_categories_default` is set to `list`, you use this array to specify the custom categories that you want to pass in your bid requests. Each object in the array represents a single custom category and contains the following fields. For formatting, see the [examples](#examples) below.

> [!TIP]
> You can use the [Content Category Service](content-category-service.md) to get the IDs of your custom content categories.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the custom content category that is passed in your bid requests. |
| `name` | string | **Read-only.** The name of the custom content category. |

### Buyer members

You use this array to define visibility rules for specific Xandr platform members. Each object in the array represents a single member and contains the following fields. For formatting, see the [examples](#examples) below.

> [!TIP]
> You can can use the [Platform Member Service](platform-member-service.md) to get the IDs of Xandr platform members.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the Xandr platform member to which you want to apply specific visibility rules.<br>**Required On:** `POST` |
| `name` | string | **Read-only.** The name of the Xandr platform member. |
| `expose_publishers` | Boolean | **Do Not Use.** This field is ignored.<br>For select customers: If `true`, publisher IDs are passed in your bid requests to the member.<br>**Default:** `true` |
| `expose_tags` | Boolean | **Do Not Use.** This field is ignored.<br>For select customers: If `true`, placement IDs are passed in your bid requests to the member.<br>**Default:** `true` |
| `expose_age` | Boolean | If `true`, age data is passed in your bid requests to the member.<br>**Default:** `true` |
| `expose_gender` | Boolean | If `true`, gender data is passed in your bid requests to the member.<br>**Default:** `true` |
| `expose_universal_categories` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_custom_categories` | enum | The visibility of your custom content categories in your bid requests to the member. Possible values:<br>- `none`: No custom categories are passed in your bid requests.<br>- `all`: All custom categories are passed in your bid requests.<br>- `list`: The custom categories listed in the `custom_categories` array are passed in your bid requests.<br>**Default:** `none` |
| `custom_categories` | array of objects | The custom content categories that are passed in your bid requests to the member. For the fields in this array, see [Custom Categories](#custom-categories) above.<br>**Required On:** `POST`, if `expose_custom_categories_default` is `list`. |
| `url_exposure` | enum | The visibility of inventory URLs in your bid requests to the member. Possible values:<br>- `full`: Full URLs are passed in your bid requests.<br>- `domain`: Only domains of URLs are passed in your bid requests.<br>- `hidden`: URLs are not passed in your bid requests.<br>**Default:** `full` |
| `expose_bid_requests` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_auction_id` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_locale` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_ecp` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_reserve_price` | Boolean | If `true`, reserve prices are exposed to the owning member.<br>**Default:** `true` |
| `expose_user_id` | Boolean | If `true`, user IDs are exposed to the owning member.<br>**Default:** `true` |
| `expose_ip` | Boolean | If `true`, IP addresses are exposed to the owning member.<br>**Default:** `true` |
| `expose_venue_id` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_user_agent` | Boolean | If `true`, user agents are exposed to the owning member.<br>**Default:** `true` |
| `expose_city` | Boolean | If `true`, cities are available for targeting and reporting for the Microsoft Invest buyer.<br>**Default:** `true` |
| `expose_state` | Boolean | If `true`, states are available for targeting and reporting for the Microsoft Invest buyer.<br>**Default:** `true` |
| `expose_dma` | Boolean | If `true`, DMAs are available for targeting and reporting for the Microsoft Invest buyer.<br>**Default:** `true` |
| `expose_postal_code` | Boolean | If `true`, postal codes are exposed to the owning member.<br>**Default:** `true` |
| `expose_geo_lat_lon` | Boolean | If `true`, latitude and longitude information is exposed to the owning member.<br>**Default:** `true` |
| `expose_device_id` | Boolean | If `true`, device IDs are exposed to the owning member.<br>**Default:** `true` |
| `expose_device_model_id` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_querystring` | Boolean | If `true`, query strings are exposed to the owning member.<br>**Default:** `true` |
| `expose_application_id` | Boolean | If `true`, Android or iOS mobile application IDs are exposed to the owning member.<br>**Default:** `true` |
| `expose_site_id` | Boolean | If `true`, placement group (site) IDs are exposed to the owning member.<br>**Default:** `true` |
| `expose_datetime` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |

### Bidders

You use this array to define visibility rules for specific external bidders and/or contextual data providers. Each object in the array represents a single bidder and contains the following fields. For formatting, see the [examples](#examples) below.

> [!TIP]
> There is no service for directly getting external bidder IDs; however, the [Platform Member Service](platform-member-service.md) gets you information about platform members, including the bidders that they are using.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the external bidder to which you want to apply specific visibility rules.<br>**Required On:** `POST` |
| `name` | string | **Read-only.** The name of the external bidder. |
| `expose_publishers` | Boolean | **Do Not Use.** This field is ignored.<br>For select customers: If `true`, publisher IDs are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_tags` | Boolean | **Do Not Use.** This field is ignored.<br>For select customers: If `true`, placement IDs are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_age` | Boolean | If `true`, age data is passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_gender` | Boolean | If `true`, gender data is passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_universal_categories` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_custom_categories` | enum | The visibility of your custom content categories in your bid requests to the bidder. <br>Possible values:<br>- `none`: No custom categories are passed in your bid requests.<br>- `all`: All custom categories are passed in your bid requests.<br>- `list`: The custom categories listed in the `custom_categories` array are passed in your bid requests.<br>**Default:** `none` |
| `custom_categories` | array of objects | The custom content categories that are passed in your bid requests to the bidder. For the fields in this array, see [Custom Categories](#custom-categories) above.<br>**Required On:** `POST`, if `expose_custom_categories_default` is `list`. |
| `url_exposure` | enum | The visibility of inventory URLs in your bid requests to the bidder.<br>Possible values:<br>- `full`: Full URLs are passed in your bid requests.<br>- `domain`: Only domains of URLs are passed in your bid requests.<br>- `hidden`: URLs are not passed in your bid requests.<br>**Default:** `full` |
| `expose_bid_requests` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_auction_id` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_locale` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_ecp` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_reserve_price` | Boolean | If `true`, reserve prices are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_user_id` | Boolean | If `true`, user IDs are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_ip` | Boolean | If `true`, IP addresses are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_venue_id` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_user_agent` | Boolean | If `true`, user agents passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_city` | Boolean | If `true`, cities are available for targeting and reporting for the Microsoft Invest bidder.<br>**Default:** `true` |
| `expose_state` | Boolean | If `true`, states are available for targeting and reporting for the Microsoft Invest bidder.<br>**Default:** `true` |
| `expose_dma` | Boolean | If `true`, DMAs are available for targeting and reporting for the Microsoft Invest bidder.<br>**Default:** `true` |
| `expose_postal_code` | Boolean | If `true`, postal codes are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_geo_lat_lon` | Boolean | If `true`, latitude and longitude information is passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_device_id` | Boolean | If `true`, device IDs are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_device_model_id` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |
| `expose_querystring` | Boolean | If `true`, query strings are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_application_id` | Boolean | If `true`, Android or iOS mobile application IDs are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_site_id` | Boolean | If `true`, placement group (site) IDs are passed in your bid requests to the bidder.<br>**Default:** `true` |
| `expose_datetime` | Boolean | **Do Not Use.** This field is ignored.<br>**Default:** `true` |

## Examples

### Add a visibility profile - Show inventory data to all buyers except member 9

In this example, the `POST` request creates a visibility profile that allows all Xandr platform members and external bidders except member 9 to see publisher, placement, age, gender, category, and URL information in your bid requests.

```
$ cat visibility_profile

{
    "visibility-profile": {
        "name": "Test Visibility Profile",
        "expose_age_default": true,
        "expose_gender_default": true,
        "expose_custom_categories_default": "all",
        "url_exposure_default": "full",
        "expose_reserve_price_default": true,
        "expose_user_id_default": true,
        "expose_ip_default": true,
        "expose_user_agent_default": true,
        "expose_postal_code_default": true,
        "expose_geo_lat_lon_default": true,
        "expose_device_id_default": true,
        "expose_querystring_default": true,
        "expose_application_id_default": true,
        "expose_site_id_default": true,
        "buyer_members": [
            {
                "id": 9,
                "expose_age": false,
                "expose_gender": false,
                "expose_custom_categories": "none",
                "url_exposure": "hidden"
            }
        ]
    }
}

$ curl -b cookies -X POST -d @visibility_profile 'https://api.appnexus.com/visibility-profile'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1818,
        "start_element": 0,
        "num_elements": 100,
        "visibility-profile": {
            "id": 1818,
            "member_id": 1066,
            "name": "Test Visibility Profile",
            "notes": null,
            "expose_age_default": true,
            "expose_gender_default": true,
            "expose_custom_categories_default": "all",
            "url_exposure_default": "full",
            "expose_reserve_price_default": true,
            "expose_user_id_default": true,
            "expose_ip_default": true,
            "expose_user_agent_default": true,
            "expose_postal_code_default": true,
            "expose_geo_lat_lon_default": true,
            "expose_device_id_default": true,
            "expose_querystring_default": true,
            "expose_application_id_default": true,
            "expose_site_id_default": true,
            "last_modified": "2015-08-31 21:18:54",
            "buyer_members": [
                {
                    "id": 9,
                    "expose_age": false,
                    "expose_gender": false,
                    "expose_custom_categories": "none",
                    "url_exposure": "hidden",
                    "expose_bid_requests": true,
                    "expose_reserve_price": true,
                    "expose_user_id": true,
                    "expose_ip": true,
                    "expose_user_agent": true,
                    "expose_postal_code": true,
                    "expose_geo_lat_lon": true,
                    "expose_device_id": true,
                    "expose_querystring": true,
                    "expose_application_id": true,
                    "expose_site_id": true,
                    "name": "DisplayWords Bidder - member 9",
                    "custom_categories": null
                }
            ],
            "bidders": null,
            "custom_categories": null
        }
    }
}
```

### Add a visibility profile - Hide inventory data from all buyers except member 9

In this example, the `POST` request creates a visibility profile that prevents all Xandr platform members and external bidders except member 9 from seeing publisher, placement, age, gender, category, and URL information in your bid requests.

```
$ cat visibility_profile

{
    "visibility-profile": {
        "name": "Test Visibility Profile",
        "expose_age_default": false,
        "expose_gender_default": false,
        "expose_custom_categories_default": "none",
        "url_exposure_default": "hidden",
        "expose_reserve_price_default": true,
        "expose_user_id_default": true,
        "expose_ip_default": true,
        "expose_user_agent_default": true,
        "expose_postal_code_default": true,
        "expose_geo_lat_lon_default": true,
        "expose_device_id_default": true,
        "expose_querystring_default": true,
        "expose_application_id_default": true,
        "expose_site_id_default": true,
        "buyer_members": [
            {
                "id": 9,
                "expose_age": true,
                "expose_gender": true,
                "expose_custom_categories": "all",
                "url_exposure": "full",
                "expose_bid_requests": true,
                "expose_reserve_price": true,
                "expose_user_id": true,
                "expose_ip": true,
                "expose_user_agent": true,
                "expose_postal_code": true,
                "expose_geo_lat_lon": true,
                "expose_device_id": true,
                "expose_querystring": true,
                "expose_application_id": true,
                "expose_site_id": true,
            }
        ]
    }

$ curl -b cookies -X POST -d @visibility_profile 'https://api.appnexus.com/visibility-profile'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1819,
        "start_element": 0,
        "num_elements": 100,
        "visibility-profile": {
            "id": 1819,
            "member_id": 1066,
            "name": "Test Visibility Profile",
            "notes": null,
            "expose_age_default": false,
            "expose_gender_default": false,
            "expose_custom_categories_default": "none",
            "url_exposure_default": "hidden",
            "expose_reserve_price_default": true,
            "expose_user_id_default": true,
            "expose_ip_default": true,
            "expose_user_agent_default": true,
            "expose_postal_code_default": true,
            "expose_geo_lat_lon_default": true,
            "expose_device_id_default": true,
            "expose_querystring_default": true,
            "expose_application_id_default": true,
            "expose_site_id_default": true,
            "last_modified": "2015-08-31 21:57:13",
            "buyer_members": [
                {
                    "id": 9,
                    "expose_age": true,
                    "expose_gender": true,
                    "expose_custom_categories": "all",
                    "url_exposure": "full",
                    "expose_reserve_price": true,
                    "expose_user_id": true,
                    "expose_ip": true,
                    "expose_user_agent": true,
                    "expose_postal_code": true,
                    "expose_geo_lat_lon": true,
                    "expose_device_id": true,
                    "expose_querystring": true,
                    "expose_application_id": true,
                    "expose_site_id": true,
                    "name": "DisplayWords Bidder - member 9",
                    "custom_categories": null
                }
            ],
            "bidders": null,
            "custom_categories": null
        }
    }
}
```

### Modify visibility profile 1818

In this example, the `PUT` request updates visibility profile 1818 to allow only custom content category 24214 to be passed in your bid requests. This applies to all Xandr platform members and external bidders except platform member 9, whose visibility is defined separately (see `{{buyer_members}}` array in the response).

```
$ cat visibility_profile_update

{
    "visibility-profile": {
        "expose_custom_categories_default": "list",
        "custom_categories": [
            {
                "id": 24214
            }
        ]
    }
}

$ curl -b cookies -X PUT -d @visibility_profile_update 'https://api.appnexus.com/visibility-profile?id=1818'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "1818",
        "start_element": 0,
        "num_elements": 100,
        "visibility-profile": {
            "id": 1818,
            "member_id": 1066,
            "name": "Test Visibility Profile",
            "notes": null,
            "expose_age_default": true,
            "expose_gender_default": true,
            "expose_custom_categories_default": "list",
            "url_exposure_default": "full",
            "expose_reserve_price_default": true,
            "expose_user_id_default": true,
            "expose_ip_default": true,
            "expose_user_agent_default": true,
            "expose_postal_code_default": true,
            "expose_geo_lat_lon_default": true,
            "expose_device_id_default": true,
            "expose_querystring_default": true,
            "expose_application_id_default": true,
            "expose_site_id_default": true,
            "last_modified": "2015-08-31 21:24:43",
            "buyer_members": [
                {
                    "id": 9,
                    "expose_age": false,
                    "expose_gender": false,
                    "expose_custom_categories": "none",
                    "url_exposure": "hidden",
                    "expose_reserve_price": true,
                    "expose_user_id": true,
                    "expose_ip": true,
                    "expose_user_agent": true,
                    "expose_postal_code": true,
                    "expose_geo_lat_lon": true,
                    "expose_device_id": true,
                    "expose_querystring": true,
                    "expose_application_id": true,
                    "expose_site_id": true,
                    "name": "DisplayWords Bidder - member 9",
                    "custom_categories": null
                }
            ],
            "bidders": null,
            "custom_categories": [
                {
                    "id": 24214,
                    "name": "TEST"
                }
            ]
        }
    }
}
```

### View all of your visibility profiles

```
$ curl -b cookies 'https://api.appnexus.com/visibility-profile'

{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "visibility-profiles": [
            {
                "id": 1816,
                "member_id": 1066,
                "name": "Test Visibility Profile",
                "notes": null,
                "expose_age_default": true,
                "expose_gender_default": true,
                "expose_custom_categories_default": "list",
                "url_exposure_default": "full",
                "expose_reserve_price_default": true,
                "expose_user_id_default": true,
                "expose_ip_default": true,
                "expose_user_agent_default": true,
                "expose_postal_code_default": true,
                "expose_geo_lat_lon_default": true,
                "expose_device_id_default": true,
                "expose_querystring_default": true,
                "expose_application_id_default": true,
                "expose_site_id_default": true,
                "last_modified": "2015-08-31 18:14:45",
                "buyer_members": [
                    {
                        "id": 9,
                        "expose_age": true,
                        "expose_gender": true,
                        "expose_custom_categories": "none",
                        "url_exposure": "full",
                        "expose_reserve_price": true,
                        "expose_user_id": true,
                        "expose_ip": true,
                        "expose_user_agent": true,
                        "expose_postal_code": true,
                        "expose_geo_lat_lon": true,
                        "expose_device_id": true,
                        "expose_querystring": true,
                        "expose_application_id": true,
                        "expose_site_id": true,
                        "name": "DisplayWords Bidder - member 9",
                        "custom_categories": null
                    }
                ],
                "bidders": [
                    {
                        "id": 6,
                        "expose_age": true,
                        "expose_gender": true,
                        "expose_custom_categories": "none",
                        "url_exposure": "full",
                        "expose_reserve_price": true,
                        "expose_user_id": true,
                        "expose_ip": true,
                        "expose_user_agent": true,
                        "expose_postal_code": true,
                        "expose_geo_lat_lon": true,
                        "expose_device_id": true,
                        "expose_querystring": true,
                        "expose_application_id": true,
                        "expose_site_id": true,
                        "name": "Dilling HBF Test New",
                        "custom_categories": null
                    }
                ],
                "custom_categories": [
                    {
                        "id": 24214,
                        "name": "TEST"
                    }
                ]
            },
            {
                "id": 1818,
                "member_id": 1066,
                "name": "Test Visibility Profile",
                "notes": null,
                "expose_age_default": true,
                "expose_gender_default": true,
                "expose_custom_categories_default": "list",
                "url_exposure_default": "full",
                "expose_reserve_price_default": true,
                "expose_user_id_default": true,
                "expose_ip_default": true,
                "expose_user_agent_default": true,
                "expose_postal_code_default": true,
                "expose_geo_lat_lon_default": true,
                "expose_device_id_default": true,
                "expose_querystring_default": true,
                "expose_application_id_default": true,
                "expose_site_id_default": true,
                "last_modified": "2015-08-31 21:24:43",
                "buyer_members": [
                    {
                        "id": 9,
                        "expose_age": false,
                        "expose_gender": false,
                        "expose_custom_categories": "none",
                        "url_exposure": "hidden",
                        "expose_reserve_price": true,
                        "expose_user_id": true,
                        "expose_ip": true,
                        "expose_user_agent": true,
                        "expose_postal_code": true,
                        "expose_geo_lat_lon": true,
                        "expose_device_id": true,
                        "expose_querystring": true,
                        "expose_application_id": true,
                        "expose_site_id": true,
                        "name": "DisplayWords Bidder - member 9",
                        "custom_categories": null
                    }
                ],
                "bidders": null,
                "custom_categories": [
                    {
                        "id": 24214,
                        "name": "TEST"
                    }
                ]
            }
        ]
    }
}
```

### View visibility profile 1818

```
$ curl -b cookies 'https://api.appnexus.com/visibility-profile?id=1818'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "visibility-profile": {
            "id": 1818,
            "member_id": 1066,
            "name": "Test Visibility Profile",
            "notes": null,
            "expose_age_default": true,
            "expose_gender_default": true,
            "expose_custom_categories_default": "list",
            "url_exposure_default": "full",
            "expose_reserve_price_default": true,
            "expose_user_id_default": true,
            "expose_ip_default": true,
            "expose_user_agent_default": true,
            "expose_postal_code_default": true,
            "expose_geo_lat_lon_default": true,
            "expose_device_id_default": true,
            "expose_querystring_default": true,
            "expose_application_id_default": true,
            "expose_site_id_default": true,
            "last_modified": "2015-08-31 21:24:43",
            "buyer_members": [
                {
                    "id": 9,
                    "expose_age": false,
                    "expose_gender": false,
                    "expose_custom_categories": "none",
                    "url_exposure": "hidden",
                    "name": "DisplayWords Bidder - member 9",
                    "custom_categories": null
                }
            ],
            "bidders": null,
            "custom_categories": [
                {
                    "id": 24214,
                    "name": "TEST"
                }
            ]
        }
    }
}
```
