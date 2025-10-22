---
title: Member Contract Service
description: Sales operations admins can use the Member Contract service to view, create, update, and delete member contracts.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member Contract service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

There are two types of pricing terms denoted by the `pricing_version` field.

- `"2007.09.01"`: These are the "legacy" pricing terms.
- `"2013.01.02"`: These are the newer pricing terms. Most client contracts negotiated post-2013 will use these new pricing terms. The upshot of the new pricing terms are that clients pay a buy-side fee for both partner and platform inventory, and that clients pay a different seller revshare for buyers on the Xandr platform than for bidder buyers.

> [!NOTE]
> This service is available only to Xandr admin users who have the `is_sales_ops` field set to true. Note that the `is_sales_ops` field can be set to true only via a direct database update. Valid reasons to have your `is_sales_ops` field set in production include:
>
> - You are a member of the Sales Ops team, and it is your regular job to create and update contracts.
> - You are an engineer, product manager, or test engineer who needs access to create or update contracts for your job.
> - You want to see Katharine, Jennifer Yang, and Alison cry. (Yes, really.)
> - If you are in Services and need to create or update contracts in sand, you should request a direct DB write for your sand user but understand that you won't have the same capability in production.
> [!WARNING]
> On a `PUT` call, if you include only specific contracts, the contracts not included will be **deleted**. Therefore it is best to include all contracts on `PUT`.
> [!NOTE]
> Updating and deleting contracts
>
> - The Sales Op can only update the following fields for contracts in progress: `notes` and `end_date`. For past contracts, she can only update the `notes`. For future contracts she can update all the fields.
> - Note that if you clone a contract whose `pricing_type` is `"2007.09.01"`, update `pricing_type` to `"2013.01.02"`, and then update it once more to `"2007.09.01"`, any minimums will be set to zero.
> - The Sales Op can only delete contracts which are in the future.

## REST API

| HTTP Methods | Enpoints | Descriptions |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/member-contract?member_id=MEMBER_ID` | View all contracts for a specific member |
| `GET` | `https://api.appnexus.com/member-contract`<br>(contract JSON) | View a specific contract |
| `POST` | `https://api.appnexus.com/member-contract`<br>(contract JSON) | Add a new contract |
| `PUT` | `https://api.appnexus.com/member-contract?id=CONTRACT_ID` <br>(contract JSON) | Modify a contract |
| `DELETE` | `https://api.appnexus.com/member-contract?id=CONTRACT_ID` | Delete a contract |
| `GET` | `https://api.appnexus.com/member-contract/meta` | Find out which fields you can filter and sort by |

## JSON fields

