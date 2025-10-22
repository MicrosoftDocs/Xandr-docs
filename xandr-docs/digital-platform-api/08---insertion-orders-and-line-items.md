---
title: Insertion Orders and Line Items
description: In this article, learn how to create an insertion order and a line item by providing the necessary fields and details.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Insertion orders and line items

Once the advertiser is properly configured, we can begin building out the sell-side hierarchy.  

## Insertion order

In order to start the hierarchy, an insertion order must be created first. For any insertion order, you should supply the following details:

- Advertiser ID (`"advertiser_id"`).
- Name (`"name"`).
- Flight dates (`"start_date"` and `"end_date"`) - **Optional**.
- Budget (`"lifetime_budget"`, `"lifetime_budget_imps"`, `"daily_budget"`, `"daily_budget_imps"`) - **Optional**.
- Pacing (`"enable_pacing"`) - **Optional**.
- Currency (`"currency"`) - **Optional (default set at advertiser level)**.

### Insertion order example

Make a file containing JSON and add the correct values. Necessary fields include advertiser ID and name.

```
$ cat insertion_order
{
  "insertion-order": {
    "name": "Q1 2011",
    "advertiser_id": 1234,
    "lifetime_budget": 10000,
    "daily_budget": 1000,
    "enable_pacing": true,
    "currency": "USD"
  }
}
```

Then to create the new insertion order, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @insertion_order 'https://api.appnexus.com/insertion-order?advertiser_id=1234'
{
   "response":{
      "status": "OK",
      "id": 53
   }
}
```

This returns the ID of the insertion order (in this case, the insertion order ID is 53). To view the newly added insertion order send a `GET` request to the insertion order service, including the advertiser ID and the insertion order ID.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/insertion-order?id=53&advertiser_id=1234'
{
  "response": {
    "status": "OK",
    "insertion-order": {
      "id": 53,
      "name": "Q1 2011",
      "code": null,
      "state": "inactive",
      "advertiser_id": 1234,
      "start_date": null,
      "end_date": null,
      "last_modified": "2011-07-13 11:58:03",
      "line_items": null,
      "users": null,
      "timezone": "EST5EDT",
      "lifetime_budget": 10000,
      "lifetime_budget_imps": null,
      "daily_budget": 1000,
      "daily_budget_imps": null,
      "enable_pacing": true,
      "currency": "USD",
      "labels": null,
      "broker_fees": null
    },
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "dbg_info": {
      ...
    }
  }
}
```

## Line item

The next level of the hierarchy is to set up the line item. The line item must be associated with an insertion order or it will not serve. For any line item, you should supply the following details:

- Advertiser ID (`"advertiser_id"`).
- Name (`"name"`).
- Flight dates (`"start_date"` and `"end_date"`) - **Optional**.
- Budget (`"lifetime_budget"`, `"lifetime_budget_imps"`, `"daily_budget"`, `"daily_budget_imps"`) - **Optional**.
- Pacing (`"enable_pacing"`) - **Optional**.
- Currency (`"currency"`) - **Optional (default set at advertiser or insertion order level)**.
- Revenue (`"revenue_type"`, `"revenue_value"`, and `"pixels"`).
- Insertion order ID (`"insertion_orders[{id}]"`).

## Line item example

Make a file containing JSON and add the correct values. Necessary fields include advertiser ID, name, and revenue.

```
$ cat line-item
{
  "line-item": {
    "name": "Q1 2011 - CPM Revenue",
    "advertiser_id": 1234,
    "lifetime_budget": 7500,
    "daily_budget": 750,
    "enable_pacing": true,
    "currency": "USD",
    "revenue_type": "cpm",
    "revenue_value": 5,
    "insertion_order": [{
        "id": 53
    }]
  }
}
```

Then to create the new line item, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @line-item 'https://api.appnexus.com/line-item?advertiser_id=1234'
{
   "response":{
      "status": "OK",
      "id": 205
   }
}
```

This returns the ID of the line item (in this case, the line item ID is 205). To view the newly added line item send a `GET` request to the line item service, including the advertiser ID and the line item ID.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?id=205&advertiser_id=1234'
{
  "response": {
    "status": "OK",
    "line-item": {
      "id": 205,
      "code": null,
      "name": "Q1 2011 - CPM Revenue",
      "advertiser_id": 1234,
      "state": "inactive",
      "start_date": null,
      "end_date": null,
      "timezone": "EST5EDT",
      "lifetime_budget": 7500,
      "lifetime_budget_imps": null,
      "daily_budget": 750,
      "daily_budget_imps": null,
      "enable_pacing": true,
      "publishers_allowed": "all",
      "lifetime_spend": null,
      "lifetime_imps": null,
      "daily_spend": null,
      "daily_imps": null,
      "revenue_value": 5,
      "revenue_type": "cpm",
      "pixels": null,
      "insertion_orders": 53,
      "goal_type": "none",
      "goal_value": null,
      "insertion_orders": [
          {
              "id": 53,
              "state": "inactive",
              "code": null,
              ...
           }
      ],
      "goal_pixels": null,
      "last_modified": "2011-07-13 19:17:21",
      "click_url": null,
      "currency": "USD",
      "require_cookie_for_tracking": true,
      "labels": null,
      "advertiser": {
        "id": 1234,
        "name": "Advertiser ABC"
      },
      "broker_fees": null,
      "profile_id": 0,
      "member_id": 123
    },
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "dbg_info": {
      ...
    }
  }
}
```
