---
title: Bidders - Deal From Package Service
description: Explore packages, select via buyer access, create deals with package service, streamlining buyer-seller transactions.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Deal from package service

A package is a deal that a seller is prepared to offer to any buyer. Buyer members use the [Package Buyer Access Service](package-buyer-access-service.md) to browse available packages and find one that meets their needs. Then buyers use the Deal From Package service to generate a deal between themselves and the seller.

Once you have generated a deal, you can view deal details including description and deal pricing using the [Deal Buyer Access Service](deal-buyer-access-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| POST | `https://api.adnxs.com/deal-from-package?buyer_member_id=BUYER_MEMBER_ID` | **Create a new deal based on a package**.<br><br>**Note**: Bidder and admin users must specify the buyer member ID in the URI; for member users, the deal record is generated with the member set as the buyer. |

## JSON fields

| Name | Type | Description |
|--|--|--|
| `id` | int | The ID of the deal creation record.<br> - **Default**: auto-generated number. |
| `package_id` | int | The ID of the package from which you are generating a deal. You can use the [Package Buyer Access](package-buyer-access-service.md) Service to get package IDs.<br> - **Required On**: POST. |

## Example

**Create a deal from a package**

```
$ cat create_deal
{
    "deal-from-package": {
        "package_id": 1234
    }
}
$ curl -b cookies -c cookies -X POST -d @create_deal.json "https://api.adnxs.com/deal-from-package?buyer_member_id=234"
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "id": 4321,
        "deal-from-package": {
            "id": 4321,
            "package_id": 1234
        }
    }
}
```
