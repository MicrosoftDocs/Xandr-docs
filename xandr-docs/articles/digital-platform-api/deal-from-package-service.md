---
title: Digital Platform API - Deal From Package Service
description: Buyers can browse packages using the package buyer access service and generate deals with sellers through the deal from package service. 
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Deal from package service

A package is a deal that a seller is prepared to offer to any buyer. Buyer members use the [Package Buyer Access Service](./package-buyer-access-service.md) to browse available packages and find one that meets their needs. Then buyers use the Deal From Package service to generate a deal between themselves and the seller.

Once you have generated a deal, you can view deal details including description and deal pricing using the [Deal Buyer Access Service](./deal-buyer-access-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | https://api.appnexus.com/deal-from-package/meta | Find out which fields you can filter and sort by. |
| `POST` | https://api.appnexus.com/deal-from-package | Create a new deal based on a package.<br><br>**Note**:<br>When a member makes a `POST` call to this service, a deal record is generated with the member set as the buyer. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the deal creation record.<br><br>**Default**: auto-generated number. |
| `package_id` | int | The ID of the package from which you are generating a deal. You can use the [Package Service](./package-service.md) to get package IDs.<br><br>**Required On**: `POST` |

## Examples

### Create a deal from a package

```
$ cat create_deal

{
 "deal-from-package":
  { 
    "package_id" : 5555
  }
}

$ curl -b cookies -c cookies -X POST -d @create_deal.json "https://api.appnexus.com/deal-from-package"

{
  "response": {
    "status": "OK",
    "count": 1,
    "deal-from-package": {
      "id": 1684,
      "package_id": 5555
    }
  }
}
```
