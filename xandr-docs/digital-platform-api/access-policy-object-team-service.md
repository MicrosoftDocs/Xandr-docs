---
title: Access Policy Object Team Service
description: In this article, learn about the Access Policy Object Team service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Policy Object Team service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-policy-object-team** service allows you to retrieve a list of all the teams a given resource is on. You can query on any combination of advertisers, insertion orders, publishers, sites, and placements. If you query on multiple objects, your results will include all the teams that any of the objects is on, not the teams that *all* of the objects are on. For example, if AdvertiserA is on Team1 and Team2, and PublisherA is on Team2 and Team3, querying access-policy-object-team on AdvertiserA and PublisherA would return Team1, Team2, and Team3.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | - [https://api.appnexus.com/access-policy-object-team?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/access-policy-object-team?advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/access-policy-object-team?insertion_order_id=INSERTION_ORDER_ID](https://api.appnexus.com/access-policy-object-team?insertion_order_id=INSERTION_ORDER_ID)<br> - [https://api.appnexus.com/access-policy-object-team?publisher_id=PUBLISHER_ID](https://api.appnexus.com/access-policy-object-team?publisher_id=PUBLISHER_ID)<br> - [https://api.appnexus.com/access-policy-object-team?site_id=SITE_ID](https://api.appnexus.com/access-policy-object-team?site_id=SITE_ID)<br> - [https://api.appnexus.com/access-policy-object-team?placement_id=PLACEMENT_ID](https://api.appnexus.com/access-policy-object-team?placement_id=PLACEMENT_ID) | View all teams a resource is on. |
| `GET` | [https://api.appnexus.com/access-member-role?resource_id=RESOURCE_ID&resource_id=RESOURCE_ID](https://api.appnexus.com/access-member-role?<resource>_id=RESOURCE_ID&<resource>_id=RESOURCE_ID) | View all teams several resources are on. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The numeric ID of the team. |
| `name` | string | The name of the team the resource is on. |

## Examples

### View all teams a resource is on

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-object-team?advertiser_id=123456'
{
    "id": 10,
    "name": "Team1",
},
{
    "id": 20,
    "name": "Team5",
}
```

### View all teams multiple resources are on

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-object-team?advertiser_id=123456&publisher_id=234567'
 
{
    "id": 10,
    "name": "Team1",
},
{
    "id": 20,
    "name": "Team5",
},
{
    "id": 15,
    "name": "Team7",
}
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
