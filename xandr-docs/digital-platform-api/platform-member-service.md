---
title: Digital Platform API - Platform Member Service
description: Use the Platform Member service to view public information about platform members and data providers for buying and selling.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Platform Member service

This is a read-only service that shows you public information about the other Xandr platform members that you can buy from and sell to. It also shows information about data providers.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/platform-member` | View all members that have exposed their information. |
| `GET` | `https://api.appnexus.com/platform-member?active=1` | View only active members that have exposed their information. |
| `GET` | `https://api.appnexus.com/platform-member?id=MEMBER_ID` | View a specific member. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `active` | Boolean | If `true`, the member is `active`. |
| `bidder` | object | The ID and name of the bidder that that member uses to buy impressions. |
| `contact_info` | object | The contact and additional info for the member. |
| `daily_imps_any_audit_status` | int | The number of daily impressions through inventory that has any audit status, to include: `unaudited`, `Xandr-reviewed`, `seller-reviewed`, and both `Xandr-and-seller-reviewed`. |
| `daily_imps_appnexus_reviewed` | int | The number of daily impressions through inventory that has been audited by Xandr. |
| `daily_imps_appnexus_seller_reviewed` | int | The number of daily impressions through inventory that has one of these three audit statuses: `seller-reviewed`, `Xandr-reviewed`, and both `Xandr-and-seller-reviewed`. |
| `daily_imps_self_audited` | int | **Deprecated**. |
| `daily_imps_unaudited` | int | **Deprecated**. |
| `daily_imps_verified` | int | **Deprecated**. |
| `default_discrepancy_pct` | double | The percent that Xandr deducts from each bid for certain external supply partners based on past discrepancies between what Xandr and the supply partner recorded as won impressions. |
| `description` | string | The description of the member. |
| `email` | string | The email address to use to contact the member. |
| `has_resold` | Boolean | If `true`, the member has exposed inventory for resale to other members. You can use the [Inventory Resold Service](./inventory-resold-service.md) to view information about the exposed inventory. |
| `id` | int | The ID of the member. |
| `is_iash_compliant` | Boolean | If `true`, the member is IASH compliant. |
| `last_modified` | timestamp | The date and time when the member entry was last modified. |
| `name` | string | The name of the member. |
| `primary_type` | enum | The type of member, which indicates the primary type of transactions this member performs with Xandr. Possible values: <br>- `"network"` <br> - `"buyer"` <br> - `"seller"` <br> - `"data_provider"` |
| `platform_exposure` | enum | The visibility of the member on the platform. Possible values:<br> - `"public"` - The member name is shown.<br> - `"private"` - Only the member ID is shown.<br> - `"hidden"` - The member is not shown by this service at all. |
| `seller_member_groups` | object | The ID, name, display order of the groups of seller members along with date and time when the entries were created and last modified. |
| `seller_type` | enum | The selling relationship between the member and Xandr. Possible values:<br> - `"platform"` - Xandr charges the member for selling inventory based on the member's contract.<br> - `"partner"` - Xandr does not charge the member for selling but rather charges buyers, based on their contracts when they buy this member's inventory. |
| `visibility_rules` | object | The level of detail included in the member's bid requests if `primary_type` is `"seller"`. See [Visibility Rules](#visibility-rules) below for details. |

### Visibility rules

| Field | Type | Description |
|:---|:---|:---|
| `expose_publishers` | Boolean | **Not Used**. The seller always sends publisher IDs in bid requests.<br><br>**For select customers only**: If `false`, the seller does not send publisher IDs in bid requests. |
| `expose_tags` | Boolean | **Not Used**. This field is not available to most customers. Placement IDs are always passed in your bid requests.<br><br>**For select customers only**: If `true`, the seller sends placement IDs in bid requests. |
| `expose_age` | Boolean | If `true`, the seller sends the age of users in bid requests. |
| `expose_gender` | Boolean | If `true`, the seller sends the gender of users in bid requests. |
| `expose_universal_categories` | Boolean | **Not Used**. |
| `expose_custom_categories` | enum | The visibility of custom content categories in the seller's bid requests. Possible values:<br> - `"none"` - No custom categories are passed in bid requests.<br> - `"all"` - All custom categories are passed in bid requests.<br> - `"list"` - The custom categories listed in the `custom_categories` array are passed in bid requests. |
| `custom_categories` | array of objects | The custom content categories that the seller passes in bid requests, if `expose_custom_categories` is `"list"`. |
| `url_exposure` | enum | The visibility of impression urls in the seller's bid requests. Possible values:<br> - `"full`" - Full URLs are passed in bid requests.<br> - `"domain"` - Only domains of URLs are passed in bid requests.<br> - `"hidden"` - URLs are not passed in bid requests. Note that you may still receive the seller's default URL, if the seller has one configured. |

## Examples

