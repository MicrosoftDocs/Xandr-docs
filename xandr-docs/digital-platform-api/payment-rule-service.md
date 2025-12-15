---
title: Payment Rule Service
description: Learn about Payment Rule service. A payment rule sets terms for networks to pay managed publishers.
ms.date: 12/15/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Payment Rule service

A payment rule defines the terms by which a network pays one of its managed publishers. A network may have more than one set of payment terms with a publisher. For instance, traffic originating from certain geographic areas may have different revenue sharing agreement terms.

> [!NOTE]
> Targeting of advertisers, or line items via the [Placement Service](./placement-service.md) will override any targeting of those objects via this service's optional `profile_id`.

## REST API

> [!NOTE]
> `publisher_code` can be used in place of `publisher_id`, and `payment_rule_code` can be used in place of `publisher_rule_id` for all of the calls below.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/payment-rule?publisher_id=PUBLISHER_ID` <br>(payment-rule JSON) | Add a new payment rule. |
| `PUT` | `https://api.appnexus.com/payment-rule?id=PAYMENT_RULE_ID&publisher_id=PUBLISHER_ID` <br>(payment-rule JSON) | Modify an existing payment rule. |
| `GET` | `https://api.appnexus.com/payment-rule?publisher_id=PUBLISHER_ID` | View all of the payment rules for a publisher. |
| `GET` | `https://api.appnexus.com/payment-rule?id=PAYMENT_RULE_ID` | View a specific payment rule for a publisher. |
| `GET` | `https://api.appnexus.com/payment-rule?id=1,2,3` | View multiple payment rules by ID using a comma-separated list. |
| `DELETE` | `https://api.appnexus.com/payment-rule?id=PAYMENT_RULE_ID` | Delete a payment rule. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of this payment rule.<br>**Required On**: `PUT`, in query string |
| `code` | string | A optional custom code you can use to reference this payment rule.<br><br>**Default**: `Null` |
| `name` | string | A name used to describe this payment rule.<br><br>**Default**: `None`<br>**Required On**: `POST` |
| `state` | enum | The state of this payment rule. Possible values: `"active"` or `"inactive"`.<br><br>**Default**: `"active"` |
| `description` | string | An optional description. |
| `start_date` | timestamp | Start date for this rule.<br><br>**Default**: `Immediately` |
| `end_date` | timestamp | End date for this rule.<br><br>**Default**: `Indefinitely` |
| `pricing_type` | enum | Possible values:<br> - `"revshare"` - The publisher gets paid a percentage of ad revenue.<br> - `"cpm"` - The publisher is paid a flat fee per ad served.<br> - `"dynamic"` - The payment terms are defined by a min and max revshare and a target eCPM.<br><br>**Default**: `"revshare"`<br>**Required On**: `POST` |
| `cost_cpm` | double | If `pricing_type` is `"cpm"`, this is the CPM fee the publisher is paid.<br><br>**Required On**: `POST`, if `pricing_type` is `"cpm"` |
| `revshare` | double | If `pricing_type` is `"revshare"`, this is the percentage paid to the publisher. If pricing type is `"dynamic"`, this is the minimum revshare percentage paid to the publisher, with the maximum defined by `max_revshare`. The percentage should be expressed as a number between 0 and 1 (inclusive), where 1 is 100%.<br><br>**Required On**: `POST`, if `pricing_type` is `"revshare"` or `"dynamic"` |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply a payment rule. A profile is a generic set of rules for targeting inventory, and certain payment rules may only apply to certain slices of inventory. See the [Profile Service](./profile-service.md) for details. |
| `priority` | int | You can optionally provide a priority which defines the level at which this rule should that be applied relative to other payment rules.<br><br>**Default**: `5` |
| `timezone` | string | The timezone used to calculate pricing data. For a list of timezones, see [API Timezones](./api-timezones.md).<br><br>**Default**: `'EST5EDT'` |
| `last_modified` | timestamp | The time of the last modification to this payment rule. |
| `filtered_advertisers` | array of objects | A list of advertisers that you'd like to apply the action specified by `demand_filter_action` to. See [Filtered Advertisers](#filtered-advertisers) below. |
| `filtered_line_items` | array of objects | A list of line items that you'd like to apply the action specified by `demand_filter_action` to. See [Filtered Line Items](#filtered-line-items) below. |
| `filtered_campaigns` | array of objects | Deprecated. A list of campaigns that you'd like to apply the action specified by `demand_filter_action` to. See [Filtered Campaigns](#filtered-campaigns) below. |
| `buyer_type` | enum | Which buyer types to apply this payment rule to.<br>Possible values:<br> - `"direct"`: your own, managed inventory<br> - `"external"`: 3rd party, managed inventory<br> - `"both"`<br><br>**Default**: `"both"` |
| `max_revshare` | double | If `pricing_type` is `"dynamic"`, this is the maximum revshare percentage paid to the publisher.<br><br>**Required On**: `POST`, if `pricing_type` is `"dynamic"`. |
| `apply_cost_on_default` | boolean | Whether or not the publisher is paid even if the auction defaults. |
| `demand_filter_action` | enum | Decide whether to include or exclude the advertisers and/or line items listed in the `filtered_advertisers`, or `filtered_line_items` arrays.<br>Possible values:<br> - `"include"`<br> - `"exclude"`<br>- `"default"` |

