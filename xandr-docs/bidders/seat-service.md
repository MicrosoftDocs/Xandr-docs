---
title: Seat Service
description: In this article, find information about the Seat Service and the fields associated with it along with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Seat service

> [!IMPORTANT]
> This feature is currently in Closed Beta. If you are interested in participating, please reach out to your Xandr representative.

The Buyer Seat ID product allows for external bidders to bid with their custom buyer IDs rather than using Xandr member IDs. This allows external bidders to utilize buyer IDs from their own systems when bidding on Xandr inventory and will allow for more seamless reporting and deal set up.

The seat service is a brand new API service used to register new seats for a bidder. This can be done manually through post calls to the API or done in real time when a bidder bids with a new seat id in the bid response.

## Summary

Seat Service is used to store a bidder's seat IDs. These seat IDs will be used in the bid response and logged in transaction reporting.

## Rest API

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/seat/BIDDER_ID` | To see all of your seats attached to your bidder |
| GET | `https://api.adnxs.com/seat/BIDDER_ID/SEAT_ID` | To see an existing seat using API seat identifier |
| GET | `https://api.adnxs.com/seat?bidder_id=BIDDER_ID&code=SEATCODE` | To see an existing seat using API bidder seat id |
| POST | `https://api.adnxs.com/seat/BIDDER_ID` | Add a new seat |
| PUT | `https://api.adnxs.com/seat/BIDDER_ID/SEAT_ID` | Modify an existing seat using API seat identifier |
| PUT | `https://api.adnxs.com/seat?bidder_id=BIDDER_ID&co6de=SEATCODE` | Modify an existing seat using bidder seat id |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `bidder_id` | int | The ID of the bidder. This is a read-only field. |
| `code` | string | Bidder seat id. |
| `id` | int | The ID of the seat. This is a read-only field. |
| `name` | string | Name of the buyer for this seat. <br><br> **Note**: In auto registered seats, the standard naming convention will be *seat_code (bidder name)* |

## Examples

The below example API calls show how you can upload new seats or edit existing seats:

### Uploading a new seat

```
$ cat seats.json
 
{
 
    "seats": [{
            "bidder_id": 1,
            "code": "sdfg54VVsh",
            "name": "sdfg54VVsh(Bidder)"
        },
        {
            "bidder_id": 129,
            "code": "54Gfa762Gbse",
            "name": "54Gfa762Gbse(Bidder)"
        }
    ]
}
 
$ curl -b cookies -c cookies -X POST -d @seats.json "https://api.adnxs.com/seat/1"
 {
    "response": {
        "status": "OK",
        "num_elements": 100,
        "seats": [
            {
                "bidder_id": 1,
                "code": "sdfg54VVsh",
                "created_on": "2018-12-13 15:31:13",
                "id": 11,
                "last_activity": "2018-12-13 15:31:13",
                "name": "sdfg54VVsh(Bidder)"
            },
            {
                "bidder_id": 1,
                "code": "54Gfa762Gbse",
                "created_on": "2018-12-13 17:09:26",
                "id": 22,
                "last_activity": "2018-12-13 17:09:26",
                "name": "54Gfa762Gbse(Bidder)"
            }
        ]
    }
}
```

### Updating an existing seat - changing the seat name

```
$ cat seats.json
 
{
 
    "seats": [{
            "bidder_id": 1,
            "code": "sdfg54VVsh",
            "name": "Bidder seat name"
        }
    ]
}
 
$ curl -b cookies -c cookies -X PUT -d @seats.json "https://api.adnxs.com/seat/1/11"
 {
    "response": {
        "status": "OK",
        "num_elements": 100,
        "seats": [
            {
                "bidder_id": 1,
                "code": "sdfg54VVsh",
                "created_on": "2018-12-13 15:31:13",
                "id": 11,
                "last_activity": "2018-12-13 15:31:13",
                "name": "Bidder seat name"
            }
        ]
    }
}
```

### Seeing an existing seat

```
$ curl -b cookies -c cookies -X GET "https://api.adnxs.com/seat/1/22"
 {
    "response": {
        "status": "OK",
        "num_elements": 100,
        "seats": [
            {
                "bidder_id": 1,
                "code": "54Gfa762Gbse",
                "created_on": "2018-12-13 17:09:26",
                "id": 22,
                "last_activity": "2018-12-13 17:09:26",
                "name": "54Gfa762Gbse(Bidder)"
            }
        ]
    }
}
```

### Seeing all seats for a specific bidder

```
$ curl -b cookies -c cookies -X GET "https://api.adnxs.com/seat/1"
 {
    "response": {
        "status": "OK",
        "num_elements": 100,
        "seats": [
            {
                "bidder_id": 1,
                "code": "sdfg54VVsh",
                "created_on": "2018-12-13 15:31:13",
                "id": 11,
                "last_activity": "2018-12-13 15:31:13",
                "name": "sdfg54VVsh(Bidder)"
            },
            {
                "bidder_id": 1,
                "code": "54Gfa762Gbse",
                "created_on": "2018-12-13 17:09:26",
                "id": 22,
                "last_activity": "2018-12-13 17:09:26",
                "name": "54Gfa762Gbse(Bidder)"
            }
        ]
    }
}
```

## Related topics

- [Bidder Service](bidder-service.md)
- [Creative Service](creative-service.md)
- [Incoming Bid Response from Bidders](incoming-bid-response-from-bidders.md)