There is a large intersection between the sets of required fields depending on whether the `pricing_version` is `"2007.09.01"` (marked below as `OLD`) or `"2013.01.02"` (marked below as `NEW`); only those fields that differ between pricing versions are marked as such in the **Old or New?** column.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the contract.<br><br>**Requird On**: `PUT`/`DELETE`, in query string. |
| `member_id` | int | The ID of the member to which the contract applies. |
| `last_activity` | timestamp | The date of the last modification of this contract "object". |
| `start_date` | datetime | The date and time when the terms of the contract start. New contracts should begin in the future, and typically on the first day of a month.<br><br>**Requird On**: `POST` |
| `end_date` | datetime | The date and time when the terms of the contract end. This should always come at the end of a month.<br><br>**Requird On**: `POST` |
| `auction_revshare` | float | This field is not used. |
| `auction_minimum_cpm` | float | This field is not used. Formerly, it was the minimum amount the buyer agrees to pay for Auction Service Fee, Auction Service Deduction, or Direct Clear Fee.<br><br>**Old or New**: `OLD` |
| `ad_serving_cpm` | float | The managed ad serving fee charged on kept impressions (to include: kept, default, PSA). This does not represent a seller ad serving fee CPM, which is not yet implemented in the system. |
| `auditing_fee_per_creative` | float | The per-creative auditing fee. |
| `creative_size_minimum_bytes` | int | The size above which a creative is considered over-sized. The member is charged a creative overage fee (based on the value in `creative_size_fee_per_gb`) for serving an oversized creative. |
| `creative_size_fee_per_gb` | float | The fee that is charged per gigabyte for a creative that exceeds the `creative_size_minimum_bytes`. |
| `monthly_minimum_spend` | float | This field is mislabeled. The monthly minimum fees the member commits to paying per month.<br><br>**Old or New**: `OLD` |
| `clearing_revshare` | float | The flat fee taken out of clearing revenues by Xandr. Members may choose to be billed as a percentage instead (see `clearing_revshare_pct` below). |
| `auction_revshare_pct` | float | The percentage charged to sellers when they sell their inventory to other members.<br><br>**Warning**: This field corresponds to the new `auction_revshare_platform_pct` field, and is used by the data pipeline for calculations involving CPA/CPC revenues. PLEASE DO NOT REMOVE THIS FIELD UNLESS YOU KNOW WHAT YOU ARE DOING.<br><br>**Old or New**: `OLD`<br>**Default**: `"0.00"` |
| `clearing_revshare_pct` | float | The clearing deduction percentage. This is charged when the member buys from an external or partner seller. |
| `auction_maximum_cpm` | float | The maximum amount the buyer agrees to pay on a per-impression basis. For this reason, the sum of client's auction service fees and deductions may not be equal to their total media cost multiplied by their auction revshare at the end of the month. |
| `apply_min_cpm_to_clearing` | boolean | This field is not used.<br><br>**Default**: `False` |
| `auction_revshare_type` | enum | The type of buyer auction revenue share. Allowed values:<br> - `"deduction"`: The buyer is charged an Auction Service Deduction.<br> - `"fee"`: The buyer is charged an Auction Service Fee.<br><br>**Warning**: This field corresponds to the new `auction_revshare_platform_inv_type` field, and is used by the data pipeline for calculations involving CPA/CPC revenues. PLEASE DO NOT REMOVE THIS FIELD UNLESS YOU KNOW WHAT YOU ARE DOING.<br><br>**Default**: - `"fee"`<br>**Old or New**: `OLD` |
| `pricing_version` | enum | The pricing version associated with this contract. With the 2013 pricing terms, clients pay a buy-side fee for both partner and platform inventory, and clients pay a different seller revshare for Xandr platform buyers than for bidder buyers. Note also that it is acceptable to use 2007 pricing terms if so dictated by the contract. Allowed values:<br> - `"2007.09.01"`<br> - `"2013.01.02"`<br><br>**Required On**: `POST` |
| `seller_type` | enum | The type of seller. Allowed values:<br> - `"platform"`: The member has a signed contract allowing Xandr to take a Seller Deduction from resold impressions.<br> - `"partner"`: The member does not have a signed contract allowing Xandr to take a Seller Deduction from resold impressions, so the buying members are charged an Auction Service Fee/Deduction instead.<br><br> **Default**: `"platform"`<br><br>**Required On**: `POST` |
| `note` | string | An optional note. |
| `data_siphon_fee` | int | The monthly charge for receiving Xandr [log-level data feeds](../log-level-data/log-level-data-feeds.md). |
| `mapuid_fee` | float | The monthly charge for using the Xandr user ID mapping service.<br>**Default**: `"0.00"` |
| `monthly_minimum_imps` | int | The minimum number of impressions that the member commits to transact per month. |
| `waive_ad_serving_fees` | boolean | This field is not used.<br>**Old or New**: `OLD` |
| `adx_auction_service_fee_pct` | float | This field is not used. Formerly, it was the auction service fee charged when buyer clients purchase inventory from Google Ad Manager. Google Ad Manager is a special case since they are a Xandr member (with a `bidder_id` of `2`) but buyer clients pay Google Ad Manager directly and don't pay Xandr for media cost. |
| `direct_clear_fee_pct` | float | The direct clear fee percentage. This is used for activity where the member clears the cost of media directly with the seller. |
| `contract_type` | enum | This field is no longer used. In the past, it was used by the finance team for revenue reporting. The allowed values were:<br> - `"NIB"`: This acronym refers to a former product offering called "Network in a box".<br> - `"XIB"`: This acronym refers to a former product offering called "Exchange in a box".<br> - `"RTBX"`: This acronym refers to a former product offering called "RTB Exchange".<br> - `"MSFT"`: A Microsoft contract.<br> - `"External"`: ...<br> - `"Partner"`: ... |
| `creative_audit_fee` | float | This field is not used. Use `auditing_fee_per_creative` instead. Formerly, it represented the total creative auditing fees. |
| `creative_priority_fee_1` | float | This field is not used. It is a placeholder for future development. |
| `creative_priority_fee_2` | float | The priority auditing fee per creative. |
| `imptracker_cpm` | float | The fees charged for recording third-party impressions. |
| `clicktracker_cpc` | float | The fees charged for recording third-party clicks. |
| `auto_renewal_term` | int | The auto-renewal term for the member, if such a term exists in the signed contract. Currently, this is only a placeholder for the term; no billing logic is associated with this field. |
| `seller_serving_cpm` | float | The CPM-based fee charged for each impression resold. Currently, this is only a placeholder for the fee; no billing logic is associated with this field. |
| `monthly_spend_based_minimum` | float | The monthly minimum based on the total buyer spend (i.e., cost of media) purchased in any given month. Currently, this is only a placeholder; no billing logic is associated with this field.<br><br>**New or Old**: `OLD` |
| `seller_revshare_pct` | float | The seller deduction percentage. This is charged when the member sells an impression to another member. |
| `seller_revshare_minimum` | boolean | Seller revshare minimum is calculated by taking the greater of (imps seen * seller auction request cpm) or (seller revshare).<br><br>**Default**: `false`<br>**New or Old**: `OLD` |
| `secure_whitelabel_pixel_fee` | float | The monthly charge for using the Secure White Label Pixel service. Currently, this is only a placeholder for the fee; no billing logic is associated with this field. |
| `monthly_minimum_requests` | int | The minimum number of requests per month based on the total number of impressions seen as recorded by Xandr. Currently this is only a placeholder for the minimum; no billing logic is associated with this field.<br><br>**New or Old**: `OLD` |
| `managed_hosted_video_cpm` | float | This is a placeholder for future development. |
| `cross_net_hosted_video_cpm` | float | This is a placeholder for future development. |
| `seller_auction_request_cpm` | float | The amount that a seller must pay every time they send us a bid request. This is charged even if there is no winning bid, or any bids at all. |
| `status` | enum | **Read Only**. Allowed values:<br> - `"in_progress"`: The contract is currently in force.<br> - `"in_past"`: The contract has ended.<br> - `"in_future"`: The contract is set to begin in the future.<br><br>**Default**: `"in_future"` |
| `member_name` | string | The name of the member. |
| `member_is_billable` | boolean | Whether the member is billable.<br><br>**Default**: `true` |
| `member_note` | string | This is used by Finance and Sales Ops to record custom contract terms or other invoice requirements.<br><br>**Default**: `""` |
| `member_enable_budget_check` | boolean | Whether this member has safety checks in place to prevent unintentional overspend.<br><br>**Default**: `true` |
| `monthly_service_fee_minimum_1` | float | The minimum monthly spend the client has committed to. This fee includes impression and click tracking.<br><br>**Old or New**: `OLD` |
| `monthly_service_fee_minimum_2` | float | The minimum monthly spend the client has committed to. This fee does not include impression and click tracking.<br><br>**Old or New**: `OLD` |
| `selling_enabled` | boolean | Whether this member is enabled to sell its inventory. This applies to both managed and cross-network selling.<br><br>**Default**: `true` |
| `seller_console_buyer_revshare_pct` | float | This percentage is charged to sellers when they sell to buyers on the Xandr platform.<br<br>**Note**: The value of this field is copied from the legacy field `seller_revshare_pct`.<br><br>**Required On**: `PUT`, when updating to the new pricing_version.<br>**Old or New**: `New` |
| `seller_bidder_buyer_revshare_pct` | float | This percentage is charged to sellers when they sell to non-Xandr bidders.<br><br>**Required On**: `PUT`, when updating to the new `pricing_version`.<br>**Old or New**: `New` |
| `auction_revshare_partner_inv_pct` | float | The percentage charged to buyers of type `"partner"` when they buy inventory from other members.<br><br>**Default**: `"0.00"`<br>**Old or New**: `New` |
| `auction_revshare_partner_inv_type` | string | The way the percentage defined in `"auction_revshare_partner_inv_pct"` is used to charge partner buyers. Allowed values:<br> - `"deduction"`: The agreed-upon percentage is subtracted directly from the buyer's auction revenue.<br>- `"fee"`: The percentage is charged as a fee after the auction.<br><br>**Note**: You may not set an `auction_revshare_partner_inv_type` that is different from `auction_revshare_platform_inv_type`. They should both be `"fee"` or `"deduction"`.<br><br>**Default**: `"fee"`<br>**Old or New**: `New` |
| `auction_revshare_platform_inv_pct` | float | The percentage charged to buyers of type `"platform"` when they buy inventory from other members.<br><br>**Note**: The value of this field is copied from the field `auction_revshare_pct`.<br><br>**Default**: `"0.00"`<br>**Old or New**: `New` |
| `auction_revshare_platform_inv_type` | string | The way the percentage defined in `"auction_revshare_platform_inv_pct"` is used to charge platform buyers. Allowed values:<br> - `"deduction"`: The agreed-upon percentage is subtracted directly from the buyer's auction revenue.<br> - `"fee"`: The percentage is charged as a fee after the auction.<br><br>**Note**:<br> - The value of this field is copied from the field `auction_revshare_type`.<br> - You may not set an `auction_revshare_platform_inv_type` that is different from `auction_revshare_partner_inv_type`. They should both be `"fee"` or `"deduction"`.<br><br>**Default**: `"fee"`<br>**Old or New**: `New` |

