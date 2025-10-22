---
title: Smart Insertion Order Service 
description: The Smart insertion order allows you to configure basic settings of the insertion order along with campaign budgeting parameters.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Smart insertion order service

> [!NOTE]
> This feature is currently in Alpha and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

The Smart insertion order allows the advertiser to configure basic settings such as the Name and State of the Insertion order along with campaign budgeting parameters. Spend from the Smart insertion order will not be factored into the member-level budget enforcement. 
> [!NOTE]
> Smart insertion order can only be associated to Smart line item(s).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` |`https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID`<br>(Smart insertion order JSON) | Add a new Smart insertion order. |
| `PUT` |  `https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID`<br> (Smart insertion order JSON)<br> | Modify an existing Smart insertion order. |
| `DELETE` | `https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID` | Delete a Smart insertion order.<br><br> **Warning:** Deleting a Smart insertion order does not necessarily mean that associated Smart line item(s) will be deleted as the relationship between a Smart insertion order and a Smart line item can be many to many. Also, deletion of an Smart insertion order results in deletion of the associated budget intervals.|
| `GET` | `https://api.appnexus.com/insertion-order?enhanced_performance=true&advertiser_id=ADVERTISER_ID` | View all the Smart insertion order(s) for any of your advertisers. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `name` | string(255) | The name of the Smart insertion order.<br> **Required On:** `POST` |
| `advertiser_id` | int |The ID of the advertiser.<br>**Required On**: `POST` |
| `enhanced_performance` | boolean | When this field is set to true, it will be used for creating a Smart insertion order which is then sent to the bidder. |
| `budget_interval` | array of objects | The `budget_interval` object allows you to configure budgeting parameters.<br> **Note:** For Smart insertion order only a single budget interval per Insertion order can be passed in. For more information, see [Budget Interval](#budget-interval) object below. |

### Budget interval

The budget_interval object contains the following fields.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `daily_budget` | double | The daily budget in revenue.<br> <br> **Note:** If you add Smart line item(s) to the Smart insertion order, any impressions associated with those line items are NOT counted in the lifetime budget of the insertion order. Only impressions that occur while the line item is a child of the insertion order is counted. <br> **Default:** null (unlimited) |
| `start_date` | timestamp | The start date and time during which the Smart insertion order should run. Limited to (00:00:00) |
| `end_date` | timestamp | The end date and time of the Smart insertion order. Limited to (23:59:59) |

## Example

### Create a JSON file and populate it with the appropriate values. 

```
$ cat smart-insertion-order
{  
    "insertion-order": {  
        "name": "Smart IO - 1",  
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

### Create a Smart insertion order using the JSON

```
$ curl -b cookies -c cookies -X POST -d @smart-insertion-order.json 'https://api.appnexus.com/insertion-order?advertiser_id=123'
{
   "response":{
      "status": "OK",
      "id": 207
   }
}
```