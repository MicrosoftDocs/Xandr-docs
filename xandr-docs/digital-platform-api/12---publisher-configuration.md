---
title: Publisher Configuration
description: In this article, learn about publisher configuration and explore detailed information about the various parameters configured at the publisher level.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Publisher configuration

Prior to creating any pieces of the sell-side hierarchy via the API, it is best practice to fully configure the publisher first. The reason for this is that there are defaults that can be specified on a publisher level which cascade to child objects under the publisher.

There are a number of different parameters which can be configured at the publisher level. These settings fall under a few services:

## Publisher

### Timezone

This parameter, stored in the `"timezone"` field, defines the default timezone that will be applied to newly created objects unless otherwise specified at the time of their creation. For a list of valid timezone values, see [API Timezones](api-timezones.md). The sample JSON below shows how to set this parameter.

```
{
  "publisher": {
    "timezone": "EST5EDT",
    ...
  }
}
```

### Allow internal and external CPA/CPC deals

These settings determine whether internal (managed/direct) and external (platform) can buy impressions using a CPC or CPA payment type. The sample JSON below shows how to set these parameters.

```
{
  "publisher": {
    "allow_cpa_managed": true,
    "allow_cpa_external": true,
    "allow_cpc_managed": true,
    "allow_cpc_external": true,
    "managed_cpc_bias_pct": 100,
    "managed_cpa_bias_pct": 100,
    "external_cpc_bias_pct": 90,
    "external_cpc_bias_pct": 90,
    ...
  }
}
```

### Billing address

This setting, stored in the parameter in the sample below, specifies the billing address for the advertiser. The sample JSON below shows how to set this parameter.

```
{
  "publisher": {
    "billing_dba": "Publisher Doing Business As",
    "billing_address1": "123 Main Street",
    "billing_address2": "Floor 4",
    "billing_city": "Smallville",
    "billing_state": "PA",
    "billing_country": "United States",
    "billing_zip": "12345",
    ...
  }
}
```

## Ad quality settings

The ad profile service allows you to specify the types of creatives which are eligible to serve on a given publisher based on creative attributes. The JSON samples below show how to set these parameters.

### Buyers

```
{
  "ad_profile": {
    "default_member_status": "trusted",
    "members": [
      {"id": 123, "status": "banned"},
      {"id": 231, "status": "banned"},
      {"id": 312, "status": "banned"}
    ]
    ...
  }
}
```

### Brands

```
{
  "ad_profile": {
    "default_brand_status": "trusted",
    "brands": [
      {"id": 321, "status": "banned"},
      {"id": 213, "status": "banned"},
      {"id": 132, "status": "banned"}
    ]
    ...
  }
}
```

### Languages

```
{
  "ad_profile": {
    "default_language_status": "banned",
    "languages": [
      {"id": 1, "status": "trusted"}
    ]
    ...
  }
}
```

### Ad servers

```
{
  "ad_profile": {
    "default_ad_server_status": "trusted",
    "ad_servers": [
      {"id": 4, "status": "banned"},
      {"id": 8, "status": "banned"},
      {"id": 11, "status": "banned"}
    ]
    ...
  }
}
```

### Categories

```
{
  "ad_profile": {
    "default_category_status": "banned",
    "categories": [
      {"id": 456, "status": "trusted"},
      {"id": 564, "status": "trusted"},
      {"id": 645, "status": "trusted"}
    ]
    ...
  }
}
```

### Attributes

```
{
  "ad_profile": {
    "default_technical_attribute_status": "trusted",
    "technical_attribute": [
      {"id": 5, "status": "banned"},
      {"id": 7, "status": "banned"}
    ]
    ...
  }
}
```

### Creatives

```
{
  "ad_profile": {
    "creatives": [
      {"id": 1, "status": "banned"},
      {"id": 2, "status": "trusted"},
      {"id": 3, "status": "banned"},
      {"id": 4, "status": "banned"},
      {"id": 5, "status": "trusted"},
      {"id": 6, "status": "trusted"},
      {"id": 7, "status": "banned"},
      {"id": 8, "status": "trusted"},
      {"id": 9, "status": "banned"},
      {"id": 10, "status": "banned"},
      {"id": 11, "status": "banned"},
      {"id": 12, "status": "banned"},
      {"id": 13, "status": "trusted"},
      {"id": 14, "status": "banned"},
      {"id": 15, "status": "trusted"},
      {"id": 16, "status": "trusted"},
      {"id": 17, "status": "banned"}
    ]
    ...
  }
}
```

## Payment rules

### Pricing type

The payment type setting specifies the way that the publisher is going to be paid. The choices for pricing type are `"cpm"` and `"revshare"`. The sample JSON below shows how to set these parameters:

```
{
  "payment-rule": {
    "pricing_type": "cpm",
    "cost_cpm": 1,
    ...
  }
  }
```
