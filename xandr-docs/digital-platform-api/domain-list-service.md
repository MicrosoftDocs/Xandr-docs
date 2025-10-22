---
title: Digital Platform API - Domain List Service
description: Use the Domain List service to define a list of domains that can be included or excluded from a campaign's targeting profile.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Domain List service

> [!NOTE]
> Going forward, "allowlist" and "blocklist" terminology will be followed for our APIs. This is a part of an ongoing effort to evaluate our current terminology usage and usher in more inclusive terminology for Xandr platforms.

The Domain List service lets you define a list of domains that can be included or excluded from a campaign's targeting profile. Domain lists in targeting profiles are used to place domains with similar characteristics in groups that you can use to easily include or exclude domains from campaign targeting. They're generally used as *allowlists* or *blocklists.* Allowlists contain domains that you want to include in your campaign targeting, and blocklists contain domains that you want to exclude. (See `domain_list_targets` and `domain_list_action` in the [Profile Service](./profile-service.md) to see how to include these lists in your profiles).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/domain-list` | View all domain lists. |
| `GET` | `https://api.appnexus.com/domain-list?id=DOMAIN_LIST_ID` | View a specific domain list. |
| `GET` | `https://api.appnexus.com/domain-list?search=SEARCH_TERM` | Search for domain lists with names or descriptions containing certain characters. |
| `POST` | `https://api.appnexus.com/domain-list` | Add a new domain list. |
| `PUT` | `https://api.appnexus.com/domain-list?id=DOMAIN_LIST_ID` | Modify an existing domain list. |
| `DELETE` | `https://api.appnexus.com/domain-list?id=DOMAIN_LIST_ID` | Delete an existing domain list. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `description` | string(100) | A description of the domain list. |
| `domains` | array | Array of domains in the format `["domain1.com", "domain2.com", ... , "domain10.com"]`.<br><br>**Note**: `"www"` is stripped from domains.<br>Domains which begin with `"www"` will have the `"www"` substring stripped out before being stored in our system. For example, `"www.example.org"` will be shortened to `"example.org"`. |
| `id` | int | The internal system identifier for the domain list.<br>**Required On**: `PUT` |
| `last_modified` | string | Read-only timestamp of when the domain list was last changed. |
| `name` | string(100) | The name of the domain list as specified by the user. This name must be unique.<br>**Required On**: `POST` |
| `type` | string | The type of domain list. Possible values are `black` and `white`. This value is strictly informational; it does not determine whether the list is included or excluded in targeting.<br>**Default**: `"white"` |

## Examples

### Adding a domain list

```
$ cat domain-list

{
   "domain-list":{
      "name":"Domains to target",
      "description":"A list of the domains to target for Campaign A",
      "type":"white",
      "domains":["domain-a.com", "domain-b.net", "domain-c.org"]
   }
}

$ curl -b cookies -c cookies -X POST --data-binary @domain-list 'https://api.appnexus.com/domain-list'

{
   "response":{
      "status":"OK",
      "id":9
   }
}
```

### Viewing domain list `9`

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/domain-list?id=9'

{
   "response":{
      "domain-list":{
         "id":9,
         "name":"Domains to target",
         "description":"A list of the domains to target for Campaign A",
         "type":"white",
         "domains":["domain-a.com", "domain-b.net", "domain-c.org"]
      }
      "status":"OK"
   }
}
```

### Adding domain lists to profile `35` as a `"allowlist"`

```
$ cat domain-list-profile

{
   "profile":{
      "id":35,
      "domain_list_targets":[{"id":9}, {"id":10}, {"id":15}, {"id":18}],
      "domain_list_action":"include",
   }
}

$ curl -b cookies -c cookies -X PUT --data-binary @domain-list-profile 'https://api.appnexus.com/profile?id=35'

{
   "response":{
      "status":"OK",
      "id":35
   }
}
```

### Searching for domain lists with names or descriptions containing `"test"`

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/domain-list?search=test'

{
  "response": {
    "status": "OK",
    "domain-lists": [
      {
        "id": 1733,
        "name": "Add Test",
        "description": "",
        "type": "white",
        "domains": [
          "amblergazette.com",
          "facebook.com",
          "google.com",
          "zwire.com"
        ],
        "last_modified": "2011-03-10 18:03:07"
      }
      }
```

## Related topics

- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
