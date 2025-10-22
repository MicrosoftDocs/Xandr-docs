---
title: Identity Type Service
description: Explore the Identity Type service, including its JSON fields, methods for retrieval, creation, update, and deletion of an identifier illustrated with detailed examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Identity Type service

> [!NOTE]
> This service currently is in Alpha. It is still under development and may be subject to change without notice. Contact your Microsoft Account Representative to get it enabled.

The Identity Type service in Identity Management Framework can be used to retrieve, create, update and delete an identifier in the platform. Additionally this service allows owners to manage permissions for their identity solutions. Using this service, identity owners can:

- Determine the publisher(s) that are permitted to utilize their identifier within the bidstream.
- Decide the partner(s) on the platform who can incorporate data using their identifier.
- Choose the external bidder(s) who are eligible to access their identifier.
- Select the partner(s) on the platform who are eligible to receive the identifier's value in their log level data feeds.

> [!IMPORTANT]
> To register or create a new identifier, contact your Microsoft Account Representative as this functionality is restricted to Microsoft Admin role.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/identity-type?id=IDENTITY_ID1](https://api.appnexus.com/identity-type?id=IDENTITY_ID1) | View a specific identifier by its ID. Here, `IDENTITY_ID1` is example of an identifier's ID. |
| `GET` | [https://api.appnexus.com/identity-type?id=IDENTITY_ID1,IDENTITY_ID2,IDENTITY_ID3](https://api.appnexus.com/identity-type?id=IDENTITY_ID1,IDENTITY_ID2,IDENTITY_ID3) | View multiple identifiers by their IDs using a comma-separated list. |
| `GET` | [https://api.appnexus.com/identity-type?source=SOURCE1](https://api.appnexus.com/identity-type?source=SOURCE1) | View a specific identifier by a source such as LiveRamp, Warner Media, etc. Here, `SOURCE1` is an example of the source of an identifier. |
| `GET` | [https://api.appnexus.com/identity-type?source=SOURCE1,SOURCE2](https://api.appnexus.com/identity-type?source=SOURCE1,SOURCE2) | View multiple identifiers by source using a comma-separated list. |
| `GET` | [https://api.appnexus.com/identity-type?member_owner_id=OWNERID1](https://api.appnexus.com/identity-type?member_owner_id=OWNERID1) | View identifier(s) by the ID of an identity owner. |
| `GET` | [https://api.appnexus.com/identity-type?member_owner_id=OWNERID1,OWNERID2](https://api.appnexus.com/identity-type?member_owner_id=OWNERID1,OWNERID2) | View multiple identifiers by multiple IDs of owners using a comma-separated list. |
| `PUT` | [https://api.appnexus.com/identity-type?id=IDENTITY_ID1](https://api.appnexus.com/identity-type?id=IDENTITY_ID1) | Update a specific identifier by its ID. |
| `POST` | [https://api.appnexus.com/identity-type](https://api.appnexus.com/identity-type) | Add an identifier using payload JSON as shown in the example.<br> **Microsoft admin only field.** |
| `DELETE` | [https://api.appnexus.com/identity-type?id=IDENTITY_ID1&member_id=MEMBER_ID1](https://api.appnexus.com/identity-type?id=IDENTITY_ID1&member_id=MEMBER_ID1) | Delete an existing identifier belong to a member.<br> **Microsoft admin only field.** |

## JSON fields

### Registration fields with admin-only control

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | Microsoft created ID of the identifier.<br>**Read Only.**<br>**Required On:** `PUT` and `DELETE`. |
| `member_owner_id` | int | The member ID of the identifier owner (typically a publisher).<br>**Required On:** `POST`<br>Microsoft admin write only field. |
| `source` | string | The source of the identifier. For example, LiveRamp, Warner Media, etc. The source needs to unique to the identifier.<br>**Required On:** `POST` |
| `requires_platform_resolution` | boolean | Is platform resolution required by an identifier for encoding and decoding.<br>**Required On:** `POST` |
| `requires_seat_resolution` | boolean | Is seat resolution required by identifier for each bidder (RampID). |
| `identity_resolver_check` |  |  |
| `is_auction_usage_single_context` | boolean | The identifier context set for relevant privacy usage (CPRA). If the identifier is used to identify a user on 2 or more domains/websites, this should be set to `false`.<br>**Required On:** `POST` |
| `is_passthrough` | boolean | The master settings to allow frequency capping and audience segmentation on the platform.<br>**Default:** `False` |
| `requires_rti_partner_match` | boolean | The field required for The Trade Desk related identifiers. |
| `rti_partner` | boolean | The field required for The Trade Desk related identifiers. |
| `is_experimental` | boolean | The field used for FLoC/ Topics. For more information on FLoC, see [Federated Learning of Cohorts (FLoC)](https://privacysandbox.com/proposals/floc/) |
| `opt_out_default` | boolean | When `true`, the industry type identifier is opted out by default and *vice versa*.<br>When the identity type is opted in, there is no need to consult the identity resolver to verify if there is any opt-out. However, when the identity type is initially opted out by default, the identity resolver must determine whether the identifier should be opted in or out. |
| `enforce_adx_specification` | boolean | The field specifies if the drive validation ID length in Impression Bus is greater than 32. |

### The master control settings for an identifier owner

| Field | Type | Description |
|:---|:---|:---|
| `status` | string | The status of the identifier whether its `active` or `inactive`. |
| `auction_participation_control` | object | The master setting to control whether other publishers can employ this identifier and specify the ones who are permitted to do so. For more details, see [Auction Participation Contols](#auction-participation-control) below. |
| `audience_segmentation_control` | object | The master setting to control permissions to other members for audience segmentation using the identifier. This field in request defines list of members for which segment onboarding is allowed for the registered identifier. |
| `external_bidder_control` | object | The master setting to control if the identifier can be sent to the external bidders and specify the eligible external bidders. This field defines default list of bidders who will be receiving the newly registered source and identifier. By default, member participants can use the bidders defined at the identifier level or they can override using the identity type participant API. |
| `lld_exposure_control` | object | The master setting to regulate if the identifier can be utilized in log-level data (LLD) and determine the authorized recipients. This field defines the list of members who will be able see actual ID values in LLD feed for the newly registered source and identifier. By default, member participants can use the members defined at the identifier level or they can override the identity type participant API. |

### Auction participation control

The master setting to control whether other publishers can employ this identifier and specify the ones who are permitted to do so. This field in request defines list of member for which auction is enabled. Auction enabled members become the participants for an identifier in the framework.

| Field | Type | Description |
|:---|:---|:---|
| `allow_participation` | string | Sellers enabled for auction participation:<br>Options:<br>- `"all"`<br> - `"none"`<br> - `“include_subset”` |
| `participant_member_list` | array of integers | List of `member_id` enabled for: `“include_subset”` |

### Audience segmentation control

The master setting to control permissions to other members for audience segmentation using the identifier. This field in request defines list of members for which segment onboarding is allowed for the registered identifier.

| Field | Type | Description |
|:---|:---|:---|
| `allow_segmentation` | string | Members enabled for audience segmentation:<br>Options:<br> - `"all"`<br> - `"none"`<br> - `“include_subset”` |
| `segmentation_member_list` | array of integers | List of `member_id` enabled for: `“include_subset”` |

### External bidder control

The master setting to control if the identifier can be sent to the external bidders and specify the eligible external bidders. This field defines default list of bidders who will be receiving the newly registered source and identifier. By default, member participants can use the bidders defined at the identifier level or they can override using the identity type participant API.

| Field | Type | Description |
|:---|:---|:---|
| `allow_bidders` | array | External bidders Members enabled to recieve the identifier:<br>Options:<br> - `"all"`<br> - `"none"`<br> - `“include_subset”` |
| `external_bidder_list` | array of integers | List of `member_id` enabled for: `“include_subset”` |

### Log-level data exposure control

The master setting to regulate if the identifier can be utilized in log-level data (LLD) and determine the authorized recipients. This field defines the list of members who will be able see actual ID values in LLD feed for the newly registered source and identifier. By default, member participants can use the members defined at the identifier level or they can override the identity type participant API where publishers have the option to utilize the participant service to exert additional control over how the identifier they provide is employed and surfaced by the platform.

| Field | Type | Description |
|:---|:---|:---|
| `lld_exposure_allowed` | array | Members enabled to receive identifier values in LLD.<br>Options:<br> - `"all"`<br> - `"none"`<br> - `“include_subset”`<br> - `"participant_only"` |
| `exposure_member_list` | array of integers | List of `member_id` enabled for: `“include_subset”` |

## Examples

### Create an identifier

```
$ cat new_identifier.json
{
  "identity_type": {
      "source": "test.com",
      "member_owner_id": 958,
      "requires_platform_resolution": true,
      "identity_resolver_check": true,
      "is_auction_usage_single_context": true,
      "is_passthrough": true,
      "requires_seat_resolution": false,
      "requires_rti_partner_match": false,
      "rti_partner": "",
      "is_experimental": false,
      "opt_out_default": false,
      "status": "active",
      "enforce_adx_specification": false,
      "auction_participation_control": {
        "allow_participation": "include_subset",
        "participant_member_list": [
          123,
          456
        ]
      },
      "audience_segmentation_control": {
        "allow_segmentation": "include_subset",
        "segmentation_member_list": [
          456
        ]
      },
      "external_bidder_control": {
        "allow_bidders": "all",
        "external_bidder_list": [
          111,
          112
        ]
      },
      "lld_exposure_control": {
        "lld_exposure_allowed": "include_subset",
        "exposure_member_list": [
          311,
          312
        ]
      }
    }
  }
$ curl -b cookie -c cookie -X POST  'https://api.appnexus.com/identity-type'
{
    "response": {
        "status":"OK",
        "id":IDENTITY_ID_001
        }
        }
```

> [!NOTE]
> For newly registered sources, IDs are generated in the incremental order, whereas the rest of the field values are stored in the database based on the request sent through the API.

### View the details of a specific identifier

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/identity-type?id=IDENTITY_ID_001'
{
  "response": {
    "status": "OK",
    "identity_type": {
        "id": IDENTITY_ID_001,
        "source": "test.com",
        "member_owner_id": 958,
        "requires_platform_resolution": true,
        "identity_resolver_check": true,
        "is_auction_usage_single_context": true,
        "is_passthrough": true,
        "requires_seat_resolution": false,
        "requires_rti_partner_match": false,
        "rti_partner": "",
        "is_experimental": false,
        "opt_out_default": false,
        "status": "active",
        "enforce_adx_specification": false,
        "auction_participation_control": {
          "allow_participation": "include_subset",
          "participant_member_list": [
            123,
            456
          ]
        },
        "audience_segmentation_control": {
        "allow_segmentation": "include_subset",
        "segmentation_member_list": [
          456
         ]
        },
        "external_bidder_control": {
        "allow_bidders": "all",
        "external_bidder_list": [
          111,
          112
         ]
        },
        "lld_exposure_control": {
        "lld_exposure_allowed": "include_subset",
        "exposure_member_list": [
          311,
          312
        ]
      }
    }
  }
}
```

## Related topic

[Identity Type Participant Service](identity-type-participant-service.md)
