---
title: Member Profile Service
description: Use the Member Profile service to create a global profile to limit third-party impressions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member Profile service

The Member Profile Service allows you to establish a single, global profile to limit the countries/regions and domains from which you accept third-party impressions. Your campaigns will not bid on third-party impressions that do not match the requirements of the member profile.

## Align campaign profiles with member profile

Be sure to align your campaign [profiles](./profile-service.md) with your member profile; otherwise, your campaign targeting may not be effective.

- **Example 1**: Your member profile is set to accept third-party impressions from the US and Canada. A campaign is set to target impressions from the US, Canada, and Mexico. In this case, the campaign will never have the chance to target impressions from Mexico because the member profile prevents those impressions from being available for bidding.
- **Example 2**: Your member profile is set to block third-party impressions from domain list 1, which includes apples.com, oranges.com, and pears.com. A campaign is set to target domain list 3, which includes plums.com, bananas.com, and apples.com. Note that apples.com is included in both domain list 1 and domain list 3. In this case, the campaign will never have the chance to target impressions from apples com because the member profile blocks domain list 1.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/member-profile` <br>(member-profile JSON) | Create your member profile |
| `PUT`  | `https://api.appnexus.com/member-profile` <br>(member-profile JSON) | Update your member profile |
| `GET`  | `https://api.appnexus.com/member-profile` | View your member profile |
| `DELETE`  | `https://api.appnexus.com/member-profile` | Delete your member profile |
| `GET`  | `https://api.appnexus.com/member-profile/meta` | Find out which fields you can filter and sort by |

> [!NOTE]
> Since you have only one member profile, you do not need to include the profile ID in `PUT`, `GET`, or `DELETE` requests.

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the member profile. |
| `domain_list_action` | enum | The action to perform on `domain_list_targets`. <br><br>Possible values:<br> - `"include"` - You will accept third-party impressions only from the domains in the specified domain lists. <br> - `"exclude"` - You will accept third-party impressions from all domains except those in the specified domain lists.<br><br>**Default**: `"exclude"` |
| `domain_list_targets` | array | The [domain lists](./domain-list-service.md) to include or exclude. See the [examples](#examples) below for formatting. |
| `country_targets` | array | The countries/regions from which you will accept third-party impressions. You will accept impressions only from these countries/regions. Note that if you do not specify any countries/regions, you will accept third-party impressions from all countries/regions. See [examples](#examples) below.   |
| `last_modified` | date | **Read-only**. The date on which the member profile was last modified. |
| `inventory_url_list_targets` | array of objects | Contains a list of inventory list IDs (allowlists and/or blocklists). Used to attach a single allowlist and/or one or more blocklists to the profile.<br><br> - The allowlist contains a list of domains or apps to be targeted by the line item using the profile. If an allowlist is included, domains and apps not in the allowlist will not be targeted.<br><br> - Each blocklist contains a list of domains or apps that are to be excluded from targeting by line item that uses the profile.<br><br>See **Inventory Lists** in [Profile Service](./profile-service.md) for more details. |
| `require_transparency_and_consent_framework_string` | boolean | If `true`, only allow associated objects to purchase inventory where valid TCF string is present<br><br>If `false`, allow associated objects to purchase any inventory that falls within pre-defined targeting declarations.<br><br>**Note**: This parameter is only applicable to the traffic coming from territories where GDPR applies.<br><br>**Default**: `false` |

## Examples

### Creating your member profile

```
$ cat profile { "member-profile": { "domain_list_action": "include", "domain_list_targets": [ { "id": 23620 }, { "id": 23625 } ], "country_targets": [ { "id": 1 }, { "id": 2 } ] } } $ curl -b cookies -X POST -d @profile 'https://api.appnexus.com/member-profile' { "response": { "status": "OK", "id": 121740 } } 
```

### Updating your member profile to accept third-party impressions from an additional country

```
$ cat profile_update { "member-profile": { "country_targets": [ { "id": 233 }, { "id": 59 } ] } } $ curl -b cookies -X PUT -d @profile_update 'https://api.appnexus.com/member-profile' { "response": { "status": "OK", "id": 121740 } } 
```

### Viewing your member profile

```
$ curl -b cookies 'https://api.appnexus.com/member-profile' { "response": { "status": "OK", "member-profile": { "id": 121740, "domain_list_action": "include", "country_targets": [ { "id": 233, "name": "United States", "code": "US"  }, {  "id": 58, "name": "Czech Republic", "code": "CZ" }, { "id": 59, "name": "Germany", "code": "DE" } ], "domain_list_targets": [ { "id": "23620", "name": "Domain List 1", "description": "Include Domain List 1", "type": "white" }, { "id": "23625", "name": "Domain List 2", "description": "Include Domain List 2", "type": "white" } ], "last_modified": "2011-12-15 16:57:51" }, "count": 1, "start_element": 0, "num_elements": 100 } } 
```

### Require transparency and consent framework string

```
{
    "profile": {
        "require_transparency_and_consent_framework_string": "false",
         
    }
}
```