## Examples

### Create and view a legacy contract

```
$ cat update.json
{
  "member-contract": {
    "start_date": "2013-01-01 00:00:00",
    "end_date": "2013-06-30 23:59:59",
    "seller_type": "platform",
    "pricing_version": "2007.09.01",
  }
}
```

```
$ curl -b cookies -X POST -d @/tmp/legacy.json "http://68.67.148.153:16011/member-contract?member_id=1309"

{
    "response": {
        
        "": "",
        "num_elements": "",
        "start_element": "",
        "id": 3794,
        "count": "",
        "status": "OK"
    }
}
```

```
$ curl -b cookies "http://68.67.148.153:16011/member-contract?id=3794"
{
    "response": {
        
        "member-contract": {
            "member_note": "",
            "member_enable_budget_check": true,
            "member_is_billable": true,
            "member_name": "i8N6LZ6uN",
            "auction_revshare_platform_inv_type": "fee",
            "auction_revshare_platform_inv_pct": 0,
            "auction_revshare_partner_inv_type": "fee",
            "auction_revshare_partner_inv_pct": 0,
            "seller_bidder_buyer_revshare_pct": "",
            "seller_console_buyer_revshare_pct": "",
            "selling_enabled": true,
            "monthly_service_fee_minimum_2": "",
            "monthly_service_fee_minimum_1": "",
            "status": "in_future",
            "seller_auction_request_cpm": "",
            "cross_net_hosted_video_cpm": "",
            "managed_hosted_video_cpm": "",
            "monthly_minimum_requests": "",
            "secure_whitelabel_pixel_fee": 0,
            "seller_revshare_minimum": false,
            "seller_revshare_pct": "",
            "monthly_spend_based_minimum": "",
            "seller_serving_cpm": 0,
            "auto_renewal_term": "",
            "clicktracker_cpc": "",
            "imptracker_cpm": "",
            "creative_priority_fee_2": 25,
            "creative_priority_fee_1": 0,
            "creative_audit_fee": 0,
            "contract_type": "",
            "direct_clear_fee_pct": "",
            "adx_auction_service_fee_pct": "",
            "waive_ad_serving_fees": false,
            "monthly_minimum_imps": "",
            "mapuid_fee": 0,
            "data_siphon_fee": "",
            "note": "",
            "seller_type": "platform",
            "pricing_version": "2007.09.01",
            "auction_revshare_type": "fee",
            "apply_min_cpm_to_clearing": false,
            "auction_maximum_cpm": "",
            "clearing_revshare_pct": "",
            "auction_revshare_pct": "",
            "clearing_revshare": "",
            "monthly_minimum_spend": "",
            "creative_size_fee_per_gb": "",
            "creative_size_minimum_bytes": "",
            "auditing_fee_per_creative": "",
            "ad_serving_cpm": "",
            "auction_minimum_cpm": "",
            "auction_revshare": "",
            "end_date": "2013-06-30 23:59:59",
            "start_date": "2013-01-01 00:00:00",
            "last_activity": "2012-12-20 16:03:38",
            "member_id": 1309,
            "id": 3794
        },
        "num_elements": "",
        "start_element": "",
        "count": 1,
        "status": "OK"
    }
}
```

