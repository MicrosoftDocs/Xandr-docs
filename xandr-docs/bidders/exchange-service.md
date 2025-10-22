---
title: Exchange Service
description: Explore seller groups for efficient supply targeting, effortlessly target inventory, combine domain and member targeting, exclude/include members individually.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Exchange service

Exchanges are groups of sellers organized to allow for easier supply targeting.

- This inventory will be targeted all at once. You can combine it with domain list targeting and member targeting.
- As new sellers are added, you do not have to update your profile or targeting. When targeting a single exchange, you will receive all members within it and any new members that join.
- We took our premium publishers and put them all in one group, called "Supply". When you access and target inventory, you can target Supply. This will target all those premium publishers for you.
  - You can find out more information about Supply here: [Supply for External Demand Partners](xandr-monetize-supply-for-external-demand-partners.md)
- Sellers that belong to Exchange 1, Supply, cannot be individually included and excluded. The group must be targeted as a whole. You can individually include/exclude members that belong to other exchanges.

Today we have three exchanges:

| ID | Name | Description |
|--|--|--|
| 1 | Direct | These are premium publishers on our platform that we have direct integrations with. This inventory is brought to you directly through Xandr's SSP technology, and is formed at its core from our direct-to-publisher supply most frequently requested and purchased by our buyers across all formats (display, mobile, video, and native). |
| 2 | Connect | These are the SSPs such as Pubmatic, Google Ad Manager, etc. |
| 3 | Network | All ad-networks that represent many publishers and act as SSPs. |

## Rest API

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/exchange` | To see all of the exchanges and members that belong to them. |
| GET | `https://api.adnxs.com/exchange?id=[EXCHANGE_ID]` | To view members in a specific exchange. |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `created_on` | array | The timestamp when the exchange was created. |
| `description` | array | Description of sellers that belong to the exchange. |
| `id` | int | The ID of the exchange. Today, we only have 3 exchanges. |
| `last_activity` | enum | The timestamp of last modification. |
| `members` | array of objects | Array of members that belong to that exchange. |
| `name` | int | The name of the exchange. |
| `restricted` | boolean | Indicates if the members within the exchange can be individually targeted or blocked.<br> - If `true`, the members within this exchange can not be individually included or excluded.<br> - If `false`, the members within this exchange can be individually included or excluded. |

## Members object

The following table describes Member Object fields.

| Field | Type | Description |
|--|--|--|
| `id` | int | ID of the member |
| `name` | string | Name of the member |

## Examples

**View all members who belong to exchange 2**

