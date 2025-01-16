---
title: Seller Report
description: The Seller report helps estimate inventory availability based on targeting criteria and can be filtered by geography, creative size, or audit status.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Seller report

> [!NOTE]
>
> This service is currently available to a limited set of clients and Microsoft employees only.

The Seller Report allows you to estimate the amount of available inventory given a set of possible targeting criteria that you specify. You can compare the overall volume of inventory available through a seller with what's available after you filter by geography, creative size, or audit status.

It offers answers to questions such as:

- How many platform-reviewed impressions are available per day from seller ID 123? In creative size 300x250? What if I allow some seller-reviewed inventory?
- How many unique impressions are available per day in Canada from seller ID 456?

The goal of this report is to show you inventory that you can actually target for purchase. It will only return inventory that is exposed for reselling to you. Sellers also have the ability to block specific buyers; as a result, some sellers may not appear in this report.

This report takes into account publisher-side settings from the [Member Service](./member-service.md), [Platform Member Service](./platform-member-service.md), and [Ad Profile Service](./ad-profile-service.md).

> [!NOTE]
> **Statistical Sampling**
>
> Due to the high volume of impressions across our platform, the data in this report is based on a statistical sampling.

## Admin users and reselling exposure logic

Calls to this report without the `member_id` query string parameter will return information about all available inventory without any reselling exposure logic applied. In addition, a separate `query` object will be returned in the JSON response that describes the database logic used to pull the data. Therefore, employees logged in as admin users will need to pass a `member_id` via the query string in order for that member's reselling exposure logic to be applied.

This report applies reselling exposure and ad quality settings from the [Member Service](./member-service.md), [Platform Member Service](./platform-member-service.md), and [Ad Profile Service](./ad-profile-service.md).

## Time frame

