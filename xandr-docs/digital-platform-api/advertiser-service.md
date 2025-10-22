---
title: Advertiser Service
description: Networks can use the advertiser service to add, modify, and view the advertisers that interact with Xandr.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Advertiser service

The Advertiser service lets networks add, modify, and view the advertisers that interact with Xandr. Direct marketers rarely use the Advertiser service because they have only one advertiser (themselves).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/advertiser` | View all of your advertisers. |
| `GET` | `https://api.appnexus.com/advertiser?id=ADVERTISER_ID` | View a specific advertiser. |
| `GET` | `https://api.appnexus.com/advertiser?code=ADVERTISER_CODE` | View a specific advertiser. |
| `GET` | `https://api.appnexus.com/advertiser?id=1,2,3` | View multiple advertisers by ID using a comma-separated list. |
| `GET` | `https://api.appnexus.com/advertiser?search=SEARCH_TERM` | Search for advertisers with IDs or names containing certain characters. |
| `GET` | `https://api.appnexus.com/advertiser/meta` | Find out which fields you can filter and sort by. |
| `POST` | `https://api.appnexus.com/advertiser` | Add a new advertiser. |
| `PUT` | `https://api.appnexus.com/advertiser?id=ADVERTISER_ID` | Modify an existing advertiser. |
| `PUT` | `https://api.appnexus.com/advertiser?code=ADVERTISER_CODE` | Modify an existing advertiser. |
| `DELETE` | `https://api.appnexus.com/advertiser?id=ADVERTISER_ID` | Delete an advertiser.<br><br>**Note**:<br>Deleting an advertiser will delete all of its child insertion orders, line items, campaigns, creatives, conversion pixels, and segments. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings, such as revenue budget for line items, cost budget, and targeting for campaigns. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `allow_safety_pacing` | boolean | **Admin-only**. If `true`, spend per minute is limited to a maximum of 1% of the lifetime budget and 5% of the daily budget. |
| `audience_size_check_state` | enum | The state of the audience size validation check. We use an external service provided by Yield Analytics to confirm that the audience size meets our criteria for the Netflix Deal Defined Line Item targeting.<br>Possible values:<br>- `passed`<br>- `failed`<br>- `in_progress`<br>- `unchecked`<br><br>**Note:** This field is visible only for the Netflix Deal Defined Line Item. |
| `audience_size_check_last_run` | timestamp | Timestamp of the last time the audience size validation check was done, which is when the status changed to `passed` or `failed`.<br><br>**Note:** This field is visible only for the Netflix Deal Defined Line Item. |
| `billing_address1` | string (100) | For reference. |
| `billing_address2` | string (100) | For reference. |
| `billing_city` | string (100) | For reference. |
| `billing_country` | string (100) | For reference. |
| `billing_internal_user` | array | For reference. This is a list of people (strings) who work at this advertiser. |
| `billing_name` | string (50) | For reference. Value may be a maximum of 50 characters. |
| `billing_phone` | string (20) | For reference. |
| `billing_state` | string (100) | For reference. |
| `billing_zip` | string (25) | For reference. |
| `code` | string (100) | A custom code for the advertiser. Xandr will assign a unique ID, but advertisers may use their own ID system. Either `"code"` or the Xandr-assigned ID will be allowed fields in other services. |
| `legal_entity_name` | string (255) | Represents the legal entity on whose behalf the advertisement is being displayed and who is covering the cost of the advertiser's ad. This field is used in bid responses in order to comply with the European Union [Digital Services Act (DSA)](../invest/digital-services-act.md). |
| `competitive_brands` | array | An array of brand IDs. Creatives associated with the brands in this array will not serve together in `/mtj` auctions. The classic example of competing brands is Coke vs. Pepsi. For more information about the brands in our system, see the [Brand Service](./brand-service.md).|
| `competitive_categories` | array | An array of category IDs. Creatives associated with the categories in this array will not serve together in `/mtj` auctions, e.g., `"Dating"` and `"Education"`. For more information about the categories that we apply to creatives (and brands), see the [Category Service](./category-service.md). |
| `control_pct` | double | The percentage of users in the control group for this advertiser. This must be expressed as a number between `0` and `1`, inclusive. These users will be shown a control creative in order to gauge effectiveness of other creatives. For more information, see [Test and Control Targeting (Standard Line Item)](../monetize/test-and-control-targeting.md) in the UI documentation. |
| `daily_budget` | double | The daily budget for the advertiser. (See `lifetime_budget` below.) |
| `daily_budget_imps` | int | The daily impression budget for the advertiser. (See `lifetime_budget` below.) |
| `default_brand` | object | Information about the default brand. See [Default Brand](#default-brand) below for more details.<br><br>**Default**: `null` |
| `default_brand_id` | int | The internal ID of the default brand for all creatives of this advertiser. The brand for each creative will be checked during the auditing process. |
| `default_category` | object | This feature is not functioning at this time. It will be used in future development. |
| `default_currency` | string (3) | The default currency to be used for the advertiser. This will be a three-letter code that you can retrieve from the read-only [Currency Service](./currency-service.md). See [Currency Support](../monetize/currency-support.md) in the UI documentation for details about the concept.<br><br>**Note**: As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience.<br><br>**Default**: Member's default currency |
| `enable_pacing` | boolean | If `true`, then spending will be paced for this advertiser over the course of the day. |
| `enable_political_io_by_default` | boolean | Possible values: `0` or `1`.<br><br>If set to `true`, insertion orders created for this advertiser using the UI will have political advertising enabled by default. This does not affect insertion orders created using the API.<br><br>**Default**: `1` (true) |
| `id` | int | The ID of the Advertiser.<br><br>**Read Only**<br>**Required On**: `PUT`<br>**Default**: auto-incremented number |
| `is_malicious` | boolean | **Admin-only**. If `true`, the advertiser's status will be set to inactive. Xandr administrators will set this field to `true` for advertisers determined to be directing users to malicious landing pages. Users will not be able to set the advertiser's status back to active until a Xandr administrator sets the `is_malicious` field back to `false`.<br><br>**Default**: `false` |
| `is_mediated` | boolean | **Admin-only**. If `true`, the advertiser will not be displayed in the UI. Xandr administrators can set this field to `true` when the Advertiser is associated with a mediated bid.<br><br>**Default**: `false` |
| `is_running_political_ads` | boolean | Possible values: `0` or `1`.<br><br>Declares whether or not this advertiser conducts political advertising (defined as advertising related to an election, ballot initiative, or political candidate, in the United States).<br>If an existing advertiser already has insertion orders with political advertising enabled, you will not be able to set `is_running_political_ads` to `false`.<br><br>**Default**: `0` (false) |
| `labels` | array | The optional labels applied to the advertiser. Currently, three labels are available for advertisers: <br> - `"Salesperson"` <br> - `"Account Manager"` <br> - `"Advertiser Type"`. See [Labels](#labels) below for more details.<br><br>**Note**: You can report on advertiser labels with the [Network Analytics](./network-analytics.md) report. For example, if you use the "Salesperson" label to specify the name of the salesperson responsible for each advertiser, you can run the Network Analytics report filtered by `"salesperson_for_advertiser"` to focus on the advertisers that a particular salesperson is responsible for or grouped by `"salesperson_for_advertiser"` to rank the performance of your salespeople. |
| `last_modified` | timestamp | Timestamp of the last time this advertiser was modified. |
| `lifetime_budget` | double | You can set all of the budget parameters at the advertiser level as well as the campaign and media buy levels. Budgets at the advertiser level will apply to all traffic for your advertiser. This is a dollar (media cost) budget. |
| `lifetime_budget_imps` | int | The lifetime impression budget for the advertiser. (See `lifetime_budget` above.) |
| `name` | string (255) | The name of the advertiser.<br><br>**Required On**: `POST` |
| `object_stats` | object | The number of total, active, and inactive insertion orders, line items, campaigns, and creatives under the advertiser, as well as the number of creatives with particular audit statuses. To include this object in a `GET` response, pass `object_stats=true` in the query string.<br><br>**Read Only**. |
| `partner_fees` | array | An array of partner fees applied to this advertiser. You can create, attach, view, or remove partner fees with the [Partner Fee Service](./partner-fee-service.md). |
| `profile_id` | int | You can set an optional `profile_id` at the advertiser, line item, campaign and creative levels. A profile is a generic set of rules for targeting inventory. A profile set at the advertiser level will apply to all traffic for your advertiser, so you will probably want to keep this profile very broad. Ad calls must pass all profile targeting at any level. See the [Profile Service](./profile-service.md) for details. |
| `remarketing_segment_id` | int | A segment is marked as "remarketing" for reporting and filtering purposes only. If you mark a segment as remarketing in the UI, it will show up here. Or you can add segment IDs here, and they will be marked as remarketing for reporting purposes. |
| `state` | enum | The state of the advertiser. Possible values: `"active"` or `"inactive"`.<br><br>**Default**: `"active"` |
| `stats` | object | The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](./report-service.md) to obtain statistical information instead. |
| `timezone` | enum | The timezone of the advertiser. See [API Timezones](./api-timezones.md) for details and accepted values. For details on how to make the advertiser timezone "trickle down" to child objects, see [Timezone for Dependent Objects](#timezone-for-dependent-objects) below.<br><br>**Default**: `"EST5EDT"`, or the member's timezone. |
| `thirdparty_pixels` | array | An array of third-party pixels associated with the advertiser. You can automatically attach these pixels to all creatives owned by this advertiser using the [Third-party Pixel service](./third-party-pixel-service.md) or attach them individually at the creative level using the [Creative Service](./creative-service.md).<br><br>**Read Only**.<br>**Default**: `null` |
| `time_format` | enum | The format in which you would like to see times displayed in the UI. Possible values: `"12-hour"` or `"24-hour"`.<br><br>**Default**: `"12-hour"` |
| `use_insertion_orders` | boolean | If `true`, the use of insertion orders which contain collections of line items, will be enabled for this advertiser. You will not be able to create insertion orders, if this field is set to `"false"`. See the [Insertion Order Service](./insertion-order-service.md) for details.<br><br>**CAUTION**:<br>**Pre-existing line items**<br>If you set this field to `true` and have already created line items prior to enabling this setting, those line items will stop spending. To allow those line items to continue spending, create an insertion order (using the [Insertion Order Service](./insertion-order-service.md)) and associate the line items with the insertion order (using the [Line Item Service](./line-item-service.md)). All newly created line items will require an insertion order.<br><br>**Note**:<br>When the advertiser has associated insertion orders, you will not be able to update the value of `"use_insertion_orders"` to `false`.<br><br>**Default**: `true` |

### Third-party pixels

The `thirdparty_pixels` array contains fields in the table below. These fields are read-only. To update or create third-party pixels and/or attach third-party pixels to all creatives owned by the advertiser, use the [Third-party Pixel service](./third-party-pixel-service.md). To attach third-party pixels to individual creatives, use the [Creative Service](./creative-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `active` | boolean | The current status of the pixel (`true = active`).<br>**Read Only**. |
| `audit_statu`s | string | Audit status of the pixel.<br>**Read Only**. |
| `id` | int | The pixel's ID.<br>**Read Only**. |
| `name` | string | The full name of the pixel.<br>**Read Only**. |

### Stats

The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](./report-service.md) to obtain statistical information instead.

### Labels

You can use the read-only [Label Service](./label-service.md) to view all possible labels for advertisers, insertion orders, line items, campaigns, and publishers. This service allows you to view the labels that is already applied to your objects.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the label. Possible values: <br>`1` (Salesperson) <br>`3` (Account Manager) <br>`12` (Advertiser Type). |
| `name` | enum | The name of the label. Possible values: <br> - `"Salesperson"` <br> - `"Account Manager"` <br> - `"Advertiser Type"`.<br>**Read Only**. |
| `value` | string (100) | The value assigned to the label. For example, for the `"Salesperson"` label, this could be a name such as `"Michael Sellers"`. |

### Pagination

You can request a certain number of objects through these fields:

```
"count": 8,
    "start_element": null,
    "num_elements": null
```

| Field | Type | Description |
|:---|:---|:---|
| `count` | int | How many objects are in this service? For example, 8 advertisers. |
| `num_elements` | int | How many elements to return? For example, start at object # 4 and return 3 objects, or # 4, 5, 6. |
| `start_element` | int | The number at which to start counting. |

### Default brand

| Field | Type | Description |
|:---|:---|:---|
| `category_id` | int | The ID of the brand's category. |
| `id` | int | The brand's ID. |
| `name` | string | The name of the brand. |

### Timezone for dependent objects

When you change an advertiser's timezone, you can choose whether or not to make the change "trickle down" to child objects (campaigns, line items, and creatives). To do this, you should pass `set_child_timezone=true` in the query string of the URL during your request to create or update the timezone.

For example:

```
$ curl -b cookies -X PUT -d @advertiser 'https://api.appnexus.com
/advertiser?id=111&set_child_timezone=true'
```

- If `true`, then timezone on all child objects is set to the Advertiser's timezone. Note that any timezone settings on lower-level objects (e.g., Insertion orders, Line Items, Campaigns) will be overridden with the Advertiser's timezone.
- If `false`, timezone is only set on the advertiser.

## Examples

### Add an advertiser

```
$ cat advertiser.json

{
   "advertiser":
   {
      "name":"Advertiser B",
      "legal_entity_name":"Toyota UK",
      "state":"active"
   }
}

$ curl -b cookies -c cookies -X POST --data-binary @advertiser.json 'https://api.appnexus.com/advertiser'

{
   "response":{
      "status":"OK",
      "id":51
   }
}
```

### Update an advertiser

```
$ cat advertiser_update

{
   "advertiser":
   {
      "name":"Advertiser B",
      "legal_entity_name":"Toyota UK",
      "state":"active",
      "code":"PSS"
   }
}

$ curl -b cookies -c cookies -X PUT --data-binary @advertiser_update 'https://api.appnexus.com/advertiser?id=51'

{
   "response":{
      "status":"OK",
      "id":492
   }
}
```

### View all advertisers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/advertiser'

{
  "response": {
    "status": "OK",
    "advertisers": [
      {
        "id": 51,
        "code": null,
        "name": "Advertiser B",
        "legal_entity_name":"Toyota France",
        "state": "active",
        "default_brand_id": 0,
        "remarketing_segment_id": null,
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "enable_pacing": true,
        "profile_id": null,
        "thirdparty_pixels": [
          {
            "id":145,
            "name":"sample pixel",
            "audit_status":"pending",
            "active":true
          },
          {
            "id":314,
            "name":"another sample pixel",
            "audit_status":"pending",
            "active":true
          }
        ],
        "control_pct": 0,
        "timezone": "EST5EDT",
        "last_modified": "2010-08-03 23:07:02",
        "stats": null,
        "billing_internal_user": null,
        "billing_address1": "123 Happy Street",
        "billing_address2": "",
        "billing_city": "New York",
        "billing_state": "NY",
        "billing_country": "US",
        "billing_zip": "10011",
        "default_category": null,
        "default_currency": "USD",
        "labels": null,
        "use_insertion_orders": false,
        "time_format": "12-hour",
        "default_brand": null,
        "is_malicious": false
      },
      {
        "id": 493,
        "code": null,
        "name": "Cheese Club",
        "legal_entity_name":"Toyota Germany",
        "state": "active",
        "default_brand_id": 0,
        "remarketing_segment_id": 11111,
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "enable_pacing": true,
        "profile_id": null,
        "thirdparty_pixels":null,
        "control_pct": 0,
        "timezone": "EST5EDT",
        "last_modified": "2010-09-15 21:02:37",
        "stats": null,
        "billing_internal_user": null,
        "billing_address1": null,
        "billing_address2": null,
        "billing_city": null,
        "billing_state": null,
        "billing_country": null,
        "billing_zip": null,
        "default_category": null,
        "default_currency": "USD",
        "labels": null,
        "use_insertion_orders": false,
        "time_format": "12-hour",
        "default_brand": null,
        "is_malicious": false
      }
    ],
    "count": 5,
    "start_element": null,
    "num_elements": null,
    "dbg_info": {
      ...
    }
  }
}
```

### View a specific advertiser

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/advertiser?id=51'

{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "advertiser":{
            "id":51,
            "code":null,
            "name":"Advertiser A",
            "legal_entity_name":"Toyota UK",
            "state":"active",
            "default_brand_id":0,
            "remarketing_segment_id":null,
            "profile_id":null,
            "control_pct":0,
            "timezone":"EST5EDT",
            "last_modified":"2010-05-06 20:21:56",
            "member_id":79,
            "billing_name":null,
            "billing_phone":null,
            "billing_address1":null,
            "billing_address2":null,
            "billing_city":null,
            "billing_state":null,
            "billing_country":null,
            "billing_zip":null,
            "default_currency":"USD",
            "use_insertion_orders":false,
            "time_format":"12-hour",
            "is_malicious":false,
            "billing_internal_user":null,
            "default_category":null,
            "default_brand":null,
            "labels":null,
            "competitive_brands":null,
            "competitive_categories":null,
            "lifetime_budget":null,
            "lifetime_budget_imps":null,
            "daily_budget":null,
            "daily_budget_imps":null,
            "enable_pacing":null,
            "lifetime_pacing":null,
            "lifetime_pacing_span":null,
            "allow_safety_pacing":null,
            "stats":null
      }
   }
}
```
