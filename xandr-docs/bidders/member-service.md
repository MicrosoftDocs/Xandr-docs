---
title: Bidders - Member Service
description: In this article, learn about bidders member service, their members and contracts, JSON fields, and REST API with a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Member service

> [!NOTE]
> Members are integrated into Xandr's system and managed via the Member Service.

Any entity that has a financial relationship with Xandr's platform (usually a buyer or seller) needs to be added to Xandr's system as a "member" before they can conduct transactions. Members can be registered with the Member Service either by a bidder or by Xandr personnel.

## Members and contracts

Before they can buy or sell ads, a member needs a contract with Xandr. This contract will establish financial terms and credit facilities (if applicable), and bind the member to the terms and conditions of Xandr, such as content quality and use of personally identifiable information. Any bidder can create a member at any time, but members will not be able to place bids until their contract has been approved.

> [!NOTE]
>
> - If you are looking for information about other platform members use the [Platform Member Service](member-service.md).
> - In bidder sandbox environments, all functionality of the Member Service is available.
> - The Member Service does not grant API access. That is done via the [User Service](user-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/member](https://api.adnxs.com/member) | To see all your members. |
| `GET` | [https://api.adnxs.com/member/MEMBER_ID](https://api.adnxs.com/member/MEMBER_ID) | To see a particular member. |

> [!NOTE]
> The calls below are visible to Xandr employees only. They can be made by users with the "admin" `user_type`.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.adnxs.com/member](https://api.adnxs.com/member) | To add a new member. |
| `PUT` | [https://api.adnxs.com/member/MEMBER_ID](https://api.adnxs.com/member/MEMBER_ID) | To modify an existing member. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `active` | Boolean | Whether the member can provide and/or bid for inventory. |
| `agent_id` | string | Used for inventory aggregator members. |
| `allow_ad_profile_override` |  | This field is not currently used. |
| `audit_notify_email` | string | Each time Xandr audits a creative belonging to this member, a detailed response is sent to this email address. The response includes the creative's audit status and any reasons why the creative has not passed audit. This field supports multiple comma-separated email addresses. |
| `bidder_id` | int | The bidder that manages bidding for the member. Can be blank for members that only sell inventory. |
| `billing_address_1` | string(255) | The first line of the member's address. |
| `billing_address_2` | string(255) | The second line of the member's address. |
| `billing_city` | string(100) | The city of the member's address. |
| `billing_country` | string(50) | The country of the member. |
| `billing_name` | string(100) | The billing name (who to write checks to).<br>**Required On:** `POST`. |
| `billing_postal_code` | string(50) | The postal code for the member's address. |
| `billing_region` | string | The region of the member's address. |
| `buyer_clearing_fee_pct` | double | The percent of the CPM paid for inventory charged as a fee. |
| `buyer_credit_limit` | double | The credit limit for this member when buying inventory through Xandr. Read-only. |
| `code` | string(100) | Optional way to add an internal identification. |
| `contact_email` |  | This field is not currently used. |
| `default_ad_profile_id` | int | If you want to set an ad profile for all TinyTags belonging to a member. |
| `default_tag_id` | int | The ID of the creative to serve in the case where tags are being called using unknown codes. |
| `dongle` | string | A password that can be passed into a debug auction (as the "dongle" parameter) that will allow a member access to relevant debug output from their bidder. |
| `email_code` | string(50) | Email code is a unique value used when TinyTags are processed via our email tag processing tool. Must be an alphanumeric value. |
| `id` | int | The ID of the member.<br>**Required On:** `PUT`. |
| `last_activity` | timestamp | The timestamp of last modification to this bidder instance. |
| `platform_exposure` |  | See below for details.  |
| `price_buckets` | array | When using Preemptive Tags, a selling member may require Price Bucket for 3rd party ad server pricing. Depending on the kind of integration a 3rd party adserver requires, the values might be `[{"price_bucket": 10}, {"price_bucket": 20}. . . ]` <br>or<br> `[{"price_bucket": 10, "width": 300, "height":200", "pixel_url": "https://..."}, . . . ]`. |
| `prioritize_margin` | Boolean | If set to `"true"`, Xandr will perform a bid/no bid check for managed campaigns based on line item minimum margin settings.  <br> <br>If set to `"false"`, Xandr will not not perform any bid/no bid check for managed campaigns based on the line item minimum. |
| `seller_revshare_pct` | double | Read-only for bidder-users and members.<br>Percentage amount that Xandr takes out of seller revenue. |
| `serving_domain` | array of strings | Used when generating tags for selling members. (i.e. `mycompany.adnxs.com` instead `ib.adnxs.com`). <br>`"serving_domain": {"cname": null,"type": null}`<br> Read only. |
| `sherlock_notify_email` | string | Each time Sherlock, our automated creative scanning system, scans a creative belonging to this member, a response is sent to this email address. The response includes the creative's audit status and any reasons why the creative has not passed audit. For more information, see [Sherlock](../monetize/sherlock-creative-quality-control.md). <br>This field supports multiple comma-separated email addresses. |
| `timezone` | string | The member timezone is the default timezone for your reports. <br>For possible values, see [Reporting Timezones](reporting-timezones.md). <br>Default is `"EST5EDT"`.   |

### Platform exposure

The platform exposure setting determines how your account is displayed to other members on the platform. There are three values which result in slightly different behaviors as outlined below:

| Platform Exposure Value | Behavior |
|:---|:---|
| `hidden` | Member is not displayed.<br><br>**Note:** Setting `platform_exposure` to `"hidden"` will hide your member `"name"` and `"domain"` fields in our [sellers.json](https://xandr.com/sellers.json) file and list your member seat as `"is_confidential": 1`. For example, see [`hidden` example](#hidden-example).<br>This can limit the monetization of your inventory as some DSPs may not choose to buy impressions from sellers who are not transparent in the `"schain"` object. |
| `private` | Member is displayed as "Member 123" where 123 is the member ID. |
| `public` | Member is displayed using the billing name.<br><br>**Note:** Setting `platform_exposure` to `"public"` will display your member `"name"` and `"domain"` fields in our [sellers.json](https://xandr.com/sellers.json) file. For example, see [`public` example](#public-example). |

#### `hidden` example

```

{
  "seller_id": "8253",
  "is_confidential": 1,
  "seller_type": "PUBLISHER"
}

```

#### `public` example

```

{
  "seller_id": "7694",
  "seller_type": "INTERMEDIARY",
  "domain": "groupm.com",
  "name": "Xaxis – Slovakia Marketplace"
}

```

The sample JSON below shows how to set this parameter.

```
{
  "member": {
    "platform_exposure": "public"
  }
}
```

## Authentication token

Authentication is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use. For more detailed instructions, see [Authentication Service](authentication-service.md).

## Examples

### Create a JSON-formatted file describing the member

The only required fields are `billing_name` and `bidder_id` if the member is associated with a bidder, but since a member has a financial relationship with Xandr, you will probably want to include other billing-related information.

```
$ cat member
{
        "member" : {
                "active" : true,
                "billing_name" : "My Company",
                "bidder_id" : 2,
                "billing_address_1" : "One Coke Way",
                "billing_city" : "Atlanta",
                "billing_region" : "GA",
                "billing_country" : "US",
        "email_code" : "cola"
        }
}
```

### Add the member file to the impression bus cache

```
$ curl -b cookies -c cookies -X POST --data-binary @member 'https://api.adnxs.com/member'
{
        "response":{
                "status":"OK","id":1
        }
}
```

### Now modify the member via a modified JSON-formatted file

```
$ cat member_mod
{
        "member" : {
                "active" : true,
                "billing_name" : "My Company",
                "bidder_id" : 2,
                "billing_address_1" : "Building 5",
                "billing_address_2" : "Company Complex",
                "billing_city" : "Atlanta",
                "billing_region" : "GA",
                "billing_country" : "US",
                "billing_postal_code" : "33608"
        }
}
```

### Update the member information in the impression bus cache, using the member ID

```
$ curl -b cookies -c cookies-X PUT --data-binary @member_mod 'https://api.adnxs.com/member/1'
{
        "response":{
                "status":"OK"
        }
}
```

### View information about the member

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/member/1'
{
   "response":{
      "status":"OK",
      "member": {
        "id": 334,
        "agent_id": null,
        "code": null,
        "active": true,
        "buyer_credit_limit": 0,
        "billing_name" : "My Company",
                "bidder_id" : 2,
                "billing_address_1" : "Building 5",
                "billing_address_2" : "Company Complex",
                "billing_city" : "Atlanta",
                "billing_region" : "GA",
                "billing_country" : "US",
                "billing_postal_code" : "33608"
        "email_code": "cola",
        "seller_revshare_pct": 95,
        "price_buckets": [
        ],
        "default_tag_id": null,
        "default_ad_profile_id": 251,
        "buyer_clearing_fee_pct": null,
        "serving_domain": {
          "cname": null,
          "type": null
        },
        "last_activity": "2010-04-08 03:38:16",
        "timezone": "EST5EDT"
      }
   }
}
```