### Demand filtering

Demand filtering can be a useful targeting capability, but it’s important to understand how it works before using it in payment rules or placements.

#### Key considerations #####

1. Applies only to managed demand: Demand filtering in payment rules or placements applies only to managed demand. If a placement is enabled for reselling, campaigns from third-party demand sources are not affected by demand filtering.
2. One payment rule applies per impression: Each impression uses a single payment rule, which is selected at the start of the auction. Once selected, the payment rule determines which demand is eligible to participate.
Because of this behavior, you can’t use payment rule demand filtering to adjust publisher payouts based on which demand source wins the auction. Specifically:
  - **Including a line item**: 
    When a payment rule _includes_ a specific line item, that line item is excluded from the auction when the payment rule is applied. Only other managed line items and RTB        demand are eligible to serve. For example, if filtered_line_items = `1234` and demand_filter_action = `include`, line item `1234` won’t be eligible to bid when this            payment rule is selected.
  - **Excluding a line item**:
    When a payment rule excludes a specific line item, only that line item is eligible to bid from managed demand. All other managed line items are excluded, while RTB demand      remains eligible. For example, if filtered_line_items = `1234` and demand_filter_action = `exclude`, only line item `1234` can bid from managed demand when this payment        rule is selected. If that line item reaches its frequency cap, is pacing, or is otherwise ineligible, no managed demand will be eligible to serve while the payment rule        remains selected.
