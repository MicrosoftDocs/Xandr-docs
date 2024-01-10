---
title: Data Buyer Provider Service
description: Learn how using Data Buyer Provider Service you can view all activated buyers on the Data Marketplace that have access to your data and have activated data clearing with you.    
ms.custom: data-providers
ms.date: 11/29/2023
---


# Data buyer provider service

## Data buyer provider service

The Data Buyer Provider Service allows you to view all activated buyers
on the Data Marketplace that have access to your data and have activated
data clearing with you. Any segment that you’ve mapped using the
existing [Segment Billing Category Service](segment-billing-category-service.md) will
automatically be cleared for these buyers.  
  
## REST API

**View all current buyers:**

GET https://api.appnexus.com/data-buyer-provider 

## JSON fields

| Field                   | Type (Length) | Description                                                                                | Default               |
|-------------------------|---------------|--------------------------------------------------------------------------------------------|-----------------------|
| `active`                  | boolean       | View whether the record is active or inactive                                              |                       |
| `buyer_member_id`         | int           | Member ID of the buyer                                                                     |                       |
| `data_cost_type`          | string        | Set cost type (inherited from data provider member) <br> - 1: CPM  <br> - 2: %MediaCost                   |                       |
| `data_provider_member_id` | int           | ID of data provider member assigned to you by the Data Marketplace                         |                       |
| `data_revshare_pct`       | double        | Data revenue share of the total cost (inherited from data provider member), e.g., 20% = `20` |                       |
| `id`                      | int           | ID of the sharing record                                                                   | Auto-generated number |
| `last_modified`           | date          | When the `data_buyer_provider` record was last modified                                      |                       |

## Example

**View all current buyers activated for data clearing**

``` 
curl -b cookies -c cookies "https://api.appnexus.com/data-buyer-provider?member_id=958&data_provider_member_id=958"
{
        "response": {
                "count": 1,
                "data_buyer_providers": [
                        {
                                "active": true,
                                "buyer_member_id": 1370,
                                "data_cost_type": "cpm",
                                "data_provider_member_id": 958,
                                "data_revshare_pct": 20,
                                "id": 2605,
                                "last_modified": "2017-10-05 20:57:21"
                        }
                ],
                "dbg_info":
                {
                        "output_term": "data_buyer_providers",
                        "version": "1.18.888",
                        "warnings": []
                },
                "num_elements": 100,
                "start_element": 0,
                "status": "OK"
        }
}
```
