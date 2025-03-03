---
title: Deal eligibility requirements setting up deals
description: In this article, learn about the deal eligibility requirements and ways to set up a deal for test buyer members AN Talent (882) and AN Challenge (1370).
ms.custom: supply-partners
ms.date: 10/28/2023
---

# Deal eligibility requirements: setting up deals

One of the requirements that needs to be met to transact on Xandr's open exchange is to confirm that you understand the Deal Service. In order to demonstrate your understanding, you’ll create deals with two Xandr test members, AN Talent(882) and AN Challenge(1370). The deal must represent the same inventory, and therefore should always appear on the same bid requests. Each deal must see over 10,000 impressions per day.

## Step 1: Set up a deal with buyer member AN Talent (882)

| Field | Type (Length) | Description | Expected Value (For Test) |
|:---|:---|:---|:---|
| `code` | string (100) | The custom code for the deal.<br><br>**Note:** This field is mandatory and represents your internal deal ID, passed in the [incoming bid request](incoming-bid-request-from-ssps.md) through the deal ID field in the PMP object. | Value that you will be passing in PMP's object, deal ID field. |
| `nacme` | string (255) | The name of the deal. | APN Test Deal 1 |
| `active` | Boolean | If true, the deal is active. Note that the deal will be available to the buyer only when this field is true, `start_date` is in the past (or null), and `end_date` is in the future (or null). | true |
| `start_date` | timestamp | The day and time when the deal starts being available to the buyer. If this is set, the format must be "YYYY-MM-DD HH:MM:SS". | 2017-01-01 00:00:00 |
| `end_date` | timestamp | The day and time when the deal stops being available to the buyer. If this is set, the format must be "YYYY-MM-DD HH:MM:SS". | 2037-01-01 00:00:00 |
| `floor_price` | double | The minimum CPM value that the buyer must bid to be eligible for the deal. | 0.5 |
| `use_deal_floor` | Boolean | If true, the `floor_price` is applied for the deal. | true |
| `buyer` | object | The buying member who can target this deal. For more details, see [Buyer](#buyer) below. | 882 |
| `type` | object | The type of deal. For platform sellers, a deal can be an open auction or a private auction. For more details, see [Type](#type) below. | 2 |

### Buyer

The buyer object can be set on a `POST`, but cannot be updated with a `PUT`. If you want to change the buyer, you need to create a new deal. The `buyer` object should contain the following fields.

| Field | Type | Description | Expected Value (For Test) |
|:---|:---|:---|:---|
| `id`  | int | The member ID of the buyer. |  882 |

### Type

The `type` object should contain the following fields.

| Field | Type (Length) | Description | Expected Value (For Test) |
|:---|:---|:---|:---|
| `id`  | int | The ID representing the type of deal. Possible values:<br> - 1 = Open Auction<br>In an "Open Auction", buyers targeting the deals and buyers targeting the inventory via other means compete for the impression. If a buyer targeting a deal submits the highest bid and the bid clears the deal's floor, that buyer wins the auction, paying either the second-highest bid or the deal floor price, whichever is higher. If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying either the second-highest bid or ECP, whichever is higher. <br><br> - 2 = Private Auction<br>In a "Private Auction", buyers targeting the private deals compete for the impression first. Then, if none of the deal buyers win, the auction is opened to buyers targeting the inventory via other means. If a buyer targeting a deal submits a bid higher than the deal's floor and higher than any other private auction bids, that buyer wins the auction, paying either the second-highest bid from the private auction or the deal floor price, whichever is higher. If no private auction deals clear their floors, the highest bid in the open auction wins, paying either the second-highest bid from the open auction or ECP, whichever is higher.<br><br>For examples showing how these different types of auctions work, see "Deal Auction Mechanics" in documentation. | Private Auction |

## Step 2: Set up the same deal for buyer member AN Challenge (1370)

| Field | Type (Length) | Description | Expected Value (For Test) |
|:---|:---|:---|:---|
| `code` | string (100) | The custom code for the deal.<br><br>**Note:** This field is mandatory and represents your internal deal ID, passed in the [incoming bid request](incoming-bid-request-from-ssps.md) through the PMP's object, deal ID field. | Value that you will be passing in PMP's object, deal ID field. |
| `name` | string (255) | The name of the deal. | APN Test Deal 2 |
| `active` | Boolean | If true, the deal is active. Note that the deal will be available to the buyer only when this field is true, `start_date` is in the past (or null), and `end_date` is in the future (or null). | true |
| `start_date` | timestamp | The day and time when the deal starts being available to the buyer. If this is set, the format must be "YYYY-MM-DD HH:MM:SS". | 2017-01-01 00:00:00 |
| `end_date` | timestamp | The day and time when the deal stops being available to the buyer. If this is set, the format must be "YYYY-MM-DD HH:MM:SS". | 2037-01-01 00:00:00 |
| `floor_price` | double | The minimum CPM value that the buyer must bid to be eligible for the deal. | 0.5 |
| `use_deal_floor` | Boolean | If true, the `floor_price` is applied for the deal. | true |
| `buyer` | object | The buying member who can target this deal. For more details, see [Buyer](#buyer-member-an-challenge-1370) below. | 1370 |
| `type` | object | The type of deal. For platform sellers, a deal can be an open auction or a private auction. For more details, see [Type](#type-of-deal) below. | 2 |

### Buyer member AN Challenge (1370)
  
The buyer object can be set on a `POST`, but cannot be updated with a `PUT`. If you want to change the buyer, you need to create a new deal.

The `buyer` object should contain the following fields.

| Field | Type | Description | Expected Value (For Test) |
|:---|:---|:---|:---|
| `id`  | int | The member ID of the buyer. |  1370 |

### Type of deal

The `type` object should contains the following fields.

| Field | Type (Length) | Description | Expected Value (For Test) |
|:---|:---|:---|:---|
| `id`  | int | The ID representing the type of deal. Possible values:<br> - 1 = Open Auction<br>In an "Open Auction", buyers targeting the deals and buyers targeting the inventory via other means compete for the impression. If a buyer targeting a deal submits the highest bid and the bid clears the deal's floor, that buyer wins the auction, paying either the second-highest bid or the deal floor price, whichever is higher. If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying either the second-highest bid or ECP, whichever is higher. <br><br> - 2 = Private Auction<br>In a "Private Auction", buyers targeting the private deals compete for the impression first. Then, if none of the deal buyers win, the auction is opened to buyers targeting the inventory via other means. If a buyer targeting a deal submits a bid higher than the deal's floor and higher than any other private auction bids, that buyer wins the auction, paying either the second-highest bid from the private auction or the deal floor price, whichever is higher. If no private auction deals clear their floors, the highest bid in the open auction wins, paying either the second-highest bid from the open auction or ECP, whichever is higher.<br><br>For examples showing how these different types of auctions work, see "Deal Auction Mechanics" in documentation. | Private Auction |

## Step 3: Submit the deals for review

Once you feel confident that you've appropriately built to our [Deal Service](../digital-platform-api/deal-service.md), and have set up both your deals as outlined above, submit a [support case]( https://support.ads.microsoft.com) in order to have your traffic reviewed. Include both the Xandr deal IDs you've created. We will update you on the final steps of the process.

## Deal Service API

### REST API

Add a new deal:

```
POST https://api.appnexus.com/deal 
(deal JSON)
```

Modify an existing deal:

```
PUT https://api.appnexus.com/deal?id=DEAL_ID
(deal_update JSON)
```

View all deals you have with buyers:

``` 
GET https://api.appnexus.com/deal
```

View a specific deal:

``` 
GET https://api.appnexus.com/deal?id=DEAL_ID 
```

View multiple deals by ID using a comma-separated list:

``` 
GET https://api.appnexus.com/deal?id=1,2,3
```

Delete a deal:

``` 
DELETE https://api.appnexus.com/deal?id=DEAL_ID
```

## Example

Example `POST` call

``` 
$ cat new_test_deal_1
 
{
    "deal": {
        "code": "APN-TEST1",
        "use_deal_floor": true,
        "name": "APN Test Deal 1",
        "active": true,
        "start_date": "2016-12-01 01:00:00",
        "end_date": "2037-01-01 00:00:00",
        "floor_price": 0.5,
        "currency": "USD",
        "buyer": {
            "id": 882
        },
        "type": {
            "id": 2
        }
    }
}
 
$ curl -b cookies -c cookies -X POST -d @new_test_deal_1.json 'https://api.appnexus.com/deal'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 64,
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "id": 64,
            "code": "APN-TEST1,
            "name": "APN Test Deal 1",
            "description": null,
            "active": true,
            "start_date": "2016-12-01 01:00:00",
            "end_date": "2037-01-01 00:00:00",
            "profile_id": null,
            "package_id": null,
            "floor_price": 0.5,
            "currency": "USD",
            "use_deal_floor": true,
            "last_modified": "2013-12-04 20:43:44",
            "seller": {
                "id": 2345,
                "name": "Seller 123"
            },
            "buyer": {
                "id": 882,
                "bidder_id": 2,
                "name": "AN Talent"
            },
            "type": {
                "id": 2,
                "name": "Private Auction"
            },
            "brands": null,
            "ask_price": 0,
            "size_preference": null
        }
    }
}
```
