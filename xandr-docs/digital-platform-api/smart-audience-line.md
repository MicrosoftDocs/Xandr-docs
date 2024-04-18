---
title: Smart Audience Line
description: The Smart Audience Line serves to optimize the performance campaign for Invest users by utilizing MSAN Bidder that offers potentially higher ROAS.
ms.date: 04/17/2024
ms.custom: digital-platform-api
---

# Smart Audience Line

> [!NOTE]
> This feature is currently in Alpha and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

The Smart Line serves to optimize the performance campaign for Invest users by utilizing MSAN Bidder that offers potentially higher Return on Ad Spend (ROAS). Our aim is not solely to achieve a specific supply volume, but to capitalize on bidding strategies accessible within MSAN.

The process begins when the advertiser invokes the Buy Side API to set up the following objects: 
- Smart Insertion Order(s)
- Smart Line Item(s)
- Creative(s) 

## Smart Insertion Order(s)
Smart Insertion Orders are for performance buying on Microsoft Audience Network only. It can only be associated to Smart Audience Line Items. Spend from this Insertion Order will not be factored into the member-level budget enforcement. 

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` |`https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID`<br>(insertion order JSON) | Add a new Smart Insertion Order. |
| `PUT` |  `https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID`<br>(insertion order JSON)<br> | Modify an existing Smart Insertion Order. |
| `DELETE` | `https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID`<br> **Important:** Deleting an insertion order does not necessarily mean that associated line items will be deleted as the relationship between an insertion order and line item can be many to many. Also, deletion of an insertion order results in deletion of the associated budget intervals. | Delete a Smart Insertion Order. |
| `GET` | `https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID` | View all the Smart Insertion Order(s) for one of your advertisers. |
| `GET` | `https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID` | View a specific Smart Insertion Order for one of your advertisers. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `name` | string(255) | The name of the Smart Insertion Order.<br> **Required On:** `POST` |
| `advertiser_id` | int |The ID of the advertiser.<br>**Required On**: `POST` |
| `daily_budget` | double | The daily budget in revenue. The revenue currency is defined by the currency field.<br> **Note:** If you add line items to the Smart Insertion Order, any impressions associated to those line items when they are added to the insertion order are NOT counted under the lifetime budget of the insertion order. Only impressions that occur while the line item is a child of the insertion order are counted. <br> **Default:** null (unlimited) |
| `enhanced_performance` | boolean | When this field is set to true, it will be used for a Smart  Insertion Order which is sent to MSAN. <br> **Required:** True |

### Budget Interval

| Field | Type (Length) | Description |
|:---|:---|:---|
| `start_date` | timestamp | The start date and time during which the Insertion Order should run.Limited to (00:00:00) |
| `end_date` | timestamp | The end date and time of the Smart Insertion Order. Limited to (23:59:59) |
|`daily_budget_imps`| int | The daily budget in impressions.<br> **Default:** null (unlimited) |
|`enable_pacing`| boolean | If enabled, then spending will be paced over the course of the day. Only applicable if there is a daily_budget.<br> **Required:** To be set to False |
|`lifetime_budget`| double | The lifetime budget in revenue. The revenue currency is defined by the currency field.<br> **Default:** null (unlimited) |
|`lifetime_budget_imps`| int | The lifetime budget in impressions.<br> **Note:** If you add line items to the Smart Insertion Order, any spend already associated with those line items before they are added to the insertion order is NOT counted against the lifetime budget of the insertion order. Only spend that occurs while the line item is a child of the insertion order is counted. Only applicable to non-seamless insertion orders.<br> **Default:** null (unlimited) |
|`lifetime_pacing`| boolean | If enabled, the insertion order will attempt to spend its overall lifetime budget evenly over the insertion order flight dates. If true:<br> - You must establish a lifetime_budget or lifetime_budget_imps.<br> - You must establish a start_date and end_date.<br> - You cannot set a daily_budget.<br> - You cannot set enable_pacing to false.<br> <br> **Required:** To be set to False  |

## Insertion order example

### Make a file containing JSON and add the correct values. Necessary fields include advertiser ID and name.

```
{  
    "insertion-order": {  
        "name": "My Performance IO",  
        "advertiser_id": 123,  
        "budget_intervals": [  
            {  
                "start_date": "2030-10-10 00:00:00",  
                "end_date": "2030-10-12 23:59:59",  
                "daily_budget": 100,  
                "daily_budget_imps": null,  
                "enable_pacing": false,  
                "lifetime_budget": null,  
                "lifetime_budget_imps": null,  
                "lifetime_pacing": false  
            }  
        ],  
  "enhanced_performance": true  
    }  
} 
```

## Smart Line Item(s)
Smart Line Item(s) are set up for buying Microsoft Audience Network with automated CPC optimization. A Smart Insertion Order is required to associate budgeting and flighting controls to be associated before setting up a Smart Line Item. The line items under a Smart Insertion Order represent the agreed upon strategies you will be executing for the advertiser.  

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
|`POST` | `https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID`<br> (line item JSON) | Add a new Smart Line Item. |
|`PUT` | `https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID` <br> `https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE` <br> (line item JSON) | Modify an existing Smart Line Item |
|`GET` | `https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID` <br> `https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE` | View all the Smart Line Item(s) for one of your advertisers. |
|`DELETE` | `https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID`<br> `https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE`<br> **Warning:** Deletion is Recursive and Permanent. Deleting a Smart Line Item will also delete all its associated budget intervals, and splits. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., revenue budget, tracking, cost budget and targeting). | Delete a Smart Line Item |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
|`name`| string | The name of the line item.<br> **Required On:** POST |
|`line_item_type` | enum | The type of line item. This must be set to standard_v2 for Smart Line Item(s).  |
| `line_item_subtype` |  enum | The is the subtype of the Smart Line Item and cannot be changed after the line item is created. For Invest buyers, the supported values are as follows:<br> - **standard_buying:** Augmented line item eligible to serve on managed, RTB, or deals. Omitting the line_item_subtype on `POST` requests will default to this subtype behaviour.<br> - **pg_buying:** Eligible only to transact on PG deals. If the subtype is passed on the POST, the line_item_type, bid_object_type, delivery_model_type, and supply_strategies fields are not required.<br> - **standard_curated:** For curated deal line items. For more details, see `line_item_subtype` in [Curated Deal Line Item API Setup Guide](https://learn.microsoft.com/en-us/xandr/digital-platform-api/curated-deal-ad-quality-api-setup-guide).<br> **Default:** standard_buying |
|`ad_types`| array of strings | The type of creative used for this line item is native. <br> **Required On:** POST/PUT |
| `advertiser_id`| int | The ID of the advertiser to which the line item belongs. |
| `profile_id`| int | A profile is a generic set of rules for targeting inventory. You may associate an optional `profile_id` with this line item. For details, see the [Profile Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service). |
| `bid_cpc` | int | The maximum amount paid per click for a Smart Line Item |
|`insertion_orders`| array of objects | Objects containing metadata for the insertion orders this line item is associated with. For more information, see [Insertion Orders](https://learn.microsoft.com/en-us/xandr/digital-platform-api/line-item-service---ali#insertion-orders) below.<br> **Note:** Once a line item is associated with a seamless insertion order, it cannot be associated to a legacy insertion order |

### Payload

```
{  
    "line-item": {  
       	"name": "My Performance LI", 	
		"line_item_type": "standard_v2",  
  		"line_item_subtype": "enhanced_performance",  
  		 "ad_types": ["native"],  
        "advertiser_id": 123,  
        "profile_id": 999,  
        "bid_cpc": 1234567890123.45,  
  		 "insertion_orders": [{"id": 23444}],  
    }  
} 
```

## Profile Service 
A profile is a set of targeting parameters, such as gender, age, geography, and frequency. It can be applied to several objects in the system, most of which are listed below. The most common use of the profile service is to run a campaign; you create a profile and then associate it with the [Campaign Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/campaign-service). <br>
> [!NOTE]: 
> Profile ID will only be used on the line-item level by an enhanced_performance Line Items. 

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
|`POST`|`https://api.appnexus.com/profile?advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID`<br>(profile JSON) | Add a new profile. |
| `POST` | `https://api.appnexus.com/profile?advertiser_code=ADVERTISER_CODE`<br>(profile JSON) | Add a new profile.  |
|`PUT` | `https://api.appnexus.com/profile?id=PROFILE_ID&advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID`<br> (profile JSON) | Modify an existing profile. |
| `PUT` | `https://api.appnexus.com/profile?code=PROFILE_CODE&advertiser_code=ADVERTISER_CODE`<br> (profile JSON) | Modify an existing profile. |
| `GET` | `https://api.appnexus.com/profile?advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID` | View all of the profiles for one of your advertisers.
|`GET` | `https://api.appnexus.com/profile?advertiser_code=ADVERTISER_CODE` | View all of the profiles for one of your advertisers. |
|`GET` | `https://api.appnexus.com/profile?id=PROFILE_ID&advertiser_id=ADVERTISER_ID&member_id=MEMBER_ID` | View a specific profile for one of your advertisers. |
| `GET` | `https://api.appnexus.com/profile?code=PROFILE_CODE&advertiser_code=ADVERTISER_CODE` | View a specific profile for one of your advertisers. |
 
## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
|`age_targets` |array of strings | The list of age ranges to target for this profile. The allow_unknown field is available as a Boolean in order to account for ad calls where the age of the user is not available. For more description and examples, see the Age Targets section below. Only the following ranges are allowed: <br>- `['low' => 18, 'high' => 24]`,<br> -`['low' => 25, 'high' => 34]`,<br> -`['low' => 35, 'high' => 49]`,<br> -`['low' => 50, 'high' => 64]`,<br> -`['low' => 65, 'high' => 100]` |
|`city_action` | enum | Action to be taken on the city_targets list. Possible values:<br> - include <br> - exclude.<br> **Default:** exclude |
|`city_target`| array of objects | The IDs of cities to be either included or excluded in a profile, as defined by the city_action field. You can use the [City Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/city-service) to retrieve a list of city IDs. For more details and format, see [City Targets](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service#city-targets) below.<br> **Required On:** POST/PUT, when `city_action` is include. |
|`country_action`| enum | Action to be taken on the country_targetslist. Possible values:<br> - include<br> - exclude.<br> **Default:** exclude |
| `country_targets` | array of objects | The country IDs to be either excluded or included in a profile, as defined by the country_action field. You can use the [Country Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/country-service) to retrieve a list of country IDs. For more details and format, see [Country Targets](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service#country-targets).<br> **Required On:** POST/PUT, when country_actionis include. |
|`daypart_targets`| array of objects | The day parts during which to serve the campaign. For more details, see Daypart Targets below.<br> **Note:** If you do not set any daypart targets, the campaign will serve on all days of the week at all times. |
| `device_type_targets` | array of strings | The types of devices to either include in or exclude from your targeting, as defined by the device_type_action field.<br> Possible values: <br> - phone <br> - tablet <br> - pc <br> - tv <br> - gameconsole <br> - stb <br> - mediaplayer <br> <br> For format, see [Device Type Targets](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service#device-type-targets) |
|`device_type_action` | enum | Action to be taken on device_type_targets. device_type can only be defined using `device_type_action = include`, and can only target the following device types: <br> - `'pc'`, <br> - `'phone'`, <br> - `'tablet'`, <br> **Possible values:** include or exclude. <br> **Default:** exclude |
|`gender_targets`| object | The gender targeting used for the profile. Possible values for gender are m(male) or f(female). The allow_unknown field is available as a Boolean in order to account for ad calls where the gender of the user is not available. See the [Gender Targets](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service#device-type-targets). |
| `postal_code_targets` | object | The postal code IDs to target. IDs can be fetched using the [Postal Code Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/postal-code-service). |
| `postal_code_action_include` | array of objects | The postal code list IDs to target. IDs can be fetched using the [Postal Code List Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/postal-code-list-service) |
|`region_action` | enum | Action to be taken on the region_targets list.<br> Possible values: <br> - include <br> - exclude <br> **Default:** exclude |
|`region_targets`|array of objects | The region/state IDs to be either excluded or included in a profile, as defined by the region_action field. You can use the [Region Service](https://nam06.safelinks.protection.outlook.com/GetUrlReputation) to retrieve a list of region IDs. For more details and format, see [Region Targets](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service#region-targets).<br> **Required On:** POST/PUT, when `region_action` is include. |
| `segment_group_target` | array of objects | The segment groups to target. Whereas the `segment_targets` array allows you to define Boolean logic between individual segments, this array allows you to establish groups of segments, defining Boolean logic between the groups as well as between the segments within each group. You define the Boolean logic between groups with the `segment_boolean_operator` field outside of the array; you define the Boolean logic between segments in a group with the `boolean_operator` field within the group object. For more details, see [Segment Group Targets](https://learn.microsoft.com/en-us/xandr/digital-platform-api/profile-service#segment-group-targets). Segment group targets can only define 1 exclude group and 1 include group, and these two can only be OR’ed. Only 'In-Market' segments are allowed to be targeted. <br> **Note:** Null segments cannot be added. You may not add null segments to this array using `POST` or `PUT`. |

## Creatives
The Creative Service can be used to add creatives to our system. All creatives must be attached to an advertiser or publisher. Microsoft works with members who care deeply about brand and reputation. For this reason, we are careful to ensure that the advertisements (creatives) that pass through our system are acceptable to all parties. For quality assurance, all creatives that serve on third-party inventory must be pre-registered using the Creative Service. For more information, see [Creative Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/creative-service). <br>

When associating a creative with a Smart Line Item:  
- It must have `native_attribute` set, with an `image_asset` of type “main_image”  
    - The width of this image asset must be greater than 703 pixels, and the height must be greater than 368 pixels. 

 