```
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2909  100  2909    0     0  34085      0 --:--:-- --:--:-- --:--:-- 34223
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "exchange": {
            "id": 2,
            "name": "Connect",
            "description": "Includes all SSPs/exchanges.",
            "last_activity": "2018-04-17 16:04:28",
            "created_on": "2018-04-17 16:04:28",
            "restricted": false,
            "members": [
                {
                    "id": 459,
                    "name": "Rubicon"
                },
                {
                    "id": 1752,
                    "name": "Smaato Inc."
                },
                {
                    "id": 1813,
                    "name": "MoPub Inc."
                },
                {
                    "id": 357,
                    "name": "OpenX"
                },
                {
                    "id": 74,
                    "name": "PubMatic"
                },
                {
                    "id": 3053,
                    "name": "FreeWheel SSP"
                },
                {
                    "id": 3332,
                    "name": "Telaria, Inc."
                },
                {
                    "id": 1868,
                    "name": "ONE by AOL Mobile Marketplace"
                },
                {
                    "id": 181,
                    "name": "Google AdExchange"
                },
                {
                    "id": 1226,
                    "name": "AOL ONE Display"
                },
                {
                    "id": 2850,
                    "name": "MobFox"
                },
                {
                    "id": 1117,
                    "name": "Switch Concepts Limited"
                },
                {
                    "id": 1314,
                    "name": "TripleLift Inc."
                },
                {
                    "id": 2551,
                    "name": "Sonobi - Premium"
                },
                {
                    "id": 1410,
                    "name": "Index Exchange Inc"
                },
                {
                    "id": 3292,
                    "name": "Adap.TV"
                },
                {
                    "id": 1872,
                    "name": "Media.Net Ltd"
                },
                {
                    "id": 1944,
                    "name": "Centro Media, Inc."
                },
                {
                    "id": 1942,
                    "name": "Floor6"
                },
                {
                    "id": 3703,
                    "name": "Smart RTB+"
                },
                {
                    "id": 1360,
                    "name": "Sovrn"
                },
                {
                    "id": 1354,
                    "name": "Improve Digital"
                },
                {
                    "id": 273,
                    "name": "Yahoo Ad Exchange"
                },
                {
                    "id": 3918,
                    "name": "xAd, Inc."
                },
                {
                    "id": 3425,
                    "name": "Sharethrough"
                },
                {
                    "id": 1548,
                    "name": "Criteo"
                },
                {
                    "id": 1405,
                    "name": "Ströer SSP GmbH"
                },
                {
                    "id": 2014,
                    "name": "Conversant, Inc."
                },
                {
                    "id": 3366,
                    "name": "AerServ LLC"
                },
                {
                    "id": 2568,
                    "name": "Engage:BDR"
                },
                {
                    "id": 1063,
                    "name": "Cox Digital Solutions LLC"
                },
                {
                    "id": 1263,
                    "name": "PulsePoint, Inc."
                },
                {
                    "id": 3016,
                    "name": "Yieldlab AG"
                },
                {
                    "id": 3287,
                    "name": "RTK.io (Phaedrus Media, LLC)"
                },
                {
                    "id": 2047,
                    "name": "Inneractive LTD"
                },
                {
                    "id": 3470,
                    "name": "Falk Technologies GmbH"
                },
                {
                    "id": 1475,
                    "name": "Lifestreet"
                },
                {
                    "id": 1899,
                    "name": "Zedo (ZINC)"
                },
                {
                    "id": 2877,
                    "name": "Amobee, Inc."
                },
                {
                    "id": 3104,
                    "name": "SpotXchange Inc."
                },
                {
                    "id": 3335,
                    "name": "Optimatic Inc."
                },
                {
                    "id": 3351,
                    "name": "SmartClip (Video)"
                },
                {
                    "id": 3368,
                    "name": "SMARTSTREAM.TV GmbH"
                },
                {
                    "id": 7044,
                    "name": "fluct, Inc."
                },
                {
                    "id": 1081,
                    "name": "Sonobi"
                },
                {
                    "id": 1505,
                    "name": "AdConductor"
                },
                {
                    "id": 7122,
                    "name": "Geniee, Inc. / SSP"
                },
                {
                    "id": 6901,
                    "name": "MicroAd, Inc."
                },
                {
                    "id": 1583,
                    "name": "Admeta AB"
                },
                {
                    "id": 3334,
                    "name": "Teads France SAS"
                },
                {
                    "id": 3364,
                    "name": "Taboola Inc"
                },
                {
                    "id": 7824,
                    "name": "Brightroll Exchange Video"
                },
                {
                    "id": 7911,
                    "name": "Yieldmo, Inc."
                },
                {
                    "id": 8173,
                    "name": "Kargo Global, Inc"
                },
                {
                    "id": 8128,
                    "name": "Adrizer LLC"
                },
                {
                    "id": 7702,
                    "name": "Platform-One"
                },
                {
                    "id": 3144,
                    "name": "Media.net Ltd."
                },
                {
                    "id": 7851,
                    "name": "Axonix Ltd."
                },
                {
                    "id": 8178,
                    "name": "PubNative"
                },
                {
                    "id": 4052,
                    "name": "Conversant, Inc."
                },
                {
                    "id": 7906,
                    "name": "AdForm A/S"
                },
                {
                    "id": 3360,
                    "name": "Nsight by Dailymotion"
                },
                {
                    "id": 7666,
                    "name": "Revcontent, LLC"
                },
                {
                    "id": 8678,
                    "name": "United Inc. / AdStir"
                },
                {
                    "id": 6887,
                    "name": "Vdopia, Inc."
                },
                {
                    "id": 8449,
                    "name": "Supership Inc. / Ad Generation"
                },
                {
                    "id": 8847,
                    "name": "Beacon Spark Ltd."
                },
                {
                    "id": 6933,
                    "name": "Spot.IM Inc."
                },
                {
                    "id": 3277,
                    "name": "AdsWizz Inc."
                },
                {
                    "id": 8804,
                    "name": "Adman Media USA"
                }
            ]
        },
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.673",
            "output_term": "exchange"
        }
    }
}
```

## Related topics

- [Enhanced Bidder Profiles](enhanced-bidder-profiles.md)
- [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)
- [API Use Cases for Enhanced Bidder Profiles](api-use-cases-for-enhanced-bidder-profiles.md)
- [Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles](frequently-asked-questions-faq-for-enhanced-bidder-profiles.md)
- [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md)
