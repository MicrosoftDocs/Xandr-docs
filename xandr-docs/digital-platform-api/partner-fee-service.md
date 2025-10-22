---
title: Partner Fee Service
description: Use the Partner Fee service to reserve budget for third-party costs owed to parties other than the publisher.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Partner Fee service

> [!NOTE]
> Partner Fees are an enhancement and replacement for broker fees for [augmented line items (ALIs)](./line-item-service---ali.md).

If you need to reserve a portion of your budget for third-party costs (costs owed to parties other than the publisher), you can define this information with the Partner Fee service. Fees can be tracked on a CPM, cost share, or revenue share basis, and can be applied to multiple advertisers and line items, if desired. A single advertiser or line item can have multiple fees applied.

Common fees you might need to budget for are:

- Advertiser **ad serving fees** and **creative hosting fees**, which are charged for delivering a line item's creative assets.
- **Data fees** that are not cleared by Xandr as part of the Data Marketplace.
- Post-bid **reporting fees** – for example, using a pixel to track where impressions are served and then auditing retroactively how many transactions violated brand safety standards.
- **Revenue share agreements** with other ad tech partners.
- **Incremental fees** charged by an intermediary to the advertiser, such as a managed service fee or consulting fee.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/partner-fee?advertiser_id=ADVERTISER_ID` | View all partner fees for an advertiser. |
| `GET` | `https://api.appnexus.com/partner-fee?id=PARTNER_FEE_ID` | View a specific partner fee. |
| `POST` | `https://api.appnexus.com/partner-fee` | Create a new partner fee. |
| `PUT` | `https://api.appnexus.com/partner-fee?id=PARTNER_FEE_ID` | Modify a partner fee. |
| `DELETE` | `https://api.appnexus.com/partner-fee?id=PARTNER_FEE_ID` | Delete a partner fee.<br><br>**Note**:<br>You can only delete a fee that is not applied to any line items. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `advertisers` | mapping | The advertisers for which this fee is eligible. This field must be passed in as an array of object with the following format:<br>`[{'id':ADVERTISER_ID_1},{'id'}:ADVERTISER_ID_2}]` |
| `apply_to_deals` | bool | Determines whether this fee applies to deals.<br><br>**Required On**: `POST`<br>**Default**: `true` |
| `apply_to_managed` | bool | Determines whether this fee applies to managed inventory.<br><br>**Required On**: `POST`<br>**Default**: `true` |
| `apply_to_rtb` | bool | Determines whether this fee applies to RTB inventory.<br><br>**Required On**: `POST`<br>**Default**: `true` |
| `available_for_all_advertisers` | bool | When `true`, this fee is eligible to be applied to all advertisers for this member. This is available only to users with [Member](./member-service.md)-level access.<br><br>**Default**: `false` |
| `description` | text | Optional. User-supplied description of the fee. |
| `currency` | char(3) | The currency in which the fee is calculated.<br> - If `partner_fee_payment_type_id` is cpm, a value is required.<br> - If `partner_fee_payment_type_id` is `revshare`, this field must be `null`.<br>Use the [Currency Service](./currency-service.md) to see a list of available currencies. |
| `id` | int | Unique identifier for the fee.<br><br>**Required On**: `PUT` and `DELETE`<br>**Default**: auto-generated number. |
| `name` | varchar(255) | The fee name.<br><br>**Required On**: `POST` |
| `partner_fee_payment_type_id` | int | Determines the payment type for this fee:<br> - `"1"` for cpm. If cpm is selected, you must specify the currency with currency.<br> - `"2"` for revenue sharing.<br><br>**Required On**: `POST` |
| `partner_fee_basis_id` | int | Determines the basis from which a percentage fee is derived.<br> - `"1"` for net media cost.<br> - `"2"` for gross media cost (media cost including [BASC](../invest/buyer-auction-service-charge-mechanics.md).<br> - `"3"` for net media cost (media cost without BASC) + data costs.<br> - `"4"` for gross media cost (media cost including BASC) + data costs.<br> - `"5"` for revenue.<br>CPM fees can only be set to `"5"` (revenue).<br><br>**Required On**: `POST` |
| `partner_fee_type_id` | int | Defines the type of fee. Supported values are:<br> - `"1"` for ad serving<br> - `"2"` for algorithm<br> - `"3"` for data<br> - `"4"` for reporting<br> - `"5"` for service<br> - `"6"` for technology<br> - `"7"` for viewability<br> - `"8"` for other<br><br>**Required On**: `POST` |
| `partner_fee_vendor_id` | int | The ID of vendor charging the fee. Supported values are:<br> - `"1"` for Adloox<br> - `"2"` for ComScore<br> - `"3"` for DoubleClick<br> - `"4"` for DoubleVerify<br> - `"5"` for Evidon<br> - `"6"` for Flashtalking<br> - `"7"` for Ghostery<br> - `"8"` for GroovinAds<br> - `"9"` for Integral Ad Science (IAS)<br> - `"10"` for MOAT<br> - `"11"` for Ninth Decimal<br> - `"12"` for Sizmek<br> - `"13"` for TrustArc<br> - `"14"` for Custom Vendor 1<br> - `"15"` for Custom Vendor 2<br> - `"16"` for Custom Vendor 3<br> - `"17"` for Custom Vendor 4<br> - `"18"` for Custom Vendor 5<br>Custom vendors will appear as Custom Vendor 1, Custom Vendor 2, etc. in reporting. We recommend that you include the partner name in the fee's name field for easy identification.<br><br>**Required On**: `POST` |
| `required` | bool | When `true`, this fee will be required for and applied to all new line items for eligible advertisers. It will not be automatically applied retroactively to existing line items.<br><br>**Note**: You cannot remove a fee from a line item if `required` is `true`. You must first set `required` to `false` and then remove the fee from the line item.<br><br>**Default**: `false` |
| `value` | decimal(15,5) | The fee being charged.<br> - If the payment type is `cpm`, this value will be in the defined `currency`.<br> - If the payment type is revenue sharing, the value should be a fraction between `0` and `1`. For example, a 10% revshare fee is specified by 0.1.<br><br>**Required On**: `POST` |

## Examples

### Create a partner fee

```
$ cat partner-fee.json

{
    "partner_fee": {
        "name" : "Test1",
        "apply_to_managed" : true,
        "apply_to_rtb" : true,
        "apply_to_deals" : true,
        "value" : .5,
        "partner_fee_vendor_id" : 3,
        "partner_fee_payment_type_id" : 2,
        "partner_fee_basis_id" : 2,
        "partner_fee_type_id" : 1,
        "required" : true,
        "advertisers" : [
            {
                "id" : 1
            }
        ]
    }
}

$curl -b cookie -X POST -d @partner-fee.json "https://api.appnexus.com/partner-fee"

{
    "response": {
        "status" : "OK",
        "id": 4401
    }
}
```

### View a partner fee's details

```
$ curl -b cookie "https://api.appnexus.com/partner-fee?id=4401"

{
    "response": {
        "status": "OK",
        "partner_fees": [
            {
                "name" : "Test1",
                "apply_to_managed" : true,
                "apply_to_rtb" : true,
                "apply_to_deals" : true,
                "currency" : null,
                "value" : .5,
                "partner_fee_vendor_id" : 3,
                "partner_fee_payment_type_id" : 2,
                "partner_fee_basis_id" : 2,
                "partner_fee_type_id" : 1,
                "required" : true,
                "advertisers" : [
                    {
                      "id" : 1
                    }
                ]
            }        
        ]
    }
}
```

### View revenue-sharing partner fees for managed inventory

```
$ curl -b cookie "https://api.appnexus.com/partner-fee?apply_to_managed=true&partner_fee_payment_type_id=2"

{
    "response": {
        "count": "2",
        "partner_fees": [
            {
                "id" : 4401,
                "name" : "Test1",
                "apply_to_managed" : true,
                "apply_to_rtb" : true,
                "apply_to_deals" : true,
                "value" : .1,
                "partner_fee_vendor_id" : 3,
                "partner_fee_payment_type_id" : 2,
                "partner_fee_basis_id" : 2,
                "partner_fee_type_id" : 1,
                "required" : true,
                "available_for_all_advertisers": true,
                "advertisers" : [
                ]
            },
            {
                "id" : 4402,
                "name" : "Test2",
                "apply_to_managed" : true,
                "apply_to_rtb" : false,
                "apply_to_deals" : false,
                "currency" : "null",
                "value" : .5,
                "partner_fee_vendor_id" : 14,
                "partner_fee_payment_type_id" : 2,
                "partner_fee_basis_id" : 2,
                "partner_fee_type_id" : 6,
                "required" : false,
                "available_for_all_advertiser" : true,
                "advertisers" : [
                ]
            } 
        ]
    }
}
```

### Change a partner fee's payment type

```
$ cat partner-fee.json

{
    "partner_fee": {
        "currency" : USD,
        "value" : 1.2,
        "partner_fee_payment_type_id" : 1,
        "partner_fee_basis_id": 5 
    }
}

$ curl -b cookie -X PUT -d @partner-fee.json "https://api.appnexus.com/partner-fee?id=4401"

{
    "response": {
        "status" : "OK",
        "id": 4401
    }
}
```

### Apply a partner fee to a line item

```
$ cat LI-update.json

{       
    "line-item": {
        "partner_fees": [
            {
                "id": 4401
            },
            { 
                "id": 4402
            }
        ]
    }
}

$ curl -b cookie -X PUT -d @LI-update.json "https://api.appnexus.com/line-item?id=2345432"

{
    "response": {
        "status" : "OK",
        "id": 2345432
    }
}
```

### Remove a fee from a line item

```
$ curl -b cookie -x GET "https://api.appnexus.com/line-item?id=1234"

 {
    "line-item": {
        ...,
        "partner_fees": [
            {
                "id": 1
            },
            {
                "id": 2
            }, 
            {
                "id": 3
            }
        ],
        ...
    }
}


$ cat LI-update.json

{
    "line-item": {
        "partner_fees": [
            {
                "id": 1
            },
            {
                "id": 3
            } 
        ]
    }
}

$ curl -b cookie -X PUT "https://api.appnexus.com/line-item?id=1234"

{
    "line-item": {
        ...,
        "partner_fees": [
            {
                "id": 1
            },
            {
                "id": 3
            }
        ],
        ...
    }
}

$ curl -b cookie -x GET "https://api.appnexus.com/line-item?id=1234"

 {
    "line-item": {
        ...,
        "partner_fees": [
            {
                "id": 1
            }, 
            {
                "id": 3
            }
        ],
        ...
    }
}
```

> [!NOTE]
> You cannot remove a fee from a line item if `required` is `true`. You must first set `required` to `false` and then remove the fee from the line item.

### Remove a fee from an advertiser

```
$ curl -b cookie -x GET "https://api.appnexus.com/advertiser?id=5678"

 {
    "advertiser": {
        ...,
        "partner_fees": [
            {
                "id": 1
            },
            {
                "id": 2
            }, 
            {
                "id": 3
            }
        ],
        ...
    }
}



$ cat partner-fee-update.json

{
    "partner-fee": {
        "advertisers": [
            {
                "id": 5677
            },
            {
                "id": 5679
            }
        ]
    }
}

$ curl -b cookie -X PUT -d @partner-fee-update.json "https://api.appnexus.com/partner-fee?id=1"

{
    "response": {
        "status" : "OK",
        "id": 1
    }
}
```

You cannot remove a fee from an advertiser if the fee is currently applied to any of that advertiser's line items. You must first remove the fee from any line items and then remove the fee from the advertiser.
