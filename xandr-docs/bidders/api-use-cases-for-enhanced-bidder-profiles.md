---
title: API Use Cases for Enhanced Bidder Profiles
description: In this article, find some common use cases with Enhanced Bidder Profiles.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# API use cases for enhanced bidder profiles

Below are some common use cases with Enhanced Bidder Profiles.

## Create new profiles

Find IDs and example JSON files and calls for various actions related to creating new profiles in this section.

### Create a new profile that targets exchanges and has included/excluded members

**ID**: 1

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"exchanges": {
"targets": [{
"id": 1
}, {
"id": 3
}],
"action": "exclude",
"excluded_members": [{
"id": 389
}, {
"id": 1202
}],
"included_members": [{
"id": 101
}, {
"id": 1200
}]
},
"non_audited_url_action": "include"
}
}
}
```

**POST call**:

```
curl -b cookies -c cookies -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 1318 100 913 100 405 947 420 --:--:-- --:--:-- --:--:-- 947
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 12,
"bidder_profile": {
"id": 12,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"exchanges": {
"action": "exclude",
"targets": [
{
"id": 1,
"name": "Direct"
},
{
"id": 3,
"name": "Network"
}
],
"included_members": [
{
"id": 101,
"billing_name": "AdNexus (DW)"
},
{
"id": 1200,
"billing_name": "Performance Advertising GmbH"
}
],
"excluded_members": [
{
"id": 389,
"billing_name": "Admeld - KickApps"
},
{
"id": 1202,
"billing_name": "Agenda Media Ltd."
}
]
},
"ad_types": {
"banner": {
"action": "include"
},
"video": {
"action": "include"
},
"audio": {
"action": "include"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-05-31 16:15:20",
"created_on": "2018-05-31 16:15:20",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.552",
"output_term": "bidder_profile"
}
}
}
```

### Create a new profile that only targets native inventory

**ID**: 2

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"ad_types": {
"native": {
"action": "include"
}
}
}
}
}
```

**POST call**:

```
curlpost bidder-profile?bidder_id=129 @np_4.json
Using: curl -b ./auth/apiprodcookie -c ./auth/apiprodcookie -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 588 100 484 100 104 3123 671 --:--:-- --:--:-- --:--:-- 3142
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 67,
"bidder_profile": {
"id": 67,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"ad_types": {
"banner": {
"action": "exclude"
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-12-05 21:45:04",
"created_on": "2018-12-05 21:45:04",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.923",
"output_term": "bidder_profile"
}
}
}
```

### Create a new profile that targets a member (id 958)

> [!WARNING]
> Expected Error: Members in Exchange 1 can only be excluded.

**ID**: 3

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"exchanges": {
"included_members": [{
"id": 958
}]
}
}
}
}
```

**POST call**:

```
curl -b ./auth/apiprodcookie -c ./auth/apiprodcookie -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 629 100 447 100 182 2066 841 --:--:-- --:--:-- --:--:-- 2069
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 277,
"bidder_profile": {
"id": 277,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"exchanges": {
"included_members": [
{
"id": 958,
"billing_name": "AppNexus Services Network"
}
]
}
},
"last_activity": "2018-12-05 21:43:42",
"created_on": "2018-12-05 21:43:42",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.923",
"output_term": "bidder_profile"
}
}
}
```

### Create a new profile that excludes Pesto Harel Shemesh LTD (id 8495), a member in Exchange 3

**ID**: 4

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"exchanges": {
"excluded_members": [{
"id": 8945
}]
}
}
}
}
```

**POST call**:

```
curl -b cookies -c cookies -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 755 100 572 100 183 2003 640 --:--:-- --:--:-- --:--:-- 2000
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 14,
"bidder_profile": {
"id": 14,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"exchanges": {
"excluded_members": [
{
"id": 8945,
"billing_name": "Pesto Harel Shemesh LTD"
}
]
},
"ad_types": {
"banner": {
"action": "include"
},
"video": {
"action": "include"
},
"audio": {
"action": "include"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-06-15 20:16:00",
"created_on": "2018-06-15 20:16:00",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.594",
"output_term": "bidder_profile"
}
}
}
```

### Create a new active profile that targets only banner inventory sized 200x100 and a domain list