The time frame covered by this report is the previous seven days, with daily updates. Because of the fixed time frame availability, there is no `report_interval` field required in the JSON request. For more information see [Examples](#examples) below.

## Dimensions

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `seller_member_id` | int | `123` | The member ID of the seller whose inventory you're interested in.<br><br>**Note**: You can select multiple `seller_member_id` values using an array in your JSON report request.<br><br>**Filter by**: Yes<br>**Sort by**: Yes |
| `search` | string, int | `"Awesome Seller, Inc.", 256` | Search for a seller by name or ID.<br><br>**Filter by**: No<br>**Sort by**: No |
| `geo_country` | enum | `"CA"` | A two-character string denoting the country/region in which the impression was viewed. <br><br>**Filter by**: Yes<br>**Sort by**: No<br><br>**Default**: `"--"` (This means "worldwide targeting, all countries included.") |
| `audit_type` | enum | `"any_audit_status"` | The audit status of the inventory on which the impression was recorded. Allowed values:<br> - `"any_audit_status"`: Includes all four possible audit statuses: `unaudited`, `AppNexus-reviewed`, `seller-reviewed`, and `AppNexus-and-seller-reviewed inventory`.<br> - `"appnexus_reviewed"`: Includes one audit status: only `AppNexus-reviewed` inventory.<br> - `"appnexus_seller_reviewed"`: Includes three audit statuses: `seller-reviewed`, `AppNexus-reviewed`, and `seller-and-AppNexus-reviewed`.<br><br>**Note**: Because of the way audit status data is aggregated, adding together impressions with different audit types will result in overcounting impressions.<br><br>**Filter by**: Yes<br>**Sorty by**: No<br><br>**Default**: `"any_audit_status"` |
| `size` | enum | `[ "160x250", "300x200" ]` | Discover available inventory matching the creative size(s) you specify here. Allowed values:<br> - `"all"`: All creative sizes across the AppNexus platform.<br>- `"uncategorized"`: All creatives that do not fit into the heights and widths specified in [Creative Sizes](#creative-sizes).<br> - `"160x250"`: Specify a single creative size as a string.<br> - `[ "160x250", "300x200" ]`: Pass an array of strings representing the creative sizes you're interested in. In this case the `avg_imps` and `avg_uniques` values in [Metrics](#metrics) will represent the sum of impressions across those sizes.<br><br>For a list of the accepted standard and mobile creative sizes, see [Creative Sizes](#creative-sizes) below.<br><br>**Filter by**: Yes<br>**Sort by**: No<br><br>**Default**: `"all"` |
| `iash` | boolean | `true` | Whether the inventory in question is being served by an IASH accredited member. If no value is specified, the default is to show inventory with any IASH status (e.g. both `false` and `true`).<br><br>**Filter by**: Yes <br>**Sort by**: No |
| `seller_type` | enum | `"platform"` | The type of seller whose inventory you're researching. Allowed values:<br> - `"platform"`: When you purchase platform inventory, an auction service fee **is not** charged.<br> - `"partner"`: When you purchase inventory from one of our external supply partners, an auction service fee **is** charged.<br> - `"unknown"`: The seller type is not identifiable.<br><br>**Filter by**: Yes<br>**Sort by**: No |
| `inventory_trust` | enum | `"platform"` | **Read Only**. This field is returned inside the API's JSON response. The value reflects your current settings from the `inventory_trust` array in the [Member Service](./member-service.md), which affects how many impressions are available to you from that seller. Allowed values:<br> - `"appnexus"`: You've chosen to trust AppNexus-audited inventory.<br> - `"seller"`: You trust this particular seller's inventory.<br> - `"banned"`: You don't trust this seller, and they are banned.<br> - `"all"`: You trust all inventory, even unaudited inventory.<br><br>**Filter by**: No<br>**Sort by**: No |
| `device_type` | string | `"tablets"` | The type of device on which the impression was served. Possible values are:<br>- `"desktops & laptops"`<br> - `"tablets"`<br> - `"mobile phones"`<br> - `"tv"`<br> - `"game consoles"`<br> - `"set top box"`<br> - `"media players"`<br> - `"other devices"`<br><br>**Filter by**: Yes<br>**Default**: n/a |
| `supply_type` | int | `2` | Allowed values:<br>`0`: Web<br>`1`: Mobile Web<br>`2`: Mobile App<br><br>**Note**: You will get the sum across all supply types by default – if that's what you want, there's no need to send this field.<br><br>**Filter by**: Yes<br>**Default**: n/a |
| `os_family_id` | int | `2` | See the [Operating System Family Service](./operating-system-family-service.md).<br><br>**Filter by**: Yes<br>**Default**: n/a |

## Creative sizes

The sizes listed here correspond to those available in the Console user interface for this report. For a list of other allowed values, see the description of the `size` field above.

| Sizes |
|:---|
| 120x160 |
| 160x600 |
| 300x250 |
| 480x80 |
| 728x90 |
| 300x50 |
| 468x80 |
| 320x50 |
| 480x80 |
| 300x480 |

## Metrics

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `total_imps` | int | `512` | The daily average number of available impressions given your chosen combination of `seller_member_id` and `geo_country`, without any other filters applied.<br><br>**Sort by**: Yes |
| `total_uniques` | int | `1024` | The daily average number of available uniques given your chosen combination of `seller_member_id` and `geo_country`, without any other filters applied.<br><br>**Sort by**: Yes |
| `avg_imps` | int | `12571` | The daily average number of available impressions, given any filters you've selected in addition to `seller_type` and `geo_country`. Compare it to `total_imps` to see what subset of the seller's total impressions are available given your current filters.<br><br>**Sort by**: Yes |
| `avg_uniques` | int | `8432` | The daily average number of available impressions associated with unique users, updated to take into account any filters you've selected in addition to `seller_type` and `geo_country`. Compare it to total_uniques to see how what subset of the seller's total uniques are available given your current filters.<br><br>**Note**: <br>**Limited Availability of Uniques**<br> - The `avg_uniques` metric is available only:<br> - When you filter by `seller_member_id` and a `geo_country` of `"--"` (This means "worldwide targeting, all countries included.").<br> - When you filter by `seller_member_id` and a single `geo_country`, e.g. `"CA"`.<br>**Adding Uniques not Recommended**<br>Adding uniques across several pulls of this report with different values of `seller_member_id` is not recommended. This will result in overcounting uniques, since the same user can easily browse across several sellers' inventory.<br><br>**Sort by**: Yes |

## Examples

For more information about using the sorting and pagination capabilities of this report, see the examples below and refer to the [Sync Report Service](./sync-report-service.md).

### Learn more about a seller's Canadian inventory across all creative sizes

In the following example, we request information on all inventory available in Canada from seller ID `128`, ordered from greatest to fewest average daily impressions.

Note that you will see the `avg_uniques` metric since we are not specifying any additional filters beyond seller and geographic location.

```
$ cat report-request.json
{
  "sync-report": {
    "filters": [
      {
        "seller_member_id": 128,
        "geo_country": "CA"
      }
    ],
    "orders": [
      {
        "direction": "DESC",
        "order_by": "avg_imps"
      }
    ],
    "report_type": "seller"
  }
}
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/sync-report"
{
  "response": {
    "status": "OK",
    "sync-report": {
      "data": [
        {
          "seller_type": "platform",
          "total_imps": 901571100,
          "total_uniques": 78145500,
          "size": [
            "all"
          ],
          "avg_imps": 33776500,
          "iash": true,
          "avg_uniques": 2987000,
          "seller_member_id": 128,
          "seller_member_name": "Awesome Advertising Exchange",
          "geo_country": "CA",
          "geo_country_name": "Canada",
          "inventory_trust": "all",
          "audit_type": "any_status"
        }
      ],
      "total_count": 1,
      "offset": 0,
      "count": 1,
      "query": {
        "ast": {
          "geo_country": "CA",
          "seller_member_id": 128,
          "agg_audit_type": 0
        },
        "string": "geo_country:CA AND seller_member_id:128 AND agg_audit_type:0",
        "orders": [
          {
            "direction": "DESC",
            "order_by": "avg_imps_all"
          }
        ]
      }
    },
    "dbg_info": {
      "instance": "17.bm-hbapi.prod.nym1",
      "s1ave_hit": false,
      "db": "master",
      "warnings": [
      ],
      "time": 77.229022979736,
      "start_microtime": 1345043286.1646,
      "version": "1.12.37"
    }
  }
}
```

### Learn more about available Canadian inventory for two creative sizes

```
$ cat report-request.json
{
  "sync-report": {
    "report_type": "seller",
    "orders": [
      {
        "order_by": "avg_imps",
        "direction": "DESC"
      }
    ],
    "filters": [
      {
        "geo_country": "CA",
        "size": [
          "300x250",
          "728x90"
        ]
      }
    ]
  }
}
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/sync-report"
{
  "response": {
    "dbg_info": {
      "version": "1.12.37",
      "start_microtime": 1345045269.1188,
      "time": 198.60792160034,
      "warnings": [
      ],
      "db": "master",
      "s1ave_hit": false,
      "instance": "28.bm-hbapi.prod.nym1"
    },
    "sync-report": {
      "query": {
        "orders": [
          {
            "direction": "DESC",
            "order_by": "sum(avg_imps_300x250,avg_imps_728x90)"
          }
        ],
        "string": "geo_country:CA AND agg_audit_type:0",
        "ast": {
          "agg_audit_type": 0,
          "geo_country": "CA"
        }
      },
      "count": 20,
      "offset": 0,
      "total_count": 96,
      "data": [
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "PubliX.com",
          "seller_member_id": 789,
          "avg_uniques": 220900,
          "iash": false,
          "avg_imps": 8637700,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 76798900,
          "total_imps": 3688399200.0,
          "seller_type": "external"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "MMXV Ads",
          "seller_member_id": 1024,
          "avg_uniques": 155600,
          "iash": true,
          "avg_imps": 3423300,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 69376200,
          "total_imps": 2154961000.0,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "Gallagher AdExchange",
          "seller_member_id": 818,
          "avg_uniques": 154100,
          "iash": true,
          "avg_imps": 3284900,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 168621200,
          "total_imps": 5929275900.0,
          "seller_type": "external"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "Awesome Advertising Exchange",
          "seller_member_id": 802,
          "avg_uniques": 433500,
          "iash": true,
          "avg_imps": 1746200,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 78145500,
          "total_imps": 901571100.0,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "Hart Inc.",
          "seller_member_id": 436,
          "avg_uniques": 83800,
          "iash": true,
          "avg_imps": 444500,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 29766400,
          "total_imps": 232643600,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "AdSluicers Media",
          "seller_member_id": 410,
          "avg_uniques": 53800,
          "iash": true,
          "avg_imps": 382300,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 24541300,
          "total_imps": 249273700,
          "seller_type": "external"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "FilledAds.com",
          "seller_member_id": 888,
          "avg_uniques": 94100,
          "iash": false,
          "avg_imps": 355300,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 15251100,
          "total_imps": 92387000,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Canada",
          "geo_country": "CA",
          "seller_member_name": "ConnectXLTD",
          "seller_member_id": 299,
          "avg_uniques": 53400,
          "iash": true,
          "avg_imps": 294000,
          "size": [
            "300x250",
            "728x90"
          ],
          "total_uniques": 11763100,
          "total_imps": 65154400,
          "seller_type": "platform"
        },
        ...
      ]
    },
    "status": "OK"
  }
}
```

### List iASH-compliant sellers by volume (from greatest to least)

```
$ cat report-request.json
{
  "sync-report": {
    "filters": [
      {
        "iash": true
      }
    ],
    "orders": [
      {
        "direction": "DESC",
        "order_by": "avg_imps"
      }
    ],
    "report_type": "seller"
  }
}
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/sync-report"
{
  "response": {
    "dbg_info": {
      "version": "1.12.37",
      "start_microtime": 1345043998.6495,
      "time": 40.778875350952,
      "warnings": [
      ],
      "db": "master",
      "s1ave_hit": false,
      "instance": "28.bm-hbapi.prod.nym1"
    },
    "sync-report": {
      "query": {
        "orders": [
          {
            "direction": "DESC",
            "order_by": "avg_imps_all"
          }
        ],
        "string": "geo_country:\\-\\- AND iash:1 AND agg_audit_type:0",
        "ast": {
          "agg_audit_type": 0,
          "iash": 1,
          "geo_country": "\\-\\-"
        }
      },
      "count": 20,
      "offset": 0,
      "total_count": 65,
      "data": [
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Worldwide",
          "geo_country": "--",
          "seller_member_name": "Gallagher AdExchange",
          "seller_member_id": 818,
          "avg_uniques": 168621200,
          "iash": true,
          "avg_imps": 5929275900.0,
          "size": [
            "all"
          ],
          "total_uniques": 168621200,
          "total_imps": 5929275900.0,
          "seller_type": "external"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Worldwide",
          "geo_country": "--",
          "seller_member_name": "MMXV Ads",
          "seller_member_id": 1024,
          "avg_uniques": 69376200,
          "iash": true,
          "avg_imps": 2154961000.0,
          "size": [
            "all"
          ],
          "total_uniques": 69376200,
          "total_imps": 2154961000.0,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Worldwide",
          "geo_country": "--",
          "seller_member_name": "DirectX",
          "seller_member_id": 7812,
          "avg_uniques": 37026800,
          "iash": true,
          "avg_imps": 1862256900.0,
          "size": [
            "all"
          ],
          "total_uniques": 37026800,
          "total_imps": 1862256900.0,
          "seller_type": "external"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "Worldwide",
          "geo_country": "--",
          "seller_member_name": "Awesome Advertising Exchange",
          "seller_member_id": 802,
          "avg_uniques": 78145500,
          "iash": true,
          "avg_imps": 901571100.0,
          "size": [
            "all"
          ],
          "total_uniques": 78145500,
          "total_imps": 901571100.0,
          "seller_type": "platform"
        },
        ...
      ]
    },
    "status": "OK"
  }
}
```

### List the top three sellers ordered by uniques on U.S. inventory, in CSV format

```
$ cat report-request.json
{
  "sync-report": {
    "filters": [
      {
        "geo_country": "US"
      }
    ],
    "orders": [
      {
        "direction": "DESC",
        "order_by": "avg_uniques"
      }
    ],
    "report_type": "seller",
    "count": 3,
    "format": "csv"
  }
}
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/sync-report"
{
  "response": {
    "dbg_info": {
      "version": "1.12.37",
      "start_microtime": 1345044206.9015,
      "time": 73.539018630981,
      "warnings": [
      ],
      "db": "master",
      "s1ave_hit": false,
      "instance": "18.bm-hbapi.prod.nym1"
    },
    "sync-report": {
      "query": {
        "orders": [
          {
            "direction": "DESC",
            "order_by": "avg_uniques"
          }
        ],
        "string": "geo_country:US AND agg_audit_type:0",
        "ast": {
          "agg_audit_type": 0,
          "geo_country": "US"
        }
      },
      "count": 1,
      "offset": 0,
      "total_count": 121,
      "data": "geo_country,seller_member_id,seller_member_name,size,audit_type,inventory_type,inventory_id,inventory_name,avg_imps,avg_uniques\nUS,818,Gallagher AdExchange,\"all\",any_status,--,--,--,1720324800,53269000\nUS,128,Steinfeld,\"all\",any_status,--,--,--,583702200,28959400\nUS,918,Prendergast,\"all\",any_status,--,--,--,1318701300,28842700\n"
    },
    "status": "OK"
  }
}
```

### List the third-through thirteenth-highest ranking sellers by volume in New Zealand

```
$ cat report-request.json
{
  "sync-report": {
    "filters": [
      {
        "geo_country": "NZ"
      }
    ],
    "orders": [
      {
        "direction": "DESC",
        "order_by": "avg_imps"
      }
    ],
    "report_type": "seller",
    "offset": 2,
    "count": 10,
    "format": "csv"
  }
}
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/sync-report"
{
  "response": {
    "dbg_info": {
      "version": "1.12.37",
      "start_microtime": 1345044560.0698,
      "time": 75.410127639771,
      "warnings": [
      ],
      "db": "master",
      "s1ave_hit": false,
      "instance": "19.bm-hbapi.prod.nym1"
    },
    "sync-report": {
      "query": {
        "orders": [
          {
            "direction": "DESC",
            "order_by": "avg_imps_all"
          }
        ],
        "string": "geo_country:NZ AND agg_audit_type:0",
        "ast": {
          "agg_audit_type": 0,
          "geo_country": "NZ"
        }
      },
      "count": 10,
      "offset": 2,
      "total_count": 96,
      "data": [
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "New Zealand",
          "geo_country": "NZ",
          "seller_member_name": "Gallagher AdExchange",
          "seller_member_id": 818,
          "avg_uniques": 1102400,
          "iash": true,
          "avg_imps": 4701200,
          "size": [
            "all"
          ],
          "total_uniques": 168621200,
          "total_imps": 5929275900.0,
          "seller_type": "external"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "New Zealand",
          "geo_country": "NZ",
          "seller_member_name": "MMXV Ads",
          "seller_member_id": 1024,
          "avg_uniques": 155600,
          "iash": true,
          "avg_imps": 4552300,
          "size": [
            "all"
          ],
          "total_uniques": 69376200,
          "total_imps": 2154961000.0,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "New Zealand",
          "geo_country": "NZ",
          "seller_member_name": "FilledAds.com",
          "seller_member_id": 876,
          "avg_uniques": 94100,
          "iash": false,
          "avg_imps": 563300,
          "size": [
            "all"
          ],
          "total_uniques": 15251100,
          "total_imps": 92387000,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "New Zealand",
          "geo_country": "NZ",
          "seller_member_name": "Hart Inc.",
          "seller_member_id": 436,
          "avg_uniques": 83800,
          "iash": true,
          "avg_imps": 543900,
          "size": [
            "all"
          ],
          "total_uniques": 29766400,
          "total_imps": 232643600,
          "seller_type": "platform"
        },
        {
          "audit_type": "any_status",
          "inventory_trust": "all",
          "geo_country_name": "New Zealand",
          "geo_country": "NZ",
          "seller_member_name": "AdSluicers Media",
          "seller_member_id": 410,
          "avg_uniques": 53800,
          "iash": true,
          "avg_imps": 478400,
          "size": [
            "all"
          ],
          "total_uniques": 24541300,
          "total_imps": 249273700,
          "seller_type": "external"
        },
        ...
      ]
    },
    "status": "OK"
  }
}
```

### View the highest ranking sellers of AppNexus-and-seller-reviewed inventory by volume in the United States

```
$ cat report-request.json
{
  "sync-report": {
    "filters": [
      {
        "audit_type": "appnexus_seller_reviewed",
        "geo_country": "US"
      }
    ],
    "orders": [
      {
        "direction": "DESC",
        "order_by": "total_imps"
      }
    ],
    "report_type": "seller"
  }
}
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/sync-report"
{
  "response": {
    "dbg_info": {
      "version": "1.12.39",
      "start_microtime": 1345476555.4577,
      "time": 186.30194664001,
      "warnings": [
      ],
      "db": "master",
      "s1ave_hit": false,
      "instance": "29.bm-hbapi.prod.nym1"
    },
    "sync-report": {
      "query": {
        "orders": [
          {
            "order_by": "avg_total_imps",
            "direction": "DESC"
          }
        ],
        "string": "geo_country:US AND agg_audit_type:1",
        "ast": {
          "agg_audit_type": 1,
          "geo_country": "US"
        }
      },
      "count": 20,
      "offset": 0,
      "total_count": 119,
      "data": [
        {
          "audit_type": "appnexus_seller_reviewed",
          "inventory_trust": "all",
          "geo_country_name": "United States",
          "geo_country": "US",
          "seller_member_name": "Google AdExchange",
          "seller_member_id": 181,
          "iash": false,
          "avg_imps": 1363388300.0,
          "size": [
            "all"
          ],
          "total_uniques": 168062900,
          "total_imps": 5893391929.0,
          "seller_type": "external"
        },
        {
          "audit_type": "appnexus_seller_reviewed",
          "inventory_trust": "all",
          "geo_country_name": "United States",
          "geo_country": "US",
          "seller_member_name": "Rubicon",
          "seller_member_id": 459,
          "iash": false,
          "avg_imps": 748632000.0,
          "size": [
            "all"
          ],
          "total_uniques": 78389400,
          "total_imps": 3759216471.0,
          "seller_type": "external"
        },
        {
          "audit_type": "appnexus_seller_reviewed",
          "inventory_trust": "all",
          "geo_country_name": "United States",
          "geo_country": "US",
          "seller_member_name": "CPXInteractive",
          "seller_member_id": 541,
          "iash": false,
          "avg_imps": 264269900,
          "size": [
            "all"
          ],
          "total_uniques": 68507900,
          "total_imps": 2105549500.0,
          "seller_type": "platform"
        },
        {
          "audit_type": "appnexus_seller_reviewed",
          "inventory_trust": "all",
          "geo_country_name": "United States",
          "geo_country": "US",
          "seller_member_name": "OpenX",
          "seller_member_id": 357,
          "iash": false,
          "avg_imps": 837277600.0,
          "size": [
            "all"
          ],
          "total_uniques": 37319000,
          "total_imps": 1839651057.0,
          "seller_type": "external"
        },
        {
          "audit_type": "appnexus_seller_reviewed",
          "inventory_trust": "all",
          "geo_country_name": "United States",
          "geo_country": "US",
          "seller_member_name": "Microsoft Advertising Exchange",
          "seller_member_id": 280,
          "iash": false,
          "avg_imps": 350405700,
          "size": [
            "all"
          ],
          "total_uniques": 76802700,
          "total_imps": 891904514.0,
          "seller_type": "platform"
        },
      ...
      ]
    },
    "status": "OK"
  }
  }
```
