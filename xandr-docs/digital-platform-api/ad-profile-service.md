---
title: Digital Platform API - Ad Profile Service
description: In this article, learn about Digital Platform API's Ad Profile service, their JSON fields, and REST API with thorough examples.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Ad profile service

A network may want to create "ad approval profiles" to define what kinds of brands and creatives can and cannot run on their publishers' pages. The Ad Profile Service lets you create your ad approval profiles at the member level or the publisher level. To create them at the publisher level, include a publisher ID. If no publisher ID is included, it will be a network-level profile available for use with all publishers.

Ad profiles consist of several elements: members, brands, creatives, language, technical attributes, categories, and ad servers. When creating an ad profile, you can approve or ban each creative in the system individually, but you may prefer to save time by approving or banning entire brands or members.

- **A member should be trusted:** If you believe their ads will always be acceptable. For instance, you may "trust" Network A to run quality ads, so you can mitigate the need to audit each of their creatives.
- **A brand should be trusted:** If you believe that ads of this brand will almost always be acceptable. However you will always have the ability to ban a specific creative even if it is part of a "trusted" brand. If the specific creative is not banned, it will run by default.
- **A brand should be banned:** If you believe that ads of this brand will never be acceptable. You will still have the ability to approve a specific creative assigned a "banned" brand, unless the member is banned.
- The default profile (blank or ID set to `0`) will ban unaudited ads from other members (i.e. where the `member_id` of the creative is different than the `member_id` of the TinyTag).