3. Placement-level filtering takes precedence: Demand filtering configured at the placement level overrides demand filtering configured at the payment rule level. If demand inclusions or exclusions are set on a placement, all payment rule–level demand filtering is ignored. For more information, see [Placement demand filtering](https://learn.microsoft.com/xandr/monetize/create-a-placement#step-7-apply-advanced-settings-to-your-placement-optional).

### Filtered advertisers

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the advertiser. |
| `name` | string | The name of the advertiser. |

### Filtered line items

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item. |
| `name` | string | The name of the line item. |

### Filtered campaigns

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the campaign. |
| `name` | string | The name of the campaign. |

## Examples

### Create a payment rule

```
$ cat payment_rule.json

{
    "payment-rule":{
        "name": "France - 1/24 - $.40 CPM",
        "code": "france_payment_rule",
        "pricing_type": "cpm",
        "cost_cpm": "0.4",
        "state": "active",
        "start_date": "2010-01-01 00:00:00",
        "end_date": "2010-03-31 11:59:59",
        "priority": 8,
        "profile_id": 12345
    }
}

$ curl -c cookies -b cookies -X POST -d @payment_rule.json 'https://api.appnexus.com/payment-rule?publisher_id=65103'

{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 66323,
    "start_element": 0,
    "num_elements": 100,
    "payment-rule": {
      "id": 66323,
      "code": "france_payment_rule",
      "name": "France - 1/24 - $.40 CPM",
      "description": "",
      "pricing_type": "cpm",
      "cost_cpm": 0.4,
      "revshare": null,
      "state": "active",
      "start_date": "2010-01-01 00:00:00",
      "end_date": "2010-03-31 11:59:59",
      "profile_id": 12345,
      "timezone": "EST5EDT",
      "priority": 8,
      "last_modified": "2011-02-18 21:19:52"
    }
  }
}
```

### Read a single payment rule

```
$ curl -b cookies 'https://api.appnexus.com/payment-rule?id=92873'

{
    "payment-rule": {
    "apply_cost_on_default": true,
    "target_ecpm": 0.8,
    "max_revshare": 0.8,
    "buyer_type": "both",
    "last_modified": "2012-08-02 19:04:00",
    "priority": 10,
    "timezone": "EST5EDT",
    "profile_id": null,
    "end_date": null,
    "start_date": "2013-01-01 00:00:00",
    "state": "active",
    "revshare": 0.67,
    "cost_cpm": 40,
    "pricing_type": "dynamic",
    "description": "A payment rule for targeting USA users",
    "name": "USA",
    "code": "usa_payment_rule",
    "id": 98273
    }
}
```

### Read all of a publisher's payment rules

```
$ curl -c cookies -b cookies 'https://api.appnexus.com/payment-rule?publisher_id=65103'

{
  "response": {
    "status": "OK",
    "count": 4,
    "start_element": null,
    "num_elements": null,
    "payment-rules": [
      {
        "id": 95479,
        "code": null,
        "name": "Base Payment Rule",
        "description": "",
        "pricing_type": "revshare",
        "cost_cpm": null,
        "revshare": 0.6,
        "state": "active",
        "start_date": null,
        "end_date": null,
        "profile_id": null,
        "timezone": "EST5EDT",
        "priority": 1,
        "last_modified": "2012-04-09 11:40:54",
        "buyer_type": "both",
        "max_revshare": null,
        "target_ecpm": null,
        "apply_cost_on_default": false,
        "demand_filter_action": "default",
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "filtered_advertisers": null,
        "filtered_line_items": null
      },
      {
        "id": 95480,
        "code": null,
        "name": "AbenBog Unique Impressions",
        "description": "",
        "pricing_type": "revshare",
        "cost_cpm": null,
        "revshare": 0.7,
        "state": "active",
        "start_date": "2012-04-09 00:00:00",
        "end_date": null,
        "profile_id": 142958,
        "timezone": "EST5EDT",
        "priority": 5,
        "last_modified": "2012-04-09 11:46:32",
        "buyer_type": "both",
        "max_revshare": null,
        "target_ecpm": null,
        "apply_cost_on_default": false,
        "demand_filter_action": "exclude",
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "filtered_advertisers": null,
        "filtered_line_items": null
      },
      {
        "id": 98434,
        "code": null,
        "name": "Rich's cool payment rule",
        "description": "",
        "pricing_type": "revshare",
        "cost_cpm": null,
        "revshare": 0.7,
        "state": "active",
        "start_date": null,
        "end_date": null,
        "profile_id": null,
        "timezone": "EST5EDT",
        "priority": 5,
        "last_modified": "2012-08-03 17:37:17",
        "buyer_type": "both",
        "max_revshare": null,
        "target_ecpm": null,
        "apply_cost_on_default": true,
        "demand_filter_action": "default",
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "filtered_advertisers": null,
        "filtered_line_items": null
      },
      {
        "id": 98435,
        "code": "this_is_a_test",
        "name": "Rich's other cool payment rule",
        "description": "",
        "pricing_type": "revshare",
        "cost_cpm": null,
        "revshare": 0.7,
        "state": "active",
        "start_date": null,
        "end_date": null,
        "profile_id": null,
        "timezone": "EST5EDT",
        "priority": 5,
        "last_modified": "2012-08-03 17:57:27",
        "buyer_type": "both",
        "max_revshare": null,
        "target_ecpm": null,
        "apply_cost_on_default": true,
        "demand_filter_action": "default",
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "filtered_advertisers": null,
        "filtered_line_items": null
      }
    ]
  }
}
```

### Update a payment rule

```
$ cat payment_rule.json

{
    "payment-rule": {
    "apply_cost_on_default": true,
    "target_ecpm": 0.8,
    "max_revshare": 0.8,
    "priority": 10,
    "timezone": "EST5EDT",
    "revshare": 0.67,
    "cost_cpm": 40,
    "pricing_type": "dynamic",
    "description": "A payment rule for targeting USA users"
    }
}

$ curl -b cookies -X PUT -d @payment_rule.json
'https://api.appnexus.com/payment-rule?publisher_id=65103&id=98273'

{
    "payment-rule": {
    "apply_cost_on_default": true,
    "target_ecpm": 0.8,
    "max_revshare": 0.8,
    "buyer_type": "both",
    "last_modified": "2012-08-02 19:04:00",
    "priority": 10,
    "timezone": "EST5EDT",
    "profile_id": null,
    "end_date": null,
    "start_date": "2013-01-01 00:00:00",
    "state": "active",
    "revshare": 0.67,
    "cost_cpm": 40,
    "pricing_type": "dynamic",
    "description": "A payment rule for targeting USA users",
    "name": "USA",
    "code": "usa_payment_rule",
    "id": 98273
    }
}
```

### Delete a payment rule

```
$ curl -b cookies -X DELETE "https://api.appnexus.com/payment-rule?id=98384"

{
  "response": {
    "status": "OK"
  }
}
```
