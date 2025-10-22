---
title: Digital Platform API - Language Service
description: Explore the Language service, offering insights into the list of language IDs available for use in the Profile service or the Ad Profile service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Language service

This read-only service shows you the list of language IDs that you can use in the [Profile Service](profile-service.md) (to target browser languages) or in the [Ad Profile Service](ad-profile-service.md) (to trust or ban creative languages).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/language](https://api.appnexus.com/language) | View all languages available for targeting. |
| `GET` | [https://api.appnexus.com/language?search=SEARCH_TERM](https://api.appnexus.com/language?search=SEARCH_TERM) | View all languages with IDs, names, or codes containing certain characters. |
| `GET` | [https://api.appnexus.com/language?id=LANGUAGE_ID](https://api.appnexus.com/language?id=LANGUAGE_ID) | View a specific language. |
| `GET` | [https://api.appnexus.com/language?name=LANGUAGE_NAME](https://api.appnexus.com/language?name=LANGUAGE_NAME) | View a specific language. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | The 2 letter ISO-639-1 code for the language.|
| `id` | int | The ID of the language. |
| `last_activity` | timestamp | The date and time of the last update to the language entry. |
| `name` | string | The name of the language. |

### Available languages

| ID | Name | Code |
|:---|:---|:---|
| 0 |  Unknown     |  NULL  |
| 1 |  English     |  EN    |
| 2 |  Chinese     |  ZH    |
| 3 |  Spanish     |  ES    |
| 4 |  Japanese    |  JA    |
| 5 |  French      |  FR    |
| 6 |  German      |  DE    |
| 7 |  Arabic      |  AR    |
| 8 |  Portuguese  |  PT    |
| 9 |  Russian     |  RU    |
| 10 |  Korean     |  KO    |
| 11 |  Italian    |  IT    |
| 12 |  Dutch      |  NL    |
| 14 |  Danish     |  DA    |
| 15 |  Swedish    |  SV    |
| 16 |  Norwegian  |  NB    |
| 17 |  Polish     |  PL    |
| 18 |  Turkish    |  TR    |
| 19 |  Finnish    |  FI    |
| 20 |  Czech      |  CS    |
| 21 |  Slovak     |  SK    |
| 22 |  Romanian   |  RM    |
| 23 |  Bulgarian  |  BG    |
| 24 |  Slovene    |  SL    |
| 25 |  Hungarian  |  HU    |
| 26 |  Ukranian   |  UK    |
| 27 |  Croatian   |  HR    |
| 28 |  Serbian    |  SR    |
| 29 |  Bosnian    |  BS    |
| 30 |  Albanian   |  SQ    |
| 31 |  Macedonian |  MK    |
| 32 |  Vietnamese |  VI    |
| 33 |  Hindi      |  HI    |
| 34 |  Urdu       |  UR    |
| 35 |  Tamil      |  TA    |
| 36 |  Thai       |  TH    |
| 37 |  Greek      |  FL    |
| 38 |  Persian    |  FA    |
| 39 |  Welsh      |  CY    |
| 40 |  Hebrew     |  HE    |
| 41 |  Lithuanian |  LT    |
| 42 |  Estonian   |  ET    |
| 43 |  Latvian    |  LV    |
| 44 |  Indonesian |  ID    |
| 45 |  Azerbaijani|  AZ    |
| 46 |  Galician   |  GL    |
| 47 |  Georgian   | KA     |
| 48 |  Malay      | MS     |
| 49 |  Armenian   | HY     |
| 50 |  Catalan    | CA     |
| 51 |  Uzbek      | UZ     |
| 52 |  Burmese    | MY     |
| 53 | Kazakh      | KK     |
| 54 | Basque      | EU     |

## Examples

### View all languages

```
$ curl -b cookies -c cookies  https://api.appnexus.com/language'
{
  "response": {
    "status": "OK",
    "count": 36,
    "start_element": 0,
    "num_elements": 100,
    "languages": [
      {
        "id": 0,
        "name": "Unknown",
        "last_activity": "2010-12-17 15:19:49",
        "code": null
      },
      {
        "id": 1,
        "name": "English",
        "last_activity": "2013-04-01 19:12:00",
        "code": "EN"
      },
      {
        "id": 2,
        "name": "Chinese",
        "last_activity": "2013-04-01 19:12:00",
        "code": "ZH"
      },
      {
        "id": 3,
        "name": "Spanish",
        "last_activity": "2013-04-01 19:12:00",
        "code": "ES"
      },
      {
        "id": 4,
        "name": "Japanese",
        "last_activity": "2013-04-01 19:12:00",
        "code": "JA"
      },
      {
        "id": 5,
        "name": "French",
        "last_activity": "2013-04-01 19:12:00",
        "code": "FR"
      },
      {
        "id": 6,
        "name": "German",
        "last_activity": "2013-04-01 19:12:00",
        "code": "DE"
      },
      {
        "id": 7,
        "name": "Arabic",
        "last_activity": "2013-04-01 19:12:00",
        "code": "AR"
      },
      {
        "id": 8,
        "name": "Portuguese",
        "last_activity": "2013-04-01 19:12:00",
        "code": "PT"
      },
      {
        "id": 9,
        "name": "Russian",
        "last_activity": "2013-04-01 19:12:00",
        "code": "RU"
      },
      {
        "id": 10,
        "name": "Korean",
        "last_activity": "2013-04-01 19:12:00",
        "code": "KO"
      },
      {
        "id": 11,
        "name": "Italian",
        "last_activity": "2013-04-01 19:12:00",
        "code": "IT"
      },
      {
        "id": 12,
        "name": "Dutch",
        "last_activity": "2013-04-01 19:12:00",
        "code": "NL"
      },
      {
        "id": 14,
        "name": "Danish",
        "last_activity": "2013-04-01 19:12:00",
        "code": "DA"
      },
      {
        "id": 15,
        "name": "Swedish",
        "last_activity": "2013-04-01 19:12:00",
        "code": "SV"
      },
      {
        "id": 16,
        "name": "Norwegian",
        "last_activity": "2013-04-01 19:12:00",
        "code": "NB"
      },
      {
        "id": 17,
        "name": "Polish",
        "last_activity": "2012-07-23 19:14:56",
        "code": "PL"
      },
      {
        "id": 18,
        "name": "Turkish",
        "last_activity": "2014-01-21 17:08:22",
        "code": "TR"
      },
      {
        "id": 19,
        "name": "Finnish",
        "last_activity": "2014-01-21 17:08:58",
        "code": "FI"
      },
      {
        "id": 20,
        "name": "Czech",
        "last_activity": "2014-07-14 18:00:07",
        "code": "CS"
      },
      {
        "id": 21,
        "name": "Slovak",
        "last_activity": "2014-07-14 18:00:07",
        "code": "SK"
      },
      {
        "id": 22,
        "name": "Romanian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "RM"
      },
      {
        "id": 23,
        "name": "Bulgarian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "BG"
      },
      {
        "id": 24,
        "name": "Slovene",
        "last_activity": "2014-07-14 18:00:07",
        "code": "SL"
      },
      {
        "id": 25,
        "name": "Hungarian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "HU"
      },
      {
        "id": 26,
        "name": "Ukranian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "UK"
      },
      {
        "id": 27,
        "name": "Croatian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "HR"
      },
      {
        "id": 28,
        "name": "Serbian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "SR"
      },
      {
        "id": 29,
        "name": "Bosnian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "BS"
      },
      {
        "id": 30,
        "name": "Albanian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "SQ"
      },
      {
        "id": 31,
        "name": "Macedonian",
        "last_activity": "2014-07-14 18:00:07",
        "code": "MK"
      },
      {
        "id": 32,
        "name": "Vietnamese",
        "last_activity": "2014-07-14 18:00:07",
        "code": "VI"
      },
      {
        "id": 33,
        "name": "Hindi",
        "last_activity": "2014-07-14 18:00:07",
        "code": "HI"
      },
      {
        "id": 34,
        "name": "Urdu",
        "last_activity": "2014-07-14 18:00:07",
        "code": "UR"
      },
      {
        "id": 35,
        "name": "Tamil",
        "last_activity": "2014-07-14 18:00:07",
        "code": "TA"
      },
      {
        "id": 36,
        "name": "Thai",
        "last_activity": "2014-07-14 18:00:07",
        "code": "TH"
      }
    ]
  }
}
```

### View the language entry for Chinese

```
$ curl -b cookies -c cookies  https://api.appnexus.com/language?name=Chinese'
{
    "response": {
        "status": "OK",
        "languages": [
            {
                "id": 2,
                "name": "Chinese",
                "code": null,
                "last_activity": "2010-05-21 21:05:28"
            }
        ],
        "count": 1,
        "start_element": null,
        "num_elements": null
    }
}
```