**ID**: 5

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"ad_types": {
"banner": {
"action": "include",
"sizes": [{
"width": 200,
"height": 100
}]
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "exclude"
}
},
"domain_lists": {
"targets": [{
"id": 100675
}],
"action": "include"
}
},
"active": true
}
}
```

**POST call**:

```
curl -b cookies -c cookies -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 1065 100 660 100 405 1872 1149 --:--:-- --:--:-- --:--:-- 1875
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 16,
"bidder_profile": {
"id": 16,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"domain_lists": {
"action": "include",
"targets": [
{
"id": 100675,
"name": "Domains to exclude",
"description": "block facebook.com",
"type": "black"
}
]
},
"ad_types": {
"banner": {
"action": "include",
"sizes": [
{
"width": 200,
"height": 100
}
]
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "exclude"
}
}
},
"last_activity": "2018-06-15 20:31:03",
"created_on": "2018-06-15 20:31:03",
"active": true
},
"dbg": {
"warnings": [
],
"version": "1.18.594",
"output_term": "bidder_profile"
}
}
}
```

### Create a new inactive profile that excludes video inventory sized 100x100, excludes inventory with non-english languages (inventory attribute id 17), and targets the country France

**ID**: 6

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"ad_types": {
"banner": {
"action": "include"
},
"video": {
"action": "exclude",
"sizes": [{
"width": 200,
"height": 100
}]
},
"audio": {
"action": "include"
},
"native": {
"action": "include"
}
},
"inventory_attributes": {
"action": "include",
"targets": [{
"id": 2
}, {
"id": 4
}, {
"id": 6
}, {
"id": 8
}, {
"id": 10
}, {
"id": 12
}, {
"id": 16
}, {
"id": 17
}, {
"id": 29
}]
},
"countries": {
"action": "include",
"targets": [{
"id": 78
}]
}
}
}
}
```

**POST call**:

```
curl -b cookies -c cookies -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 1656 100 1018 100 638 2241 1405 --:--:-- --:--:-- --:--:-- 2237
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 19,
"bidder_profile": {
"id": 19,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"countries": {
"action": "include",
"targets": [
{
"id": 78,
"name": "France",
"code": "FR",
"active": true
}
]
},
"inventory_attributes": {
"action": "include",
"targets": [
{
"id": 2,
"name": "Political"
},
{
"id": 4,
"name": "Social media"
},
{
"id": 6,
"name": "Photo & video sharing"
},
{
"id": 8,
"name": "Forums (moderated)"
},
{
"id": 10,
"name": "Forums (unmoderated)"
},
{
"id": 12,
"name": "Incentivized clicks"
},
{
"id": 16,
"name": "Streaming media"
},
{
"id": 17,
"name": "Toolbars, plugins, or extensions"
},
{
"id": 29,
"name": "Contextual Nudity"
}
]
},
"ad_types": {
"banner": {
"action": "include"
},
"video": {
"action": "exclude",
"sizes": [
{
"width": 200,
"height": 100
}
]
},
"audio": {
"action": "include"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-06-15 20:52:43",
"created_on": "2018-06-15 20:52:43",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.594",
"output_term": "bidder_profile"
}
}
}
```

### Create a new profile that targets video inventory sized 1x1

> [!WARNING]
> Expected Error: User can not target the size 1x1 or 0x0.

**ID**: 7

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"ad_types": {
"video": {
"action": "include",
"sizes": [{
"width": 1,
"height": 1
}]
}
}
}
}
}
```

**POST call**:

```
curl -b cookies -c cookies -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 897 100 263 100 634 2322 5599 --:--:-- --:--:-- --:--:-- 5610
{
"response": {
"error_id": "SYNTAX",
"error": "1x1 and 0x0 sizes aren't valid for video size",
"error_description": null,
"error_code": "INVALID_VIDEO_SIZE",
"service": "bidder-profile",
"method": "POST",
"dbg": {
"warnings": [
],
"version": "1.18.594",
"output_term": "not_found"
}
}
}
```

## Modify existing profile

Find IDs and example JSON files and calls for various actions related to modifying existing profiles in this section.

### Remove targeting on all exchanges from an existing profile

**ID**: 1

**Existing profile**:

```
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": "11",
"bidder_profile": {
"id": 11,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"exchanges": {
"action": "include",
"targets": [
{
"id": 1,
"name": "Direct"
}
]
},
"ad_types": {
"banner": {
"action": "include"
},
"video": {
"action": "include"
},
"audio": {
"action": "include"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-05-30 21:59:47",
"created_on": "2018-05-30 21:58:53",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.552",
"output_term": "bidder_profile"
}
}
}
```

**JSON file**:

```
cat np_3
{
"bidder_profile":{
"targeting":{
"exchanges":{"targets":[]}
}
}
}
```

**PUT call**:

```
curl -b cookies -c cookies -X PUT -d '@np_3' "https://api.adnxs.com/bidder-profile/129/11" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 725 100 585 100 140 1811 433 --:--:-- --:--:-- --:--:-- 1811
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": "11",
"bidder_profile": {
"id": 11,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"ad_types": {
"banner": {
"action": "include"
},
"video": {
"action": "include"
},
"audio": {
"action": "include"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-05-30 22:00:25",
"created_on": "2018-05-30 21:58:53",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.552",
"output_term": "bidder_profile"
}
}
}
```

### Activate an existing profile

> [!NOTE]
> By default, profiles are inactive. In order for them to be in effect, the active flag will have to be set to true.

**ID**: 2

**Existing profile**:

```
curl -b cookies -c cookies -X POST -d '@np_4.json' "https://api.adnxs.com/bidder-profile?bidder_id=129" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 676 100 484 100 192 2364 937 --:--:-- --:--:-- --:--:-- 2372
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": 13,
"bidder_profile": {
"id": 13,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"ad_types": {
"banner": {
"action": "exclude"
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-06-13 20:25:21",
"created_on": "2018-06-13 20:25:21",
"active": false
},
"dbg": {
"warnings": [
],
"version": "1.18.591",
"output_term": "bidder_profile"
}
}
}
```

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"active": true
}
}
```

