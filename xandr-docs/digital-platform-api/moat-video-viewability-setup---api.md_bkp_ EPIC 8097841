---
title: Moat Video Viewability Setup - API
description: Use Moat to improve video viewability metrics. Learn how to link an account or create one from scratch on Moat Video Viewability Measurement Setup page.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Moat Video Viewability Setup - API

You can amplify your video viewability metrics by tapping into a third-party video viewability data provider like Moat. This document will guide you through the process of updating a video creative to include Moat's reporting. For steps to link an existing account with Moat or to create one from scratch, see the [Moat Video Viewability Measurement Setup](../invest/moat-video-viewability-measurement.md) page in the UI.

## Update a video creative

The steps below explain how to update a video creative.

### Step 1. Include the following array in your JSON file

```
"thirdparty_viewability_providers": [
      {
        "thirdparty_provider_id": 1
      }
     ],
```

### Step 2. Make a `PUT` call to the creative VAST service with your updated JSON file

```
curl -b -c "Authorization:$TOKEN" "https://api.appnexus.com/creative-vast?member_id=1234&advertiser_id=1234567" -X PUT -d @myvideocreative.json
```

```
{
  "creative-vast": {
    "id": "46629877",
    "thirdparty_viewability_providers": [
      {
        "thirdparty_provider_id": 1
      }
    ]
  }
}
```

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `thirdparty_viewability_providers` | array | This array includes a collection of third party video viewability providers that will draw data on the given hosted video creative. |
| `thirdparty_provider_id` | int | This ID specifies which data provider will be granted access to historical data on this hosted video creative. |

### Third-party provider ID

| Provider Name | ID |
|:---|:---|
| MOAT | 1 |

## Remove third-party providers

To remove third-party providers from your hosted video creative, set the field `thirdparty_providers` to `null`. Then make a `PUT` call to the Creative Service to update your creative.

```
curl -b -c "Authorization:$TOKEN" "https://api.appnexus.com/creative-vast?member_id=1234&advertiser_id=1234567" -X PUT -d @myvideocreative.json
```

```
{
  "creative-vast": {
    "id": "46629877",
    "thirdparty_viewability_providers": null
  }
}
```

## Delete

If you wish to permanently remove this creative you can make a `DELETE` call pointed to the specific creative as outlined in the example below.

```
curl -b -c "Authorization:$TOKEN" "https://api.appnexus.com/creative-vast?member_id=1234&advertiser_id=1234567" -X DELETE 
```
