---
title: Smart Line Item Service 
description: The Smart line item represents the agreed-upon strategies that is executed for the advertiser.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Smart line item service

> [!NOTE]
> This feature is currently in Alpha and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

The Smart line item represents the agreed-upon strategies that is executed for the advertiser. It allows the advertiser to configure basic settings such as the Name, State, Ad type of the Smart line item, budgeting with automated CPC optimization, creatives, and targeting parameters.
> [!NOTE]
> To establish budgeting and flighting controls, a Smart insertion order must be associated before setting up a Smart line item.  

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
|`POST` | `https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID`<br> (Smart line item JSON) | Add a new Smart line item. |
|`PUT` | `https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID` <br> `https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE` <br> (Smart line item JSON) | Modify an existing Smart line item |
|`GET` | `https://api.appnexus.com/line-item?line_item_subtype=enhanced_performance&advertiser_id=ADVERTISER_ID` <br> `https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE` | View all the Smart line item(s) for one of your advertisers. |
|`DELETE` | `https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID`<br> `https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE` | Delete a Smart line item. <br><br> **Warning:** Deletion is Recursive and Permanent. Deleting a Smart line item will also delete all its associated budget intervals, and splits. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., revenue budget, tracking, cost budget and targeting). |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
|`name`| string | The name of the Smart line item.<br> **Required On:** POST |
|`line_item_type` | enum | The type of line item. This must be set to standard_v2 for Smart line item(s).  |
| `line_item_subtype` |  enum | The is the subtype of the Smart line item and cannot be changed after the line item is created. This needs to be set to `enhanced_performance` while creating a Smart line item. |
|`ad_types`| array of strings | The type of creative used for Smart line item. This must be set to native. <br> **Required On:** POST/PUT |
| `advertiser_id`| int | The ID of the advertiser to which the Smart line item is associated with. |
| `profile_id`| int | A profile is a generic set of rules for targeting inventory. You may associate an optional `profile_id` with a Smart line item. For details, see [Profile Service](profile-service.md). |
| `bid_cpc` | int | The maximum amount paid per click for a Smart line item. |
|`insertion_orders`| array of objects | These are objects containing metadata for the Smart insertion order(s) to which the Smart line item is associated with. The unique ID of the insertion order is used to associate the Smart line item to the insertion order by specifying the IDs in the `insertion_orders` array. |

## Example

### Create a JSON file and populate it with the appropriate values.

```
$ cat smart-line-item
{  
    "line-item": {  
      "name": "Smart LI - 1", 	
		"line_item_type": "standard_v2",  
  		"line_item_subtype": "enhanced_performance",  
  		"ad_types": ["native"],  
      "advertiser_id": 123,  
      "profile_id": 999,  
      "bid_cpc": 12.45,  
  		"insertion_orders": [{"id": 207}],  
    }  
} 
```

### Create a Smart line item using the JSON.

```
$ curl -b cookies -c cookies -X POST -d @smart-line-item 'https://api.appnexus.com/line-item?advertiser_id=123'
{
   "response":{
      "status": "OK",
      "id": 112
   }
}
```
