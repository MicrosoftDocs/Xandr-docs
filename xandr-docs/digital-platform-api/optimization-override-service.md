---
title: Optimization Override Service
description: Use the Optimization Override service to override a line item's default settings. You can turn off discovery and adjust the discovery fail criteria.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Optimization Override service

The Optimization Override service allows clients with sophisticated optimization needs to override a line item's default settings for Discovery, an optimization feature ranks inventory based on its historical CPC and stops your line item from serving on inventory that doesn't perform. Discovery uses a **fail criterion** to cap amount of budget or number of impressions spent before a section of inventory is "axed" (considered failed and removed from eligibility for this line item).

The Optimization Override service allows you to:

- Turn off Discovery.
- Adjust the Discovery fail criteria.

When you set custom fail criteria, these are the rules followed based on the objective you choose for line item optimization preference:

- When **Prefer performance** is selected, Xandr axes inventory at 1x the fail criteria value.
- When **Prefer delivery** is selected, Xandr axes inventory at a dynamic threshold up to 10x the fail criteria value.
- When **Prefer margin** is selected, Xandr axes inventory at 1x the fail criteria.

For more about selecting to prefer performance, delivery, or margin, see [Line Item Service - ALI](./line-item-service---ali.md).

Optimization override can be useful if:

- You're using CPC optimization to value clicks, but do not want to filter the inventory you serve on based on its historical CPC.
- You want to use Discovery, but you want to set a fail criteria at a threshold that's less strict than the line item's CPC goal.
- You want to turn off Discovery altogether and leverage only Xandr click prediction.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/discovery` | Retrieve Discovery settings for all customized line items in a member.<br><br>**Note**: Information is returned only when the Discovery settings have been customized. If the Discovery settings are the default settings, no details are returned. |
| `GET` | `https://api.appnexus.com/discovery?line_item_id=LINE_ITEM_ID` | Retrieve custom Discovery settings for a single line item. <br><br>**Note**: Information is returned only when the Discovery settings have been customized. If the Discovery settings are the default settings, no details are returned. |
| `PUT` | `https://api.appnexus.com/discovery?line_item_id=LINE_ITEM_ID` | Update custom Discovery settings. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `discovery_enabled` | Boolean | Turn discovery on or off. <br><br>**Note**: Discovery can only be enabled on Augmented Line Items where the goal type is CPC or post-click CPA.<br><br>**Default**: `true` |
| `fail_criteria_amount` | decimal | The amount of booked revenue (in the local currency set at the advertiser level) to spend on a selection of inventory before the inventory is failed. |
| `id` | int | The ID of the Discovery settings profile.<br><br>**Default**: auto-generated number. |
| `line_item_id` | int | The ID of the line item whose Discovery Settings are being altered. |
| `member_id` | int | Member ID. |

## Examples

### View custom discovery settings for a line item

```
curl -X GET -c cookies -b cookies "https://api.appnexus.com/discovery?line_item_id=LINE_ITEM_ID"
 
[
   {
      "id" : 1,
      "member_id" : MEMBER_ID,
      "line_item_id" : LINE_ITEM_ID,
      "discovery_enabled" : true,
      "fail_criteria_amount" : 3
   }
]
```

### Disable discovery

Check to see if a discovery profile exists.

```
$ curl -b cookie "https://api.appnexus.com/discovery?line_item_id=LINE_ITEM_ID"
```

If a profile doesn't exist (a blank is returned instead of a profile), you must create a discovery profile. You can create a discovery profile that is already disabled or disable an existing discovery profile with the same JSON.

```
$ cat discovery.json
{
    "member_id" : MEMBER_ID,
    "line_item_id" : LINE_ITEM_ID,
    "discovery_enabled": false
}

$ curl -X POST -b cookies -d @discovery.json "https://api.appnexus.com/discovery?line_item_id=LINE_ITEM_ID"
```

### Update discovery settings

```
$ cat discovery
{
    "id" : ID_VALUE,
    "member_id" : MEMBER_ID,
    "line_item_id" : LINE_ITEM_ID,
    "discovery_enabled": true,
    "fail_criteria_amount": FAIL_CRITERIA_AMOUNT
}

$ curl -b cookie -X PUT -d @discovery "https://api.appnexus.com/discovery?line_item_id=LINE_ITEM_ID"
```
