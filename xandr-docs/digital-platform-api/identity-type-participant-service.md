---
title: Identity Type Participant Service
description: Learn about the Identity Type Participant service, their JSON fields, ways to manage permissions for all identity solutions, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Identity Type Participant service

> [!NOTE]
> This service currently is in Alpha. It is still under development and may be subject to change without notice. Contact your Xandr Account Representative to get enabled.

The Identity Type Participant service in Identity Management Framework allows identity framework participants to manage permissions for all identity solutions that they are leveraging. With the Identity Type Participant service, each publisher participant can:

- Choose the external bidder(s) permitted to access their identifier.
- Determine the partner(s) on the platform that are entitled to receive the identifier's value within their log data feeds.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/identity-type-participant](https://api.appnexus.com/identity-type-participant) | View all the participants in the platform. |
| `GET` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1) | View details of a participants of a specific identifier. Here, `IDENTITY_ID1` of the identifier is passed as query string in the method. |
| `GET` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1,IDENTITY_ID2,IDENTITY_ID3](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1,IDENTITY_ID2,IDENTITY_ID3) | View participants mapped to multiple identifiers using a comma-separated list. |
| `GET` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1&participant_member_id=MEMBER_ID1](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1&participant_member_id=MEMBER_ID1) | View participants mapped to an identifier and filters by a member. |
| `GET` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1&participant_member_id=MEMBER_ID1,MEMBER_ID2,MEMBER_ID3](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1&participant_member_id=MEMBER_ID1,MEMBER_ID2,MEMBER_ID3) | View participants that are mapped to an identifier and filters by multiple members. |
| `POST` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1) | Add an identity type participant under a specific identifier. Here, `IDENTITY_ID1` is an example of an identifier of the publisher participant.<br> Participant and Microsoft admin only field. |
| `PUT` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1) | Update an existing identity type participant details.<br> Participant and Microsoft admin only field. |
| `DELETE` | [https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1&participant_member_id=MEMBER_ID1](https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID1&participant_member_id=MEMBER_ID1) | Delete an existing identity type participant.<br> Participant and Microsoft admin only field. |

## JSON fields

### Registration fields for Identity Type Participant

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | Microsoft created ID of the identity type participant.<br>**Read Only.**<br>**Required On:** `POST`, `PUT`, and `DELETE`. |
| `participant_member_id` | int | The member ID to which the identity type participant belong.<br>**Required On:** `POST`, `PUT`, and `DELETE`. |

### Control settings for an Identity Type Participant service

| Field | Type | Description |
|:---|:---|:---|
| `external_bidder_control` | object | Setting that enables sending of identifiers to the external bidders and specifies the eligible ones. For more information, see [External Bidder Control](#external-bidder-control) below. |
| `lld_exposure_control` | object | Setting that configures if the identifier can be utilized in log-level data (LLD) and determine the authorized recipients. For more information, see [Log Level Data Exposure Control](#log-level-data-exposure-control) below. |

### External bidder control

The master setting to control if the identifier can be sent to the external bidders and specifies the eligible external bidders. This field defines default list of bidders who will be receiving the newly registered source and identifier. By default, member participants can use the bidders defined at the identifier level.

| Field | Type | Description |
|:---|:---|:---|
| `allow_bidders` | string  | External bidders' members enabled to recieve the identifier:<br>Options:<br> - `“use_master_settings”`<br>- `“none”`<br> - `“include_subset”` |
| `external_bidder_list` | array of integers | List of `member_id` enabled for: `“include_subset”`.  |

### Log-level data exposure control

The participant setting to regulate if the identifier can be utilized in log-level data (LLD) and determine the authorized recipients. This field defines the list of members who will be able to see actual ID values in LLD feed for the newly registered source and identifier. By default, member participants can use the members defined at the identifier level.

| Field | Type | Description |
|:---|:---|:---|
| `lld_exposure_allowed` | string  | Members enabled to receive identifier values in LLD. <br>Options:<br> - `“use_master_settings”`<br>- `“none”`<br> - `“include_subset”` |
| `exposure_member_list` | array of integers | List of `member_id` enabled for: `“include_subset”`.  |

## Examples

### Create an Identity Type Participant

```
$ cat identity_type_participant.json
{
  "identity_type_particpant": {
    "id": 103,
    "participant_member_id": "113",
    "external_bidder_control": {
      "allow_bidders": "use_master_settings",
      "external_bidder_list": []
    },
    "lld_exposure_control": {
      "lld_exposure_allowed": "include_subset",
      "exposure_member_list": [
        312
      ]
    }
  }
}
$ curl -b cookie -c cookie -X POST  'https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID001'
{
    "response": {
        "status":"OK",
        "id":103
        }
}
```

### View details of an Identity Type Participant

```
$ curl -b cookie -c cookie 'https://api.appnexus.com/identity-type-participant?id=IDENTITY_ID001&participant_member_id=113'
{
    "response": {
        "status":"OK",
        "identity_type_particpant": {
              "id": 103,
              "participant_member_id": "113",
              "external_bidder_control": {
                    "allow_bidders": "use_master_settings",
                    "external_bidder_list": []
                  },
                "lld_exposure_control": {
                    "lld_exposure_allowed": "include_subset",
                    "exposure_member_list": [312]
                  }
               }
          }
}
```

## Related topic

[Identity Type Service](identity-type-service.md)
