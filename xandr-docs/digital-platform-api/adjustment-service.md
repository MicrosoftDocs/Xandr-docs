---
title: Adjustment Service
description: This article explains about the Adjustment service and the types.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Adjustment service

> [!NOTE]
> **This service is currently available to a limited set of clients and Microsoft employees only.**
>
>These docs (and the related feature) are visible to select clients only. Do not send links to these docs or mention this feature to clients unless you've confirmed they should have access.
>
> The Adjustment Service is used to make changes to booked revenue and media cost values in reporting.

## Adjustment types

You can currently make three types of reporting adjustments:

### Advertiser adjustments

- `advertiser_revenue` - This adjustment type changes the booked revenue and/or impressions, clicks, and conversions you see in reporting for an advertiser **and** adjusts your media cost payout to revshare publishers. See the first [example](#examples) below for more details about how payout to revshare publishers is adjusted.
- `advertiser_credit` - This adjustment type changes the booked revenue and/or impressions, clicks, and conversions you see in reporting for an advertiser. It does **not** adjust your media cost payout to revshare publishers.

### Publisher adjustments

`"publisher"` - This adjustment type changes the media cost and/or impressions, clicks, and conversions you see in reporting for a publisher.

## Adjustment status

Adjustments are applied asynchronously to reporting and will appear several hours from the time they are created. The Adjustment Service provides an interface to check the current status of an adjustment.

> [!NOTE]
> In order for Adjustments to be processed the associated objects must be active. For example, if a line item is inactive the associated adjustment jobs will not be executed.

Status can be one of the following values:

| Status | Description |
|:---|:---|
| `new` | Adjustment has been entered into the system. |
| `pending` | Adjustment has been picked up for processing. |
| `processing` | Adjustment is being processed. |
| `propagating` | Adjustment is complete and is propagating to reporting caches. |
| `completed` | Adjustment is complete and should be available in reporting. |
| `failed` | Error while processing adjustment. |
| `cancelled` | User cancelled adjustment. |

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/adjustment` | To add a new adjustment |
| `PUT` | `https://api.appnexus.com/adjustment?id=ADJUSTMENT_ID` | To modify or cancel an existing adjustment: |
| `GET` | `https://api.appnexus.com/adjustment` | To view all adjustments: |
| `GET` | `https://api.appnexus.com/adjustment?advertiser_id=ADVERTISER_ID` | To view all adjustments for an advertiser: |
| `GET` | `https://api.appnexus.com/adjustment?id=ADJUSTMENT_ID` | To view a specific adjustment: |
| `GET` | `https://api.appnexus.com/adjustment?state=new,processing,propagating,pending,completed,failed,cancelled` | To view all adjustments in a given state: |
| `GET` | `https://api.appnexus.com/adjustment?like_start_date=START_DATE&like_end_date=END_DATE` | To view all adjustments within a given time period: |

## JSON fields

### General

| Field | Type | Description |
|:---|:---|:---|
| `adjustment_type` | enum | **Default**: `"advertiser_revenue"`<br><br>The type of adjustment. Possible values:<br> - `"advertiser_revenue"` - Adjusts the amount of revenue from the advertiser to the network and also re-attributes revshare payouts to publishers.<br> - `"advertiser_credit"` - Changes only the amount of revenue from the advertiser but does not re-attribute publisher payouts.<br> - `"publisher"` - Adjusts the media cost paid by the network to the publisher. |
| `created_on` | datetime | The date and time when the adjustment request was created. |
| `end_date` | datetime | **Default**: `Yesterday` <br><br> The end date for the adjustment period. This must be at least 24 hours in the past. |
| `id` | int | **Default**: Auto-incremented number (i.e. 123)<br><br>**Required On**: `PUT`, in query string.<br><br> The unique identifier for the adjustment. |
| `last_modified` | datetime | The date and time when the adjustment request was last modified. |
| `member_id` | int | The ID of the member who owns the adjustment. |
| `notes` | string | Optional note to associate with this adjustment. |
| `start_date` | datetime | **Required On**: `POST` <br><br> The start date for the adjustment. Adjustments will be applied evenly over the time range defined by `start_date` and `end_date`.<br><br>Adjustments are only eligible for processing if they have a `start_date` within 90 days from the time the adjustment is attempted to be executed. |
| `status` | enum | **Default**: `"new"` <br><br> The current processing state for the adjustment. Possible values: <br> - `"new"` <br> - `"processing"` <br> - `"propagating"` <br> - `"pending"` <br> - `"completed"` <br> - `"failed"` <br> - `"cancelled"`. |
| `timezone` | string | **Default**: Default member timezone <br><br>The timezone the adjustment will be made in. Adjustments will be made to the first hour of the day of the given timezone. For a list of acceptable timezone values, see [API Timezones](./api-timezones.md). |
| `user_id` | int | The ID of the user who made the adjustment. |

### Advertiser adjustments

| Field | Type | Description |
|:---|:---|:---|
| `booked_revenue` | double | The new booked revenue paid by the advertiser to the network over the given adjustment period (`start_date` to `end_date`). If set to `null` or left blank, booked revenue will not be changed. |
| `clicks` | int | Optional value for number of clicks over the adjustment period. Note that changing the number of clicks on a CPC line item will *not* affect the line item's booked revenue. If set to `null` or left blank, clicks will not be changed. |
| `delete_overlapping_adjustments` | boolean | **Default**: `true`, if `adjustment_type` is `"advertiser_revenue"` <br><br>If `true`, any prior adjustments to the same line item within the start/end date of the current adjustment will be deleted before the adjustment is applied. |
| `imps` | int | Optional value for number of impressions over the adjustment period. Note that changing the number of imps on a CPM line item will not affect the line item's booked revenue. To change the payment from advertiser to the network, you need to set `booked_revenue` separately. If set to `null` or left blank, imps will not be changed. |
| `line_item_id` | int | **Required On**: `POST`, if `adjustment_type` is `"advertiser_revenue"` or `"advertiser_credit"`.<br><br> The ID of the line item to be adjusted. |
|`post_click_convs` | int | Optional value for number of post click conversions over the adjustment period. Note that changing the number of post click conversions on a CPA line item will not affect the line item's booked revenue. If set to `null` or left blank, post click conversions will not be changed. |
| `post_view_convs` | int | Optional value for number of post view conversions over the adjustment period. Note that changing the number of post view conversions on a CPA line item will not affect the line item's booked revenue. If set to `null` or left blank, post view conversions will not be changed. |

### Publisher adjustments

| Field | Type | Described |
|:---|:---|:---|
| `clicks` | int | Optional value for number of clicks over the adjustment period. |
| `country` | string | The two-letter code for the country or region for which impression data will be adjusted. |
| `height` | int | The height of placements for which data will be adjusted. |
| `imp_types` | string | **Default**: `"kept"`<br><br>The types of impressions for which data will be adjusted. Possible values:<br> - `"default"`: A default creative served because no campaigns bid or no other creative was eligible.<br> - `"kept"`: One of your managed advertisers served a creative.<br> - `"resold"`: The impression was sold to a third-party buyer. |
| `imps` | int | Optional value for the number of impressions over the adjustment period. |
| `media_cost` | money | The new media cost paid by the network to the publisher over the given adjustment period (`start_date` to `end_date`). If set to `null` or left blank, media cost will not be changed. |
| `media_type` | object | The type of media for which data will be adjusted. Possible values: <br> - `"banner"` <br> - `"pop"` <br> - `"text"` <br> - `"interstitial"` <br> - `"expandable"` <br> - `"video"`. |
| `placement_id` | int | **Required On**: `POST`, if `adjustment_type` is `"publisher"`. <br><br>The ID of the placement for which data will be adjusted. |
| `post_click_convs` | int | Optional value for number of post click conversions over the adjustment period. |
| `post_view_convs` | int | Optional value for number of post view conversions over the adjustment period. |
| `publisher_id` | int | The ID of the publisher for which data will be adjusted. |
| `site_id` | int | The ID of the site for which data will be adjusted. |
| `width` | int | The width of placements for which data will be adjusted. |

## Examples

#### Adjusting advertiser revenue and impression count with attribution to publishers

For `"advertiser_revenue"` adjustments, attribution of booked revenue adjustments to revshare publishers is done proportionally based on the number of impressions served by a publisher.

> [!NOTE]
> - Advertiser runs a $1 CPM Line Item.
> - Xandr records 10,000 impressions and $10 booked revenue for this line item, served across 3 publishers.
> - Advertiser records 9,000 impressions and offers to pay $9.

*Report before adjustment*

| Advertiser Line Item | Publisher | Payment Rule | Impressions | Booked Revenue | Media Cost |
|:---|:---|:---|:---|:---|:---|
| $1 CPM Line Item | Publisher 1 | 60% Revshare Payment Rule | 1,000 | $1.00 | $0.60 |
| $1 CPM Line Item | Publisher 2 | 60% Revshare Payment Rule | 5,000 | $5.00 | $3.00 |
| $1 CPM Line Item | Publisher 3 | $0.50 CPM Payment Rule | 1,000 | $1.00 | $0.50 |
| $1 CPM Line Item | Publisher 4 | 70% Revshare Payment Rule | 3,000 | $3.00 | $2.10 |

To adjust revenue down to $9 and impressions to 9,000 for the line item, you create and `POST` the following JSON-formatted file:

```
$ cat adjustment
  
{
   "adjustment": {
      "adjustment_type": "advertiser_revenue",
      "line_item_id": 4243,
      "booked_revenue": 9.00,
      "imps": 9000
      "start_date": "2011-01-01 00:00:00",
      "end_date": "2011-01-01 23:59:59",
      "note": "This is a note..."
   }
}
  
$ curl -b cookies -c cookies -X POST -d @adjustment 'https://api.appnexus.com/adjustment'
```

*Report after adjustment*

| Advertiser Line Item | Publisher | Payment Rule | Adjusted Impressions | Adjusted Booked Revenue | Adjusted Media Cost |
|:---|:---|:---|:---|:---|:---|
| $1 CPM Line Item | Publisher 1 | 60% Revshare Payment Rule | 1,000 | $0.90 | $0.54 |
| $1 CPM Line Item | Publisher 2 | 60% Revshare Payment Rule | 5,000 | $4.50 | $2.70 |
| $1 CPM Line Item | Publisher 2 | $0.50 CPM Payment Rule | 1,000 | $0.90 | $0.50 |
| $1 CPM Line Item | Publisher 3 | 70% Revshare Payment Rule | 3,000 | $2.70 | $1.89 |
| $1 CPM Line Item | - | - | -1,000 | $0.00 | $0.00 |

> [!NOTE]
> - We insert an additional row for changes to impression, click, or conversion counts. This row will appear in network reporting when grouping by Publisher. However, this row will not appear in reports run by Advertisers because they cannot group by Publisher.
>
> - Media cost is *not* adjusted for publishers paid on a cpm basis, or to payments to other platform members.

#### Adjusting advertising revenue and impression, click, and conversion count without attribution to publishers

```
$ cat adjustment
  
{
   "adjustment": {
      "adjustment_type": "advertiser_credit",
      "line_item_id": 4321,
      "booked_revenue": 100.00,
      "imps": 10000,
      "clicks": 10,
      "conversions": 1,
      "start_date": "2011-01-01 00:00:00",
      "end_date": "2011-01-01 23:59:59",
      "note": "This is a note..."
   }
}
```

#### Adjusting publisher media cost and impression count for placements served with creatives

*Report before adjustment*

| Publisher | Site | Placement | Payment Rule | Country/Region | Size | Media Type | Payment Type | Media Cost | Imps |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| NY Post | Business | Home Page | $1 CPM | US | 728x90 | Banner | Owner CPM | 1 | 1000 |
| NY Post | Business | Home Page | $1 CPM | CA | 728x90 | Banner | Owner CPM | 0.5 | 500 |
| NY Post | Business | Home Page Pop | $10 CPM | US | 0x0 | Popup | Owner CPM | 10 | 1000 |
| NY Post | Business | Home Page | $2 CPM | US | 300x250 | Banner | Owner CPM | 2 | 1000 |
| NY Post | Business | Home Page | 60% Revshare | GB | 300x250 | Banner | Owner Revshare | 1.25 | 500 |

To adjust media cost down to $10 and impressions to 3500, you create and `POST` the following JSON-formatted file:

```
$ cat adjustment
  
{
   "adjustment": {
      "adjustment_type": "publisher",
      "publisher_id": 23,
      "media_cost": 10.00,
      "imps": 3500,
      "start_date": "2011-01-01 00:00:00",
      "end_date": "2011-01-01 23:59:59",
      "note": "This is a note...",
      "imp_types": [
         "resold"
      ]
   }
}
  
$ curl -b cookies -c cookies -X POST -d @adjustment 'https://api.appnexus.com/adjustment'
```

*Report after adjustment*

| Adjustment ID | Publisher | Site | Placement | Payment Rule | Country/Region | Size | Media Type | Payment Type | Media Cost | Imps |
|:---|:---|:---|*:---|:---|:---|:---|:---|:---|:---|:---|
| 0 | NY Post | Business | Home Page | $1 CPM | US | 728x90 | Banner | Owner CPM | 1 | 1000 |
| 1 | NY Post | Business | Home Page | $1 CPM | US | 728x90 | Banner | Owner CPM | -0.322033898305085 | -125 |
| 0 | NY Post | Business | Home Page | $1 CPM | CA | 728x90 | Banner | Owner CPM | 0.5 | 500 |
| 1 | NY Post | Business | Home Page | $1 CPM | CA | 728x90 | Banner | Owner CPM | -0.161016949152542 | -62.5 |
| 0 | NY Post | Business | Home Page Pop | $10 CPM | US | 0x0 | Popup | Owner CPM | 10 | 1000 |
| 1 | NY Post | Business | Home Page Pop | $10 CPM | US | 0x0 | Popup | Owner CPM | 3.22033898305085 | -125 |
| 0 | NY Post | Business | Home Page | $2 CPM | US | 300x250 | Banner | Owner CPM | 2 | 1000 |
| 1 | NY Post | Business | Home Page | $2 CPM | US | 300x250 | Banner | Owner CPM | -0.64406779661017 | -125 |
| 0 | NY Post | Business | Home Page | 60% Revshare | GB | 300x250 | Banner | Owner Revshare | 1.25 | 500 |
| 1 | NY Post | Business | Home Page | 60% Revshare | GB | 300x250 | Banner | Owner Revshare | -0.402542372881356 | -62.5 |

### Canceling an adjustment

You can cancel adjustments that have the status `"new"` or `"pending"`.

```
$ cat modify_adjustment
  
{
   "adjustment": {
      "id": 5,
      "status": "cancelled"
   }
}
  
$ curl -b cookies -c cookies -X PUT -d @modify_adjustment 'https://api.appnexus.com/adjustment'
```

### Viewing all adjustments

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/adjustment'
  
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "adjustments": [
            {
                "id": 5,
                "member_id": 294,
                "line_item_id": 2725,
                "timezone": "EST5EDT",
                "start_date": "2011-03-02 00:00:00",
                "end_date": "2011-03-04 23:59:59",
                "status": "completed",
                "adjustment_type": "advertiser_revenue",
                "booked_revenue": 100,
                "imps": 2000,
                "clicks": null,
                "post_click_convs": null,
                "post_view_convs": null,
                "notes": null,
                "created_on": "0000-00-00 00:00:00",
                "last_modified": "2011-03-15 17:56:40",
                "publisher_id": null,
                "site_id": null,
                "placement_id": null,
                "payment_rule_id": null,
                "width": null,
                "height": null,
                "country": null,
                "imp_type_kept": false,
                "imp_type_resold": false,
                "imp_type_default": false,
                "media_cost": null,
                "delete_overlapping_adjustments": false,
                "media_type": null,
                "user": null,
                "imp_types": null
            },
            {
                "id": 6,
                "member_id": 294,
                "line_item_id": 2725,
                "timezone": "EST5EDT",
                "start_date": "2011-03-02 00:00:00",
                "end_date": "2011-03-04 23:59:59",
                "status": "completed",
                "adjustment_type": "advertiser_revenue",
                "booked_revenue": 200,
                "imps": 1000,
                "clicks": null,
                "post_click_convs": null,
                "post_view_convs": null,
                "notes": null,
                "created_on": "0000-00-00 00:00:00",
                "last_modified": "2011-03-16 22:56:29",
                "publisher_id": null,
                "site_id": null,
                "placement_id": null,
                "payment_rule_id": null,
                "width": null,
                "height": null,
                "country": null,
                "imp_type_kept": false,
                "imp_type_resold": false,
                "imp_type_default": false,
                "media_cost": null,
                "delete_overlapping_adjustments": false,
                "media_type": null,
                "user": null,
                "imp_types": null
            },
            ...
        ]
    }
}
```
