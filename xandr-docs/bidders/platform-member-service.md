---
title: Bidders - Platform Member Service
description: In this article, find information about the Platform Member service and the variables associated with it along with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Platform member service

Public information about members is available to other members on the platform through the Platform Member service.

Any entity that has a financial relationship with the Xandr platform (usually a buyer or seller) needs to be added to the Xandr system as a "member" before they can conduct transactions. Members can be registered with the [Member Service](member-service.md) either by a bidder or by Xandr personnel.

## REST API

| HTTP method | End point | Description |
|---|---|---|
| GET  | `https://api.adnxs.com/platform-member` | To see all the members that have exposed their information |
| GET | `https://api.adnxs.com/platform-member/MEMBER_ID` | To see a particular member |

## JSON structure

| JSON variable | Type | Description |
|---|---|---|
| `bidder` | object | The bidder that that member uses to buy |
| `contact_email` | string | The email address to use to contact the member. |
| `daily_imps_self_audited` | int | The number of daily impressions through inventory that have been audited by the member. |
| `daily_imps_unaudited` | int | The number of daily impression through inventory that have not been audited. |
| `daily_imps_verified` | int | The number of daily impressions through inventory that have been verified by Xandr. |
| `id` | int | The ID of the member. |
| `is_iash_compliant` | bool | Whether or not the member is IASH compliant. |
| `name` | string | The name of the member. |
| `platform_exposure` | "hidden", "private", "public" | The visibility of the member on the platform. Hidden members should not appear. |
| `primary_type` | "network", "buyer", "seller", "data_provider" | The type of member. This indicates the primary type of transactions this member performs with Xandr. |
| `visibility_rules` | object | The visibility rules associated with that member |

## Visibility rules

| JSON variable | Type | Description |
|---|---|---|
| `custom_categories` | array of objects | The custom content categories that the seller sends in the bid request, if expose_custom_categories is "list". |
| `expose_age` | bool | Whether or not the seller sends the age of the user in the bid request |
| `expose_custom_categories` | "none", "all", "list" | If the seller sends no custom categories, all custom categories, or only those custom categories listed in the custom_categories array. |
| `expose_gender` | bool | Whether or not the seller sends the gender of the user in the bid request |
| `expose_publishers` | bool | **Not Used.** <br><br> For select customers: Whether or not the seller sends publisher_id in the bid request  |
| `expose_tags` | bool | **Not Used.** <br><br> For select customers: Whether or not the seller sends the id of the tag in the bid request |
| `expose_universal_categories` | bool | **Not Used.** |
| `url_exposure` | "full", "domain", "hidden" | If the seller sends the full url of impression, the domain only, or the url is completely hidden. If the url_exposure is "hidden", you may still receive the seller's default URL if the seller has one configured for that impression. |

## Bidder

| JSON variable | Type | Description |
|---|---|---|
| `id` | int | The ID of the bidder that the member uses to buy impressions |
| `name` | string | The name of the bidder that the member uses to buy impressions |

## Example

### Authentication token

Authentication is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use. Please see [Authentication Service](authentication-service.md) for more detailed instructions.

### View information about the member

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/platform-member/1'
{
   "response":{
      "status":"OK",
      "platform_members": [
       {
         "id": 1,
         "name": "My Company",
         "primary_type": "network",
         "platform_exposure": "public",
         "email": "admin@mycompany.com",
         "daily_imps_verified": null,
         "daily_imps_self_audited": null,
         "daily_imps_unaudited": null,
         "is_iash_compliant": false,
         "visibility_rules": {
           "expose_publishers": true,
           "expose_tags": true,
           "expose_age": true,
           "expose_gender": true,
           "expose_universal_categories": true,
           "url_exposure": "full"
         },
         "bidder": {
           "id": "2",
           "name": "DisplayWords"
         }
      }]
   }
}
```

## Related topics

- [Member Service](member-service.md)
- [Read-Only Services](read-only-services.md)
- [API Services](api-services.md)