**PUT call**:

```
curl -b cookies -c cookies -X PUT -d '@np_4.json' "https://api.adnxs.com/bidder-profile/129/13" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 522 100 485 100 37 1212 92 --:--:-- --:--:-- --:--:-- 1212
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": "13",
"bidder_profile": {
"id": 13,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"ad_types": {
"banner": {
"action": "exclude"
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "include"
}
}
},
"last_activity": "2018-06-13 20:47:01",
"created_on": "2018-06-13 20:25:21",
"active": true
},
"dbg": {
"warnings": [
],
"version": "1.18.591",
"output_term": "bidder_profile"
}
}
}
```

### Remove banner size targeting on an existing profile

**ID**: 3

**Existing profile**:

```
curl -b cookies -c cookies -X PUT -d '@np_4.json' "https://api.adnxs.com/bidder-profile/129/16" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 781 100 662 100 119 1999 359 --:--:-- --:--:-- --:--:-- 1993
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": "16",
"bidder_profile": {
"id": 16,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"domain_lists": {
"action": "include",
"targets": [
{
"id": 100675,
"name": "Domains to exclude",
"description": "block facebook.com",
"type": "black"
}
]
},
"ad_types": {
"banner": {
"action": "include",
"sizes": [
{
"width": 200,
"height": 100
}
]
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "exclude"
}
}
},
"last_activity": "2018-06-15 21:06:36",
"created_on": "2018-06-15 20:31:03",
"active": true
},
"dbg": {
"warnings": [
],
"version": "1.18.594",
"output_term": "bidder_profile"
}
}
}
```

**JSON file**:

```
cat np_4.json
{
"bidder_profile": {
"targeting": {
"ad_types": {
"banner": {
"action": "include",
"sizes":[]
}
}
}
}
}
```

**PUT call**:

```
curl -b cookies -c cookies -X PUT -d '@np_4.json' "https://api.adnxs.com/bidder-profile/129/16" | json_reformat
% Total % Received % Xferd Average Speed Time Time Time Current
Dload Upload Total Spent Left Speed
100 756 100 636 100 120 3211 606 --:--:-- --:--:-- --:--:-- 3228
{
"response": {
"status": "OK",
"count": 1,
"start_element": 0,
"num_elements": 100,
"id": "16",
"bidder_profile": {
"id": 16,
"bidder_id": 129,
"code": null,
"description": null,
"targeting": {
"domain_lists": {
"action": "include",
"targets": [
{
"id": 100675,
"name": "Domains to exclude",
"description": "block facebook.com",
"type": "black"
}
]
},
"ad_types": {
"banner": {
"action": "include",
"sizes": [
]
},
"video": {
"action": "exclude"
},
"audio": {
"action": "exclude"
},
"native": {
"action": "exclude"
}
}
},
"last_activity": "2018-06-15 21:06:50",
"created_on": "2018-06-15 20:31:03",
"active": true
},
"dbg": {
"warnings": [
],
"version": "1.18.594",
"output_term": "bidder_profile"
}
}
}
```

## Related topics

- [Enhanced Bidder Profiles](enhanced-bidder-profiles.md)
- [Exchange Service](exchange-service.md)
- [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)
- [Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles](frequently-asked-questions-faq-for-enhanced-bidder-profiles.md)
- [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md)
- [Bidder Profile Migration Guide](bidder-profile-migration-guide.md)