### Create and view a contract with the current `pricing_version`

```
$ cat update.json
{
  "member-contract": {
    "start_date": "2013-01-01 00:00:00",
    "end_date": "2013-06-30 23:59:59",
    "seller_type": "platform",
    "pricing_version": "2013.01.02",
    "auction_revshare_partner_inv_type": "fee",
    "auction_revshare_platform_inv_type": "fee"
  }
}
```

```
$ curl -b cookies -c cookies -X POST -d @update.json "https://api.appnexus.com/member-contract?member_id=1309"

{"response":{"status":"OK","count":null,"id":7543,"start_element":null,"num_elements":null,"":null,}}
```

```
$ curl -b cookies "http://68.67.148.153:16011/member-contract?member_id=4"
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "member-contracts": [
      {
        "id": 7543,
        "member_id": 4,
        "last_activity": "2012-12-07 18:30:12",
        "start_date": "2013-01-01 00:00:00",
        "end_date": "2013-06-30 23:59:59",
        "auction_revshare": null,
        "ad_serving_cpm": null,
        "auditing_fee_per_creative": null,
        "creative_size_minimum_bytes": null,
        "creative_size_fee_per_gb": null,
        "clearing_revshare": null,
        "clearing_revshare_pct": null,
        "auction_maximum_cpm": null,
        "apply_min_cpm_to_clearing": false,
        "pricing_version": "2013.01.02",
        "seller_type": "platform",
        "note": null,
        "data_siphon_fee": null,
        "mapuid_fee": "0.00",
        "waive_ad_serving_fees": false,
        "adx_auction_service_fee_pct": null,
        "direct_clear_fee_pct": null,
        "contract_type": null,
        "creative_audit_fee": "0.00",
        "creative_priority_fee_1": "0.00",
        "creative_priority_fee_2": "25.00",
        "imptracker_cpm": null,
        "clicktracker_cpc": null,
        "auto_renewal_term": null,
        "seller_serving_cpm": "0.0000",
        "secure_whitelabel_pixel_fee": "0.00",
        "managed_hosted_video_cpm": null,
        "cross_net_hosted_video_cpm": null,
        "seller_auction_request_cpm": null,
        "status": "in_future",
        "selling_enabled": true,
        "seller_console_buyer_revshare_pct": null,
        "seller_bidder_buyer_revshare_pct": null,
        "auction_revshare_partner_inv_pct": "0.00",
        "auction_revshare_partner_inv_type": "fee",
        "auction_revshare_platform_inv_pct": "0.00",
        "auction_revshare_platform_inv_type": "fee",
        "member_name": "6Ax3NT0ST",
        "member_is_billable": true,
        "member_enable_budget_check": true
      }
    ]
  }
  }
```