> [!NOTE]
> A brand can have a Parent Brand, as a way of gathering brands by parent company/ child company. If a seller blocks/approves a parent brand, all child brands without an \*explicit\* approve/block setting will match the parent brand setting.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/ad-profile](https://api.appnexus.com/ad-profile) | View all ad profiles for a member. |
| `GET` | [https://api.appnexus.com/ad-profile?id=AD_PROFILE_ID](https://api.appnexus.com/ad-profile?id=AD_PROFILE_ID) | View a particular ad profile. |
| `GET` | [https://api.appnexus.com/ad-profile?publisher_id=PUBLISHER_ID](https://api.appnexus.com/ad-profile?publisher_id=PUBLISHER_ID) | View all ad profiles for a specific publisher. |
| `POST` | [https://api.appnexus.com/ad-profile](https://api.appnexus.com/ad-profile)<br>(`ad_profile` JSON) | Add a new ad profile at the member level. |
| `POST` | [https://api.appnexus.com/ad-profile?publisher_id=PUBLISHER_ID](https://api.appnexus.com/ad-profile?publisher_id=PUBLISHER_ID)<br>(`ad_profile` JSON) | Add a new ad profile at the publisher level. |
| `PUT` | [https://api.appnexus.com/ad-profile?id=AD_PROFILE_ID](https://api.appnexus.com/ad-profile?id=AD_PROFILE_ID)<br>(`ad_profile` JSON) | Modify an existing ad profile. |
| `DELETE` | [https://api.appnexus.com/ad-profile?id=AD_PROFILE_ID](https://api.appnexus.com/ad-profile?id=AD_PROFILE_ID) | Delete an existing ad profile. |
| `GET` | [https://api.appnexus.com/ad-profile?sort=description](https://api.appnexus.com/ad-profile?sort=description) | Sort ad profiles alphabetically by description. |
| `GET` | [https://api.appnexus.com/ad-profile?search=text_of_description](https://api.appnexus.com/ad-profile?search=text_of_description) | Search for an ad profile by its description. |

## JSON fields

| Fields | Type | Description |
|:---|:---|:---|
| `id` | int | Xandr ID assigned by the API to reference this `ad_profile`.<br>**Required On:** `PUT`, in query string. |
| `state` | enum | The state of the ad profile. Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"` |
| `member_id` | int | The member ID that owns this `ad_profile`. |
| `description` | string | Optional description. |
| `apply_aq_on_psp` |  boolean | If set to true [plain text], checks bids from Prebid Server Premium demand partners against brand and category blocks in the ad profile or `badv` [plain text] / `bcat` [plain text] fields of the bid request. Uses `seatbid.bid.adomain [plain text]` field to infer brand. |
| `reject_unknown_adomain_on_psp` | boolean | Related to apply_aq_on_psp [plain text]. When set to true [plain text], rejects bids from [Prebid Server Premium](prebid-server-premium.md) demand partners where seatbid.bid.adomain [plain text] values are missing or have not yet been mapped to brands. Also checks bids from [Prebid Server Premium](prebid-server-premium.md) demand partners against brand and category blocks in the ad profile or `badv` [plain text] / `bcat` [plain text] fields of the bid request. Uses `seatbid.bid.adomain [plain text]` field to infer brand. |
| `default_member_status` | enum | The member status to be used by default when no explicit selection is made. Possible values:<br> - `"case-by-case"`: This member's creatives must pass all brand, language, technical attribute, category, and ad server filtering defined on the ad profile<br> - `"banned"`: None of this member's creatives are allowed to serve. |
| `default_brand_status` | enum | The brand status to be used by default when no explicit selection is made. Possible values: `"trusted"` or `"banned"`. |
| `default_language_status` | enum | The language status to be used by default when no explicit selection is made. Possible values: `"trusted"` or `"banned"`. |
| `default_ad_server_status` | enum | The ad server status to be used by default when no explicit selection is made. Possible values: `"trusted"` or `"banned"`. |
| `default_category_status` | enum | The category status to be used by default when no explicit selection is made. Possible values: `"trusted"` or `"banned"`. |
| `default_technical_attribute_status` | enum | The technical attribute status to be used by default when no explicit selection is made. Possible values: `"trusted"` or `"banned"`. |
| `default_audit_type` | enum | The audit status to be used by default when no explicit selection is made. Possible values:<br> - `"platform"`: Creatives must have undergone the Xandr platform audit.<br> - `"platform_or_self"`: Creatives must have been self-audited by the member, or undergone Xandr audit. |
| `members` | array of objects | Array of members with their status. For more details, see [Members](#members) below. |
| `brands` | array of objects | Array of brands (Parent brands and Child brands) with their status. For more details, see [Brands](#brands) below. |
| `creatives` | array of objects | Array of creatives with their status. For more details, see [Creatives](#creatives) below. |
| `languages` | array of objects | Array of languages with their status. For more details, see [Languages](#languages) below. |
| `ad_servers` | array of objects | Array of ad servers with their status. For more details, see [Ad Servers](#ad-servers) below. |
| `categories` | array of objects | Array of categories with their status. For more details, see [Categories](#categories) below. |
| `technical_attributes` | array of objects | Array of technical attributes with their status. For more details, see [Technical Attributes](#technical-attributes) below. |
| `frequency_caps` | array of objects | Array of frequency/recency caps. For more details, see [Frequency Caps](#frequency-caps) below. |
| `total_creative_count` | int | Number of creatives. |
| `approved_creative_count` | int | Number of approved creatives. |
| `banned_creative_count` | int | Number of banned creatives. |
| `creatives_approved_percent` | double | Percentage of total creatives which are approved. |
| `creatives_unreviewed` | int | Number of creatives pending review. |
| `brands_unreviewed` | int | The number of brands pending review. |
| `exclude_unaudited` | boolean | Whether or not to exclude creatives that have not been audited. |
| `exclude_unaudited_direct` | boolean | Whether or not to exclude creatives that have not been audited for direct advertisers. |
| `audit_type_direct` | string | Specifies the type of audit required to serve creatives for direct advertisers. Allowed values: <br> - `"platform"`: Creatives must undergo Xandr platform audit.<br> - `"platform_or_self"`: Creatives must either be self-audited by the member, or undergo Xandr audit. |
| `check_attributes_direct` | boolean | Determines whether creatives with technical attributes can or cannot be run for direct advertisers. |
| `excluded_landing_page_urls` | array of URLs | Not available. Bans for competitive exclusions should be effected through brand exclusions. |
| `notes` | string | Optional notes. |
| `publisher_id` | int | The ID of the publisher to associate with the ad profile. |
| `last_modified` | timestamp | **Read Only.** The timestamp of last modification to this ad profile. |
| `require_seller_audit_default` | boolean | Whether or not seller audit is required.<br>**Default:** false |

### Members

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the member. |
| `status` | enum | Whether the member can or cannot run creatives on your publishers' pages. Allowed values:<br> - `"trusted"`: Any of this member's creatives may serve.<br> - `"case-by-case"`: This member's creatives must pass all brand, language, technical attribute, category, and ad server filtering defined on the ad profile.<br> - `"banned"`: None of this member's creatives are allowed to serve. |
| `audit_type` | enum | The type of audit you will require in order to serve creatives from this member. Allowed values:<br> - `"platform"`: Creatives must have undergone Xandr platform audit.<br> - `"platform_or_self"`: Creatives must have been self-audited by the member, or undergone Xandr audit. |
| `exclude_unaudited` | boolean | If `true`, unaudited creatives are excluded from this member. |
| `require_seller_audit_status` | enum | Whether the member can require its own audit for creatives from a given buyer:<br> - `"always"`: This member can always require audit for creatives from a given buyer.<br> - `"never"`: This member can never require audit for creatives from a given buyer.<br> - `"case-by-case"`: Fall back to `ad_profile.require_seller_audit_default` for audit required status. |

> [!TIP]
> The combination of the Member `status`, `audit_type`, and `exclude_unaudited` fields determines the buyer trust level shown in the Network Ad Quality profile.
>
> | `status` | `audit_type` | `exclude_unaudited` | Trust Level in UI |
> |:---|:---|:---|:---|
> | `banned` | N/A | N/A | Banned |
> | `case-by-case` | `platform` | `true` | Standard |
> | `case-by-case` | `platform_or_self` | `true` | Medium |
> | `trusted` | `platform` | `true` | High |
> | `trusted` | `platform` | `false` | Maximum |

### Brands

| Field | Type | Description |
|---|---|---|
| `id` | int | The ID of the brand. You can use the [Brand Service](brand-service.md) to retrieve brand IDs. |
| `status` | enum | Whether creatives of this brand can or cannot run on your publishers' pages. Possible values: `"trusted"` or `"banned"`.<br><br>**Note:** If a brand is marked as Eligible, creatives associated with this brand will serve even if the brand's category is Banned. For example, if you mark the brand "1 and 1 Internet (17310)" as Eligible it will serve even if you ban its overall category, "Telecommunications (27)". |
| `parent_brand_id` | int | When a brand has a parent brand, the default value is set to `null`.  |

### Creatives

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative. You can use the [Creative Service](creative-service.md) to retrieve creative IDs. |
| `approved` | boolean | If `true`, the creative can run on your publishers' pages. |

### Languages

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the language. You can use the [Language Service](language-service.md) to retrieve language IDs. |
| `status` | enum | Whether creatives of this language can or cannot run creatives on your publishers' pages. Possible values: `"trusted"` or `"banned"`. |

### Ad servers

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the ad server. You can use the [Ad Server Service](ad-server-service.md) to retrieve ad server IDs. |
| `status` | enum | Whether the ad server can or cannot run creatives on your publishers' pages. Possible values: `"trusted"` or `"banned"`. |

### Categories

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the category. You can use the [Category Service](category-service.md) to retrieve category IDs. |
| `status` | enum | Whether creatives with this category can or cannot run on your publishers' pages. Possible values: `"trusted"` or `"banned"`. |

### Technical attributes

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the technical attribute. You can use the [Technical Attribute Service](technical-attribute-service.md) to retrieve technical attribute IDs. |
| `status` | enum | Whether creatives with this technical attribute can or cannot run on your publishers' pages. Possible values: `"trusted"` or `"banned"`. |

### Frequency caps

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | **Read Only.** The ID of the frequency cap definition. |
| `member_id` | int | **Read Only.** The ID of the member that owns the ad profile. |
| `max_session_imps` | int | The maximum number of impressions per person per session for creatives with the specified `technical_attributes` or `categories`. If set, this value must be between `0` and `255`. |
| `max_day_imps` | int | The maximum number of impressions per person per day for creatives with the specified `technical_attributes` or `categories`. If set, this value must be between `0` and `255`. |
| `min_minutes_per_imp` | int | The minimum number of minutes between impressions per user for creatives with the specified `technical_attributes` or `categories`. |
| `cap_users_without_cookie` | boolean | If `true`, users without cookies will never be shown creatives with the specified `technical_attributes` or `categories`. They will be treated as if they've reached the frequency cap.<br>If `false`, no frequency cap for the specific `technical_attributes` or `categories` will apply to users without cookies. It will be possible for them to see an unlimited number of creatives with the specified `technical_attributes` or `categories`. |
| `technical_attributes` | array | The IDs of the technical attributes that you are limiting. You can use the [Technical Attribute Service](technical-attribute-service.md) to get a complete list of technical attributes. The `technical_attributes` and `categories` fields have an OR-relationship. |
| `categories` | array | The IDs of the categories that you are limiting. You can use the [Category Service](category-service.md) to get a complete list of categories. The `technical_attributes` and `categories` fields have an OR-relationship. |

## Examples

> [!WARNING]
> **Append on `PUT`**
>
> You will overwrite existing data with the contents of your `PUT` request unless you add the query string parameters `append=true` to the request. For more information, see [API Semantics](api-semantics.md) and the example **Update an existing ad profile** below.

### Create a new ad profile

This is a fairly complex profile. Below we have used the `cat` command to output an ad profile JSON file example.

```
$ cat ad_profile
{
    "ad-profile": {
        "description": "Network Level ad profile",
        "member_id": 326,
        "brands": [
            {
                "id": "168",
                "status": "banned"
            },
            {
                "id": "255",
                "status": "banned"
            },
            {
                "id": "1072",
                "status": "trusted"
            },
            {
                "id": "1090",
                "status": "trusted"
            }
        ],
        "creatives": [
            {
                "id": "5",
                "approved": true
            }
        ],
        "notes": "This is a great ad profile",
        "default_language_status": "banned",
        "default_ad_server_status": "trusted",
        "default_category_status": "trusted",
        "default_technical_attribute_status": "trusted",
        "excluded_landing_page_urls": ["https://www.netflix.com","https://www.blockbuster.com"],
        "languages": [
            {
                "id": 1,
                "status": "trusted"
            }
        ],
        "ad_servers": null,
        "categories": [
            {
                "id": 41,
                "status": "banned"
            },
            {
                "id": 43,
                "status": "trusted"
            }
        ]
    }
}
```

### Update an existing ad profile

Given the ad profile JSON in the first example, let's say you want to update the `categories` array to include another item. In a real-world use case there might be 47 categories in the array. The semantics of `PUT` mean that in order to add another category to the array, you'll need to pass in all 47 of the existing categories plus the new one.

You can avoid this extra work by adding the query string parameters `append=true` to your request as shown in the example below. For backwards compatibility reasons the parameters `append_only=true` will also work.

```
$ cat ad-profile-update.json
{
  "ad-profiles":
  [
    {
      "id": 984276,
      "categories" : [
        {
          "id" : 42,
          "status" : "banned"
        }
      ]
    }
  ]
}
$ curl -b cookies -X PUT -d '@/tmp/ad-profile-update.json' \
'https://api.appnexus.com/ad-profile?id=984276&member_id=1282&append=true'
{
   "response" : {
      "id" : 984276,
      "ad-profile" : {
         "id" : 984276,
         "description" : "Rich's Crazy Reseller - Network Ad Profile",
         "categories" : [
            {
               "id" : 41,
               "status" : "banned"
            },
            {
               "id" : 42,
               "status" : "banned"
            },
            {
               "id" : 43,
               "status" : "trusted"
            }
         ],
         // many other fields...
         "default_category_status" : "trusted"
      },
      "status" : "OK",
      "count" : 1,
      "start_element" : 0,
      "num_elements" : 100,
   }
}
```

### Add an ad profile to your member

```
$ curl -b cookies -c cookies -X POST -d @ad_profile  "https://api.appnexus.com/ad-profile"
{
    "response": {
        "status": "OK",
        "id": "1317"
    }
}
```

### View an ad profile

```
$ curl -b cookies -c cookies "https://api.appnexus.com/ad-profile?id=1317"
{
  "response": {
    "status": "OK",
    "ad-profile": {
      "id": 1317,
      "state": "active",
      "description": "Network Level ad profile",
      "member_id": 326,
      "default_brand_status": "trusted",
      "members": null,
      "brands": [
        {
          "id": "168",
          "status": "banned"
        },
        {
          "id": "255",
          "status": "banned"
        },
        {
          "id": "1072",
          "status": "trusted"
        },
        {
          "id": "1090",
          "status": "trusted"
        }
      ],
      "creatives": [
        {
          "id": "5",
          "approved": true
        }
      ],
      "total_creative_count": 8369,
      "approved_creative_count": 1,
      "banned_creative_count": 8368,
      "creatives_approved_percent": 0.011948858883977,
      "creatives_unreviewed": 8367,
      "brands_unreviewed": null,
      "exclude_unaudited": true,
      "exclude_unaudited_direct": false,
      "notes": "This is a great ad profile.",
      "publisher_id": null,
      "last_modified": "2010-07-23 16:15:49",
      "default_language_status": "banned",
      "default_ad_server_status": "trusted",
      "default_category_status": "trusted",
      "excluded_landing_page_urls": ["https://www.netflix.com","https://www.blockbuster.com"],
      "default_technical_attribute_status": "trusted",
      "languages": [
        {
          "id": 1,
          "status": "trusted"
        }
      ],
      "ad_servers": null,
      "categories": [
        {
          "id": 41,
          "status": "banned"
        },
        {
          "id": 43,
          "status": "trusted"
        }
      ],
      "technical_attributes": null
    }
  }
}
```

### Creative attribute frequency capping examples

#### Add a frequency cap rule to an ad profile

The `{{"frequency_caps"}}` field will be `{{null}}` at first:

```
$ curl -b cookies -c cookies -X GET "https://sand.api.appnexus.com/ad-profile?id=199943"
{
  "response": {
    "status": "OK",
    "ad-profile": {
      "id": 199943,
      "state": "active",
      "description": null,
      "member_id": 941,
      ...
      "frequency_caps": null
    }
}
```

#### Add a frequency cap rule

```
$ cat add_freq_cap_rule.json
{
   "ad-profile": {
      "id": 199943,
      "frequency_caps": [
        {
          "max_day_imps": 5,
          "min_minutes_per_imp": 120,
          "technical_attributes": [ {"id":4},{"id":6} ],
          "categories": [ {"id":59},{"id":37} ]
        }
      ]
   }
}
$ curl -b cookies -c cookies -X PUT --data-binary @add_freq_cap_rule.json "https://sand.api.appnexus.com/ad-profile?id=199943"
{
  "response": {
    "status": "OK",
    "id": "199943"
  }
}
```

#### Ad profile will now have the frequency cap rule

```
$ curl -b cookies -c cookies -X GET "https://sand.api.appnexus.com/ad-profile?id=199943"
{
  "response": {
    "status": "OK",
    "ad-profile": {
      "id": 199943,
      "state": "active",
      "description": null,
      "member_id": 941,
      ...
      "frequency_caps": [
        {
          "id": 64,
          "max_session_imps": null,
          "max_day_imps": 5,
          "min_minutes_per_imp": 120,
          "member_id": 941,
          "technical_attributes": [
            {
              "id": 4,
              "name": "Video"
            },
            {
              "id": 6,
              "name": "Expandable"
            }
          ],
          "categories": [
            {
              "id": 37,
              "name": "Politics"
            },
            {
              "id": 59,
              "name": "Get Rich Quick"
            }
          ]
        }
      ]
      ...
```

#### Modify a frequency cap rule

Use the `{{PUT}}` command on the `{{ad-profile}}` service. The frequency cap's ID must be specified in the update JSON. If the frequency cap ID is not specified, the existing rule will be deleted, and a new rule will be created.

```
{code}
$ cat update_freq_cap_rule.json
{
   "ad-profile": {
      "id": 199943,
      "frequency_caps": [
        {
          "id": 64,
          "technical_attributes": [ {"id":4} ],
          "categories": [ ],
          "max_day_imps": 20
        }
      ]
   }
}
$ curl -b cookies -c cookies -X PUT --data-binary @update_freq_cap_rule.json "https://sand.api.appnexus.com/ad-profile?id=199943"
{
  "response": {
    "status": "OK",
    "id": "199943"
  }
}
{code}
```

#### Check the ad profile to see the updated rule

```
$ curl -b cookies -c cookies -X GET "https://sand.api.appnexus.com/ad-profile?id=199943"
{
  "response": {
    "status": "OK",
    "ad-profile": {
      "id": 199943,
      "state": "active",
      "description": null,
      "member_id": 941,
      ...
      "frequency_caps": [
        {
          "id": 64,
          "max_session_imps": null,
          "max_day_imps": 20,
          "min_minutes_per_imp": 120,
          "member_id": 941,
          "technical_attributes": [
            {
              "id": 4,
              "name": "Video"
            }
          ],
          "categories": null
        }
      ]
      ...
```
