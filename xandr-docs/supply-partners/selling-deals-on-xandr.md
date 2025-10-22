---
title: Selling Deals on Xandr
description: This page walks you through steps so that as a supply partner you can use deals to provide Xandr buyers special access to your inventory. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---


# Selling deals on Xandr

> [!NOTE]
> You must be certified by Xandr to sell deals on our platform. Please contact [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) or your Xandr representative to find out how to become certified.

As a supply partner, you can use deals to provide Xandr buyers special access to your inventory and/or data. For example, a deal might provide preferential pricing on inventory, access to exclusive inventory, reduced competition on inventory, or other opportunities.

This page walks you through the process.

## Before you begin

Before you can add deals to Xandr and transact on them with buyers, you must:

1. Be certified to sell deals on the platform.
1. Understand the [OpenRTB protocol](openrtb-specs.md) for requesting and receiving bids from Xandr.
1. Learn how to use Xandr's API. See our [API Onboarding Process](../digital-platform-api/api-onboarding-process.md).

## Step 1. Create the deal in your system

1. Negotiate the deal with the Xandr buyer.
1. Add the deal to your own system.
1. Ask the Xandr buyer for their Xandr member ID, which you will need in the next step.

## Step 2. Add the deal to Xandr

> [!NOTE]
> This step shows you how to use Xandr's API to add a deal to Xandr manually. However, we recommend building an automated mechanism to sync your deals to Xandr whenever they are created in your own system.

1. [Authenticate](../digital-platform-api/authentication-service.md) in Xandr's API.
1. If the buyer did not give you their Xandr member ID, use the [Platform Member Service](../digital-platform-api/platform-member-service.md) to find it.  

> [!TIP]
> You can use the  `search`  query string parameter to search for the buyer by name. The example below shows the response that would be returned when searching for buyers with "Place" in their names. Note that the `id` field contains the member ID.

``` 
$curl -b cookies -c cookies 'https://api.appnexus.com/platform-member?search=Place
 
{
    "response": {
        "status": "OK",
        "count": 3,
        "start_element": 0,
        "num_elements": 100,
        "platform-members": [
            {
                "id": 1001,
                "name": "Some Place",
                "description": null,
                "primary_type": "network",
                "platform_exposure": "public",
                "email": null,
                "daily_imps_verified": null,
                "daily_imps_self_audited": null,
                "daily_imps_unaudited": null,
                "is_iash_compliant": false,
                "seller_type": "platform",
                "active": true,
                "last_modified": "2015-07-29 16:53:35",
                "default_discrepancy_pct": null,
                "bidder": {
                    "id": "2",
                    "name": "Bidder1"
                },
                "contact_info": [
                    {
                        "name": "Joe Smith",
                        "title": "VP Media Operations",
                        "email": "jsmith@example.com",
                        "phone": "",
                        "address": "",
                        "address_2": "",
                        "city": "New York",
                        "country": "US",
                        "region": "NY",
                        "postal_code": "10012",
                        "additional_info": "We use proprietary technology to...",
                        "website_url": null,
                        "types": [
                            "supply",
                            "demand"
                        ]
                    }
                ],
                "daily_imps_appnexus_seller_reviewed": 16542600,
                "daily_imps_any_audit_status": 16542600,
                "daily_imps_appnexus_reviewed": 15226100,
                "has_resold": true,
                "visibility_rules": {
                    "id": 55,
                    "expose_publishers": true,
                    "expose_tags": true,
                    "expose_age": true,
                    "expose_gender": true,
                    "expose_universal_categories": true,
                    "expose_custom_categories": "all",
                    "url_exposure": "full",
                    "custom_categories": null
                }
            },
            ...
        ],
        "dbg_info": {...
        }
    }
}
```

1. Use the [Deal Service](../digital-platform-api/deal-service.md) to add your deal to Xandr. In your JSON POST, be sure to:
    - Set the `code` field to your internal ID for the deal.
    - Set the `id` field in the `buyer` object to the buyer's member ID.
    - Set the `use_deal_floor` field to "true" and configure a deal floor by setting the `floor_price` field. When `use_deal_floor` is true, the deal's floor price overrides any other floors you may have, i.e., in placements or yield management profiles.
    - Always exclude the following fields in your JSON:
      - `profile_id`, `package_id` , `created_by`, `payment_type`
    - We recommend excluding the following fields in your JSON for most deals:
      - `size_preference`, `audit_status_option`, `brand_restrict`, `category_restrict`, `language_restrict`, `technical_attribute_restrict`, `brands`, `categories`, `languages`, `technical_attributes`, `creatives`, `priority`, `allowed_media_types`, `allowed_media_subtypes`, `media_preference`

## Step 3. Submit a bid request with your deal ID

For basic guidelines of how to create a bid request, see OpenRTB Bid Request. In addition, note the following requirements for deals:

- Your bid request must contain an additional object called `pmp`.
- Within the `pmp` object, you must also include a `deals` array containing the deal codes you wish to expose. Each deal code must be specified as the value of the `id` field in that array.

A sample JSON file including an array of deal codes is shown below.

``` 
cat bid_deal_request.json
 
{
 "id": "TEGY5Ate8u",
 "imp": [
  {
   "id": "4aXAJyMUJe",
   "tagid": "yvU4UdeVeT",
 "banner": {
    "w": 300,
    "h": 250
   },
 "pmp": {
   "deals": [
      {
        "id": "Deal 1"
      },
      {
        "id": "Deal 2"
       }
     ]
 },
 "minduration": 0,
 "maxduration": 3600,
    "w": 300,
    "h": 360,
 "startdelay": 0
   }
  }
 ],
 "site": {
  "id": "yvU4UdeVeT",
 "publisher": {
   "id": "AQA1udaHAB"
  }
 },
"member_id": 95
}
```

Then, POST the JSON-formatted file. Be sure to include your member ID in the querystring.

``` 
$ curl -X POST -d @bid_deal_request 'https://ib.adnxs.com/openrtb?member_id=123'
```

## Step 4. Listen for bid responses to your deal ID

Be sure that you are listening for the relevant `dealid` value in the OpenRTB Bid Response.

``` 
{
 "id": "TEGY5Ate8u",
 "seatbid": [
  {
   "seat": "57",
   "bid": [
    {
     "impid": "4aXAJyMUJe",
     "price": 0.002000,
     "id": "4715012638089865238",
     "adm": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><VAST version=\"2.0\"><Ad id=\"38\"></Ad></VAST>",
     "adomain": ["appnexus.com"],
     "crid": "38",
     "cid": "57",
     "iurl": "https://01-impbus-test17987.envnxs.net/cr?id=38",
     "adid": "38",
     "dealid": "Deal 1"
    }
   ]
  }
 ],
 "cur": "USD"
}
```
