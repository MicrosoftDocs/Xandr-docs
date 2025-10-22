---
title: Bidders - Ad Profile Service
description: In this article, learn how to create ad approval profiles using the Ad Profile Service.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Ad profile service

A member who owns inventory may want to create "ad approval profiles" to define what kinds of ads can and cannot run on their pages for quality control purposes. The Ad Profile Service lets you create your ad approval profiles. Once an ad profile has been created, it can either be associated to individual TinyTags through the [TinyTag Service](tinytag-service.md) or broadly set at the member level through the [Member Service](member-service.md).

Approval profiles consist of three elements: members, brands, and creatives. When creating an ad profile, you can approve or ban each creative in the system individually, but you may prefer to save time by approving or banning entire brands or members.

- A member should be trusted if you believe their ads will **always** be acceptable. For instance, you may "trust" Specific Media to run quality ads, so you can mitigate the need to audit each of their creatives.
- A brand should be trusted if you believe that ads of this brand will **almost always** be acceptable. However, you will always have the ability to ban a specific creative even if it is part of a "trusted" brand. If the specific creative is not banned, it will run by default.
- A brand should be banned if you believe that ads of this brand will **never** be acceptable. You will **not** have the ability to approve a specific creative assigned by a "banned" brand.
- The default profile (blank or ID set to 0) will ban unaudited ads from other members (i.e. where the `member_id` of the creative is different than the `member_id` of the TinyTag).

## Rest API

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/ad-profile/MEMBER_ID` | View all ad profiles for a member. |
| GET | `https://api.adnxs.com/ad-profile/MEMBER_ID/AD_PROFILE_ID` | View a particular ad profile. |
| POST | `https://api.adnxs.com/ad-profile/MEMBER_ID` | Add a new ad profile. |
| PUT | `https://api.adnxs.com/ad-profile/MEMBER_ID/AD_PROFILE_ID` | Modify an existing ad profile. |
| DELETE | `https://api.adnxs.com/ad-profile/MEMBER_ID/AD_PROFILE_ID` | Delete an existing ad profile. |

## JSON fields

> [!NOTE]
> "Brands" and "creatives" make up subsections of the ad profile.

### Ad profile

| Field | Type | Description |
|---|---|---|
| `active` | boolean | **Default**: true <br> The state of the ad profile (active/inactive). |
| `default_brand_status` | enum ('trusted', 'banned') | The brand status to be used by default when no explicit selection is made. |
| `description` | string | Optional description |
| `id` | int | **Required On**: Update <br> Xandr ID assigned by the API to reference this ad_profile. |
| `last_activity` | timestamp | The timestamp of last modification to this ad profile. |
| `member_id` | int | **Required** <br> The member ID that owns this ad_profile. |

### Brands

| Field | Type | Description |
|---|---|---|
| `id` | int | **Required** <br> The ID of the brand within Xandr's brand list. |
| `status` | enum ('trusted', 'banned') | **Required** <br> The trust setting for the specified brand. <br><br> **Note**: If a `brand`'s `status` is set to `"trusted"`, creatives associated with that brand will serve even if the brand's overall category is `"banned"`. For example, if you mark the brand "1 and 1 Internet" (ID 17310) as trusted, creatives associated with that brand will serve even if you ban its category, "Telecommunications" (ID 27). To get brand IDs and see what category a brand belongs to, use the **Brand Service**. For category IDs, use the **Category Service**. |

### Creatives

| Field | Type | Description |
|---|---|---|
| `approved` | boolean | **Required** <br> Whether the creative specified is an approved or banned. |
| `id` | int | **Required** <br> The ID of the creative within the Xandr set of exchange creatives. |

### Members

| Field | Type | Description |
|---|---|---|
| `id` | int | Member ID. |
| `status` | enum ('trusted', 'banned') | The action to be used for a member's creatives within the ad profile. |

## Example

### To create a new ad profile, create a text file in JSON format

Below we have used the "cat" command to output an example ad profile JSON file.

```
$ cat ad_profile
{
   "ad_profile":{
      "member_id":25,
      "brands":[
         {
            "id":23,
            "status":"trusted"
         },
         {
            "id":120,
            "status":"banned"
         },
         {
            "id":123,
            "status":"banned"
         }
      ],
      "creatives":[
         {
            "id":4,
            "approved":true
         },
         {
            "id":12,
            "approved":true
         },
         {
            "id":123,
            "approved":false
         }
      ]
   }
}
```

### Add this ad profile to your member (25) with a POST request

```
$ curl -b cookies -c cookies -d @ad_profile  "https://api.adnxs.com/ad-profile/25"
{
    "response": {
        "status": "OK",
        "id": "50"
    }
}
```

### The ID of the ad profile is 50. You can view it with a GET request.

```
$ curl -b cookies -c cookies "https://api.adnxs.com/ad-profile/25/50"
{
   "response":{
      "ad_profile":[
         {
            "id":50,
            "member_id":25,
            "brands":[
               {
                  "id":"23",
                  "status":"trusted"
               },
               {
                  "id":"120",
                  "status":"banned"
               },
               {
                  "id":"123",
                  "status":"banned"
               }
            ],
            "creatives":[
               {
                  "id":"4",
                  "approved":"true"
               },
               {
                  "id":"12",
                  "approved":"true"
               },
               {
                  "id":"123",
                  "approved":"false"
               }
            ],
            "active":true,
            "last_activity":"2009-01-03 05:29:57"
         }
      ],
      "status":"OK"
   }
}
```