### View information about member `74`

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/platform-member?id=74'
{
    "response": {
        "status": "OK",
        "platform-member": {
            "id": 74,
            "name": "PubMatic",
            "description": null,
            "primary_type": "seller",
            "platform_exposure": "public",
            "email": null,
            "daily_imps_verified": 200168000,
            "daily_imps_self_audited": 200168000,
            "daily_imps_unaudited": 168582133,
            "daily_imps_any_audit_status": 885677200,
            "daily_imps_appnexus_reviewed": 557187900,
            "daily_imps_appnexus_seller_reviewed": 557187900,
            "is_iash_compliant": false,
            "has_resold": false,
            "visibility_rules": {
                "expose_publishers": true,
                "expose_tags": true,
                "expose_age": true,
                "expose_gender": true,
                "expose_universal_categories": true,
                "url_exposure": "full",
                "expose_custom_categories": "none"
            },
            "bidder": {
                "id": "0",
                "name": "internal bidder"
            },
            "seller_type": "partner",
            "contact_info": [
                {
                    "name": "PubMatic RTB Team",
                    "title": null,
                    "email": "RTB@pubmatic.com",
                    "phone": null,
                    "address": null,
                    "address_2": null,
                    "city": "New York",
                    "country": "USA",
                    "region": "NY",
                    "postal_code": null,
                    "additional_info": "PubMatic can significantly increase the reach of your media buy, increase the efficiency of acquiring new publishers, and strengthen your publisher relationships. Contact us to learn how we can work together.",
                    "website_url": null,
                    "types": [
                        "supply"
                    ]
                }
            ],
            "active": true,
            "last_modified": "2013-06-21 17:48:49",
            "default_discrepancy_pct": 1
        },
        "count": 1,
        "start_element": 0,
        "num_elements": 100
    }
}
```

### View information about all members that have exposed their information

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/platform-member'
{
    "response": {
        "status": "OK",
        "platform-members": [
            {
                "id": 3,
                "name": "MikeOnAds",
                "description": null,
                "primary_type": "seller",
                "platform_exposure": "public",
                "email": null,
                "daily_imps_verified": 100,
                "daily_imps_self_audited": 100,
                "daily_imps_unaudited": 0,
                "daily_imps_any_audit_status": 2800,
                "daily_imps_appnexus_reviewed": 2600,
                "daily_imps_appnexus_seller_reviewed": 2600,
                "is_iash_compliant": false,
                "has_resold": true,
                "visibility_rules": {
                    "expose_publishers": true,
                    "expose_tags": true,
                    "expose_age": true,
                    "expose_gender": true,
                    "expose_universal_categories": true,
                    "url_exposure": "full",
                    "expose_custom_categories": "none"
                },
                "bidder": {
                    "id": "2",
                    "name": "DisplayWords"
                },
                "seller_type": "partner",
                "active": true,
                "last_modified": "2013-06-18 10:10:51",
                "default_discrepancy_pct": null
            },
            {
                "id": 7,
                "name": "Adify",
                "description": null,
                "primary_type": "network",
                "platform_exposure": "public",
                "email": null,
                "daily_imps_verified": null,
                "daily_imps_self_audited": null,
                "daily_imps_unaudited": null,
                "daily_imps_any_audit_status": null,
                "daily_imps_appnexus_reviewed": null,
                "daily_imps_appnexus_seller_reviewed": null,
                "is_iash_compliant": true,
                "has_resold": true,
                "visibility_rules": {
                    "expose_publishers": true,
                    "expose_tags": true,
                    "expose_age": true,
                    "expose_gender": true,
                    "expose_universal_categories": true,
                    "url_exposure": "full",
                    "expose_custom_categories": "none"
                },
                "bidder": {
                    "id": "0",
                    "name": "internal bidder"
                },
                "seller_type": "partner",
                "active": false,
                "last_modified": "2012-09-13 13:13:39",
                "default_discrepancy_pct": null
            },
            {
                "id": 8,
                "name": "Ning",
                "description": null,
                "primary_type": "network",
                "platform_exposure": "public",
                "email": null,
                "daily_imps_verified": null,
                "daily_imps_self_audited": null,
                "daily_imps_unaudited": null,
                "daily_imps_any_audit_status": null,
                "daily_imps_appnexus_reviewed": null,
                "daily_imps_appnexus_seller_reviewed": null,
                "is_iash_compliant": false,
                "has_resold": true,
                "visibility_rules": {
                    "expose_publishers": true,
                    "expose_tags": true,
                    "expose_age": true,
                    "expose_gender": true,
                    "expose_universal_categories": true,
                    "url_exposure": "full",
                    "expose_custom_categories": "none"
                },
                "bidder": {
                    "id": "0",
                    "name": "internal bidder"
                },
                "seller_type": "platform",
                "active": false,
                "last_modified": "2012-09-13 13:13:39",
                "default_discrepancy_pct": null
            },
            ...
        ],
        "count": 335,
        "start_element": 0,
        "num_elements": 100
    }
}  
```
